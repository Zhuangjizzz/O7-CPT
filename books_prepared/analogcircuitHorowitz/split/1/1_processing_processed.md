# FOUNDATIONS

## 1.1 Introduction

The field of electronics is one of the great success stories of the 20th century. From the crude spark-gap transmitters and "cat's-whisker" detectors at its beginning, the first halfcentury brought an era of vacuum-tube electronics that developed considerable sophistication and found ready application in areas such as communications, navigation, instrumentation, control, and computation. The latter halfcentury brought "solid-state" electronics - first as discrete transistors, then as magnificent arrays of them within "integrated circuits" (ICs) - in a flood of stunning advances that shows no sign of abating. Compact and inexpensive consumer products now routinely contain many millions of transistors in VLSI (very large-scale integration) chips, combined with elegant optoelectronics (displays, lasers, and so on); they can process sounds, images, and data, and (for example) permit wireless networking and shirt-pocket access to the pooled capabilities of the Internet. Perhaps as noteworthy is the pleasant trend toward increased performance per dollar. ${ }^{1}$ The cost of an electronic microcircuit routinely decreases to a fraction of its initial cost as the manufacturing process is perfected (see Figure 10.87 for an example). In fact, it is often the case that the panel controls and cabinet hardware of an instrument cost more than the electronics inside.

On reading of these exciting new developments in electronics, you may get the impression that you should be able to construct powerful, elegant, yet inexpensive, little gadgets to do almost any conceivable task - all you need to know is how all these miracle devices work. If you've had that feeling, this book is for you. In it we have attempted to convey the excitement and know-how of the subject of electronics.

In this chapter we begin the study of the laws, rules of thumb, and tricks that constitute the art of electronics as we see it. It is necessary to begin at the beginning - with talk of voltage, current, power, and the components that make up

[^0]electronic circuits. Because you can't touch, see, smell, or hear electricity, there will be a certain amount of abstraction (particularly in the first chapter), as well as some dependence on such visualizing instruments as oscilloscopes and voltmeters. In many ways the first chapter is also the most mathematical, in spite of our efforts to keep mathematics to a minimum in order to foster a good intuitive understanding of circuit design and behavior.

In this new edition we've included some intuition-aiding approximations that our students have found helpful. And, by introducing one or two "active" components ahead of their time, we're able to jump directly into some applications that are usually impossible in a traditional textbook "passive electronics" chapter; this will keep things interesting, and even exciting.

Once we have considered the foundations of electronics, we will quickly get into the active circuits (amplifiers, oscillators, logic circuits, etc.) that make electronics the exciting field it is. The reader with some background in electronics may wish to skip over this chapter, since it assumes no prior knowledge of electronics. Further generalizations at this time would be pointless, so let's just dive right in.

## 1.2 Voltage, current, and resistance

### 1.2.1 Voltage and current

There are two quantities that we like to keep track of in electronic circuits: voltage and current. These are usually changing with time; otherwise nothing interesting is happening.
Voltage (symbol $V$ or sometimes $E$ ). Officially, the voltage between two points is the cost in energy (work done) required to move a unit of positive charge from the more negative point (lower potential) to the more positive point (higher potential). Equivalently, it is the energy released when a unit charge moves "downhill" from the higher potential to the lower. ${ }^{2}$ Voltage is also called

[^1]potential difference or electromotive force (EMF). The unit of measure is the volt, with voltages usually expressed in volts $(\mathrm{V})$, kilovolts $\left(1 \mathrm{kV}=10^{3} \mathrm{~V}\right)$, millivolts $\left(1 \mathrm{mV}=10^{-3} \mathrm{~V}\right)$, or microvolts $\left(1 \mu \mathrm{~V}=10^{-6} \mathrm{~V}\right.$ ) (see the box on prefixes). A joule (J) of work is done in moving a coulomb (C) of charge through a potential difference of 1 V . (The coulomb is the unit of electric charge, and it equals the charge of approximately $6 \times 10^{18}$ electrons.) For reasons that will become clear later, the opportunities to talk about nanovolts ( $\left.1 \mathrm{nV}=10^{-9} \mathrm{~V}\right)$ and megavolts ( $1 \mathrm{MV}=10^{6} \mathrm{~V}$ ) are rare.
Current (symbol $I$ ). Current is the rate of flow of electric charge past a point. The unit of measure is the ampere, or amp, with currents usually expressed in amperes $(\mathrm{A})$, milliamperes $\left(1 \mathrm{~mA}=10^{-3} \mathrm{~A}\right)$, microamperes $\left(1 \mu \mathrm{~A}=10^{-6} \mathrm{~A}\right)$, nanoamperes $\left(1 \mathrm{nA}=10^{-9} \mathrm{~A}\right)$, or occasionally picoamperes ( $\left.1 \mathrm{pA}=10^{-12} \mathrm{~A}\right)$. A current of 1 amp equals a flow of 1 coulomb of charge per second. By convention, current in a circuit is considered to flow from a more positive point to a more negative point, even though the actual electron flow is in the opposite direction.
Important: from these definitions you can see that currents flow through things, and voltages are applied (or appear) across things. So you've got to say it right: always refer to the voltage between two points or across two points in a circuit. Always refer to current through a device or connection in a circuit.

To say something like "the voltage through a resistor .." is nonsense. However, we do frequently speak of the voltage at a point in a circuit. This is always understood to mean the voltage between that point and "ground," a common point in the circuit that everyone seems to know about. Soon you will, too.

We generate voltages by doing work on charges in devices such as batteries (conversion of electrochemical energy), generators (conversion of mechanical energy by magnetic forces), solar cells (photovoltaic conversion of the energy of photons), etc. We get currents by placing voltages across things.

At this point you may well wonder how to "see" voltages and currents. The single most useful electronic instrument is the oscilloscope, which allows you to look at voltages (or occasionally currents) in a circuit as a function of time. ${ }^{3}$ We will deal with oscilloscopes, and also voltmeters, when we discuss signals shortly; for a preview see Appendix O, and the multimeter box later in this chapter.

[^2]In real circuits we connect things together with wires (metallic conductors), each of which has the same voltage on it everywhere (with respect to ground, say). ${ }^{4}$ We mention this now so that you will realize that an actual circuit doesn't have to look like its schematic diagram, because wires can be rearranged.

Here are some simple rules about voltage and current:

1. The sum of the currents into a point in a circuit equals the sum of the currents out (conservation of charge). This is sometimes called Kirchhoff's current law (KCL). Engineers like to refer to such a point as a node. It follows that, for a series circuit (a bunch of two-terminal things all connected end-to-end), the current is the same everywhere.
image_name:Figure 1.1
description:The circuit consists of two devices connected in parallel between nodes A and B.

Figure 1.1. Parallel connection.
2. Things hooked in parallel (Figure 1.1) have the same voltage across them. Restated, the sum of the "voltage drops" from $A$ to $B$ via one path through a circuit equals the sum by any other route, and is simply the voltage between $A$ and $B$. Another way to say it is that the sum of the voltage drops around any closed circuit is zero. This is Kirchhoff's voltage law (KVL).
3. The power (energy per unit time) consumed by a circuit device is

$$
\begin{equation*}
P=V I \tag{1.1}
\end{equation*}
$$

This is simply (energy/charge) $\times$ (charge/time). For $V$ in volts and $I$ in amps, $P$ comes out in watts. A watt is a joule per second ( $1 \mathrm{~W}=1 \mathrm{~J} / \mathrm{s}$ ). So, for example, the current flowing through a 60 W lightbulb running on 120 V is 0.5 A .

Power goes into heat (usually), or sometimes mechanical work (motors), radiated energy (lamps, transmitters), or stored energy (batteries, capacitors, inductors). Managing the heat load in a complicated system (e.g., a large computer, in which many kilowatts of electrical energy are converted to heat, with the energetically insignificant byproduct of a few pages of computational results) can be a crucial part of the system design.

[^3]image_name:Figure 1.2
description:The image, labeled as Figure 1.2, showcases a variety of common resistor types arranged in three rows.

1. **Identification of Components and Structure:**
- **Top Row:** This row features wirewound ceramic power resistors. From left to right, there is a 20W vitreous enamel resistor with leads, a 20W resistor with mounting studs, a 30W vitreous enamel resistor, and two resistors (5W and 20W) with mounting studs. These resistors are typically used in applications requiring high power dissipation.

- **Middle Row:** This row displays wirewound power resistors in various configurations. It includes 1W, 3W, and 5W axial ceramic resistors, followed by conduction-cooled resistors, often referred to as "Dale-type," with power ratings of 5W, 10W, 25W, and 50W. These resistors are characterized by their robust construction and ability to handle significant power loads.

- **Bottom Row:** This row consists of smaller resistors with lower power ratings, including 2W, 1W, 1/2W, 1/4W, and 1/8W resistors. These are used in circuits where lower power dissipation is sufficient.

2. **Connections and Interactions:**
- The resistors are standalone components, each with two leads for electrical connections. These leads are used to integrate the resistors into electrical circuits, allowing for current flow and resistance.

3. **Labels, Annotations, and Key Features:**
- The resistors have various markings indicating their power ratings and manufacturers, such as "Ohmite" and "Dale." These labels are crucial for identifying the specifications and appropriate applications for each resistor.
- A scale indicating 1 cm is included at the bottom right of the image, providing a sense of the actual size of the components.

Overall, the image serves as a visual reference for different resistor types, illustrating their physical characteristics and typical power ratings.

Figure 1.2. A selection of common resistor types. Top row, left to right (wirewound ceramic power resistors): 20W vitreous enamel with leads, 20 W with mounting studs, 30 W vitreous enamel, 5 W and 20 W with mounting studs. Middle row (wirewound power resistors): 1W, 3 W , and 5 W axial ceramic; $5 \mathrm{~W}, 10 \mathrm{~W}, 25 \mathrm{~W}$, and 50 W conduction-cooled ("Dale-type"). Bottom row: $2 \mathrm{~W}, 1 \mathrm{~W}, \frac{1}{2} \mathrm{~W}, \frac{1}{4} \mathrm{~W}$, and $\frac{1}{8} \mathrm{~W}$ carbon composition; surface-mount thick-film (2010, 1206, 0805, 0603, and 0402 sizes); surface-mount resistor array; 6-, 8-, and 10-pin single in-line package arrays; dual in-line package array. The resistor at bottom is the ubiquitous RN55D $\frac{1}{4} \mathrm{~W}, 1 \%$ metal-film type; and the pair of resistors above are Victoreen high-resistance types (glass, $2 \mathrm{G} \Omega$; ceramic, $5 \mathrm{G} \Omega$ ).

Soon, when we deal with periodically varying voltages and currents, we will have to generalize the simple equation $P=V I$ to deal with average power, but it's correct as a statement of instantaneous power just as it stands.

Incidentally, don't call current "amperage"; that's strictly bush league. ${ }^{5}$ The same caution will apply to the term "ohmage" ${ }^{6}$ when we get to resistance in the next section.

### 1.2.2 Relationship between voltage and current: resistors

This is a long and interesting story. It is the heart of electronics. Crudely speaking, the name of the game is to make and use gadgets that have interesting and useful $I$-versus$V$ characteristics. Resistors ( $I$ simply proportional to $V$ ),

[^4]capacitors ( $I$ proportional to rate of change of $V$ ), diodes (I flows in only one direction), thermistors (temperaturedependent resistor), photoresistors (light-dependent resistor), strain gauges (strain-dependent resistor), etc., are examples. Perhaps more interesting still are three-terminal devices, such as transistors, in which the current that can flow between a pair of terminals is controlled by the voltage applied to a third terminal. We will gradually get into some of these exotic devices; for now, we will start with the most mundane (and most widely used) circuit element, the resistor (Figure 1.3).
image_name:Figure 1.3
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: Node1, N2: Node2}
]
extrainfo:The diagram shows a simple resistor with two nodes connected.

Figure 1.3. Resistor.

#### A. Resistance and resistors

It is an interesting fact that the current through a metallic conductor (or other partially conducting material) is proportional to the voltage across it. (In the case of wire

#### PREFIXES

| Multiple | Prefix | Symbol | Derivation |
| :--- | :--- | :---: | :--- |
| $10^{24}$ | yotta | Y | end-1 of Latin alphabet, hint of Greek iota |
| $10^{21}$ | zetta | Z | end of Latin alphabet, hint of Greek zeta |
| $10^{18}$ | exa | E | Greek hexa (six: power of 1000) |
| $10^{15}$ | peta | P | Greek penta (five: power of 1000) |
| $10^{12}$ | tera | T | Greek teras (monster) |
| $10^{9}$ | giga | G | Greek gigas (giant) |
| $10^{6}$ | mega | M | Greek megas (great) |
| $10^{3}$ | kilo | k | Greek khilioi (thousand) |
| $10^{-3}$ | milli | m | Latin milli (thousand) |
| $10^{-6}$ | micro | $\mu$ | Greek mikros (small) |
| $10^{-9}$ | nano | n | Greek nanos (dwarf) |
| $10^{-12}$ | pico | p | from Italian/Spanish piccolo/pico (small) |
| $10^{-15}$ | femto | f | Danish/Norwegian femten (fifteen) |
| $10^{-18}$ | atto | a | Danish/Norwegian atten (eighteen) |
| $10^{-21}$ | zepto | z | end of Latin alphabet, mirrors zetta |
| $10^{-24}$ | yocto | y | end-1 of Latin alphabet, mirrors yotta |

These prefixes are universally used to scale units in science and engineering. Their etymological derivations are a matter of some controversy and should not be considered historically reliable. When abbreviating a unit with a prefix, the symbol for the unit follows the prefix without space. Be careful about uppercase and lowercase letters (especially m and M ) in both prefix and unit: 1 mW
is a milliwatt, or one-thousandth of a watt; 1 MHz is a megahertz or 1 million hertz. In general, units are spelled with lowercase letters, even when they are derived from proper names. The unit name is not capitalized when it is spelled out and used with a prefix, only when abbreviated. Thus: hertz and kilohertz, but Hz and kHz; watt, milliwatt, and megawatt, but W, mW, and MW.
conductors used in circuits, we usually choose a thickenough gauge of wire so that these "voltage drops" will be negligible.) This is by no means a universal law for all objects. For instance, the current through a neon bulb is a highly nonlinear function of the applied voltage (it is zero up to a critical voltage, at which point it rises dramatically). The same goes for a variety of interesting special devices - diodes, transistors, lightbulbs, etc. (If you are interested in understanding why metallic conductors behave this way, read $\S \S 4.4-4.5$ in Purcell and Morin's splendid text Electricity and Magnetism).

A resistor is made out of some conducting stuff (carbon, or a thin metal or carbon film, or wire of poor conductivity), with a wire or contacts at each end. It is characterized by its resistance:

$$
\begin{equation*}
R=V / I \tag{1.2}
\end{equation*}
$$

$R$ is in ohms for $V$ in volts and $I$ in amps. This is known as Ohm's law. Typical resistors of the most frequently used type (metal-oxide film, metal film, or carbon film) come in
values from 1 ohm ( $1 \Omega$ ) to about 10 megohms (10M $\Omega$ ). Resistors are also characterized by how much power they can safely dissipate (the most commonly used ones are rated at $1 / 4$ or $1 / 8 \mathrm{~W}$ ), their physical size, ${ }^{7}$ and by other parameters such as tolerance (accuracy), temperature coefficient, noise, voltage coefficient (the extent to which $R$ depends on applied $V$ ), stability with time, inductance, etc. See the box on resistors, Chapter $1 x$, and Appendix C for further details. Figure 1.2 shows a collection of resistors, with most of the available morphologies represented.

Roughly speaking, resistors are used to convert a

[^5]
#### RESISTORS

Resistors are truly ubiquitous. There are almost as many types as there are applications. Resistors are used in amplifiers as loads for active devices, in bias networks, and as feedback elements. In combination with capacitors they establish time constants and act as filters. They are used to set operating currents and signal levels. Resistors are used in power circuits to reduce voltages by dissipating power, to measure currents, and to discharge capacitors after power is removed. They are used in precision circuits to establish currents, to provide accurate voltage ratios, and to set precise gain values. In logic circuits they act as bus and line terminators and as "pullup" and "pull-down" resistors. In high-voltage circuits they are used to measure voltages and to equalize leakage currents among diodes or capacitors connected in series. In radiofrequency (RF) circuits they set the bandwidth of resonant circuits, and they are even used as coil forms for inductors.

Resistors are available with resistances from $0.0002 \Omega$ through $10^{12} \Omega$, standard power ratings from $1 / 8$ watt through 250 watts, and accuracies from $0.005 \%$ through $20 \%$. Resistors can be made from metal films, metaloxide films, or carbon films; from carbon-composition or
ceramic-composition moldings; from metal foil or metal wire wound on a form; or from semiconductor elements similar to field-effect transistors (FETs). The most commonly used resistor type is formed from a carbon, metal, or oxide film, and comes in two widely used "packages": the cylindrical axial-lead type (typified by the generic RN55D $1 \% 1 / 4 \mathrm{~W}$ metal-film resistor), ${ }^{8}$ and the much smaller surface-mount "chip resistor." These common types come in $5 \%, 2 \%$, and $1 \%$ tolerances, in a standard set of values ranging from $1 \Omega$ to $10 \mathrm{M} \Omega$. The $1 \%$ types have 96 values per decade, whereas the $2 \%$ and $5 \%$ types have 48 and 24 values per decade (see Appendix C). Figure 1.2 illustrates most of the common resistor packages.

Resistors are so easy to use and well behaved that they're often taken for granted. They're not perfect, though, and you should be aware of some of their limitations so that you won't be surprised someday. The principal defects are variations in resistance with temperature, voltage, time, and humidity. Other defects relate to inductance (which may be serious at high frequencies), the development of thermal hot spots in power applications, or electrical noise generation in low-noise amplifiers. We treat these in the advanced Chapter $1 x$.
voltage to a current, and vice versa. This may sound awfully trite, but you will soon see what we mean.

#### B. Resistors in series and parallel

From the definition of $R$, some simple results follow:

1. The resistance of two resistors in series (Figure 1.4) is

$$
\begin{equation*}
R=R_{1}+R_{2} \tag{1.3}
\end{equation*}
$$

By putting resistors in series, you always get a larger resistor.
2. The resistance of two resistors in parallel (Figure 1.5) is

$$
\begin{equation*}
R=\frac{R_{1} R_{2}}{R_{1}+R_{2}} \quad \text { or } \quad R=\frac{1}{\frac{1}{R_{1}}+\frac{1}{R_{2}}} \tag{1.4}
\end{equation*}
$$

By putting resistors in parallel, you always get a smaller resistor. Resistance is measured in ohms $(\Omega)$, but in practice we frequently omit the $\Omega$ symbol when referring to resistors that are more than $1000 \Omega(1 \mathrm{k} \Omega)$. Thus, a $4.7 \mathrm{k} \Omega$ resistor is often referred to as a 4.7 k resistor, and a $1 \mathrm{M} \Omega$

[^6]image_name:Figure 1.4. Resistors in series.
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: 1, N2: 2}
name: R2, type: Resistor, value: R2, ports: {N1: 2, N2: 3}
]
extrainfo:The circuit diagram shows two resistors R1 and R2 connected in series. The total resistance is the sum of R1 and R2.

Figure 1.4. Resistors in series.
image_name:Figure 1.5. Resistors in parallel.
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: 1, N2: 2}
name: R2, type: Resistor, value: R2, ports: {N1: 1, N2: 2}
]
extrainfo:The circuit diagram shows two resistors R1 and R2 connected in parallel. The total resistance is given by the formula 1/R_total = 1/R1 + 1/R2.

Figure 1.5. Resistors in parallel.
resistor as a 1 M resistor (or 1 meg ). ${ }^{9}$ If these preliminaries bore you, please have patience - we'll soon get to numerous amusing applications.
Exercise 1.1. You have a 5 k resistor and a 10 k resistor. What is their combined resistance (a) in series and (b) in parallel?
Exercise 1.2. If you place a 1 ohm resistor across a 12 volt car battery, how much power will it dissipate?

Exercise 1.3. Prove the formulas for series and parallel resistors.

[^7]Exercise 1.4. Show that several resistors in parallel have resistance

$$
\begin{equation*}
R=\frac{1}{\frac{1}{R_{1}}+\frac{1}{R_{2}}+\frac{1}{R_{3}}+\cdots} \tag{1.5}
\end{equation*}
$$

Beginners tend to get carried away with complicated algebra in designing or trying to understand electronics. Now is the time to begin learning intuition and shortcuts. Here are a couple of good tricks:

Shortcut \#1 A large resistor in series (parallel) with a small resistor has the resistance of the larger (smaller) one, roughly. So you can "trim" the value of a resistor up or down by connecting a second resistor in series or parallel: to trim up, choose an available resistor value below the target value, then add a (much smaller) series resistor to make up the difference; to trim down, choose an available resistor value above the target value, then connect a (much larger) resistor in parallel. For the latter you can approximate with proportions - to lower the value of a resistor by $1 \%$, say, put a resistor 100 times as large in parallel. ${ }^{10}$
Shortcut \#2 Suppose you want the resistance of 5k in parallel with 10 k . If you think of the 5 k as two 10 k 's in parallel, then the whole circuit is like three 10k's in parallel. Because the resistance of $n$ equal resistors in parallel is $1 / n$th the resistance of the individual resistors, the answer in this case is $10 \mathrm{k} / 3$, or 3.33 k . This trick is handy because it allows you to analyze circuits quickly in your head, without distractions. We want to encourage mental designing, or at least "back-of-the-envelope" designing, for idea brainstorming.

Some more home-grown philosophy: there is a tendency among beginners to want to compute resistor values and other circuit component values to many significant places, particularly with calculators and computers that readily oblige. There are two reasons you should try to avoid falling into this habit: (a) the components themselves are of finite precision (resistors typically have tolerances of $\pm 5 \%$ or $\pm 1 \%$; for capacitors it's typically $\pm 10 \%$ or $\pm 5 \%$; and the parameters that characterize transistors, say, frequently are known only to a factor of 2); (b) one mark of a good circuit design is insensitivity of the finished circuit to precise values of the components (there are exceptions, of course). You'll also learn circuit intuition more quickly if you get into the habit of doing approximate calculations in your head, rather than watching meaningless numbers pop up on a calculator display. We believe strongly that reliance on formulas and equations early in your electronic circuit

[^8]education is a fine way to prevent you from understanding what's really going on.

In trying to develop intuition about resistance, some people find it helpful to think about conductance, $G=1 / R$. The current through a device of conductance $G$ bridging a voltage $V$ is then given by $I=G V$ (Ohm's law). A small resistance is a large conductance, with correspondingly large current under the influence of an applied voltage. Viewed in this light, the formula for parallel resistors is obvious: when several resistors or conducting paths are connected across the same voltage, the total current is the sum of the individual currents. Therefore the net conductance is simply the sum of the individual conductances, $G=G_{1}+G_{2}+G_{3}+\cdots$, which is the same as the formula for parallel resistors derived earlier.

Engineers are fond of defining reciprocal units, and they have designated as the unit of conductance the siemens $(\mathrm{S}=1 / \Omega$ ), also known as the mho (that's ohm spelled backward, given the symbol $\mho$ ). Although the concept of conductance is helpful in developing intuition, it is not used widely; ${ }^{11}$ most people prefer to talk about resistance instead.

#### C. Power in resistors

The power dissipated by a resistor (or any other device) is $P=I V$. Using Ohm's law, you can get the equivalent forms $P=I^{2} R$ and $P=V^{2} / R$.
Exercise 1.5. Show that it is not possible to exceed the power rating of a $1 / 4$ watt resistor of resistance greater than 1 k , no matter how you connect it, in a circuit operating from a 15 volt battery.

Exercise 1.6. Optional exercise: New York City requires about $10^{10}$ watts of electrical power, at 115 volts ${ }^{12}$ (this is plausible: 10 million people averaging 1 kilowatt each). A heavy power cable might be an inch in diameter. Let's calculate what will happen if we try to supply the power through a cable 1 foot in diameter made of pure copper. Its resistance is $0.05 \mu \Omega\left(5 \times 10^{-8}\right.$ ohms) per foot. Calculate (a) the power lost per foot from " $I^{2} R$ losses," (b) the length of cable over which you will lose all $10^{10}$ watts, and (c) how hot the cable will get, if you know the physics involved ( $\sigma=6 \times 10^{-12} \mathrm{~W} / \mathrm{K}^{4} \mathrm{~cm}^{2}$ ). If you have done your computations correctly, the result should seem preposterous. What is the solution to this puzzle?
${ }^{11}$ Although the elegant Millman's theorem has its admirers: it says that the output voltage from a set of resistors (call them $R_{i}$ ) that are driven from a set of corresponding input voltages $\left(V_{i}\right)$ and connected together at the output is $V_{\text {out }}=\left(\sum V_{i} G_{i}\right) / \sum G_{i}$, where the $G_{i}$ are the conductances $\left(G_{i}=1 / R_{i}\right)$.
${ }^{12}$ Although the "official" line voltage is $120 \mathrm{~V} \pm 5 \%$, you'll sometimes see $110 \mathrm{~V}, 115 \mathrm{~V}$, or 117 V . This loose language is OK (and we use it in this book), because (a) the median voltage at the wall plug is 3 to 5 volts lower, when powering stuff; and (b) the minimum wall-plug voltage is 110 V . See ANSI standard C84.1.

#### D. Input and output

Nearly all electronic circuits accept some sort of applied input (usually a voltage) and produce some sort of corresponding output (which again is often a voltage). For example, an audio amplifier might produce a (varying) output voltage that is 100 times as large as a (similarly varying) input voltage. When describing such an amplifier, we imagine measuring the output voltage for a given applied input voltage. Engineers speak of the transfer function $\mathbf{H}$, the ratio of (measured) output divided by (applied) input; for the audio amplifier above, $\mathbf{H}$ is simply a constant $(\mathbf{H}=100)$. We'll get to amplifiers soon enough, in the next chapter. However, with only resistors we can already look at a very important circuit fragment, the voltage divider (which you might call a "de-amplifier").

### 1.2.3 Voltage dividers

We now come to the subject of the voltage divider, one of the most widespread electronic circuit fragments. Show us any real-life circuit and we'll show you half a dozen voltage dividers. To put it very simply, a voltage divider is a circuit that, given a certain voltage input, produces a predictable fraction of the input voltage as the output voltage. The simplest voltage divider is shown in Figure 1.6.
image_name:Figure 1.6 Voltage divider
description:
[
'name': 'R1', 'type': 'Resistor', 'value': 'R1', 'ports': {'N1': 'Vin', 'N2': 'Vout'
'name': 'R2', 'type': 'Resistor', 'value': 'R2', 'ports': {'N1': 'N1', 'N2': 'Vout'
]
extrainfo:The circuit is a voltage divider where the output voltage Vout is a fraction of the input voltage Vin, determined by the resistor values R1 and R2. The formula for the output voltage is Vout = Vin * (R2 / (R1 + R2)).

Figure 1.6. Voltage divider. An applied voltage $V_{\text {in }}$ results in a (smaller) output voltage $V_{\text {out }}$.

An important word of explanation: when engineers draw a circuit like this, it's generally assumed that the $V_{\text {in }}$ on the left is a voltage that you are applying to the circuit, and that the $V_{\text {out }}$ on the right is the resulting output voltage (produced by the circuit) that you are measuring (or at least are interested in). You are supposed to know all this (a) because of the convention that signals generally flow from left to right, (b) from the suggestive names ("in," "out") of the signals, and (c) from familiarity with circuits like this. This may be confusing at first, but with time it becomes easy.

What is $V_{\text {out }}$ ? Well, the current (same everywhere, assuming no "load" on the output; i.e., nothing connected across the output) is

$$
I=\frac{V_{\text {in }}}{R_{1}+R_{2}}
$$

image_name:A
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: Vin, N2: Vout}
name: R2, type: Resistor, value: R2 (adjustable), ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit in diagram A is an adjustable voltage divider using a fixed resistor R1 and an adjustable resistor R2. Signal in is applied across R1 and R2, and signal out is taken from the junction of R1 and R2 to ground.
image_name:B
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: signal in, N2: signal out}
name: R2, type: Resistor, value: R2, ports: {N1: signal out, N2: GND}
]
extrainfo:The circuit is a basic adjustable voltage divider using a fixed resistor R1 and an adjustable resistor R2. The input is 'signal in' and the output is 'signal out'. The output voltage can be adjusted by changing the resistance of R2.

Figure 1.7. An adjustable voltage divider can be made from a fixed and variable resistor, or from a potentiometer. In some contemporary circuits you'll find instead a long series chain of equal-value resistors, with an arrangement of electronic switches that lets you choose any one of the junctions as the output; this sounds much more complicated - but it has the advantage that you can adjust the voltage ratio electrically (rather than mechanically).
(We've used the definition of resistance and the series law.) Then, for $R_{2}$,

$$
\begin{equation*}
V_{\mathrm{out}}=I R_{2}=\frac{R_{2}}{R_{1}+R_{2}} V_{\mathrm{in}} \tag{1.6}
\end{equation*}
$$

Note that the output voltage is always less than (or equal to) the input voltage; that's why it's called a divider. You could get amplification (more output than input) if one of the resistances were negative. This isn't as crazy as it sounds; it is possible to make devices with negative "incremental" resistances (e.g., the component known as a tunnel diode) or even true negative resistances (e.g., the negativeimpedance converter that we will talk about later in the book, §6.2.4B). However, these applications are rather specialized and need not concern you now.

Voltage dividers are often used in circuits to generate a particular voltage from a larger fixed (or varying) voltage. For instance, if $V_{\text {in }}$ is a varying voltage and $R_{2}$ is an adjustable resistor (Figure 1.7A), you have a "volume control"; more simply, the combination $R_{1} R_{2}$ can be made from a single variable resistor, or potentiometer (Figure 1.7B). This and similar applications are common, and potentiometers come in a variety of styles, some of which are shown in Figure 1.8.

The humble voltage divider is even more useful, though, as a way of thinking about a circuit: the input voltage and upper resistance might represent the output of an amplifier, say, and the lower resistance might represent the input of
image_name:Figure 1.8
description:The image labeled "Figure 1.8" displays a variety of common potentiometer styles, organized into three rows. These components are essential in electronic circuits for adjusting resistance and controlling voltage.

**Top Row (Panel Mount):**
1. **Power Wirewound Potentiometer:** Characterized by its robust build, suitable for high-power applications.
2. **"Type AB" 2W Carbon Composition Potentiometer:** Known for its carbon resistive element, often used for general-purpose applications.
3. **10-Turn Wirewound/Plastic Hybrid Potentiometer:** Allows precise resistance adjustments over multiple turns.
4. **Ganged Dual Potentiometer:** Consists of two potentiometers mechanically linked for synchronized adjustment.

**Middle Row (Panel Mount):**
1. **Optical Encoder (Continuous Rotation, 128 Cycles per Turn):** Used for precise position sensing, providing continuous rotation without stops.
2. **Single-Turn Cermet Potentiometer:** Features a ceramic-metal resistive element, offering stability and precision.
3. **Single-Turn Carbon Potentiometer:** Simple design for basic resistance adjustment.
4. **Screw-Adjust Single-Turn Locking Potentiometer:** Includes a locking mechanism to maintain set resistance.

**Front Row (Board-Mount Trimmers):**
1. **Multiturn Side-Adjust Trimmers (Two Styles):** Compact trimmers for fine-tuning resistance on circuit boards.
2. **Quad Single-Turn Trimmer:** A single unit housing four independently adjustable resistors.
3. **3/8'' (9.5 mm) Square Trimmer:** Small form factor for space-constrained applications.

**Key Features and Annotations:**
- The components are shown with their typical mounting styles, either panel or board mount.
- Each potentiometer style is designed for specific applications, from high power to precision tuning.
- The image includes a scale bar indicating 1 cm for size reference, helping to understand the relative sizes of the components.

Figure 1.8. Most of the common potentiometer styles are shown here. Top row, left to right (panel mount): power wirewound, "type AB" 2W carbon composition, 10-turn wirewound/plastic hybrid, ganged dual pot. Middle row (panel mount): optical encoder (continuous rotation, 128 cycles per turn), single-turn cermet, single-turn carbon, screw-adjust single-turn locking. Front row (board-mount trimmers): multiturn side-adjust (two styles), quad single-turn, $3 / 8^{\prime \prime}$ ( 9.5 mm ) square single-turn, $1 / 4^{\prime \prime}$ ( 6.4 mm ) square single-turn, $1 / 4^{\prime \prime}$ ( 6.4 mm ) round single-turn, 4 mm square single-turn surface mount, 4 mm square multiturn surface mount, $3 / 8^{\prime \prime}(9.5 \mathrm{~mm}$ ) square multiturn, quad nonvolatile 256-step integrated pot ( $\mathrm{E}^{2} \mathrm{POT}$ ) in 24-pin small-outline IC.
the following stage. In this case the voltage-divider equation tells you how much signal gets to the input of that last stage. This will all become clearer after you know about a remarkable fact (Thévenin's theorem) that will be discussed later. First, though, a short aside on voltage sources and current sources.

### 1.2.4 Voltage sources and current sources

A perfect voltage source is a two-terminal "black box" that maintains a fixed voltage drop across its terminals, regardless of load resistance. This means, for instance, that it must supply a current $I=V / R$ when a resistance $R$ is attached to its terminals. A real voltage source can supply only a finite maximum current, and in addition it generally behaves like a perfect voltage source with a small resistance in series. Obviously, the smaller this series resistance, the better. For example, a standard 9 volt alkaline battery behaves approximately like a perfect 9 volt voltage source in series with a $3 \Omega$ resistor, and it can provide a maximum
current (when shorted) of 3 amps (which, however, will kill the battery in a few minutes). A voltage source "likes" an open-circuit load and "hates" a short-circuit load, for obvious reasons. (The meaning of "open circuit" and "short circuit" sometimes confuse the beginner: an open circuit has nothing connected to it, whereas a short circuit is a piece of wire bridging the output.) The symbols used to indicate a voltage source are shown in Figure 1.9.

A perfect current source is a two-terminal black box that maintains a constant current through the external circuit, regardless of load resistance or applied voltage. To do this it must be capable of supplying any necessary voltage across its terminals. Real current sources (a muchneglected subject in most textbooks) have a limit to the voltage they can provide (called the output-voltage compliance, or just compliance), and in addition they do not provide absolutely constant output current. A current source "likes" a short-circuit load and "hates" an open-circuit load. The symbols used to indicate a current source are shown in Figure 1.10.
image_name:battery
description:
[
name: Battery, type: VoltageSource, ports: {Np: Battery_Pos, Nn: GND}
]
extrainfo:The circuit diagram includes a battery, a +15V voltage source with a switch, a power supply providing 110V AC, and a Vs voltage source. The battery and Vs are grounded. The power supply has a common ground (COM) connection.
image_name:volts
description:
[
name: power supply, type: VoltageSource, value: 110V ac, ports: {Np: 110V, Nn: com}
]
extrainfo:The circuit diagram contains multiple voltage sources: a battery, a +15 volts source, a power supply with 110V AC input, and a source labeled Vs. These sources provide various voltages for different parts of the circuit.
image_name:Vs
description:
[
name: Vs, type: VoltageSource, ports: {Np: Vs, Nn: GND}
]
extrainfo:The circuit diagram includes a battery connected to ground, a switch that connects +15 volts to ground, a power supply providing 110V AC with a common ground, and a voltage source labeled Vs connected to ground.

Figure 1.9. Voltage sources can be either steady (dc) or varying (ac).
image_name:Figure 1.10
description:
[
name: Device1, type: CurrentSource, value: 1mA, ports: {Np: N1, Nn: N2}
name: Device2, type: CurrentSource, value: 1mA, ports: {Np: N3, Nn: N4}
name: Device3, type: CurrentSource, value: 1mA, ports: {Np: N5, Nn: N6}
]
extrainfo:Figure 1.10 shows three different symbols for a 1mA current source.

Figure 1.10. Current-source symbols.

A battery is a real-life approximation to a voltage source (there is no analog for a current source). A standard D-size flashlight cell, for instance, has a terminal voltage of 1.5 V , an equivalent series resistance of about $0.25 \Omega$, and a total energy capacity of about 10,000 watt-seconds (its characteristics gradually deteriorate with use; at the end of its life, the voltage may be about 1.0 V , with an internal series resistance of several ohms). It is easy to construct voltage sources with far better characteristics, as you will learn when we come to the subject of feedback; this is a major topic of Chapter 9. Except in the important class of devices intended for portability, the use of batteries in electronic devices is rare.
image_name:Figure 1.11
description:The circuit diagram represents a complex network of resistors and voltage sources, which can be simplified using Thévenin's theorem to a single voltage source VTh in series with a resistor RTh. This is illustrated on the right side of the diagram.

Figure 1.11. The Thévenin equivalent circuit.

### 1.2.5 Thévenin equivalent circuit

Thévenin's theorem states ${ }^{12}$ that any two-terminal network of resistors and voltage sources is equivalent to a single

[^9]resistor $R$ in series with a single voltage source $V$. This is remarkable. Any mess of batteries and resistors can be mimicked with one battery and one resistor (Figure 1.11). (Incidentally, there's another theorem, Norton's theorem, that says you can do the same thing with a current source in parallel with a resistor.)

How do you figure out the Thévenin equivalent $R_{\mathrm{Th}}$ and $V_{\mathrm{Th}}$ for a given circuit? Easy! $V_{\mathrm{Th}}$ is the open-circuit voltage of the Thévenin equivalent circuit; so if the two circuits behave identically, it must also be the open-circuit voltage of the given circuit (which you get by calculation, if you know what the circuit is, or by measurement, if you don't). Then you find $R_{\mathrm{Th}}$ by noting that the short-circuit current of the equivalent circuit is $V_{\mathrm{Th}} / R_{\mathrm{Th}}$. In other words,

$$
\begin{align*}
V_{\mathrm{Th}} & =V(\text { open circuit }), \\
R_{\mathrm{Th}} & =\frac{V(\text { open circuit })}{I(\text { short circuit })} . \tag{1.7}
\end{align*}
$$

Let's apply this method to the voltage divider, which must have a Thévenin equivalent:

1. The open-circuit voltage is

$$
V=V_{\text {in }} \frac{R_{2}}{R_{1}+R_{2}} .
$$

2. The short-circuit current is

$$
V_{\text {in }} / R_{1}
$$

So the Thévenin equivalent circuit is a voltage source,

$$
\begin{equation*}
V_{\mathrm{Th}}=V_{\mathrm{in}} \frac{R_{2}}{R_{1}+R_{2}}, \tag{1.8}
\end{equation*}
$$

in series with a resistor,

$$
\begin{equation*}
R_{\mathrm{Th}}=\frac{R_{1} R_{2}}{R_{1}+R_{2}} \tag{1.9}
\end{equation*}
$$

(It is not a coincidence that this happens to be the parallel resistance of $R_{1}$ and $R_{2}$. The reason will become clear later.)
image_name:Figure 1.12
description:
[
'name': 'R1', 'type': 'Resistor', 'value': 'R1', 'ports': {'N1': 'Vin', 'N2': 'V1'
'name': 'R2', 'type': 'Resistor', 'value': 'R2', 'ports': {'N1': 'V1', 'N2': 'GND'
'name': 'Rload', 'type': 'Resistor', 'value': 'Rload', 'ports': {'N1': 'V1', 'N2': 'GND'
'name': 'RTh', 'type': 'Resistor', 'value': 'RTh', 'ports': {'N1': 'VTh', 'N2': 'V2'
'name': 'Rload', 'type': 'Resistor', 'value': 'Rload', 'ports': {'N1': 'V2', 'N2': 'GND'
]
extrainfo:The circuit diagram represents the Thévenin equivalent of a voltage divider. Vin is the input voltage, and VTh is the Thévenin equivalent voltage. R1 and R2 form the original voltage divider, while RTh is the equivalent resistance seen by the load Rload. The diagram demonstrates how a voltage divider's output voltage is affected when a load is attached.

Figure 1.12. Thévenin equivalent of a voltage divider.
From this example it is easy to see that a voltage divider is not a very good battery, in the sense that its output voltage drops severely when a load is attached. As an example, consider Exercise 1.10. You now know everything you need to know to calculate exactly how much the output will

#### MULTIMETERS

There are numerous instruments that let you measure voltages and currents in a circuit. The oscilloscope is the most versatile; it lets you "see" voltages versus time at one or more points in a circuit. Logic probes and logic analyzers are special-purpose instruments for troubleshooting digital circuits. The simple multimeter provides a good way to measure voltage, current, and resistance, often with good precision; however, it responds slowly, and thus it cannot replace the oscilloscope where changing voltages are of interest. Multimeters are of two varieties: those that indicate measurements on a conventional scale with a moving pointer, and those that use a digital display.

The traditional (and now largely obsolete) VOM (volt-ohmmilliammeter) multimeter uses a meter movement that measures current (typically $50 \mu \mathrm{~A}$ full scale). (See a less-design-oriented electronics book for pretty pictures of the innards of meter movements; for our purposes, it suffices to say that it uses coils and magnets.) To measure voltage, the VOM puts a resistor in series with the basic movement. For instance, one kind of VOM will generate a 1 V (full-scale) range by putting a 20 k resistor in series with the standard $50 \mu \mathrm{~A}$ movement; higher voltage ranges use correspondingly larger resistors. Such a VOM is specified as $20,000 \Omega / \mathrm{V}$, meaning that it looks like a resistor whose value is 20 k multiplied by the full-scale voltage of the particular range selected. Full scale on any voltage range is $1 / 20,000 \mathrm{amps}$, or $50 \mu \mathrm{~A}$. It should be clear that one of these voltmeters disturbs a circuit less on a higher range, since it looks like a higher resistance (think of the voltmeter as the lower leg of a voltage divider, with the Thévenin resistance of the circuit you are measuring as the upper resistor). Ideally, a voltmeter should have infinite input resistance.

Most contemporary multimeters use electronic amplification and have an input resistance of $10 \mathrm{M} \Omega$ to $1000 \mathrm{M} \Omega$ when measuring voltage; they display their results digitally, and are known collectively as digital multimeters (DMMs). A word of caution: sometimes the input resistance of these meters is very high on the most sensitive ranges, dropping to a lower resistance for the higher ranges. For instance, you might typically have an input resistance of $10^{9} \Omega$ on the 0.2 V and 2 V ranges, and $10^{7} \Omega$ on all higher ranges. Read the specifications carefully! However, for most circuit measurements these high input resistances will produce negligible loading effects. In any case, it is easy to calculate how serious the effect is by using the voltage-divider equation. Typically, multimeters provide voltage ranges from a volt (or less) to a kilovolt (or more), full scale.

A multimeter usually includes current-measuring capability, with a
set of switchable ranges. Ideally, a current-measuring meter should have zero resistance ${ }^{13}$ in order not to disturb the circuit under test, since it must be put in series with the circuit. In practice, you tolerate a few tenths of a volt drop (sometimes called "voltage burden") with both VOMs and digital multimeters. For either kind of meter, selecting a current range puts a small resistor across the meter's input terminals, typically of resistance value to create a voltage drop of 0.1 V to 0.25 V for the chosen full-scale current; the voltage drop is then converted to a corresponding current indication. ${ }^{14}$ Typically, multimeters provide current ranges from $50 \mu \mathrm{~A}$ (or less) to an amp (or more), full scale.

Multimeters also have one or more batteries in them to power the resistance measurement. By supplying a small current and measuring the voltage drop, they measure resistance, with several ranges to cover values from $1 \Omega$ (or less) to $10 \mathrm{M} \Omega$ (or more).

Important: don't try to measure "the current of a voltage source," by sticking the meter across the wall plug; the same applies for ohms. This is a leading cause of blown-out meters.

Exercise 1.7. What will a $20,000 \Omega / \mathrm{V}$ meter read, on its 1 V scale, when attached to a 1 V source with an internal resistance of 10 k ? What will it read when attached to a $10 \mathrm{k}-10 \mathrm{k}$ voltage divider driven by a "stiff" (zero source resistance) 1 V source?

Exercise 1.8. A $50 \mu \mathrm{~A}$ meter movement has an internal resistance of 5 k . What shunt resistance is needed to convert it to a $0-1$ A meter? What series resistance will convert it to a $0-10 \mathrm{~V}$ meter?

Exercise 1.9. The very high internal resistance of digital multimeters, in their voltage-measuring ranges, can be used to measure extremely low currents (even though the DMM may not offer a low current range explicitly). Suppose, for example, you want to measure the small current that flows through a $1000 \mathrm{M} \Omega$ "leakage" resistance (that term is used to describe a small current that ideally should be absent entirely, for example through the insulation of an underground cable). You have available a standard DMM, whose 2 V dc range has $10 \mathrm{M} \Omega$ internal resistance, and you have available a dc source of +10 V . How can you use what you've got to measure accurately the leakage resistance?
drop for a given load resistance: use the Thévenin equivalent circuit, attach a load, and calculate the new output, noting that the new circuit is nothing but a voltage divider (Figure 1.12).

Exercise 1.10. For the circuit shown in Figure 1.12, with

[^10]$V_{\text {in }}=30 \mathrm{~V}$ and $R_{1}=R_{2}=10 \mathrm{k}$, find (a) the output voltage with no load attached (the open-circuit voltage); (b) the output voltage with a 10 k load (treat as a voltage divider, with $R_{2}$ and $R_{\text {load }}$ combined into a single resistor); (c) the Thévenin equivalent circuit; (d) the same as in part (b), but using the Thévenin equivalent circuit [again, you wind up with a voltage divider; the answer should agree with the result in part (b)]; (e) the power dissipated in each of the resistors.

#### A. Equivalent source resistance and circuit loading

As we have just seen, a voltage divider powered from some fixed voltage is equivalent to some smaller voltage source
image_name:actual
description:
[
name: V1, type: VoltageSource, value: 30V, ports: {Np: Vin, Nn: GND}
name: R1, type: Resistor, value: 10k, ports: {N1: Vin, N2: Vout}
name: R2, type: Resistor, value: 10k, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit on the left is a voltage divider with two 10k resistors powered by a 30V source, resulting in a Thévenin equivalent circuit on the right with a 15V source and a 5k resistor.
image_name:Thévenin
description:
[
'name': 'R3', 'type': 'Resistor', 'value': '5k', 'ports': {'N1': 'Vout', 'N2': 'Vi'
'name': 'V2', 'type': 'VoltageSource', 'value': '15V', 'ports': {'Np': 'Vi', 'Nn': 'GND'
]
extrainfo:The circuit diagram shows a voltage divider and its Thévenin equivalent. The original circuit consists of two 10k resistors in series with a 30V voltage source, creating a voltage divider. The Thévenin equivalent is a 15V voltage source in series with a 5k resistor.

Figure 1.13. Voltage divider example.
in series with a resistor. For example, the output terminals of a $10 \mathrm{k}-10 \mathrm{k}$ voltage divider driven by a perfect 30 volt battery are precisely equivalent to a perfect 15 volt battery in series with a 5 k resistor (Figure 1.13). Attaching a load resistor causes the voltage divider's output to drop, owing to the finite source resistance (Thévenin equivalent resistance of the voltage divider output, viewed as a source of voltage). This is often undesirable. One solution to the problem of making a stiff voltage source ("stiff" is used in this context to describe something that doesn't bend under load) might be to use much smaller resistors in a voltage divider. Occasionally this brute-force approach is useful. However, it is usually best to construct a voltage source, or power supply, as it's commonly called, using active components like transistors or operational amplifiers, which we will treat in Chapters 2-4. In this way you can easily make a voltage source with internal (Thévenin equivalent) resistance as small as milliohms (thousandths of an ohm), without the large currents and dissipation of power characteristic of a low-resistance voltage divider delivering the same performance. In addition, with an active power supply it is easy to make the output voltage adjustable. These topics are treated extensively in Chapter 9.

The concept of equivalent internal resistance applies to all sorts of sources, not just batteries and voltage dividers. Signal sources (e.g., oscillators, amplifiers, and sensing devices) all have an equivalent internal resistance. Attaching a load whose resistance is less than or even comparable to the internal resistance will reduce the output considerably. This undesirable reduction of the open-circuit voltage (or signal) by the load is called "circuit loading." Therefore you should strive to make $R_{\text {load }} \gg R_{\text {internal }}$, because a high-resistance load has little attenuating effect on the source (Figure 1.14). ${ }^{15}$ We will see numerous circuit

[^11]examples in the chapters ahead. This high-resistance condition ideally characterizes measuring instruments such as voltmeters and oscilloscopes.

A word on language: you frequently hear things like "the resistance looking into the voltage divider" or "the output sees a load of so-and-so many ohms," as if circuits had eyes. It's OK (in fact, it's a rather good way of keeping straight which resistance you're talking about) to say what part of the circuit is doing the "looking." ${ }^{16}$
image_name:Figure 1.14
description:The graph in Figure 1.14 is a dual-axis plot with the x-axis labeled as \( R_{\text{LOAD}} / R_{\text{OUT}} \), representing the ratio of load resistance to output resistance on a logarithmic scale ranging from 0.1 to 100. The left y-axis is labeled \( V_{\text{OUT}} / V_{\text{OPEN}} \), indicating the ratio of output voltage to open-circuit voltage, with a linear scale from 0 to 1. The right y-axis is labeled as \( \% \text{Reduction from} \, V_{\text{OPEN}} \), with a linear scale from 0 to 10%.

The graph shows two curves. The first curve, plotted against the left y-axis, starts low at \( R_{\text{LOAD}} / R_{\text{OUT}} = 0.1 \) with a value of about 0.2 and increases steadily, approaching a value close to 1 as \( R_{\text{LOAD}} / R_{\text{OUT}} \) reaches 100. This indicates that as the load resistance increases compared to the output resistance, the output voltage approaches the open-circuit voltage, minimizing attenuation.

The second curve, plotted against the right y-axis, shows the percentage reduction from the open-circuit voltage. It starts at a higher percentage when \( R_{\text{LOAD}} / R_{\text{OUT}} \) is low, decreases to a minimum around \( R_{\text{LOAD}} / R_{\text{OUT}} = 10 \), and then increases again, indicating that the percentage reduction in voltage is minimized when the load resistance is significantly larger than the output resistance.

The intersection point of the two curves occurs around \( R_{\text{LOAD}} / R_{\text{OUT}} = 10 \), where the percentage reduction is minimized, and the output voltage is approximately 0.7 of the open-circuit voltage. This point represents an optimal balance between load and output resistances for minimizing signal attenuation.

Figure 1.14. To minimize the attenuation of a signal source below its open-circuit voltage, keep the load resistance large compared with the output resistance.

#### B. Power transfer

Here is an interesting problem: what load resistance will result in maximum power being transferred to the load for a given source resistance? (The terms source resistance, internal resistance, and Thévenin equivalent resistance all mean the same thing.) It is easy to see that either $R_{\text {load }}=0$ or $R_{\text {load }}=\infty$ results in zero power transferred, because $R_{\text {load }}=0$ means that $V_{\text {load }}=0$ and $I_{\text {load }}=V_{\text {source }} / R_{\text {source }}$, so that $P_{\text {load }}=V_{\text {load }} I_{\text {load }}=0$. But $R_{\text {load }}=\infty$ means that $V_{\text {load }}=V_{\text {source }}$ and $I_{\text {load }}=0$, so that again $P_{\text {load }}=0$. There has to be a maximum in between.

Exercise 1.11. Show that $R_{\text {load }}=R_{\text {source }}$ maximizes the power in the load for a given source resistance. Note: skip this exercise if you don't know calculus, and take it on faith that the answer is true.

[^12]Lest this example leave the wrong impression, we would like to emphasize again that circuits are ordinarily designed so that the load resistance is much greater than the source resistance of the signal that drives the load.

### 1.2.6 Small-signal resistance

We often deal with electronic devices for which $I$ is not proportional to $V$; in such cases there's not much point in talking about resistance, since the ratio $V / I$ will depend on $V$, rather than being a nice constant, independent of $V$. For these devices it is sometimes useful to know instead the slope of the $V-I$ curve, in other words, the ratio of a small change in applied voltage to the resulting change in current through the device, $\Delta V / \Delta I$ (or $d V / d I$ ). This quantity has the units of resistance (ohms) and substitutes for resistance in many calculations. It is called the small-signal resistance, incremental resistance, or dynamic resistance.

#### A. Zener diodes

As an example, consider the zener diode, which has the $I-V$ curve shown in Figure 1.15. Zeners are used to create a constant voltage inside a circuit somewhere, simply done by providing them with a (roughly constant) current derived from a higher voltage within the circuit. ${ }^{17}$ For example, the zener diode in Figure 1.15 will convert an applied current in the range shown to a corresponding (but fractionally narrower) range of voltages. It is important to know how the resulting zener voltage will change with applied current; this is a measure of its "regulation" against changes in the driving current provided to it. Included in the specifications of a zener will be its dynamic resistance, given at a certain current. For example, a zener might have a dynamic resistance of $10 \Omega$ at 10 mA , at its specified zener voltage of 5 V . Using the definition of dynamic resistance, we find that a $10 \%$ change in applied current will therefore result in a change in voltage of

$$
\Delta V=R_{\mathrm{dyn}} \Delta I=10 \times 0.1 \times 0.01=10 \mathrm{mV}
$$

or

$$
\Delta V / V=0.002=0.2 \%
$$

thus demonstrating good voltage-regulating ability. In this sort of application you frequently get the zener current
${ }^{17}$ Zeners belong to the more general class of diodes and rectifiers, important devices that we'll see later in the chapter (\$1.6), and indeed throughout the book. The ideal diode (or rectifier) acts as a perfect conductor for current flow in one direction, and a perfect insulator for current flow in the reverse direction; it is a "one-way valve" for current.
through a resistor from a higher voltage available somewhere in the circuit, as in Figure 1.16.
image_name:Figure 1.15. I-V curves: A. Resistor (linear)
description:The graph labeled 'Figure 1.15. I-V curves: A. Resistor (linear)' is a current-voltage (I-V) plot. This graph is divided into two parts, but the focus is on part A, which illustrates the behavior of a resistor.

1. **Type of Graph and Function:**
- This is a linear I-V graph representing the relationship between current (I) and voltage (V) for a resistor.

2. **Axes Labels and Units:**
- The horizontal axis represents voltage (V) in volts.
- The vertical axis represents current (I) in milliamperes (mA).
- The scales on both axes are linear.

3. **Overall Behavior and Trends:**
- The graph displays two straight lines originating from the origin, indicating a linear relationship between current and voltage, which is characteristic of resistors.
- The slope of each line represents the resistance value, with two different lines indicating different resistors.

4. **Key Features and Technical Details:**
- One line has a steeper slope, labeled as '1k', indicating a resistance of 1 kilo-ohm.
- The other line is less steep, labeled as '4k', indicating a resistance of 4 kilo-ohms.
- The intersection at the origin (0,0) signifies that at zero voltage, the current is also zero, consistent with Ohm's law.

5. **Annotations and Specific Data Points:**
- The graph is marked with key values, such as 1 mA on the current axis and 1 V on the voltage axis, helping to establish the scale and slope of the lines.

Overall, this graph effectively demonstrates the linear relationship between voltage and current for resistors, with the slope of each line corresponding to different resistance values, illustrating Ohm's law (V = IR).
image_name:Figure 1.15. I-V curves: B. Zener diode (nonlinear)
description:The graph labeled 'Figure 1.15. I-V curves: B. Zener diode (nonlinear)' is an I-V (current-voltage) curve illustrating the behavior of a Zener diode, which is a nonlinear device.

1. Type of Graph and Function:
This is a voltage-current (I-V) graph for a Zener diode, showcasing its nonlinear characteristics.

2. Axes Labels and Units:
- **Horizontal Axis (V):** Represents voltage across the diode. No specific units are marked, but it's understood to be in volts (V).
- **Vertical Axis (I):** Represents current through the diode. No specific units are marked, but it's understood to be in amperes (A).

3. Overall Behavior and Trends:
- **Zener Breakdown Region:** The curve shows a sharp increase in current in the reverse bias direction at a certain negative voltage, indicating the Zener breakdown region. This is where the diode conducts significantly in reverse.
- **Forward Bias Region:** On the positive side of the voltage axis, the diode begins to conduct normally, similar to a standard diode.

4. Key Features and Technical Details:
- **Real vs. Ideal Zener:** The graph distinguishes between the behavior of a real Zener diode and an ideal Zener diode. The real Zener shows a gradual increase in current as voltage decreases in reverse bias, while the ideal Zener would have an abrupt change.
- **Diode Conduction:** In the positive voltage region, the diode starts conducting normally, showing an upward curve.
- **Zener Voltage:** The point where the current sharply increases in reverse bias is the Zener breakdown voltage, though exact values are not specified.

5. Annotations and Specific Data Points:
- The graph includes annotations indicating the behavior of both real and ideal Zener diodes. The 'real zener' curve is more gradual compared to the 'ideal zener,' which is depicted as a vertical line at the breakdown voltage.
- There are no specific numerical values or markers provided for the Zener voltage or current levels.

This graph effectively illustrates the characteristic I-V behavior of Zener diodes, highlighting the differences between real and ideal conditions, particularly in the breakdown region.

Figure 1.15. I-V curves: A. Resistor (linear). B. Zener diode (nonlinear).
image_name:Figure 1.15
description:The graph in Figure 1.15 illustrates the I-V (current-voltage) characteristics of two components: a resistor and a Zener diode.

1. **Type of Graph and Function:**
- The graph is an I-V curve, which shows the relationship between current (I) and voltage (V) for different components.

2. **Axes Labels and Units:**
- The x-axis represents voltage (V) and the y-axis represents current (I). The scales are likely linear, although specific units or numerical values are not provided.

3. **Overall Behavior and Trends:**
- **Resistor (Linear):** The curve for the resistor is a straight line passing through the origin, indicating a linear relationship between current and voltage, consistent with Ohm's law.
- **Zener Diode (Nonlinear):** The Zener diode curve shows nonlinear behavior. It has two distinct regions:
- **Forward Bias Region:** Similar to a regular diode, the curve initially rises slowly, then more steeply as the forward voltage increases.
- **Reverse Bias Region:** The curve shows a sharp increase in current at a certain reverse voltage, known as the breakdown voltage. The 'real Zener' curve is more gradual compared to the 'ideal Zener,' which would be a vertical line at the breakdown voltage.

4. **Key Features and Technical Details:**
- The breakdown region of the Zener diode is the most significant feature, demonstrating its ability to maintain a constant voltage across it when reverse-biased beyond this point.
- The ideal Zener breakdown would be depicted as a vertical line, but the real Zener curve shows a more gradual increase, indicating a more realistic behavior with some slope.

5. **Annotations and Specific Data Points:**
- There are no specific numerical values or markers for the Zener voltage or current levels, nor are there any annotations indicating specific points on the curves.

This graph effectively illustrates the characteristic I-V behavior of Zener diodes, highlighting the differences between real and ideal conditions, particularly in the breakdown region, alongside the linear behavior of a resistor.
image_name:Figure 1.16
description:
[
name: R, type: Resistor, value: R, ports: {N1: Vin, N2: Vout}
name: D1, type: Diode, ports: {Na: GND, Nc: Vout}
]
extrainfo:This circuit is a basic Zener diode voltage regulator. The resistor R limits the current through the Zener diode, and the diode maintains a stable output voltage Vout.

Figure 1.16. Zener regulator.
Then,

$$
I=\frac{V_{\text {in }}-V_{\text {out }}}{R}
$$

and

$$
\Delta I=\frac{\Delta V_{\mathrm{in}}-\Delta V_{\mathrm{out}}}{R}
$$

so

$$
\Delta V_{\mathrm{out}}=R_{\mathrm{dyn}} \Delta I=\frac{R_{\mathrm{dyn}}}{R}\left(\Delta V_{\mathrm{in}}-\Delta V_{\mathrm{out}}\right)
$$

and finally

$$
\Delta V_{\mathrm{out}}=\frac{R_{\mathrm{dyn}}}{R+R_{\mathrm{dyn}}} \Delta V_{\mathrm{in}}
$$

Aha - the voltage-divider equation, again! Thus, for changes in voltage, the circuit behaves like a voltage divider, with the zener replaced by a resistor equal to its dynamic resistance at the operating current. This is the
utility of incremental resistance. For instance, suppose in the preceding circuit we have an input voltage ranging between 15 and 20 V , and we use a 1 N 4733 ( 5.1 V , 1 W zener diode) in order to generate a stable 5.1 V power supply. We choose $R=300 \Omega$, for a maximum zener current of 50 mA : $(20 \mathrm{~V}-5.1 \mathrm{~V}) / 300 \Omega$. We can now estimate the output-voltage regulation (variation in output voltage), knowing that this particular zener has a specified maximum dynamic resistance of $7.0 \Omega$ at 50 mA . The zener current varies from 50 mA to 33 mA over the input-voltage range; this 17 mA change in current then produces a voltage change at the output of $\Delta V=R_{\mathrm{dyn}} \Delta I$, or 0.12 V .

It's a useful fact, when dealing with zener diodes, that the dynamic resistance of a zener diode varies roughly in inverse proportion to current. It's worth knowing, also, that there are ICs designed to substitute for zener diodes; these "two-terminal voltage references" have superior performance - much lower dynamic resistance (less than $1 \Omega$, even at currents as small as 0.1 mA ; that's a thousand times better than the zener we just used), and excellent temperature stability (better than $0.01 \% / \mathrm{C}$ ). We will see more of zeners and voltage references in $\S \S 2.2 .4$ and 9.10.

In real life, a zener will provide better regulation if driven by a current source, which has, by definition, $R_{\text {incr }}=\infty$ (the same current, regardless of voltage). But current sources are more complex, and therefore in practice we often resort to the humble resistor. When thinking about zeners, it's worth remembering that low-voltage units (e.g., 3.3 V ) behave rather poorly, in terms of constancy of voltage versus current (Figure 1.17); if you think you need a low voltage zener, use a two-terminal reference instead (§9.10).

### 1.2.7 An example: "It's too hot!"

Some people like to turn the thermostat way up, annoying other people who like their houses cool. Here's a little gadget (Figure 1.18) that lets folks of the latter persuasion know when to complain - it lights up a red light-emitting diode (LED) indicator when the room is warmer than $30^{\circ} \mathrm{C}$ $\left(86^{\circ} \mathrm{F}\right)$. It also shows how to use the humble voltage divider (and even humbler Ohm's law), and how to deal with an LED, which behaves like a zener diode (and is sometimes used as such).

The triangular symbol is a comparator, a handy device (discussed in §12.3) that switches its output according to the relative voltages at its two input terminals. The temperature sensing device is $R_{4}$, which decreases in resistance by about $4 \% /{ }^{\circ} \mathrm{C}$, and which is $10 \mathrm{k} \Omega$ at $25^{\circ} \mathrm{C}$. So we've made
image_name:Figure 1.17
description:The graph is an I-V (Current vs. Voltage) plot, depicting the behavior of different zener diodes and voltage references. The x-axis represents Voltage in volts, ranging from 0 to 6 volts, while the y-axis represents Current in milliamperes (mA), ranging from 0 to 10 mA.

The graph includes curves for several components:
- **1.25V reference**: This is marked by a vertical dashed line at 1.25 volts, indicating a stable voltage reference point.
- **2.4V zener**: This curve begins to rise steeply just after 2 volts, showing the zener breakdown behavior typical of a 2.4V zener diode.
- **2.50V reference**: Another vertical dashed line at 2.5 volts, indicating another stable voltage reference point.
- **3.3V zener**: The curve for this zener diode starts rising steeply around 3 volts, similar to the 2.4V zener but shifted to a higher voltage.
- **5.6V zener**: This zener diode shows a steep increase in current beginning just after 5 volts, indicating its breakdown voltage is around 5.6 volts.

Overall, the graph shows how each zener diode exhibits a sharp increase in current at its respective breakdown voltage, demonstrating the zener effect. The reference lines provide a contrast, showing stable voltage levels without the steep current rise. The plot clearly illustrates the difference in performance and characteristics between low-voltage zeners and voltage references, with the steeper curves of the zeners indicating their utility in voltage regulation applications.

Figure 1.17. Low-voltage zeners are pretty dismal, as seen in these measured $I$ vs. $V$ curves (for three members of the 1N522167 series), particularly in contrast to the excellent measured performance of a pair of "IC voltage references" (LM385Z-1.2 and LM385Z-2.5, see $\S 9.10$ and Table 9.7). However, zener diodes in the neighborhood of 6 V (such as the 5.6 V 1 N 5232 B or 6.2 V 1N5234B) exhibit admirably steep curves, and are useful parts.
it the lower leg of a voltage divider $\left(R_{3} R_{4}\right)$, whose output is compared with the temperature-insensitive divider $R_{1} R_{2}$. When it's hotter than $30^{\circ} \mathrm{C}$, point " X " is at a lower voltage than point "Y," so the comparator pulls its output to ground.

At the output there's an LED, which behaves electrically like a 1.6 V zener diode; and when current is flowing, it lights up. Its lower terminal is then at $5 \mathrm{~V}-1.6 \mathrm{~V}$, or +3.4 V . So we've added a series resistor, sized to allow 5 mA when the comparator output is at ground: $R_{5}=3.4 \mathrm{~V} / 5 \mathrm{~mA}$, or $680 \Omega$.

If you wanted to, you could make the setpoint adjustable by replacing $R_{2}$ with a 5 k pot in series with a 5 k fixed resistor. We'll see later that it's also a good idea to add some hysteresis, to encourage the comparator to be decisive. Note that this circuit is insensitive to the exact powersupply voltage because it compares ratios. Ratiometric techniques are good; we'll see them again later.

## 1.3 Signals

A later section in this chapter will deal with capacitors, devices whose properties depend on the way the voltages and currents in a circuit are changing. Our analysis of dc circuits so far (Ohm's law, Thévenin equivalent circuits, etc.) still holds, even if the voltages and currents are changing in time. But for a proper understanding of alternating-current (ac) circuits, it is useful to have in mind certain common
image_name:Figure 1.18
description:
[
name: R1, type: Resistor, value: 10k, ports: {N1: LOAD1, N2: X3}
name: R2, type: Resistor, value: 8.06k, ports: {N1: X3, N2: GND}
name: R3, type: Resistor, value: 10k, ports: {N1: X4, N2: x2}
name: R4, type: Resistor, value: Thermistor #103JG1F, ports: {N1: X2, N2: GND}
name: R5, type: Resistor, value: 680Ω, ports: {N1: Out(A1), N2: k}
name: D1, type: Diode, ports: {Na: LOAD2, Nc: Out(A1)}
name: A1, type: OpAmp, value: TLC 372, ports: {InP: X2, InN: X3, OutP: Out(A1), OutN: GND}
]
extrainfo:The circuit is a temperature-sensitive LED driver using a comparator. The LED lights up when the temperature exceeds 30°C, as the thermistor R4 decreases its resistance with increasing temperature, causing the voltage at X to drop below the voltage at Y. The comparator A1 outputs low when Vx < Vy, turning on the LED through R5.

Figure 1.18. The LED lights up when it's hotter than $30^{\circ} \mathrm{C}$. The comparator (which we'll see later, in Chapters 4 and 12) pulls its output to ground when the voltage at " X " is less than the voltage at "Y." $R_{4}$ is a thermistor, which is a resistor with a deliberate negative temperature coefficient; that is, its resistance decreases with increasing temperature - by about $4 \% /{ }^{\circ} \mathrm{C}$.
types of signals, voltages that change in time in a particular way.

### 1.3.1 Sinusoidal signals

Sinusoidal signals are the most popular signals around; they're what you get out of the wall plug. If someone says something like "take a $10 \mu \mathrm{~V}$ signal at 1 MHz ," they mean a sinewave. Mathematically, what you have is a voltage described by

$$
\begin{equation*}
V=A \sin 2 \pi f t \tag{1.10}
\end{equation*}
$$

where $A$ is called the amplitude and $f$ is the frequency in hertz (cycles per second). A sinewave looks like the wave shown in Figure 1.19. Sometimes it is important to know the value of the signal at some arbitrary time $t=0$, in which case you may see a phase $\phi$ in the expression:

$$
V=A \sin (2 \pi f t+\phi)
$$

image_name:Figure 1.19
description:The graph depicted in Figure 1.19 is a time-domain waveform representing a sinewave. The x-axis is labeled as time \( t \), likely in seconds, and the y-axis is labeled as amplitude \( A \), which could be in volts or another unit of measurement depending on the context.

This sinewave graph illustrates a periodic oscillation with a consistent frequency \( f \). The waveform is characterized by its sinusoidal shape, repeating every \( 1/f \) seconds. The amplitude \( A \) represents the peak value of the voltage, which is the maximum displacement from the horizontal axis.

The graph shows one complete cycle of the sinewave, starting from zero, reaching a positive peak at \( A \), returning to zero, reaching a negative peak at \(-A\), and finally returning to zero again. The key points marked on the time axis are \( \frac{1}{2f} \), \( \frac{1}{f} \), and \( \frac{3}{2f} \), indicating the quarter-period, half-period, and three-quarter-period points, respectively.

The sinewave crosses the horizontal axis (zero crossings) at \( t = 0 \), \( t = \frac{1}{f} \), and \( t = \frac{2}{f} \). The positive peak occurs at \( t = \frac{1}{4f} \) and the negative peak at \( t = \frac{3}{4f} \). These features are typical of a sinewave, highlighting its periodic and oscillatory nature.

Figure 1.19. Sinewave of amplitude $A$ and frequency $f$.
The other variation on this simple theme is the use of angular frequency, which looks like this:

$$
V=A \sin \omega t
$$

Here $\omega$ is the angular frequency, measured in radians per
second. Just remember the important relation $\omega=2 \pi f$ and you won't go wrong.

The great merit of sinewaves (and the cause of their perennial popularity) is the fact that they are the solutions to certain linear differential equations that happen to describe many phenomena in nature as well as the properties of linear circuits. A linear circuit has the property that its output, when driven by the sum of two input signals, equals the sum of its individual outputs when driven by each input signal in turn; i.e., if $\mathscr{O}(A)$ represents the output when driven by signal $A$, then a circuit is linear if $\mathscr{O}(A+B)=\mathscr{O}(A)+\mathscr{O}(B)$. A linear circuit driven by a sinewave always responds with a sinewave, although in general the phase and amplitude are changed. No other periodic signal can make this statement. It is standard practice, in fact, to describe the behavior of a circuit by its frequency response, by which we mean the way the circuit alters the amplitude of an applied sinewave as a function of frequency. A stereo amplifier, for instance, should be characterized by a "flat" frequency response over the range 20 Hz to 20 kHz , at least.

The sinewave frequencies we usually deal with range from a few hertz to a few tens of megahertz. Lower frequencies, down to 0.0001 Hz or lower, can be generated with carefully built circuits, if needed. Higher frequencies, up to say 2000 MHz ( 2 GHz ) and above, can be generated, but they require special transmission-line techniques. Above that, you're dealing with microwaves, for which conventional wired circuits with lumped-circuit elements become impractical, and exotic waveguides or "striplines" are used instead.

### 1.3.2 Signal amplitudes and decibels

In addition to its amplitude, there are several other ways to characterize the magnitude of a sinewave or any other signal. You sometimes see it specified by peak-to-peak amplitude (pp amplitude), which is just what you would guess, namely, twice the amplitude. The other method is to give the root-mean-square amplitude (rms amplitude), which is $V_{\mathrm{rms}}=(1 / \sqrt{2}) A=0.707 A$ (this is for sinewaves only; the ratio of pp to rms will be different for other waveforms). Odd as it may seem, this is the usual method, because rms voltage is what's used to compute power. The nominal voltage across the terminals of a wall socket (in the United States) is 120 volts $\mathrm{rms}, 60 \mathrm{~Hz}$. The amplitude is 170 volts (339 volts pp). ${ }^{18}$

[^13]
#### A. Decibels

How do you compare the relative amplitudes of two signals? You could say, for instance, that signal $X$ is twice as large as signal $Y$. That's fine, and useful for many purposes. But because we often deal with ratios as large as a million, it is better to use a logarithmic measure, and for this we present the decibel (it's one-tenth as large as something called a bel, which no one ever uses). By definition, the ratio of two signals, in decibels ( dB ), is

$$
\begin{equation*}
\mathrm{dB}=10 \log _{10} \frac{P_{2}}{P_{1}} \tag{1.11}
\end{equation*}
$$

where $P_{1}$ and $P_{2}$ represent the power in the two signals. We are often dealing with signal amplitudes, however, in which case we can express the ratio of two signals having the same waveform as

$$
\begin{equation*}
\mathrm{dB}=20 \log _{10} \frac{A_{2}}{A_{1}} \tag{1.12}
\end{equation*}
$$

where $A_{1}$ and $A_{2}$ are the two signal amplitudes. So, for instance, one signal of twice the amplitude of another is +6 dB relative to it, since $\log _{10} 2=0.3010$. A signal 10 times as large is +20 dB ; a signal one-tenth as large is -20 dB .

Although decibels are ordinarily used to specify the ratio of two signals, they are sometimes used as an absolute measure of amplitude. What is happening is that you are assuming some reference signal level and expressing any other level in decibels relative to it. There are several standard levels (which are unstated, but understood) that are used in this way; the most common references are (a) $0 \mathrm{dBV}(1 \mathrm{Vms})$; (b) 0 dBm (the voltage corresponding to 1 mW into some assumed load impedance, which for radiofrequencies is usually $50 \Omega$, but for audio is often $600 \Omega$; the corresponding 0 dBm amplitudes, when loaded by those impedances, are then 0.22 V rms and 0.78 V rms ); and (c) the small noise voltage generated by a resistor at room temperature (this surprising fact is discussed in §8.1.1). In addition to these, there are reference amplitudes used for measurements in other fields of engineering and science. For instance, in acoustics, 0 dB SPL (sound pressure level) is a wave whose rms pressure is $20 \mu \mathrm{~Pa}$ (that's $2 \times 10^{-10} \mathrm{~atm}$ ); in audio communications, levels can be stated in dBrnC (relative noise reference weighted in frequency by "curve C"). When stating amplitudes this way, it is best to be specific about the 0 dB reference amplitude;

For a sinewave the relationship is $V_{\mathrm{avg}}=V_{\mathrm{rms}} / 1.11$. However, such meters are usually calibrated so that they indicate the rms sinewave amplitude. For signals other than sinewaves their indication is in error; be sure to use a "true rms" meter if you want the right answer.
say something like "an amplitude of 27 decibels relative to 1 V rms ," or abbreviate " 27 dB re $1 \mathrm{~V} \mathrm{rms,"}$ or define a term like "dBV."19

Exercise 1.12. Determine the voltage and power ratios for a pair of signals with the following decibel ratios: (a) 3 dB , (b) 6 dB , (c) 10 dB , (d) 20 dB .

Exercise 1.13. We might call this amusing exercise "Desert Island dBs ": in the table below we've started entering some values for power ratios corresponding to the first dozen integral dBs, using the results for parts (a) and (c) of the last exercise. Your job is to complete the table, without recourse to a calculator. A possibly helpful hint: starting at 10 dB , go down the table in steps of 3 dB , then up in a step of 10 dB , then down again. Finally, get rid of yucky numbers like 3.125 (and its near relatives) by noticing that it's charmingly close to $\pi$.

| dB | ratio $\left(P / P_{0}\right)$ |
| ---: | :---: |
| 0 | 1 |
| 1 |  |
| 2 |  |
| 3 | 2 |
| 4 |  |
| 5 |  |
| 6 | 4 |
| 7 |  |
| 8 |  |
| 9 | 8 |
| 10 | 10 |
| 11 |  |

### 1.3.3 Other signals

#### A. Ramp

The ramp is a signal that looks like the one shown in Figure 1.20 A . It is simply a voltage rising (or falling) at a constant rate. That can't go on forever, of course, even in science fiction movies. It is sometimes approximated by a finite ramp (Figure 1.20B) or by a periodic ramp (known as a sawtooth, Figure 1.20C).

#### B. Triangle

The triangle wave is a close cousin of the ramp; it is simply a symmetrical ramp (Figure 1.21).

#### C. Noise

Signals of interest are often mixed with noise; this is a catch-all phrase that usually applies to random noise of thermal origin. Noise voltages can be specified by their

[^14]A.
image_name:Figure 1.20A
description:The graph in Figure 1.20A is a time-domain waveform depicting a voltage-ramp function. The horizontal axis represents time (t) and the vertical axis represents voltage (V). Both axes use a linear scale, but specific units are not provided in the context.

Overall Behavior and Trends
The graph shows a linear increase in voltage over time, starting from the origin (0,0). The voltage increases at a constant rate, indicating a steady ramp function. The line is solid initially and becomes dashed, suggesting that the ramp continues indefinitely in theory, but is approximated for practical purposes.

Key Features and Technical Details
- **Linear Region:** The graph displays a straight line, indicating a uniform rate of increase in voltage over time.
- **Dashed Line:** The transition from a solid to a dashed line suggests an approximation or theoretical extension of the ramp beyond practical limits.
- **No Inflection Points or Oscillations:** The graph is a simple linear ramp without any peaks, valleys, or oscillations.

Annotations and Specific Data Points
There are no specific markers or annotations provided in the graph. The lack of specific data points or numerical values implies a general representation of a voltage ramp rather than a precise measurement.

B.
image_name:Voltage-ramp waveform
description:### Voltage-Ramp Waveform Description

1. **Type of Graph and Function:**
- The graph is a time-domain waveform representing a voltage ramp.

2. **Axes Labels and Units:**
- The horizontal axis is labeled as 't', representing time. No specific units are provided, indicating a general representation.
- The vertical axis is labeled as 'V', representing voltage. Again, no specific units are given, suggesting a conceptual illustration.

3. **Overall Behavior and Trends:**
- The graph shows a linear increase in voltage over time, starting from the origin. This linear portion indicates a constant rate of voltage increase.
- After reaching a certain point, the graph transitions to a horizontal line, indicating that the voltage remains constant over time. This suggests a saturation point or limit to the voltage increase.

4. **Key Features and Technical Details:**
- The transition from the linear ramp to the horizontal line occurs smoothly, without any inflection points or oscillations.
- The graph does not show any peaks, valleys, or zero crossings, emphasizing its simplicity as a basic ramp function.

5. **Annotations and Specific Data Points:**
- There are no specific markers, annotations, or numerical values provided on the graph. This lack of detailed data suggests a theoretical or generalized representation of a voltage ramp rather than a precise measurement.

C.
image_name:Sawtooth wave
description:The graph represents a **sawtooth wave**, a type of periodic waveform. The horizontal axis is labeled as \( t \), representing time, while the vertical axis is labeled as \( V \), representing voltage. The axes do not have specific units or numerical values, indicating a generalized representation of the waveform.

Overall Behavior and Trends:
The sawtooth wave is characterized by a linear rise over time followed by a sharp drop to the initial value, repeating periodically. This pattern creates a series of triangular shapes that ascend linearly to a peak before abruptly descending. The waveform is continuous and repeats uniformly, demonstrating its periodic nature.

Key Features and Technical Details:
- **Linear Rise:** The voltage increases linearly with time, indicating a constant rate of change during the rise phase.
- **Sharp Drop:** After reaching the peak voltage, the waveform drops sharply back to the starting voltage, marking the end of one cycle and the beginning of another.
- **Periodicity:** The wave is periodic, with each cycle having the same duration and amplitude. This regularity is a defining feature of the sawtooth wave.

Annotations and Specific Data Points:
There are no specific annotations, markers, or numerical values on the graph. The absence of these elements suggests a theoretical depiction rather than a plotted measurement, focusing on the fundamental shape and behavior of the sawtooth wave.

Figure 1.20. A: Voltage-ramp waveform. B: Ramp with limit. C: Sawtooth wave.
image_name:Figure 1.20. A
description:The graph in Figure 1.20 A depicts a voltage-ramp waveform, which is a type of time-domain waveform. This waveform is characterized by a linear increase in voltage over time, followed by an abrupt drop back to the starting voltage level, creating a sawtooth-like pattern.

Axes Labels and Units:
- **Horizontal Axis**: Represents time, although specific units (e.g., milliseconds, seconds) are not annotated.
- **Vertical Axis**: Represents voltage, with no specific units or scale indicated.

Overall Behavior and Trends:
- The waveform displays a repeating linear ramp-up in voltage, followed by a sharp drop. This cycle repeats periodically, indicating a consistent and regular pattern typical of a sawtooth waveform.
- Each cycle is identical in duration and amplitude, emphasizing the periodic nature of the waveform.

Key Features and Technical Details:
- The waveform has distinct peaks where the voltage reaches its maximum before dropping sharply.
- The slope of the ramp indicates a constant rate of voltage increase during each cycle.
- There are no specific annotations or numerical values on the graph, suggesting a theoretical representation rather than a measured signal.

Annotations and Specific Data Points:
- The absence of numerical markers or annotations highlights the focus on the fundamental shape and periodic behavior of the waveform, rather than precise quantitative analysis.
image_name:Figure 1.20. B
description:The graph depicted in Figure 1.20 B is a time-domain waveform known as a 'Ramp with Limit.' It is characterized by a linear increase in value followed by a sudden drop back to the initial level, forming a repetitive pattern. This waveform resembles a sawtooth wave but with a noticeable limit at its peak, after which it abruptly resets.

1. **Type of Graph and Function:** This is a time-domain waveform graph illustrating a ramp function with a limiting reset point, similar to a sawtooth wave but with a distinct peak limit.

2. **Axes Labels and Units:** The horizontal axis represents time, while the vertical axis represents amplitude or voltage. The scales appear to be linear, though no specific units or numerical values are provided.

3. **Overall Behavior and Trends:** The waveform exhibits a linear rise, reaching a maximum point, after which it abruptly drops to the starting level. This pattern repeats periodically, indicating a consistent cycle of increase and reset.

4. **Key Features and Technical Details:** The key feature of this waveform is the linear ramping behavior followed by an immediate drop. This creates a series of sharp, triangular peaks, each reaching the same maximum amplitude before resetting. The waveform does not display any inflection points or gradual transitions, emphasizing the abruptness of the reset.

5. **Annotations and Specific Data Points:** There are no specific annotations, markers, or numerical values on the graph, suggesting a theoretical representation focusing on the fundamental behavior of the waveform rather than precise measurements.
image_name:Figure 1.20. C
description:### Type of Graph and Function:
The graph depicted is a time-domain waveform representing a sawtooth wave. This type of waveform is characterized by a linear rise over time followed by a sudden drop, repeating periodically.

Axes Labels and Units:
The horizontal axis represents time, though it is not explicitly labeled in the image. The vertical axis represents amplitude or voltage, also not labeled. Both axes appear to use a linear scale.

Overall Behavior and Trends:
The sawtooth wave shown has a consistent, repeating pattern. Each cycle begins with a linear increase in amplitude, reaching a peak before abruptly dropping back to the initial value. This cycle then repeats indefinitely, highlighting the periodic nature of the waveform.

Key Features and Technical Details:
- **Periodic Nature:** The waveform repeats at regular intervals, indicating a consistent frequency.
- **Linear Rise:** The amplitude increases linearly over time until reaching a peak.
- **Sudden Drop:** After reaching the peak, the waveform abruptly returns to the starting amplitude, creating the sawtooth shape.
- **No Annotations:** There are no specific markers or annotations on the graph, suggesting a theoretical depiction of the waveform rather than a measured signal.

Annotations and Specific Data Points:
There are no numerical values or specific data points provided. The graph focuses on illustrating the fundamental shape and behavior of the sawtooth wave.

Figure 1.21. Triangle wave.
image_name:Figure 1.22. Noise
description:The graph labeled as "Figure 1.22. Noise" depicts a time-domain waveform representing noise. The horizontal axis is labeled 't', indicating time, while the vertical axis is labeled 'V', representing voltage. The graph does not specify units or scales for these axes, suggesting a theoretical or conceptual representation of noise rather than a precise measurement.

In terms of overall behavior, the waveform exhibits a random, irregular pattern typical of noise signals. There are no discernible periodic trends or repeating patterns, which is characteristic of noise. The amplitude fluctuates erratically above and below the zero-voltage line, indicating a mixture of positive and negative voltages over time.

Key features of the graph include numerous peaks and valleys throughout the waveform, but without any specific annotations or numerical values provided, it is difficult to quantify these features. The waveform appears to be a visual representation of band-limited white Gaussian noise, as described in the context, where the power per hertz is equal across a certain frequency band, and the amplitude distribution follows a Gaussian curve.

There are no specific markers, gridlines, or reference lines on the graph, emphasizing its role as an illustrative example of noise rather than a detailed analytical tool. The lack of annotations suggests that the focus is on understanding the general behavior and appearance of noise in a signal rather than analyzing specific data points.

Figure 1.22. Noise.
frequency spectrum (power per hertz) or by their amplitude distribution. One of the most common kind of noise is band-limited white Gaussian noise, which means a signal with equal power per hertz in some band of frequencies and that exhibits a Gaussian (bell-shaped) distribution of amplitudes when many instantaneous measurements of its amplitude are made. This kind of noise is generated by a resistor (Johnson noise or Nyquist noise), and it plagues sensitive measurements of all kinds. On an oscilloscope it appears as shown in Figure 1.22. We will discuss noise and low-noise techniques in considerable detail in Chapter 8.

#### D. Square wave

A square wave is a signal that varies in time as shown in Figure 1.23. Like the sinewave, it is characterized by amplitude and frequency (and perhaps phase). A linear circuit driven by a square wave rarely responds with a square wave. For a square wave, the peak amplitude and the rms amplitude are the same.
image_name:Figure 1.23. Square wave
description:The graph in Figure 1.23 represents a square wave signal plotted over time. The horizontal axis is labeled 't' which stands for time, and the vertical axis is labeled 'A' representing amplitude. The time axis is marked with fractions of the signal's period, specifically \( \frac{1}{2f} \), \( \frac{1}{f} \), \( \frac{2}{f} \), and \( \frac{3}{f} \), where \( f \) is the frequency of the square wave.

The square wave alternates between two amplitude levels symmetrically around zero. It has a constant amplitude of \( A \) and switches between the positive and negative amplitude levels at regular intervals, creating a series of rectangular pulses. Each complete cycle of the square wave consists of a high level for half the period and a low level for the other half, demonstrating a 50% duty cycle.

The transitions between the high and low states are vertical lines, indicating instantaneous changes in amplitude, which is characteristic of an ideal square wave. However, in practical scenarios, these transitions would have finite rise and fall times.

Overall, the graph shows a periodic waveform with sharp transitions, illustrating the fundamental characteristics of a square wave signal in the time domain.

Figure 1.23. Square wave.
image_name:Figure 1.24. Rise time of a step waveform.
description:The graph depicted in Figure 1.24 is a time-domain waveform illustrating the rise time of a step waveform. The x-axis represents time, while the y-axis represents amplitude, both in arbitrary units. The graph is linear in both axes, showing a single transition from a low to a high state.

The waveform begins at a stable low amplitude, marked as 0%, and transitions to a high amplitude, marked as 100%. The rise time, denoted as \( t_r \), is defined as the interval during which the amplitude rises from 10% to 90% of its maximum value. This is indicated by dashed horizontal lines at the 10% and 90% levels, with a vertical line marking the rise time interval.

The waveform exhibits a smooth, S-shaped curve during the rise, indicating a finite rise time typical of real-world electronic signals. This curve suggests that the transition is not instantaneous, unlike an ideal square wave. The graph also shows slight overshoot beyond the 100% level before stabilizing, which is common in practical circuits due to inductive or capacitive effects.

Overall, the graph highlights the concept of rise time, emphasizing the non-instantaneous nature of signal transitions in electronic circuits and the typical behavior of step waveforms in such contexts.

Figure 1.24. Rise time of a step waveform.

The edges of a square wave are not perfectly square; in typical electronic circuits the rise time $t_{r}$ ranges from a few nanoseconds to a few microseconds. Figure 1.24 shows the sort of thing usually seen. The rise time is conventionally defined as the time required for the signal to go from $10 \%$ to $90 \%$ of its total transition.
image_name:Figure 1.25
description:The graph in Figure 1.25 illustrates various pulse waveforms, depicting both positive and negative polarities. The graph is a time-domain waveform, with the horizontal axis labeled as 't' representing time, and the vertical axis labeled as 'V' representing voltage. The vertical axis shows positive and negative voltage levels, indicating the polarity of the pulses.

The graph consists of four distinct pulse waveforms:

1. **Positive Pulse:** The first waveform is a positive-going pulse. It begins at zero voltage, rises sharply to a positive voltage level, remains constant for a specific pulse width, and then returns to zero. This waveform demonstrates a typical positive pulse with a defined amplitude and pulse width.

2. **Negative Pulse:** The second waveform illustrates a negative-going pulse. It starts at zero voltage, drops sharply to a negative voltage level, maintains this level for a certain duration, and then returns to zero. This waveform represents a typical negative pulse.

3. **Negative Pulse (Inverted):** The third waveform is similar to the second but inverted. It starts at zero, dips into the negative voltage region, stays constant for the pulse width, and then goes back to zero.

4. **Positive Pulse (Inverted):** The fourth waveform mirrors the first one but in an inverted manner, starting at zero, rising to a positive level, maintaining this level, and then returning to zero.

These waveforms demonstrate the concept of pulses with both positive and negative polarities, highlighting the amplitude and pulse width as key characteristics. There are no specific annotations or numerical values provided in the graph, but the illustration effectively shows the basic structure and behavior of pulse waveforms in electronic circuits.

Figure 1.25. Positive- and negative-going pulses of both polarities.

#### E. Pulses

A pulse is a signal that looks like the objects shown in Figure 1.25 . It is defined by amplitude and pulse width. You can generate a train of periodic (equally spaced) pulses, in which case you can talk about the frequency, or pulse repetition rate, and the "duty cycle," the ratio of pulse width to repetition period (duty cycle ranges from zero to $100 \%$ ). Pulses can have positive or negative polarity; in addition, they can be "positive-going" or "negative-going." For
instance, the second pulse in Figure 1.25 is a negativegoing pulse of positive polarity.

#### F. Steps and spikes

Steps and spikes are signals that are talked about a lot but are not so often used. They provide a nice way of describing what happens in a circuit. If you could draw them, they would look something like the example in Figure 1.26. The step function is part of a square wave; the spike is simply a jump of vanishingly short duration.
image_name:step
description:The graph in Figure 1.26 consists of two separate diagrams labeled as 'step' and 'spike.' These diagrams illustrate fundamental signal types often referenced in circuit analysis.

1. **Type of Graph and Function:**
- The graph consists of two time-domain waveforms: a step function and a spike function.

2. **Axes Labels and Units:**
- The axes are not explicitly labeled, but it can be inferred that the horizontal axis represents time, while the vertical axis represents amplitude or voltage. There are no visible scales or units provided.

3. **Overall Behavior and Trends:**
- **Step Function:** The step function shows a sudden change in voltage. It begins at a low level, abruptly jumps to a higher level, and then remains constant. This behavior is characteristic of a step input in electrical circuits, often used to test the transient response.
- **Spike Function:** The spike function features a rapid, short-duration increase in voltage, returning immediately to the baseline level. This is indicative of a transient spike, which might represent noise or a sudden disturbance in a circuit.

4. **Key Features and Technical Details:**
- **Step Function:** The key feature is the vertical jump from one level to another, representing an instantaneous change. This is often used to simulate a switch turning on.
- **Spike Function:** The primary feature is the narrow, tall spike, suggesting a brief, high-amplitude event, often used to model impulses or glitches in a system.

5. **Annotations and Specific Data Points:**
- The diagrams are labeled directly beneath each waveform as 'step' and 'spike,' respectively. There are no numerical values or additional annotations present.

Overall, these diagrams serve as basic representations of two common signal types used in analyzing circuit behavior, particularly in understanding how circuits respond to sudden changes or disturbances.
image_name:spike
description:The graph titled "spike" in Figure 1.26 consists of two distinct parts: a step function and a spike. The graph is a time-domain waveform, typically used in digital electronics to describe signal transitions.

**Axes Labels and Units:**
- The horizontal axis represents time, though specific units are not labeled.
- The vertical axis represents voltage or signal amplitude, also without specific units.

**Overall Behavior and Trends:**
- **Step Function (left side):** This part of the graph shows a sudden transition from a low to a high state, resembling the characteristic shape of a square wave. It starts at a low level, abruptly jumps to a higher level, and maintains this level, indicating a step change in the signal.
- **Spike (right side):** This part depicts a vertical line that represents a very short-duration pulse or spike in the signal. The spike is characterized by a rapid rise and fall, returning to the baseline almost instantaneously.

**Key Features and Technical Details:**
- The step function shows a distinct transition point where the signal level changes abruptly. This is typical in digital signals to represent a change from logic state '0' to '1'.
- The spike is a narrow pulse, often used to represent transient effects or impulses in a circuit.

**Annotations and Specific Data Points:**
- The graph is labeled with the words "step" and "spike" beneath the respective parts of the waveform, indicating the type of signal each represents.

Overall, the graph illustrates basic elements of digital signal transitions, highlighting the difference between a sustained level change (step) and a transient pulse (spike).

Figure 1.26. Steps and spikes.

### 1.3.4 Logic levels

Pulses and square waves are used extensively in digital electronics, in which predefined voltage levels represent one of two possible states present at any point in the circuit. These states are called simply HIGH and Low, and correspond to the 1 (true) and 0 (false) states of Boolean logic (the algebra that describes such two-state systems).

Precise voltages are not necessary in digital electronics. You need only to distinguish which of the two possible states is present. Each digital logic family therefore specifies legal HIGH and low states. For example, the "74LVC" digital logic family runs from a single +3.3 V supply, with output levels that are typically 0 V (LOW) and $3.3 \mathrm{~V}(\mathrm{HIGH})$, and an input decision threshold of 1.5 V . However, actual outputs can be as much as 0.4 V away from ground or from +3.3 V without malfunction. We'll have much more to say about logic levels in Chapters 10 through 12.

### 1.3.5 Signal sources

Often the source of a signal is some part of the circuit you are working on. But for test purposes a flexible signal source is invaluable. They come in three flavors: signal generators, pulse generators, and function generators.

#### A. Signal generators

Signal generators are sinewave oscillators, usually equipped to give a wide range of frequency coverage,
with provision for precise control of amplitude (using a resistive divider network called an attenuator). Some units let you modulate (i.e., vary in time) the output amplitude ("AM" for "amplitude modulated") or frequency ("FM" for "frequency modulated"). A variation on this theme is the sweep generator, a signal generator that can sweep its output frequency repeatedly over some range. These are handy for testing circuits whose properties vary with frequency in a particular way, e.g., "tuned circuits" or filters. Nowadays these devices, as well as most test instruments, are available in configurations that allow you to program the frequency, amplitude, etc., from a computer or other digital instrument.

For many signal generators the signal source is a frequency synthesizer, a device that generates sinewaves whose frequencies can be set precisely. The frequency is set digitally, often to eight significant figures or more, and is internally synthesized from a precise standard (a standalone quartz-crystal oscillator or rubidium frequency standard, or a GPS-derived oscillator) by digital methods we will discuss later (§13.13.6). Typical of synthesizers is the programmable SG384 from Stanford Research Systems, with a frequency range of $1 \mu \mathrm{~Hz}$ to 4 GHz , an amplitude range of -110 dBm to $+16.5 \mathrm{dBm}(0.7 \mu \mathrm{~V}$ to 1.5 V , rms $)$, and various modulation modes such as AM, FM, and $\Phi$; it costs about $\$ 4,600$. You can get synthesized sweep generators, and you can get synthesizers that produce other waveforms (see Function Generators, below). If your requirement is for no-nonsense accurate frequency generation, you can't beat a synthesizer.

#### B. Pulse generators

Pulse generators make only pulses, but what pulses! Pulse width, repetition rate, amplitude, polarity, rise time, etc., may all be adjustable. The fastest ones go up to gigahertz pulse rates. In addition, many units allow you to generate pulse pairs, with settable spacing and repetition rate, or even programmable patterns (they are sometimes called pattern generators). Most contemporary pulse generators are provided with logic-level outputs for easy connection to digital circuitry. As with signal generators, these come in the programmable variety.

#### C. Function generators

In many ways function generators are the most flexible signal sources of all. You can make sine, triangle, and square waves over an enormous frequency range $(0.01 \mathrm{~Hz}$ to 30 MHz is typical), with control of amplitude and dc offset (a constant-dc voltage added to the signal). Many of them have provision for frequency sweeping, often in
several modes (linear or logarithmic frequency variation versus time). They are available with pulse outputs (although not with the flexibility you get with a pulse generator), and some of them have provision for modulation.

Traditional function generators used analog circuitry, but contemporary models generally are synthesized digital function generators, exhibiting all the flexibility of a function generator along with the stability and accuracy of a frequency synthesizer. In addition, they let you program an "arbitrary" waveform, specifying the amplitude at a set of equally spaced points. An example is the Tektronix AFG3102, with a lower frequency limit of 1 microhertz, which can make sine and square waves to 100 MHz , pulses and "noise" to 50 MHz , and arbitrary waveforms (up to 128 k points) to 50 MHz . It has modulation (five kinds), sweep (linear and log), and burst modes (1 to $10^{6}$ cycles), and everything is programmable, including frequency, pulse width and rise times, modulation, and amplitude ( 20 mV to 10 Vpp ); it even includes some bizarre built-in waveforms such as $\sin (x) / x$, exponential rise and fall, Gaussian, and Lorentzian. It has two independent outputs and costs about $\$ 5 k$. For general use, if you can have only one signal source, the function generator is for you.

## 1.4 Capacitors and ac circuits

Once we enter the world of changing voltages and currents, or "signals," we encounter two very interesting circuit elements that are useless in purely dc circuits: capacitors and inductors. As you will see, these humble devices, combined with resistors, complete the triad of passive linear circuit elements that form the basis of nearly all circuitry. ${ }^{20}$ Capacitors, in particular, are essential in nearly every circuit application. They are used for waveform generation, filtering, and blocking and bypass applications. They are used in integrators and differentiators. In combination with inductors, they make possible sharp filters for separating desired signals from background. You will see some of these applications as we continue with this chapter, and there will be numerous interesting examples in later chapters.

Let's proceed, then, to look at capacitors in detail. Por-

[^15]image_name:Figure 1.27
description:
[
name: C1, type: Capacitor, value: C1, ports: {Np: node1, Nn: node2}
name: C2, type: Capacitor, value: C2, ports: {Np: node1, Nn: node2}
]
extrainfo:The diagram shows two capacitors. C1 is non-polarized, and C2 is polarized, indicated by the curved electrode and a '+' sign for the positive terminal.

Figure 1.27. Capacitors. The curved electrode indicates the negative terminal of a polarized capacitor, or the "outer foil" of a wrapped-film capacitor.
tions of the treatment that follows are necessarily mathematical in nature; the reader with little mathematical preparation may find the math review in Appendix A helpful. In any case, an understanding of the details is less important in the long run than an understanding of the results.

### 1.4.1 Capacitors

A capacitor (Figure 1.27) (the old-fashioned name was condenser) is a device that has two wires sticking out of it and has the property

$$
\begin{equation*}
Q=C V \tag{1.13}
\end{equation*}
$$

Its basic form is a pair of closely-spaced metal plates, separated by some insulating material, as in the rolledup "axial-film capacitor" of Figure 1.28. A capacitor of $C$ farads with $V$ volts across its terminals has $Q$ coulombs of stored charge on one plate and $-Q$ on the other. The capacitance is proportional to the area and inversely proportional to the spacing. For the simple parallel-plate capacitor, with separation $d$ and plate area $A$ (and with the spacing $d$ much less than the dimensions of the plates), the capacitance $C$ is given by

$$
\begin{equation*}
C=8.85 \times 10^{-14} \varepsilon A / d \mathrm{~F} \tag{1.14}
\end{equation*}
$$

where $\varepsilon$ is the dielectric constant of the insulator, and the dimensions are measured in centimeters. It takes a lot of area, and tiny spacing, to make the sort of capacitances commonly used in circuits. ${ }^{21}$ For example, a pair of $1 \mathrm{~cm}^{2}$ plates separated by 1 mm is a capacitor of slightly less than $10^{-12} \mathrm{~F}$ (a picofarad); you'd need 100,000 of them just to create the $0.1 \mu \mathrm{~F}$ capacitor of Figure 1.28 (which is nothing special; we routinely use capacitors with many microfarads of capacitance). Ordinarily you don't need to calculate capacitances, because you buy a capacitor as an electronic component.

To a first approximation, capacitors are devices that might be considered simply frequency-dependent resistors.

[^16]image_name:Figure 1.28
description:The image depicts a detailed diagram of an axial-lead Mylar capacitor, illustrating its internal structure. The capacitor is shown as a rolled-up assembly, which is a common design to increase the surface area within a compact form factor.

1. **Identification of Components and Structure:**
- **Inside Foil and Outside Foil:** These are the conductive layers of the capacitor, typically made of metallized plastic films. The diagram shows these foils as being rolled together, which is a typical construction method for increasing capacitance by maximizing the area of the conductive surfaces in contact with the dielectric.
- **Dielectric (Insulator):** Positioned between the foils, this layer is crucial for storing electrical energy by maintaining an electric field between the conductive layers without allowing current to pass through.

2. **Connections and Interactions:**
- The rolled structure forms a cylindrical shape with leads extending from each end, allowing the capacitor to be connected into an electronic circuit. The leads are attached to the inside and outside foils, enabling the capacitor to function as a component that stores and releases electrical energy.

3. **Labels, Annotations, and Key Features:**
- The capacitor is labeled as "0.1 µF 100 VDC," indicating its capacitance value of 0.1 microfarads and a voltage rating of 100 volts DC. This provides information on the maximum voltage the capacitor can handle and its storage capacity.
- The diagram includes annotations pointing to the "dielectric (insulator)," "inside foil," and "outside foil," helping to clarify the function of each component within the capacitor structure.

Figure 1.28. You get a lot of area by rolling up a pair of metallized plastic films. And it's great fun unrolling one of these axial-lead Mylar capacitors (ditto for the old-style golf balls with their lengthy wound-up rubber band).

They allow you to make frequency-dependent voltage dividers, for instance. For some applications (bypass, coupling) this is almost all you need to know, but for other applications (filtering, energy storage, resonant circuits) a deeper understanding is needed. For example, ideal capacitors cannot dissipate power, even though current can flow through them, because the voltage and current are $90^{\circ}$ out of phase.

Before launching into the details of capacitors in the following dozen pages (including some necessary mathematics that describes their behavior in time and in frequency), we wish to emphasize those first two applications - bypass and coupling - because they are the most common uses of capacitors, and they are easy to understand at the simplest level. We'll see these in detail later (\$§1.7.1C and 1.7.16A), but no need to wait - it's easy, and intuitive. Because a capacitor looks like an open circuit at dc, it lets you couple a varying signal while blocking its average dc level. This is a blocking capacitor (also called a coupling capacitor), as in Figure 1.93. Likewise, because a capacitor looks like a short circuit at high frequencies, it suppresses ("bypasses") signals where you don't want them, for example on the dc voltages that power your circuits, as in Figure 8.80A (where capacitors are suppressing signals on the +5 V and -5 V dc supply voltages, and also on the base terminal of transistor $Q_{2}$ ). ${ }^{22}$ Demographically, these two applications account for the vast majority of capacitors that are wired into the world's circuits.

Taking the derivative of the defining equation 1.13 , you get

[^17]\$\$

$$
\begin{equation*}
I=C \frac{d V}{d t} \tag{1.15}
\end{equation*}
$$

\$\$

So a capacitor is more complicated than a resistor: the current is not simply proportional to the voltage, but rather to the rate of change of voltage. If you change the voltage across a farad by 1 volt per second, you are supplying an amp. Conversely, if you supply an amp, its voltage changes by 1 volt per second. A farad is an enormous capacitance, and you usually deal in microfarads ( $\mu \mathrm{F}$ ), nanofarads ( nF ), or picofarads $(\mathrm{pF}) .{ }^{23}$ For instance, if you supply a current of 1 mA to $1 \mu \mathrm{~F}$, the voltage will rise at 1000 volts per second. A 10 ms pulse of this current will increase the voltage across the capacitor by 10 volts (Figure 1.29).
image_name:Figure 1.29
description:The graph in Figure 1.29 consists of two parts, illustrating the relationship between current and voltage across a capacitor over time.

1. **Type of Graph and Function:**
- The top graph is a time-domain waveform representing current (I) as a function of time (t).
- The bottom graph is a time-domain waveform representing voltage (V) as a function of time (t).

2. **Axes Labels and Units:**
- **Top Graph:**
- The vertical axis represents current (I) in milliamperes (mA).
- The horizontal axis represents time (t) in milliseconds (ms).
- The current is shown as a rectangular pulse with a magnitude of 1 mA and a duration of 10 ms.
- **Bottom Graph:**
- The vertical axis represents voltage (V) in volts (V).
- The horizontal axis represents time (t) in milliseconds (ms).
- The voltage increases linearly during the current pulse and then remains constant.

3. **Overall Behavior and Trends:**
- **Top Graph:**
- The current is initially zero, then rises to 1 mA for a duration of 10 ms, and returns to zero.
- **Bottom Graph:**
- The voltage across the capacitor starts at an initial value \( V_{before} \), increases linearly by 10 V during the 10 ms pulse, and then stabilizes at \( V_{after} \).

4. **Key Features and Technical Details:**
- The capacitor has a capacitance of 1 microfarad (\( \mu F \)).
- The voltage increase corresponds to the integral of the current over time, consistent with the relationship \( V = \frac{1}{C} \int I \, dt \).
- During the 10 ms pulse, the voltage increases by 10 V, reflecting the charging of the capacitor by the constant current.

5. **Annotations and Specific Data Points:**
- The current pulse is clearly marked with a height of 1 mA and a width of 10 ms.
- The voltage increase is annotated with a change of 10 V, indicating the effect of the current pulse on the capacitor's voltage.
- The graph effectively demonstrates the principle that a constant current through a capacitor results in a linear voltage increase over time.

Figure 1.29. The voltage across a capacitor changes when a current flows through it.

When you charge up a capacitor, you're supplying energy. The capacitor doesn't get hot; instead, it stores the energy in its internal electric fields. It's an easy exercise to discover for yourself that the amount of stored energy in a charged capacitor is just

$$
\begin{equation*}
U_{\mathrm{C}}=\frac{1}{2} C V^{2} \tag{1.16}
\end{equation*}
$$

where $U_{\mathrm{C}}$ is in joules for $C$ in farads and $V$ in volts. This is an important result; we'll see it often.

Exercise 1.14. Take the energy challenge: imagine charging up a capacitor of capacitance $C$, from 0 V to some final voltage $V_{\mathrm{f}}$. If you do it right, the result won't depend on how you get there,

[^18]image_name:Figure 1.30
description:The image labeled "Figure 1.30" showcases a diverse collection of capacitors, illustrating the wide variety of shapes, sizes, and types available in these components. Here's a detailed description of the visible elements:

1. **Components and Structure:**
- **Large Electrolytic Capacitors:** At the top left, there are large-value polarized aluminum electrolytic capacitors. These include both radial and axial lead types, and one with screw terminals, often referred to as a computer electrolytic.
- **Film Capacitors:** A low-inductance film capacitor is visible, characterized by its wide strap terminal.
- **Variable Capacitors:** In the lower left, small-value variable capacitors are present, including one air and three ceramic types.
- **Disc Capacitors:** Various disc capacitors, typically ceramic, are seen, which are often used in high-frequency applications.
- **Tantalum Capacitors:** Smaller tantalum capacitors are also present, known for their stability and reliability.
- **Other Types:** Other capacitor types such as glass, mica, and polyester are visible, each with unique properties suitable for different applications.

2. **Connections and Interactions:**
- The capacitors are shown without connections, as this is a display of the components themselves. However, the leads and terminals indicate how they would be connected in a circuit.
- The arrangement demonstrates the variety of terminal types, including axial leads, radial leads, and screw terminals, which affect how they are mounted on a circuit board.

3. **Labels, Annotations, and Key Features:**
- The image includes capacitors with visible labels indicating voltage ratings, capacitance values, and manufacturer markings.
- A scale is provided at the bottom right, showing "1 cm," giving a sense of the size of each component.
- Some capacitors have specific markings like "LO-HENRY," indicating manufacturer or series names, which may be relevant for selecting components for specific applications.

This collection effectively demonstrates the versatility and range of capacitors used in electronic circuits, from small signal applications to high-power systems.

Figure 1.30. Capacitors masquerade as anything they like! Here is a representative collection. In the lower left are small-value variable capacitors (one air, three ceramic), with large-value polarized aluminum electrolytics above them (the three on the left have radial leads, the three on the right have axial leads, and the specimen with screw terminals at top is often called a computer electrolytic). Next in line across the top is a low-inductance film capacitor (note the wide strap terminals), then an oil-filled paper capacitor, and last, a set of disc ceramic capacitors running down the right. The four rectangular objects below are film capacitors (polyester, polycarbonate, or polypropylene). The D-subminiature connector seems misplaced - but it is a filtered connector, with a 1000 pF capacitor from each pin to the shell. To its left is a group of seven polarized tantalum electrolytics (five with axial leads, one radial, and one surface-mount). The three capacitors above them are axial-film capacitors. The ten capacitors at bottom center are all ceramic types (four with radial leads, two axial, and four surface-mount chip capacitors); above them are high-voltage capacitors - an axial-glass capacitor, and a ceramic transmitting capacitor with screw terminals. Finally, below them and to the left are four mica capacitors and a pair of diode-like objects known as varactors, which are voltage-variable capacitors made from a diode junction.
so you don't need to assume constant current charging (though you're welcome to do so). At any instant the rate of flow of energy into the capacitor is VI (joules/s); so you need to integrate $d U=$ VIdt from start to finish. Take it from there.

Capacitors come in an amazing variety of shapes and sizes (Figure 1.30 shows examples of most of them); with time, you will come to recognize their more common incarnations. For the smallest capacitances you may see examples of the basic parallel-plate (or cylindrical piston) construction. For greater capacitance, you need more area and
closer spacing; the usual approach is to plate some conductor onto a thin insulating material (the dielectric), for instance, aluminized plastic film rolled up into a small cylindrical configuration. Other popular types are thin ceramic wafers (ceramic chip capacitors), metal foils with oxide insulators (electrolytic capacitors), and metallized mica. Each of these types has unique properties; for a brief rundown, see the section on capacitors in Chapter $1 x$. In general, ceramic and polyester types are used for most noncritical circuit applications; capacitors with polycarbonate, polystyrene, polypropylene, Teflon, or glass dielectric are
used in demanding applications; tantalum capacitors are used where greater capacitance is needed; and aluminum electrolytics are used for power-supply filtering.

#### A. Capacitors in parallel and series

The capacitance of several capacitors in parallel is the sum of their individual capacitances. This is easy to see: put voltage $V$ across the parallel combination; then

$$
\begin{aligned}
C_{\text {total }} V & =Q_{\text {total }}=Q_{1}+Q_{2}+Q_{3}+\cdots \\
& =C_{1} V+C_{2} V+C_{3} V+\cdots \\
& =\left(C_{1}+C_{2}+C_{3}+\cdots\right) V
\end{aligned}
$$

or

$$
\begin{equation*}
C_{\text {total }}=C_{1}+C_{2}+C_{3}+\cdots \tag{1.17}
\end{equation*}
$$

For capacitors in series, the formula is like that for resistors in parallel:

$$
\begin{equation*}
C_{\text {total }}=\frac{1}{\frac{1}{C_{1}}+\frac{1}{C_{2}}+\frac{1}{C_{3}}+\cdots} \tag{1.18}
\end{equation*}
$$

or (two capacitors only)

$$
C_{\text {total }}=\frac{C_{1} C_{2}}{C_{1}+C_{2}} .
$$

Exercise 1.15. Derive the formula for the capacitance of two capacitors in series. Hint: because there is no external connection to the point where the two capacitors are connected together, they must have equal stored charges.

The current that flows in a capacitor during charging $(I=C d V / d t)$ has some unusual features. Unlike resistive current, it's not proportional to voltage, but rather to the rate of change (the "time derivative") of voltage. Furthermore, unlike the situation in a resistor, the power $(V \times I)$ associated with capacitive current is not turned into heat, but is stored as energy in the capacitor's internal electric field. You get all that energy back when you discharge the capacitor. We'll see another way to look at these curious properties when we talk about reactance, beginning in §1.7.

### 1.4.2 RC circuits: $V$ and $/$ versus time

When dealing with ac circuits (or, in general, any circuits that have changing voltages and currents), there are two possible approaches. You can talk about $V$ and $I$ versus time, or you can talk about amplitude versus signal frequency. Both approaches have their merits, and you find yourself switching back and forth according to which description is most convenient in each situation. We begin our
study of ac circuits in the time domain. Starting with §1.7, we will tackle the frequency domain.

What are some of the features of circuits with capacitors? To answer this question, let's begin with the simple $R C$ circuit (Figure 1.31). Application of the capacitor rules gives

$$
\begin{equation*}
C \frac{d V}{d t}=I=-\frac{V}{R} \tag{1.19}
\end{equation*}
$$

This is a differential equation, and its solution is

$$
\begin{equation*}
V=A e^{-t / R C} \tag{1.20}
\end{equation*}
$$

So a charged capacitor placed across a resistor will discharge as in Figure 1.32. Intuition serves well here: the current that flows is (from the resistor equation) proportional to the remaining voltage; but the slope of the discharge is (from the capacitor equation) proportional to that current. So the discharge curve has to be a function whose derivative is proportional to its value, i.e., an exponential.
image_name:Figure 1.31. The simplest $R C$ circuit.
description:
[
name: C, type: Capacitor, value: C, ports: {Np: N1, Nn: N2}
name: R, type: Resistor, value: R, ports: {N1: N2, N2: N1}
]
extrainfo:The circuit is a simple RC discharge circuit, where the capacitor C discharges through the resistor R. The time constant of the circuit is given by the product RC, which determines the rate of discharge.

Figure 1.31. The simplest $R C$ circuit.
image_name:A
description:The graph labeled "A" represents the voltage across a capacitor in an RC discharge circuit over time, plotted on a linear scale. The x-axis is labeled "t" for time, and the y-axis is labeled "V" for voltage. The initial voltage at time t=0 is denoted as \( V_0 \). The graph shows an exponential decay of voltage over time, following the equation \( V = V_0 e^{-t/RC} \), where \( RC \) is the time constant of the circuit.

1. **Type of Graph and Function**: This is a time-domain waveform depicting an exponential decay.

2. **Axes Labels and Units**: The x-axis represents time \( t \) in seconds, and the y-axis represents voltage \( V \) in volts. The scale is linear.

3. **Overall Behavior and Trends**: The voltage decreases exponentially from \( V_0 \) to a lower value as time progresses. At \( t = RC \), the voltage drops to approximately 37% of its initial value, \( V_0 \).

4. **Key Features and Technical Details**: The key feature of this graph is the point at \( t = RC \), where the voltage is 37% of \( V_0 \). This point is crucial in determining the time constant of the circuit.

5. **Annotations and Specific Data Points**: The graph includes annotations indicating the mathematical expression of the voltage decay and the specific percentage (37%) of \( V_0 \) at \( t = RC \).
image_name:B
description:The graph labeled as "B" is a plot of an RC discharge waveform using a logarithmic voltage axis. It represents the voltage across the capacitor as it discharges over time in an RC circuit.

1. **Type of Graph and Function:**
- This is a time-domain waveform graph.
- It shows the exponential decay of voltage in an RC circuit.

2. **Axes Labels and Units:**
- The horizontal axis represents time, labeled as "time (seconds)," with units in seconds.
- The time is marked at intervals of RC, 2RC, 3RC, 4RC, and 5RC, where RC is the time constant.
- The vertical axis represents the voltage "V," with a logarithmic scale. The voltage is initially at 1.0 and decreases exponentially.

3. **Overall Behavior and Trends:**
- The graph shows a straight line due to the logarithmic scale, indicating an exponential decay in voltage over time.
- Initially, the voltage is at 1.0 and decreases towards zero as time increases.
- The rate of decay is determined by the time constant RC.

4. **Key Features and Technical Details:**
- The voltage decreases by approximately 63% at each time constant, which is a characteristic of exponential decay.
- The graph demonstrates the theoretical behavior of an RC discharge, where the voltage falls off rapidly at first and then more slowly.

5. **Annotations and Specific Data Points:**
- Specific time points are marked on the time axis at RC intervals, highlighting the exponential nature of the discharge.
- No specific numerical data points are annotated on the graph itself, but the general trend is clearly depicted by the straight line on the logarithmic scale.

Figure 1.32. $R C$ discharge waveform, plotted with (A) linear and (B) logarithmic voltage axes.

#### A. Time constant

The product $R C$ is called the time constant of the circuit. For $R$ in ohms and $C$ in farads, the product $R C$ is in seconds. A microfarad across 1.0 k has a time constant of 1 ms ; if the capacitor is initially charged to 1.0 V , the initial current is 1.0 mA .
image_name:Figure 1.33
description:
[
name: Vf, type: VoltageSource, value: Vf, ports: {Np: Vf, Nn: GND}
name: SW1, type: Switch, ports: {N1: Vf, N2: w1}
name: R, type: Resistor, value: R, ports: {N1: w1, N2: Vout}
name: C, type: Capacitor, value: C, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is an RC charging circuit. When the switch SW1 is closed, the capacitor C charges through the resistor R from the voltage source Vf. The output voltage across the capacitor is labeled as Vout.

Figure 1.33. $R C$ charging circuit.
Figure 1.33 shows a slightly different circuit. At time $t=0$, someone connects the battery. The equation for the circuit is then

$$
I=C \frac{d V}{d t}=\frac{V_{\mathrm{f}}-V_{\mathrm{out}}}{R}
$$

with the solution

$$
V_{\text {out }}=V_{\mathrm{f}}+A e^{-t / R C}
$$

(Please don't worry if you can't follow the mathematics. What we are doing is getting some important results, which you should remember. Later we will use the results often, with no further need for the mathematics used to derive them. For readers whose knowledge of math is somewhat, uh, rusty, the brief review in Appendix A may prove helpful.) The constant $A$ is determined by initial conditions (Figure 1.34): $V=0$ at $t=0$; therefore, $A=-V_{\mathrm{f}}$, and

$$
\begin{equation*}
V_{\mathrm{out}}=V_{\mathrm{f}}\left(1-e^{-t / R C}\right) \tag{1.21}
\end{equation*}
$$

Once again there's good intuition: as the capacitor charges up, the slope (which is proportional to current, because it's a capacitor) is proportional to the remaining voltage (because that's what appears across the resistor, producing the current); so we have a waveform whose slope decreases proportionally to the vertical distance it has still to go - an exponential.

You can turn around the last equation to figure out the time required to reach a voltage $V$ on the way to the final voltage $V_{\mathrm{f}}$. Try it! (Refer to Appendix A if you need help with logarithms.) You should get

$$
\begin{equation*}
t=R C \log _{e}\left(\frac{V_{\mathrm{f}}}{V_{\mathrm{f}}-V}\right) \tag{1.22}
\end{equation*}
$$

#### B. Decay to equilibrium

Eventually (when $t \gg R C$ ), $V$ reaches $V_{\mathrm{f}}$. (Presenting the " $5 R C$ rule of thumb": a capacitor charges or decays to
image_name:Figure 1.34
description:The graph in Figure 1.34 is a time-domain waveform representing the charging of a capacitor through a resistor, commonly referred to as an RC charging curve.

Axes Labels and Units:
- **Horizontal Axis (x-axis):** Represents time \( t \), with units typically in seconds. The axis is linear.
- **Vertical Axis (y-axis):** Represents voltage \( V \), with units in volts. The axis is also linear.

Overall Behavior and Trends:
The graph shows an exponential rise in voltage from 0 volts towards a final voltage \( V_f \). The curve starts at the origin (0,0) and asymptotically approaches \( V_f \) as time increases. The voltage reaches approximately 63% of \( V_f \) at \( t = RC \), which is a characteristic time constant for the RC circuit.

Key Features and Technical Details:
- **Exponential Equation:** The voltage \( V_{out} \) is given by the equation \( V_{out} = V_f (1 - e^{-t/RC}) \).
- **Time Constant (\( t = RC \)):** At this point, the voltage reaches about 63% of its final value \( V_f \).
- **Asymptotic Behavior:** As time \( t \) becomes much larger than \( RC \), the voltage approaches \( V_f \) but never quite reaches it.

Annotations and Specific Data Points:
- The graph is annotated with the 63% marker, indicating the voltage level at \( t = RC \).
- A dashed line represents the final voltage \( V_f \), showing the asymptotic limit of the curve.

This graph effectively illustrates the concept of an RC time constant and how a capacitor charges over time in an RC circuit, reaching close to its final voltage after a few time constants.

Figure 1.34. $R C$ charging waveform.
image_name:Figure 1.35
description:The graph in Figure 1.35 consists of two parts, illustrating the behavior of an RC circuit when driven by a square wave input.

1. **Type of Graph and Function:**
- The graph is a time-domain waveform showing the input and output voltages over time in an RC circuit.

2. **Axes Labels and Units:**
- The horizontal axis represents time (t), though specific units are not provided.
- The vertical axes represent voltage, with the top graph labeled as \( V_{in} \) and the bottom graph as \( V_{out} \).
- The input waveform is a square wave, and the output waveform is the response of the RC circuit to this input.

3. **Overall Behavior and Trends:**
- **Input (\( V_{in} \)):** The input waveform is a square wave with two different frequencies depicted. The left side shows a higher frequency square wave, and the right side shows a lower frequency square wave.
- **Output (\( V_{out} \)):** The output waveform shows the response of the RC circuit. For the higher frequency input, the output is a series of exponential charging and discharging curves, creating a waveform that resembles a sawtooth pattern. For the lower frequency input, the output waveform has a more pronounced exponential rise and fall, indicating that the circuit has more time to charge and discharge closer to the input voltage levels.

4. **Key Features and Technical Details:**
- The output waveform does not reach the full amplitude of the input square wave due to the time constant of the RC circuit, which limits the rate of voltage change.
- The waveform transitions are smoother and less sharp than the input, characteristic of the exponential behavior of charging and discharging in RC circuits.

5. **Annotations and Specific Data Points:**
- The graph includes a notation indicating that the right side of the input is at a 'lower frequency,' which affects the output waveform's shape and amplitude.

This graph effectively demonstrates how an RC circuit responds to square wave inputs of different frequencies, highlighting the effect of the RC time constant on the output waveform's shape and amplitude.

Figure 1.35. Output (lower waveforms) across a capacitor, when driven by square waves through a resistor.
within $1 \%$ of its final value in five time constants.) If we then change the battery voltage to some other value (say, 0 V ), $V$ will decay toward that new value with an exponential $e^{-t / R C}$. For example, replacing the battery's step input from 0 to $+V_{\mathrm{f}}$ with a square-wave input $V_{\mathrm{in}}(t)$ would produce the output shown in Figure 1.35.

Exercise 1.16. Show that the rise time (the time required for going from $10 \%$ to $90 \%$ of its final value) of this signal is $2.2 R C$.

You might ask the obvious next question: what about $V(t)$ for arbitrary $V_{\text {in }}(t)$ ? The solution involves an inhomogeneous differential equation and can be solved by standard methods (which are, however, beyond the scope of this book). You would find

$$
V(t)=\frac{1}{R C} \int_{-\infty}^{t} V_{\mathrm{in}}(\tau) e^{-(t-\tau) / R C} d \tau
$$

That is, the $R C$ circuit averages past history at the input with a weighting factor of

$$
e^{-\Delta t / R C}
$$

In practice, you seldom ask this question. Instead, you deal in the frequency domain, in which you ask how much of each frequency component present in the input gets through. We will get to this important topic soon (§1.7). Before we do, though, there are a few other interesting
circuits we can analyze simply with this time-domain approach.
image_name:Figure 1.36
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: R1, type: Resistor, value: R1, ports: {N1: Vin, N2: V(t)}
name: R2, type: Resistor, value: R2, ports: {N1: V(t), N2: GND}
name: C, type: Capacitor, value: C, ports: {Np: V(t), Nn: GND}
]
extrainfo:This circuit is an RC low-pass filter with input voltage Vin and output across the capacitor C. It uses the Thévenin equivalent to simplify the analysis.

Figure 1.36. Looks complicated, but it's not! (Thévenin to the rescue.)

#### C. Simplification by Thévenin equivalents

We could go ahead and analyze more complicated circuits by similar methods, writing down the differential equations and trying to find solutions. For most purposes it simply isn't worth it. This is as complicated an $R C$ circuit as we will need. Many other circuits can be reduced to it; take, for example, the circuit in Figure 1.36. By just using the Thévenin equivalent of the voltage divider formed by $R_{1}$ and $R_{2}$, you can find the output $V(t)$ produced by a step input for $V_{\text {in }}$.

Exercise 1.17. In the circuit shown in Figure 1.36, $R_{1}=R_{2}=10 \mathrm{k}$, and $C=0.1 \mu \mathrm{~F}$. Find $V(t)$ and sketch it.
image_name:Figure 1.37 CMOS buffers
description:
[
name: 1G17, type: Inverter, ports: {In: A, Out: A1}
name: Resistor, type: Resistor, value: 15k, ports: {N1: A1, N2: B}
name: Capacitor, type: Capacitor, value: 1000pF, ports: {Np: B, Nn: GND}
name: 1G17, type: Inverter, ports: {In: B, Out: C}
]
extrainfo:The circuit is a time-delay circuit using CMOS buffers and an RC network. The waveform shows a delayed response at point B due to the RC time constant, with a delay of 10 microseconds between the input and output signals.
image_name:A: input, B: RC, C: output
description:The graph provided represents a time-domain waveform analysis of an RC circuit with CMOS buffers. It consists of three distinct waveforms labeled A, B, and C, each representing different stages of the circuit's operation.

1. **Type of Graph and Function:**
- This is a time-domain waveform graph showing the response of an RC circuit to a step input signal.

2. **Axes Labels and Units:**
- The horizontal axis represents time, measured in microseconds (μs).
- The vertical axis represents voltage, although specific voltage levels are not labeled on the graph.

3. **Overall Behavior and Trends:**
- **A: Input** shows a square wave input signal with a sharp rise and fall, maintaining a constant high level between transitions. The duration of the high state is approximately 10 μs.
- **B: RC** demonstrates the RC circuit's response to the input signal. It shows a gradual rise and fall, characteristic of the exponential charging and discharging of the capacitor in the RC circuit.
- **C: Output** mirrors the input waveform but is delayed compared to the input, indicating the effect of the RC time constant on the signal propagation.

4. **Key Features and Technical Details:**
- The RC waveform (B) shows a typical exponential behavior with a time constant determined by the resistor and capacitor values (15kΩ and 1000pF, respectively).
- The delay observed in the output (C) relative to the input (A) is approximately 10 μs, corresponding to the time it takes for the RC circuit to charge and discharge.

5. **Annotations and Specific Data Points:**
- The graph includes dashed vertical lines indicating the transitions of the input signal and the corresponding delays in the output signal.
- The time delay between the input and output is explicitly marked as 10 μs, which is consistent with the calculated RC time constant.

Overall, this graph effectively illustrates how an RC circuit can introduce a time delay in a digital signal, a common application in signal processing and electronic timing circuits.

Figure 1.37. Producing a delayed digital waveform with the help of an $R C$ and a pair of LVC-family logic buffers (tiny parts with a huge part number: SN74LVC1G17DCKR!).

#### D. A circuit example: time-delay circuit

Let's take a short detour to try out these theoretical ideas on a couple of real circuits. Textbooks usually avoid such pragmatism, especially in early chapters, but we think it's fun to apply electronics to practical applications. We'll need to introduce a few "black-box" components to get the job done, but you'll learn about them in detail later, so don't worry.

We have already mentioned logic levels, the voltages that digital circuits live on. Figure 1.37 shows an application of capacitors to produce a delayed pulse. The triangular symbols are "CMOS ${ }^{24}$ buffers." They give a HIGH output if the input is HIGH (more than one-half the dc powersupply voltage used to power them), and vice versa. The first buffer provides a replica of the input signal, but with low source resistance, to prevent input loading by the $R C$ (recall our earlier discussion of circuit loading in §1.2.5A). The $R C$ output has the characteristic decays and causes the output buffer to switch $10 \mu \mathrm{~s}$ after the input transitions (an $R C$ reaches $50 \%$ output after a time $t=0.7 R C$ ). In an actual application you would have to consider the effect of the buffer input threshold deviating from one-half the supply voltage, which would alter the delay and change the output pulse width. Such a circuit is sometimes used to delay a pulse so that something else can happen first. In designing circuits you try not too often to rely on tricks like this, but they're occasionally handy.

#### E. Another circuit example: "One Minute of Power"

Figure 1.38 shows another example of what can be done with simple $R C$ timing circuits. The triangular symbol is a comparator, something we'll treat in detail later, in Chapters 4 and 10 ; all you need to know, for now, is that (a) it is an IC (containing a bunch of resistors and transistors), (b) it is powered from some positive dc voltage that you connect to the pin labeled " $V_{+}$," and (c) it drives its output (the wire sticking out to the right) either to $V_{+}$or to ground, depending on whether the input labeled " + " is more or less positive than the input labeled "-," respectively. (These are called the non-inverting and the inverting inputs, respectively.) It doesn't draw any current from its inputs, but it happily drives loads that require up to 20 mA or so. And a comparator is decisive: its output is either "HIGH" (at $V_{+}$) or "LOW" (ground).

Here's how the circuit works: the voltage divider $R_{3} R_{4}$ holds the ( - ) input at $37 \%$ of the supply voltage, in this case about +1.8 V ; let's call that the "reference voltage."

[^19]image_name:Figure 1.38
description:
[
name: R1, type: Resistor, value: 1k, ports: {N1: V+, N2: InP(A1)}
name: R2, type: Resistor, value: 6.2M, ports: {N1: InP(A1), N2: GND}
name: R3, type: Resistor, value: 620k, ports: {N1: V+, N2: InN(A1)}
name: R4, type: Resistor, value: 360k, ports: {N1: InN(A1), N2: GND}
name: C1, type: Capacitor, value: 10μF, ports: {Np: InP(A1), Nn: GND}
name: A1, type: OpAmp, value: TLC 3702, ports: {InP: InP(A1), InN: InN(A1), OutP: Out(A1), OutN: GND}
]
extrainfo:The circuit is a timing circuit using a comparator TLC 3702. It generates a delayed digital waveform with a rise time determined by the RC network of R1 and C1. The reference voltage for the comparator is set by the voltage divider R3 and R4.

Figure 1.38. $R C$ timing circuit: one push $\rightarrow$ one minute!.
image_name:Figure 1.39
description:The graph in Figure 1.39 consists of two time-domain waveforms. The top waveform represents the voltage across capacitor $C_1$ ($V_{C1}$) in volts, plotted against time. The x-axis is labeled as time, though no specific units are provided on the graph itself, and the y-axis is labeled with voltage values, ranging from 0 to +5 volts.

1. **Top Waveform ($V_{C1}$):**
- **Initial Condition:** The waveform starts at 0 volts.
- **Switch Closure:** Upon the closure of the switch (indicated by a vertical line), $V_{C1}$ rapidly rises to +5 volts.
- **Exponential Decay:** After reaching +5 volts, the voltage across $C_1$ begins to decay exponentially.
- **Reference Voltage ($V_{ref}$):** The waveform passes through a reference voltage line marked at +1.8 volts. This indicates the threshold at which the comparator changes its output state.
- **Time Constant:** The exponential decay is characterized by a time constant, but specific values are not annotated on the graph.

2. **Bottom Waveform (Comparator Output):**
- **Initial State:** The comparator output is initially at a low state (ground level).
- **State Change:** As $V_{C1}$ exceeds the reference voltage of +1.8 volts, the comparator output switches to a high state (+5 volts).
- **Duration:** The high state is maintained for approximately 1 minute, as annotated on the graph.
- **Return to Low State:** After the decay of $V_{C1}$ below the reference voltage, the comparator output returns to the low state.

Overall, the graph illustrates the behavior of a timing circuit where the charging and discharging of the capacitor $C_1$ determines the output state of the comparator. The rise and fall of $V_{C1}$ and its crossing of the reference voltage threshold are critical for the operation of the circuit, producing a delayed digital waveform at the comparator output.

Figure 1.39. Producing a delayed digital waveform for the circuit of Figure 1.38. The voltage $V_{C 1}$ has a rise time of $R_{1} C_{1} \approx 10 \mathrm{~ms}$.

So if the circuit has been sitting there for a while, $C_{1}$ is fully discharged, and the comparator's output is at ground. When you push the START button momentarily, $C_{1}$ charges quickly ( 10 ms time constant) to +5 V , which makes the comparator's output switch to +5 V ; see Figure 1.39. After the button is released, the capacitor discharges exponentially toward ground, with a time constant of $\tau=R_{2} C_{1}$, which we've set to be 1 minute. At that time its voltage crosses the reference voltage, so the comparator's output switches rapidly back to ground. (Note that we've conveniently chosen the reference voltage to be a fraction $1 / e$ of $V_{+}$, so it takes exactly one time constant $\tau$ for that to happen. For $R_{2}$ we used the closest standard value to $6 \mathrm{M} \Omega$; see Appendix C.) The bottom line is that the output spends 1 minute at +5 V , after the button is pushed.

We'll add a few details shortly, but first let's use the output to do some interesting things, which are shown in Figures 1.40A-D. You can make a self-stopping flashlight key fob by connecting its output to an LED; you need to put a resistor in series, to set the current (we'll say much more about this later). If you prefer to make some noise, you could connect a piezo beeper to beep continuously (or intermittently) for a minute (this might be an end-of-cycle signal for a clothes dryer). Another possibility is to attach a small electromechanical relay, which is just an electrically operated mechanical switch, to provide a pair of contacts
that can activate pretty much any load you care to switch on and off. The use of a relay has the important property that the load - the circuit being switched by the relay - is electrically isolated from the +5 V and ground of the timing circuit itself.
image_name:A.
description:The circuit diagram A consists of a resistor in series with an LED. The resistor is connected to the power supply (VDD), and the LED is connected to ground. This setup is typically used to limit current through the LED.

image_name:A
description:The circuit diagram A consists of a resistor in series with an LED. The resistor is connected to the power supply (VDD), and the LED is connected to ground. This setup is typically used to limit current through the LED.
image_name:The circuit diagram B includes a piezo buzzer connected between the output node (Vout) and ground (GND). This setup is used to produce sound when the output voltage is applied.
image_name:C
description:The circuit diagram C includes a piezo buzzer connected between the output node (Vout) and ground (GND). This setup is typically used to produce sound when a voltage is applied to the output node.

B.
image_name:C
description:The piezo buzzer is connected between the output node (Vout) and ground (GND). It is used to produce sound when voltage is applied to Vout.

C.
image_name:C.
description:The circuit diagram C includes a mechanical relay and a solid-state relay. The mechanical relay (COTO 8L01-05) is connected between Vcc and ground, with a diode in parallel for protection. The solid-state relay (Crydom D2450) is used to control an air compressor, and it is connected in series with a resistor (270 ohms) to a control node. The diagram illustrates how to drive different types of loads using relays.
image_name:D.
description:The circuit diagram D includes a solid-state relay (Crydom D2450) used to control an air compressor. The relay is activated by a 270-ohm resistor connected to a control signal. The relay is powered by 110/220 VAC from a wall plug, and it isolates the control circuit from the high voltage AC circuit. A diode is used to protect the relay coil from voltage spikes.

Figure 1.40. Driving interesting stuff from the output of the timer circuit in Figure 1.38.

Finally, for turning serious industrial machinery on and off, you would probably use a hefty solid-state relay (SSR, §12.7), which has within it an infrared LED coupled to an ac switching device known as a triac. When activated, the triac acts as an excellent mechanical switch, capable of switching many amperes, and (like the electromechanical relay) is fully isolated electrically from its input circuit. The example shows this thing hooked to an air compressor, so your friends will get a minute's worth of air to inflate their tires at your home "gas station" (literally!) after they drop a quarter into your coin-initiated timer. You could do an analogous thing with a coin-operated hot shower (but, hey, we get only one minute?!).

Some details: (a) in the circuit of Figure 1.38 you could omit $R_{1}$ and the circuit would still work, but there would be a large transient current when the discharged capacitor was initially connected across the +5 V supply (recall $I=C d V / d t$ : here you would be trying to produce 5 V of " $d V$ " in roughly 0 s of " $d t$ "). By adding a series resistor $R_{1}$ you limit the peak current to a modest 5 mA while charging
the capacitor fast enough ( $>99 \%$ in $5 R C$ time constants, or 0.05 s ). (b) The comparator output would likely bounce around a bit (see Figure 4.31), just as the (+) input crosses the reference voltage in its leisurely exponential promenade toward ground, owing to unavoidable bits of electrical noise. To fix this problem you usually see the circuit arranged so that some of the output is coupled back to the input in a way that reinforces the switching (this is officially called hysteresis, or positive feedback; we'll see it in Chapters 4 and 10). (c) In electronic circuits it's always a good idea to bypass the dc supply by connecting one or more capacitors between the dc "rail" and ground. The capacitance is noncritical - values of $0.1 \mu \mathrm{~F}$ to $10 \mu \mathrm{~F}$ are commonly used; see §1.7.16A.

Our simple examples above all involved turning some load on and off. But there are other uses for an electronic logic signal, like the output of the comparator, that is in one of two possible binary states, called HIGH and LOw (in this case +5 V and ground), 1 and 0 , or TRUE and false. For example, such a signal can enable or disable the operation of some other circuit. Imagine that the opening of a car door triggers our 1 min HIGH output, which then enables a keypad to accept a security code so you can start the car. After a minute, if you haven't managed to type the magic code, it shuts off, thus ensuring a certain minimum of operator sobriety.
image_name:A
description:
[
name: C, type: Capacitor, value: C, ports: {Np: Vin(t), Nn: GND}
]
extrainfo:The circuit in Figure 1.41A is a perfect differentiator circuit with a capacitor connected to the input voltage Vin(t) and the ground. It differentiates the input signal over time.
image_name:B
description:
[
name: C, type: Capacitor, value: C, ports: {Np: Vin(t), Nn: N1}
name: R, type: Resistor, value: R, ports: {N1: N1, N2: GND}
]
extrainfo:This is an approximate differentiator circuit. The capacitor C is connected between the input node Vin(t) and an intermediate node N1. The resistor R is connected between node N1 and ground. The output is taken from node N1, which is also connected to the resistor R, to the output node Vout(t).

Figure 1.41. Differentiators. A. Perfect (except it has no output terminal). B. Approximate (but at least it has an output!).

### 1.4.3 Differentiators

You can make a simple circuit that differentiates an input signal; that is, $V_{\text {out }} \propto d V_{\text {in }} / d t$. Let's take it in two steps.

1. First look at the (impractical) circuit in Figure 1.41A: The input voltage $V_{\text {in }}(t)$ produces a current through the capacitor of $I_{\text {cap }}=C d V_{\text {in }} / d t$. That's just what we want - if we
could somehow use the current through $C$ as our "output"! But we can't. ${ }^{25}$
2. So we add a small resistor from the low side of the capacitor to ground, to act as a "current-sensing" resistor (Figure 1.41B). The good news is that we now have an output proportional to the current through the capacitor. The bad news is that the circuit is no longer a perfect mathematical differentiator. That's because the voltage across $C$ (whose derivative produces the current we are sensing with $R$ ) is no longer equal to $V_{\text {in }}$; it now equals the difference between $V_{\text {in }}$ and $V_{\text {out }}$.Here's how it goes: the voltage across $C$ is $V_{\text {in }}-V_{\text {out }}$, so

$$
I=C \frac{d}{d t}\left(V_{\text {in }}-V_{\text {out }}\right)=\frac{V_{\text {out }}}{R}
$$

If we choose $R$ and $C$ small enough so that $d V_{\text {out }} / d t \ll$ $d V_{\text {in }} / d t$, then

$$
C \frac{d V_{\mathrm{in}}}{d t} \approx \frac{V_{\mathrm{out}}}{R}
$$

or

$$
V_{\text {out }}(t) \approx R C \frac{d}{d t} V_{\text {in }}(t)
$$

That is, we get an output proportional to the rate of change of the input waveform.

To keep $d V_{\text {out }} / d t \ll d V_{\text {in }} / d t$, we make the product $R C$ small, taking care not to "load" the input by making $R$ too small (at the transition the change in voltage across the capacitor is zero, so $R$ is the load seen by the input). We will have a better criterion for this when we look at things in the frequency domain (\$1.7.10). If you drive this circuit with a square wave, the output will be as shown in Figure 1.42.
image_name:Figure 1.42
description:The graph in Figure 1.42 depicts a time-domain waveform analysis of a differentiator circuit's response to a square wave input. The graph is divided into two sections, with the top section representing the input voltage ($V_{in}$) and the bottom section showing the output voltage ($V_{out}$). Both axes are labeled with voltage, but no specific units are provided, suggesting a general conceptual illustration rather than a precise measurement.

**Type of Graph and Function:**
- The graph is a time-domain waveform showing the input and output of a differentiator circuit.

**Axes Labels and Units:**
- The vertical axis is labeled with voltage for both input ($V_{in}$) and output ($V_{out}$).
- The horizontal axis represents time, though it is not explicitly labeled with units.

**Overall Behavior and Trends:**
- The input waveform ($V_{in}$) is a square wave with sharp transitions between high and low states.
- The output waveform ($V_{out}$) exhibits spikes corresponding to the transitions of the input square wave. These spikes are characteristic of a differentiator circuit, which emphasizes rapid changes in the input signal.

**Key Features and Technical Details:**
- The output waveform shows positive spikes when the input transitions from low to high and negative spikes when the input transitions from high to low.
- Between these spikes, the output voltage returns to zero, indicating no change in the input signal.

**Annotations and Specific Data Points:**
- No specific numerical values or annotations are provided in the graph, as it serves to illustrate the general behavior of a differentiator circuit in response to a square wave input.

Figure 1.42. Output waveform (bottom) from differentiator driven by a square wave.

Differentiators are handy for detecting leading edges and trailing edges in pulse signals, and in digital circuitry you sometimes see things like those depicted in Figure 1.43. The $R C$ differentiator generates spikes at the transitions of the input signal, and the output buffer converts

[^20]image_name:Leading-edge detector
description:
[
name: C1, type: Capacitor, value: 100pF, ports: {Np: A1, Nn: B}
name: R1, type: Resistor, value: 10k, ports: {N1: B, N2: GND}
name: U1, type: Inverter, ports: {In: A, Out: A1}
name: U2, type: Inverter, ports: {In: B, Out: C}
]
extrainfo:The circuit is a leading-edge detector using an RC differentiator with a time constant of 1μs. The input is a square wave, and the output is a short square-topped pulse.
image_name:A: input
description:The graph labeled "A: input" depicts a time-domain waveform of a square wave input signal. The horizontal axis represents time, while the vertical axis represents voltage. The waveform is characterized by sharp transitions between high and low voltage levels, typical of a square wave. The waveform remains at a high level for a period before abruptly dropping to a low level, and then rising back to a high level, indicating the periodic nature of the input signal. This waveform serves as the input to a differentiator circuit, which is designed to detect these transitions and convert them into sharp voltage spikes at the output.
image_name:B: RC
description:The graph illustrates the behavior of an RC differentiator circuit driven by a square wave input. It consists of three sections labeled A, B, and C, representing different stages of the signal.

1. **Type of Graph and Function:**
- The graph is a time-domain waveform plot, showcasing the input and output signals of an RC differentiator circuit.

2. **Axes Labels and Units:**
- The horizontal axis represents time, though specific units are not labeled on the graph. The vertical axis represents voltage, with no specific units or scale provided.

3. **Overall Behavior and Trends:**
- **A: Input Signal** - The input is a square wave with sharp transitions between high and low states. It is characterized by a flat top and bottom, indicating constant voltage levels during the high and low phases.
- **B: RC Differentiator Output** - The output at point B shows a rapid spike at the rising edge of the input square wave, followed by an exponential decay back towards zero. This behavior is mirrored at the falling edge, with a negative spike followed by a similar decay. The time constant for this decay is noted as 1 microsecond (µs).
- **C: Final Output** - The output at point C is a processed version of the signal at B, showing short square-topped pulses at the transitions of the input signal, effectively detecting the leading and trailing edges.

4. **Key Features and Technical Details:**
- The RC circuit consists of a 100 pF capacitor and a 10 kΩ resistor, determining the time constant of 1 µs for the differentiator.
- The spikes at point B are indicative of the differentiator's function, highlighting sharp changes in the input signal.

5. **Annotations and Specific Data Points:**
- An annotation on the graph indicates the time constant of the RC circuit as 1 µs.
- The waveform at point B is characterized by a rapid rise and fall, with exponential decay, marking the circuit's response to input transitions.

This graph effectively demonstrates the differentiator's ability to convert a square wave input into sharp pulses, emphasizing the detection of signal transitions at both the leading and trailing edges.

Figure 1.43. Leading-edge detector.
the spikes to short square-topped pulses. In practice, the negative spike will be small because of a diode (a handy device discussed in §1.6) built into the buffer.

To inject some real-world realism here, we hooked up and made some measurements on a differentiator that we configured for high-speed signals. For this we used $C=1 \mathrm{pF}$ and $R=50 \Omega$ (the latter is the world-wide standard for highspeed circuits, see Appendix H), we drove it with a 5 V step of settable slew rate (i.e., $d V / d t$ ). Figure 1.44 shows both input and output waveforms, for three choices of $d V_{\text {in }} / d t$. At these speeds (note the horizontal scale: 4 nanoseconds per division!) circuits often depart from ideal performance, as can be seen in the fastest risetime. The two slower steps show reasonable behavior; that is, a flat-top output waveform during the input's upward ramp; check for yourself that the output amplitude is correctly predicted by the formula.

#### A. Unintentional capacitive coupling

Differentiators sometimes crop up unexpectedly, in situations where they're not welcome. You may see signals like those shown in Figure 1.45. The first case is caused by a square wave somewhere in the circuit coupling capacitively to the signal line you're looking at; that might indicate a missing resistor termination on your signal line. If not, you must either reduce the source resistance of the signal line or find a way to reduce capacitive coupling from the offending square wave. The second case is typical of what you might see when you look at a square wave, but have a
image_name:Figure 1.44
description:The graph in Figure 1.44 illustrates the behavior of three fast step waveforms as they pass through an RC differentiator circuit. The top part of the graph shows the differentiator output, while the bottom part depicts the input step signals.

1. **Type of Graph and Function:**
- The graph is a time-domain waveform plot showing the response of an RC differentiator circuit to different input step signals.

2. **Axes Labels and Units:**
- The horizontal axis represents time, marked as "4 ns/div," indicating a linear scale with each division corresponding to 4 nanoseconds.
- The vertical axis is split into two parts:
- The lower part shows the input step with a scale of "2 V/div," representing voltage in volts.
- The upper part shows the differentiator output with a scale of "10 mV/div," representing voltage in millivolts.

3. **Overall Behavior and Trends:**
- The input step signals have different rates of voltage change, marked as 0.25 V/ns, 0.5 V/ns, and 1 V/ns. These are linear ramps that increase over time.
- The differentiator output shows a characteristic spike for each input step, with the peak amplitude increasing as the rate of voltage change increases.
- After the spike, the output waveform quickly returns to a baseline level, showing the transient nature of the differentiator output.

4. **Key Features and Technical Details:**
- The differentiator output peaks are sharp and decrease in amplitude as the rate of change of the input step decreases, demonstrating the differentiating effect of the RC network.
- The circuit diagram inset shows a 1 pF capacitor and a 50 Ω resistor, which form the RC differentiator.
- The imperfections in the waveform are likely due to component tolerances and measurement limitations, as noted in the context.

5. **Annotations and Specific Data Points:**
- The graph has annotations for the rate of change of the input steps (dV/dt), which are crucial for understanding the differentiator's response.
- The differentiator output is sensitive to these rates, highlighting the importance of the RC time constant in shaping the output waveform.
image_name:RC network
description:The circuit is an RC differentiator network. The input step voltage is applied to the capacitor, and the output is taken across the resistor. The graph shows the differentiator output for various dV/dt values of the input step, illustrating the effect of the RC network on the waveform shape.

Figure 1.44. Three fast step waveforms, differentiated by the $R C$ network shown. For the fastest waveform ( $10^{9}$ volts per second!), imperfections in the components and measuring instruments cause deviation from the ideal.
broken connection somewhere, usually at the scope probe. The very small capacitance of the broken connection combines with the scope input resistance to form a differentiator. Knowing that you've got a differentiated "something" can help you find the trouble and eliminate it.
image_name:Figure 1.45
description:The graph in Figure 1.45 appears to illustrate two examples of unintentional capacitive coupling through two waveform diagrams. The upper waveform is a sinusoidal curve with vertical lines intersecting the curve at regular intervals, which might indicate measurement points or potential deviations due to capacitive coupling effects. This sinusoidal waveform represents a signal that is likely being affected by capacitive coupling, causing slight distortions or deviations from the ideal sinusoidal shape.

The lower waveform is a series of step-like waveforms that seem to represent the differentiated response of the upper sinusoidal waveform due to the capacitive coupling. The step-like nature of this waveform suggests that the original sinusoidal signal is being converted into a series of rapid voltage changes, which is characteristic of a differentiated signal.

Type of Graph and Function:
- The graph shows time-domain waveforms.

Axes Labels and Units:
- The axes are not labeled in the image, but it is implied that the horizontal axis represents time and the vertical axis represents voltage or current.

Overall Behavior and Trends:
- The upper waveform is a smooth sinusoidal curve, indicating a periodic signal.
- The lower waveform consists of sharp steps, indicating rapid changes in the signal, typical of a differentiated waveform.

Key Features and Technical Details:
- The periodic nature of the upper waveform suggests it is a continuous signal.
- The step-like nature of the lower waveform indicates differentiation, likely due to unintentional capacitive coupling.

Annotations and Specific Data Points:
- Vertical lines on the upper waveform may highlight measurement points or deviations.
- No specific numerical data points or annotations are provided.

Figure 1.45. Two examples of unintentional capacitive coupling.

### 1.4.4 Integrators

If $R C$ circuits can take derivatives, why not integrals? As before, let's take it in two steps.

1. Imagine that we have an input signal that is a timevarying current versus time, $I_{\mathrm{in}}(t)$ (Figure 1.46A). ${ }^{26}$ That input current is precisely the current through the capacitor, so $I_{\text {in }}(t)=C d V(t) / d t$, and therefore $V(t)=\int I_{\text {in }}(t) d t$.

image_name:A
description:
[
name: C, type: Capacitor, value: C, ports: {Np: Vout(t), Nn: GND}
]
extrainfo:Diagram A represents a perfect integrator using a capacitor with a current input signal Iin(t). Diagram B represents an approximate integrator with a resistor converting a voltage input signal Vin(t) to a current.
image_name:B
description:
[
name: R, type: Resistor, value: R, ports: {N1: Vin, N2: Vout}
name: C, type: Capacitor, value: C, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit diagram B represents an integrator circuit where a resistor R is used to convert the input voltage Vin(t) into a current, which then charges the capacitor C. The output voltage Vout(t) is the integrated value of the input signal.

Figure 1.46. Integrator. A. Perfect (but requires a current input signal). B. Approximate (see text).

That's just what we wanted! Thus a simple capacitor, with one side grounded, is an integrator, if we have an input signal in the form of a current $I_{\text {in }}(t)$. Most of the time we don't, though.
2. So we connect a resistor in series with the more usual input voltage signal $V_{\text {in }}(t)$, to convert it to a current (Figure 1.46B). The good news is that it works, sort of. The bad news is that the circuit is no longer a perfect integrator. That's because the current through $C$ (whose integral produces the output voltage) is no longer proportional to $V_{\text {in }}$; it is now proportional to the difference between $V_{\text {in }}$ and $V$. Here's how it goes: the voltage across $R$ is $V_{\text {in }}-V$, so

$$
I=C \frac{d V}{d t}=\frac{V_{\mathrm{in}}-V}{R}
$$

If we manage to keep $V \ll V_{\text {in }}$, by keeping the product $R C$ large, ${ }^{27}$ then

$$
C \frac{d V}{d t} \approx \frac{V_{\mathrm{in}}}{R}
$$

or

$$
V(t)=\frac{1}{R C} \int^{t} V_{\text {in }}(t) d t+\text { constant. }
$$

That is, we get an output proportional to the integral over time of the input waveform. You can see how the approximation works for a square-wave input: $V(t)$ is then the exponential charging curve we saw earlier (Figure 1.47). The first part of the exponential is a ramp, the integral of a constant; as we increase the time constant $R C$, we pick off a smaller part of the exponential, i.e., a better approximation to a perfect ramp.

Note that the condition $V \ll V_{\text {in }}$ is the same as saying that $I$ is proportional to $V_{\text {in }}$, which was our first integrator

[^22]image_name:Figure 1.47
description:The graph in Figure 1.47 consists of two separate plots, both representing voltage over time, illustrating the behavior of an integrator circuit.

1. **Type of Graph and Function:**
- The graphs are time-domain waveforms, demonstrating the voltage response of an integrator circuit.

2. **Axes Labels and Units:**
- Both graphs have a horizontal axis labeled as 't,' representing time.
- The vertical axis is labeled as 'V,' representing voltage.
- The input voltage is denoted as \( V_{\text{in}} \), and the output voltage as \( V_{\text{out}} \).

3. **Overall Behavior and Trends:**
- The first graph shows an exponential charging curve. \( V_{\text{out}} \) starts at zero and rises towards \( V_{\text{in}} \) but does not reach it within the time frame shown.
- The second graph depicts a straight line, representing \( V_{\text{out}} \) as a linear ramp over time, which is the ideal behavior of an integrator.

4. **Key Features and Technical Details:**
- In the first graph, \( V_{\text{out}} \) initially rises sharply and then gradually levels off as it approaches \( V_{\text{in}} \), illustrating the exponential nature of the charging curve.
- The second graph shows \( V_{\text{out}} \) increasing linearly, indicating a constant rate of change, which is a characteristic of a perfect ramp.
- A note indicates a 10% error at about 10% of \( V_{\text{in}} \), highlighting where the approximation diverges from ideal behavior.

5. **Annotations and Specific Data Points:**
- The first graph includes a circular marker to emphasize the exponential curve.
- The second graph is annotated with a note about the error, providing insight into the accuracy of the approximation at low output voltages.

Figure 1.47. Integrator approximation is good when $V_{\text {out }} \ll V_{\text {in }}$.
circuit. A large voltage across a large resistance approximates a current source and, in fact, is frequently used as one.

Later, when we get to operational amplifiers and feedback, we will be able to build integrators without the restriction $V_{\text {out }} \ll V_{\text {in }}$. They will work over large frequency and voltage ranges with negligible error.

The integrator is used extensively in analog computation. It is a useful subcircuit that finds application in control systems, feedback, analog-digital conversion, and waveform generation.

#### A. Ramp generators

At this point it is easy to understand how a ramp generator works. This nice circuit is extremely useful, for example in timing circuits, waveform and function generators, analog oscilloscope sweep circuits, and analog-digital conversion circuitry. The circuit uses a constant current to charge a capacitor (Figure 1.48). From the capacitor equation $I=$ $C(d V / d t)$, you get $V(t)=(I / C) t$. The output waveform is as shown in Figure 1.49. The ramp stops when the current source "runs out of voltage," i.e., reaches the limit of its compliance. On the same figure is shown the curve for a simple $R C$, with the resistor tied to a voltage source equal to the compliance of the current source, and with $R$ chosen so that the current at zero output voltage is the same as that of the current source. (Real current sources generally have output compliances limited by the power-supply voltages used in making them, so the comparison is realistic.) In the next chapter, which deals with transistors, we will design some current sources, with some refinements to follow in the chapters on operational amplifiers (op-amps) and FETs. Exciting things to look forward to!

Exercise 1.18. A current of 1 mA charges a $1 \mu \mathrm{~F}$ capacitor. How long does it take the ramp to reach 10 volts?
image_name:Figure 1.48
description:
[
name: I, type: CurrentSource, value: I, ports: {Np: GND, Nn: OUTPUT}
name: C, type: Capacitor, value: C, ports: {Np: OUTPUT, Nn: GND}
]
extrainfo:A constant current source charges a capacitor, generating a ramp voltage waveform at the output node V(t). The circuit illustrates the principle of constant-current charging.

Figure 1.48. A constant-current source charging a capacitor generates a ramp voltage waveform.
image_name:Figure 1.49
description:The graph in Figure 1.49 illustrates the difference between constant-current charging ("IC") and RC charging of a capacitor. The graph is a time-domain waveform plot, with the x-axis representing time (t) and the y-axis representing voltage (V). The voltage is measured in relation to the supply voltage (Vsupply), which is marked as a horizontal line on the graph.

Two curves are plotted:

1. **"IC" Curve**: This curve represents the voltage across a capacitor when charged by a constant current source. It is a linear ramp, indicating a steady increase in voltage over time, reaching the supply voltage (Vsupply) at a certain point.

2. **RC Curve**: This curve represents the voltage across a capacitor when charged through a resistor (RC charging). It shows an exponential rise, starting from zero and asymptotically approaching the supply voltage (Vsupply). This curve is initially less steep compared to the "IC" curve and gradually flattens as it approaches the supply voltage.

**Overall Behavior and Trends**:
- The "IC" curve is linear, indicating a constant rate of voltage increase.
- The RC curve shows an exponential behavior, typical of RC charging, characterized by a decreasing rate of voltage increase as it approaches the supply voltage.

**Key Features**:
- The intersection of the "IC" curve with the supply voltage line marks the point where the capacitor is fully charged in constant-current mode.
- The RC curve never actually reaches the supply voltage but gets infinitesimally close over time.

This graph effectively illustrates the difference in charging profiles between constant-current and RC charging methods, highlighting the faster and more linear charging characteristic of the constant-current method compared to the exponential, time-dependent nature of RC charging.

Figure 1.49. Constant-current charging (with finite compliance) versus $R C$ charging.

### 1.4.5 Not quite perfect...

Real capacitors (the kind you can see, and touch, and pay money for) generally behave according to theory; but they have some additional "features" that can cause problems in some demanding applications. For example, all capacitors exhibit some series resistance (which may be a function of frequency), and some series inductance (see the next section), along with some frequency-dependent parallel resistance. Then there's a "memory" effect (known as dielectric absorption), which is rarely discussed in polite society: if you charge a capacitor up to some voltage $V_{0}$ and hold it there for a while, and then discharge it to 0 V , then when you remove the short across its terminals it will tend to drift back a bit toward $V_{0}$.

Don't worry about this stuff, for now. We'll treat in detail these effects (and other oddities of real-world components) in the advanced topics Chapter $1 x$.

## 1.5 Inductors and transformers

### 1.5.1 Inductors

If you understand capacitors, you shouldn't have great trouble with inductors (Figure 1.50). They're closely related to capacitors: the rate of current change in an inductor is proportional to the voltage applied across it (for a capacitor it's the other way around - the rate of voltage change is proportional to the current through it). The defining equation for an inductor is

$$
\begin{equation*}
V=L \frac{d I}{d t} \tag{1.23}
\end{equation*}
$$

where $L$ is called the inductance and is measured in henrys (or $\mathrm{mH}, \mu \mathrm{H}, \mathrm{nH}$, etc.). Putting a constant voltage across an inductor causes the current to rise as a ramp (compare with a capacitor, in which a constant current causes the voltage to rise as a ramp); 1 V across 1 H produces a current that increases at 1 amp per second.
image_name:Figure 1.50
description:
[
name: L1, type: Inductor, value: L1, ports: {N1: X1, N2: X2}
name: L2, type: Inductor, value: L2, ports: {N1: X2, N2: X3}
]
extrainfo:The diagram shows two inductors: one with a simple coil and one with a magnetic core, represented by parallel bars above the coil.

Figure 1.50. Inductors. The parallel-bar symbol represents a core of magnetic material.

Just as with capacitors, the energy invested in ramping up the current in an inductor is stored internally, here in the form of magnetic fields. And the analogous formula is

$$
\begin{equation*}
U_{\mathrm{L}}=\frac{1}{2} L I^{2} \tag{1.24}
\end{equation*}
$$

where $U_{\mathrm{L}}$ is in joules (watt seconds) for $L$ in henrys and $I$ in amperes. As with capacitors, this is an important result, one which lies at the core of switching power conversion (exemplified by those little black "wall-warts" that provide power to all manner of consumer electronic gadgets). We'll see lots more of this in Chapter 9.

The symbol for an inductor looks like a coil of wire; that's because, in its simplest form, that's all it is. Its somewhat peculiar behavior comes about because inductors are magnetic devices, in which two things are going on: current flowing through the coil creates a magnetic field aligned along the coil's axis; and then changes in that field produce a voltage (sometimes called "back EMF") in a way that tries to cancel out those changes (an effect known as Lenz's law). The inductance $L$ of a coil is simply the ratio of magnetic flux passing through the coil divided by the current through the coil that produces that flux (multiplied by an overall constant). Inductance depends on the coil geometry (e.g., diameter and length) and the properties of any magnetic material (the "core") that may be used to confine the magnetic field. That's all you need to understand why the inductance of a coil of given geometry is proportional to the square of the number of turns.
Exercise 1.19. Explain why $L \propto n^{2}$ for an inductor consisting of a coil of $n$ turns of wire, maintaining fixed diameter and length as $n$ is varied.

We'll get into some more detail in the Chapter $1 x$. But it's worth displaying a semi-empirical formula for the approximate inductance $L$ of a coil of diameter $d$ and length $l$, in which the $n^{2}$ dependence is on display:

$$
L \approx K \frac{d^{2} n^{2}}{18 d+40 l} \quad \mu \mathrm{H}
$$

image_name:Figure 1.51. Inductors
description:The image labeled "Figure 1.51. Inductors" displays a variety of inductors, each with distinct designs and applications. The inductors are arranged in three rows, showcasing different types and sizes.

1. **Top Row**:
- **Encapsulated Toroid**: A circular inductor enclosed in a protective case, likely used for minimizing electromagnetic interference.
- **Hermetically-Sealed Toroid**: Another toroidal inductor with a sealed casing, providing protection against environmental factors.
- **Board-Mount Pot Core**: A cylindrical inductor designed to be mounted on a printed circuit board (PCB), offering a compact form factor.
- **Bare Toroid (Two Sizes)**: Two unencapsulated toroidal inductors, demonstrating different sizes, likely used for general inductance applications.

2. **Middle Row**:
- **Slug-Tuned Ferrite-Core Inductors (Three Sizes)**: Inductors with adjustable cores, allowing for tuning of the inductance value, useful in radio frequency applications.

3. **Bottom Row**:
- **High-Current Ferrite-Core Choke**: A larger inductor designed to handle high currents, often used in power supplies.
- **Ferrite-Bead Choke**: A small cylindrical inductor used to suppress high-frequency noise in electronic circuits.
- **Dipped Radial-Lead Ferrite-Core Inductor**: A compact inductor with radial leads for easy PCB mounting.
- **Surface-Mount Ferrite Chokes**: Small inductors designed for surface mounting, suitable for compact electronic devices.
- **Molded Axial-Lead Ferrite-Core Chokes (Two Styles)**: Inductors with axial leads, encased in a molded body, offering durability and ease of installation.
- **Lacquered Ferrite-Core Inductors (Two Styles)**: Inductors coated with lacquer for protection, available in different designs for varied applications.

Each component is distinctively labeled or marked, aiding in identification and application. The image provides a comprehensive overview of various inductor designs, highlighting their structural differences and potential uses in electronic circuits.

Figure 1.51. Inductors. Top row, left to right: encapsulated toroid, hermetically-sealed toroid, board-mount pot core, bare toroid (two sizes). Middle row: slug-tuned ferrite-core inductors (three sizes). Bottom row: high-current ferrite-core choke, ferrite-bead choke, dipped radial-lead ferrite-core inductor, surface-mount ferrite chokes, molded axial-lead ferrite-core chokes (two styles), lacquered ferrite-core inductors (two styles).
where $K=1.0$ or 0.395 for dimensions in inches or centimeters, respectively. This is known as Wheeler's formula and is accurate to $1 \%$ as long as $l>0.4 d$.

As with capacitive current, inductive current is not simply proportional to voltage (as in a resistor). Furthermore, unlike the situation in a resistor, the power associated with inductive current $(V \times I)$ is not turned into heat, but is stored as energy in the inductor's magnetic field (recall that for a capacitor the power associated with capacitive current is likewise not dissipated as heat, but is stored as energy in the capacitor's electric field). You get all that energy back when you interrupt the inductor's current (with a capacitor you get all the energy back when you discharge the voltage to zero).

The basic inductor is a coil, which may be just a loop with one or more turns of wire; or it may be a coil with some length, known as a solenoid. Variations include coils wound on various core materials, the most popular being iron (or iron alloys, laminations, or powder) and ferrite (a gray, nonconductive, brittle magnetic material). These are all ploys to multiply the inductance of a given coil by the "permeability" of the core material. The core may be in the shape of a rod, a toroid (doughnut), or even more bizarre shapes, such as a "pot core" (which has to be seen to be understood; the best description we can come up with is a doughnut mold split horizontally in half, if doughnuts were
made in molds). See Figure 1.51 for some typical geometries.

Inductors find heavy use in radiofrequency (RF) circuits, serving as RF "chokes" and as parts of tuned circuits (§1.7.14). A pair of closely coupled inductors forms the interesting object known as a transformer. We will talk briefly about them shortly.

An inductor is, in a real sense, the opposite of a capacitor. ${ }^{28}$ You will see how that works out later in the chapter when we deal with the important subject of impedance.

#### A. A look ahead: some magic with inductors

Just to give a taste of some of the tricks that you can do with inductors, take a look at Figure 1.52. Although we'll understand these circuits a lot better when we go at them in Chapter 9, it's possible to see what's going on with what we know already. In Figure 1.52A the left-hand side of inductor $L$ is alternately switched between a dc input voltage $V_{\text {in }}$ and ground, at some rapid rate, spending equal times
${ }^{28}$ In practice, however, capacitors are much more widely used in electronic circuits. That is because practical inductors depart significantly from ideal performance - by having winding resistance, core losses, and self-capacitance - whereas practical capacitors are nearly perfect (more on this in Chapter $1 x$ ). Inductors are indispensable, however, in switching power converters, as well as in tuned $L C$ circuits for RF applications.
connected to each (a " $50 \%$ duty cycle"). But the defining equation $V=L d I / d t$ requires that the average voltage across an inductor must be zero, otherwise the magnitude of its average current is rising without limit. (This is sometimes called the volt-second balance rule.) From this it follows that the average output voltage is half the input voltage (make sure you understand why). In this circuit $C_{2}$ acts as a storage capacitor for steadying the output voltage (more on this later, and in Chapter 9).

Producing an output that is half the voltage of an input is not very exciting; after all, a simple voltage divider can do that. But, unlike a voltage divider, this circuit does not waste any energy; apart from non-idealities of the components, it is $100 \%$ efficient. And in fact this circuit is widely used in power conversion; it's called a "synchronous buck converter."

But look now at Figure 1.52B, which is just a turnedaround version of Figure 1.52A. This time, volt-second balance requires that the output voltage be twice the input voltage. You can't do that with a voltage divider! Once again, the output capacitor ( $C_{1}$ this time) serves to hold the output voltage steady by storing charge. This configuration is called a "synchronous boost converter."

These and other switching converters are discussed extensively in Chapter 9, where Table 9.5 lists some fifty representative types.
image_name:A
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: Vin, Nn: GND}
name: C2, type: Capacitor, value: C2, ports: {Np: Vout, Nn: GND}
name: L, type: Inductor, value: L, ports: {N1: Vout, N2: Vin}
]
extrainfo:Figure A represents a synchronous buck converter where Vout = 0.5 Vin. The circuit uses an inductor L and capacitors C1 and C2 to regulate the output voltage. The operation of the circuit involves a 50% duty cycle to achieve the desired output voltage.
image_name:B
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: Vout, Nn: GND}
name: L, type: Inductor, value: L, ports: {N1: Vin, N2: Vout}
name: C2, type: Capacitor, value: C2, ports: {Np: Vin, Nn: GND}
]
extrainfo:The circuit is a synchronous boost converter where Vout is twice Vin. The inductor L and capacitors C1 and C2 play key roles in boosting and stabilizing the output voltage.

Figure 1.52. Inductors let you do neat tricks, such as increasing a dc input voltage.

### 1.5.2 Transformers

A transformer is a device consisting of two closely coupled coils (called primary and secondary). An ac voltage applied to the primary appears across the secondary, with a voltage multiplication proportional to the turns ratio of the transformer, and with a current multiplication inversely proportional to the turns ratio. Power is conserved. Figure 1.53 shows the circuit symbol for a laminated-core transformer (the kind used for 60 Hz ac power conversion).
image_name:Figure 1.53
description:The circuit diagram shows a laminated-core transformer used for 60 Hz AC power conversion. It consists of primary and secondary coils.

Figure 1.53. Transformer.

Transformers are quite efficient (output power is very nearly equal to input power); thus, a step-up transformer gives higher voltage at lower current. Jumping ahead for a moment, a transformer of turns ratio $n$ increases the impedance by $n^{2}$. There is very little primary current if the secondary is unloaded.

Power transformers (meant for use from the 115 V powerline) serve two important functions in electronic instruments: they change the ac line voltage to a useful (usually lower) value that can be used by the circuit, and they "isolate" the electronic device from actual connection to the powerline, because the windings of a transformer are electrically insulated from each other. They come in an enormous variety of secondary voltages and currents: outputs as low as 1 volt or so up to several thousand volts, current ratings from a few milliamps to hundreds of amps. Typical transformers for use in electronic instruments might have secondary voltages from 10 to 50 volts, with current ratings of 0.1 to 5 amps or so. A related class of transformers is used in electronic power conversion, in which plenty of power is flowing, but typically as pulse or square waveforms, and at much higher frequencies $(50 \mathrm{kHz}$ to 1 MHz is typical).

Transformers for signals at audio frequencies and radio frequencies are also available. At radio frequencies you sometimes use tuned transformers if only a narrow range of frequencies is present. There is also an interesting class of transmission-line transformers. In general, transformers for use at high frequencies must use special core materials or construction to minimize core losses, whereas lowfrequency transformers (e.g., ac powerline transformers) are burdened instead by large and heavy cores. The two kinds of transformers are in general not interchangeable.

#### A. Problems, problems...

This simple "first-look" description ignores interesting and important - issues. For example, there are inductances associated with the transformer, as suggested by its circuit symbol: an effective parallel inductance (called the magnetizing inductance) and an effective series inductance (called the leakage inductance). Magnetizing inductance causes a primary current even with no secondary load; more significantly, it means that you cannot make a "dc
transformer." And leakage inductance causes a voltage drop that depends on load current, as well as bedeviling circuits that have fast pulses or edges. Other departures from ideal performance include winding resistance, core losses, capacitance, and magnetic coupling to the outside world. Unlike capacitors (which behave nearly ideally in most circuit applications), the deficiencies of inductors have significant effects in real-world circuit applications. We'll deal with these in Chapter $1 x$ and Chapter 9.

## 1.6 Diodes and diode circuits

We are not done with capacitors and inductors! We have dealt with them in the time domain ( $R C$ circuits, exponential charge and discharge, differentiators and integrators, and so on), but we have not yet tackled their behavior in the frequency domain.

We will get to that soon enough. But this is a good time to take a break from "RLC" and put our knowledge to use with some clever and useful circuits. We begin by introducing a new device, the diode. It's our first example of a nonlinear device, and you can do nifty things with it.

### 1.6.1 Diodes

The circuit elements we've discussed so far (resistors, capacitors, and inductors) are all linear, meaning that a doubling of the applied signal (a voltage, say) produces a doubling of the response (a current, say). This is true even for the reactive devices (capacitors and inductors). These components are also passive, as opposed to active devices, the latter exemplified by transistors, which are semiconductor devices that control the flow of power. And they are all two-terminal devices, which is self-explanatory.
image_name:Figure 1.54
description:
[
name: A, type: Diode, ports: {Na: A, Nc: K}
]
extrainfo:The diagram shows a diode with the anode labeled 'A' and the cathode labeled 'K'. This is a two-terminal passive nonlinear device.

Figure 1.54. Diode.
The diode (Figure 1.54) is an important and useful twoterminal passive nonlinear device. It has the $V-I$ curve shown in Figure 1.55. (In keeping with the general philosophy of this book, we will not attempt to describe the solid-state physics that makes such devices possible.)

The diode's arrow (the anode terminal) points in the direction of forward current flow. For example, if the diode is in a circuit in which a current of 10 mA is flowing from anode to cathode, then (from the graph) the anode is approximately 0.6 V more positive than the cathode; this is called the "forward voltage drop." The reverse current,
which is measured in the nanoamp range for a generalpurpose diode (note the hugely different scales in the graph for forward and reverse current), is almost never of any consequence until you reach the reverse breakdown voltage (also called the peak inverse voltage, PIV), typically 75 volts for a general-purpose diode like the 1N4148. (Normally you never subject a diode to voltages large enough to cause reverse breakdown; the exception is the zener diode we mentioned earlier.) Frequently, also, the forward voltage drop of about 0.5 to 0.8 V is of little concern, and the diode can be treated as a good approximation to an ideal one-way conductor. There are other important characteristics that distinguish the thousands of diode types available, e.g., maximum forward current, capacitance, leakage current, and reverse recovery time; Table 1.1 includes a few popular diodes, to give a sense of the capabilities of these little devices.
image_name:Figure 1.55
description:The graph in Figure 1.55 is a Voltage-Current (V-I) curve for a diode, which is a type of nonlinear graph. The horizontal axis represents the voltage across the diode, labeled in volts (V), ranging from -100V to +2V. The vertical axis represents the current through the diode, labeled in microamperes (µA) and milliamperes (mA), with a notable change in scale at the transition from reverse to forward bias.

In the reverse bias region (left side of the graph), the voltage ranges from 0V to -100V. The current is minimal, in the microampere range, indicating the diode's high resistance in this state. As the reverse voltage increases, the current slightly increases but remains very low, illustrating the diode's blocking behavior in reverse bias.

In the forward bias region (right side of the graph), the voltage ranges from 0V to +2V. The current rapidly increases as the voltage exceeds approximately 0.7V, reaching up to 20mA. This indicates the diode's low resistance and its ability to conduct current efficiently in forward bias.

The graph shows a sharp transition from the reverse to the forward bias, highlighting the diode's rectifying behavior, where it allows current to flow easily in one direction while blocking it in the opposite direction. The note about the scale change emphasizes the significant difference in current levels between the reverse and forward bias regions.

Figure 1.55. Diode $V-I$ curve.
Before jumping into some circuits with diodes, we should point out two things: (a) a diode doesn't have a resistance (it doesn't obey Ohm's law). (b) If you put some diodes in a circuit, it won't have a Thévenin equivalent.

### 1.6.2 Rectification

A rectifier changes ac to dc; this is one of the simplest and most important applications of diodes (which are sometimes called rectifiers). The simplest circuit is shown in Figure 1.56. The "ac" symbol represents a source of ac voltage; in electronic circuits it is usually provided by a transformer, powered from the ac powerline. For a sinewave input that is much larger than the forward drop (about 0.6 V for silicon diodes, the usual type), the output will look like that in Figure 1.57. If you think of the diode as a one-way conductor, you won't have any trouble

Table 1.1 Representative Diodes

| Part \# | $V_{\text {R }}$ (max) | IR (typ, $25^{\circ} \mathrm{C}$ ) |  | $V_{\mathrm{F}}$ @ $\mathrm{I}_{\mathrm{F}}$ |  | Capacitance | SMT ${ }^{\text {a }} \mathrm{p} / \mathrm{n}$ | Comments |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
|  | (V) | (A @ | V) | (mV) | (mA) | (pF @ V V ) |  |  |
| Silicon |  |  |  |  |  |  |  |  |
| PAD5 | 45 | 0.25pA | 20V | 800 | 1 | 0.5pF 5V | SSTPAD5 | metal + glass can |
| 1N4148 | 75 | 10nA | 200 | 750 | 10 | 0.9pF OV | 1N4148W | jellybean sig diode |
| 1N4007 | 1000 | 50nA | 800V | 800 | 250 | 12pF 10V | DL4007 | 1N4004 lower V |
| 1N5406 | 600 | <10uA | 600V | 1.0V | 10A | 18pF 10V | none | heat through leads |
| Schottky ${ }^{\text {b }}$ |  |  |  |  |  |  |  |  |
| 1N6263 | 60 | 7nA | 20V | 400 | 1 | 0.6pF 10V | 1N6263W | see also 1N5711 |
| 1N5819 | 40 | 10HA | 32 V | 400 | 1000 | 150pF 1V | 1N5819HW | jellybean |
| 1N5822 | 40 | $40 \mu \mathrm{~A}$ | 32 V | 480 | 3000 | 450pF 1V | none | power Schottky |
| MBRP40045 | 545 | 500 4 A | 40V | 540 | 400A | 3500pF 10V | you jest! | Moby dual Schottky |

Notes: (a) SMT, surface-mount technology. (b) Schottky diodes have lower forward voltage and zero reverse-recovery time, but more capacitance.
understanding how the circuit works. This circuit is called a half-wave rectifier, because only half of the input waveform is used.
image_name:Figure 1.56. Half-wave rectifier
description:
[
name: AC Source, type: VoltageSource, ports: {Np: Vin, Nn: GND}
name: Diode, type: Diode, ports: {Na: Vin, Nc: Vout}
name: Rload, type: Resistor, ports: {N1: Vout, N2: GND}
]
extrainfo:This circuit is a half-wave rectifier, which only uses half of the input waveform to convert AC to DC.

Figure 1.56. Half-wave rectifier.
image_name:Figure 1.57. Half-wave output voltage (unfiltered)
description:The graph in Figure 1.57 represents the output voltage of a half-wave rectifier in the time domain. The x-axis represents time, although specific units are not labeled, and the y-axis represents the voltage across the load, denoted as \( V_{load} \), in volts.

Overall Behavior and Trends:
- The graph shows a series of positive half-cycles of a sinusoidal waveform. Each cycle begins at zero, rises to a peak, and then returns to zero, forming a series of arches.
- Only the positive half of each AC cycle is present, indicating that the negative half of the waveform has been removed by the rectification process.
- There are periods of zero voltage between each positive half-cycle, corresponding to the time when the input AC waveform is negative and the diode is not conducting.

Key Features and Technical Details:
- The peaks of the waveform occur at regular intervals, suggesting a consistent frequency of the input AC source.
- The waveform does not reach negative values, as expected from a half-wave rectification process.
- No filtering is applied, as indicated by the sharp transitions back to zero voltage, resulting in a non-smooth DC output.

Annotations and Specific Data Points:
- The graph does not contain specific numerical annotations or markers, but it qualitatively demonstrates the characteristic behavior of a half-wave rectified output.

Figure 1.57. Half-wave output voltage (unfiltered).
image_name:Figure 1.58 Full-wave bridge rectifier
description:
[
name: AC Source, type: VoltageSource, ports: {Np: N1, Nn: N2}
name: D1, type: Diode, ports: {Na: N1, Nc: N3}
name: D2, type: Diode, ports: {Na: N4, Nc: N1}
name: D3, type: Diode, ports: {Na: N4, Nc: N2}
name: D4, type: Diode, ports: {Na: N2, Nc: N3}
name: Rload, type: Resistor, value: Rload, ports: {N1: N3, N2: N4}
]
extrainfo:The circuit is a full-wave bridge rectifier. It uses four diodes to convert AC to DC, allowing current to pass through the load during both halves of the AC cycle.

Figure 1.58. Full-wave bridge rectifier.

Figure 1.58 shows another rectifier circuit, a "full-wave bridge." Figure 1.59 shows the voltage across the load; note that the entire input waveform is used. The gaps at zero voltage occur because of the diodes' forward voltage drop. In this circuit, two diodes are always in series with the input; when you design low-voltage power supplies, for
which the diode drop becomes significant, you have to remember that. ${ }^{29}$
image_name:Figure 1.59
description:The graph in Figure 1.59 is a time-domain waveform representing the output voltage across a load from a full-wave bridge rectifier. The x-axis represents time, while the y-axis represents the load voltage \( V_{load} \) in volts. The scale appears to be linear for both axes, although specific units or time intervals are not marked.

The waveform exhibits a series of positive half-sine waves, indicating that the entire input AC waveform is being utilized. This behavior is characteristic of a full-wave rectified output, where both halves of the AC input cycle are converted to positive voltage. The waveform does not cross into the negative voltage region, which is typical of rectified outputs.

Each cycle of the waveform starts at zero, rises to a peak, and then returns to zero, showing a periodic pattern. The peaks are consistent, suggesting a steady amplitude, while the valleys are at zero, indicating complete rectification of the input AC signal. The gaps at zero voltage between cycles are due to the forward voltage drop across the diodes in the bridge rectifier circuit.

There are no specific annotations or markers on the graph, but the periodicity and symmetry of the waveform are key features. This unfiltered waveform would typically have significant ripple, which would need to be smoothed out for use in a DC power supply application.

Figure 1.59. Full-wave output voltage (unfiltered).

### 1.6.3 Power-supply filtering

The preceding rectified waveforms aren't good for much as they stand. They're "dc" only in the sense that they don't change polarity. But they still have a lot of "ripple" (periodic variations in voltage about the steady value) that has to be smoothed out in order to generate genuine dc. This we do by attaching a relatively large value capacitor (Figure 1.60); it charges up to the peak output voltage during the diode conduction, and its stored charge ( $Q=C V$ ) provides the output current in between charging cycles. Note that the diodes prevent the capacitor from discharging back through the ac source. In this application you should think of the capacitor as an energy storage device, with stored energy $U=\frac{1}{2} C V^{2}$ (recall $\S 1.4 .1$; for $C$ in farads and $V$ in volts, $U$ comes out in joules, or equivalently, watt seconds).

The capacitor value is chosen so that

$$
R_{\text {load }} C \gg 1 / f
$$

[^23]image_name:Figure 1.60
description:
[
name: ac, type: VoltageSource, value: ac, ports: {Np: Vin, Nn: GND}
name: full-wave bridge, type: Other, ports: {N1: Vin, N2: GND, N3: Vout, N4: GND}
name: C, type: Capacitor, value: C, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is a full-wave bridge rectifier with an output storage capacitor used to smooth the output voltage. The capacitor filters the ripple voltage, ensuring a steady DC output to the load. The diodes in the bridge prevent backflow of current, maintaining charge on the capacitor.

Figure 1.60. Full-wave bridge with output storage ("filter") capacitor.
(where $f$ is the ripple frequency, here 120 Hz ) in order to ensure small ripple by making the time constant for discharge much longer than the time between recharging. We make this vague statement clearer now.

#### A. Calculation of ripple voltage

It is easy to calculate the approximate ripple voltage, particularly if it is small compared with the dc (see Figure 1.61). The load causes the capacitor to discharge somewhat between cycles (or half-cycles, for full-wave rectification). If you assume that the load current stays constant (it will, for small ripple), you have

$$
\begin{equation*}
\Delta V=\frac{I}{C} \Delta t \quad\left(\text { from } I=C \frac{d V}{d t}\right) \tag{1.25}
\end{equation*}
$$

Just use $1 / f$ (or $1 / 2 f$ for full-wave rectification) for $\Delta t$ (this estimate is a bit on the safe side, because the capacitor begins charging again in less than a half-cycle). You get ${ }^{30}$

$$
\begin{array}{ll}
\Delta V=\frac{I_{\text {load }}}{f C} & \text { (half-wave) } \\
\Delta V=\frac{I_{\text {load }}}{2 f C} & \text { (full-wave). }
\end{array}
$$

image_name:Figure 1.61
description:The graph in Figure 1.61 is a time-domain waveform illustrating the power-supply ripple calculation. It depicts the voltage across a load, \( V_{\text{load}} \), over time, \( t \). The x-axis represents time, and the y-axis represents the load voltage.

Type of Graph and Function:
- The graph is a time-domain waveform.

Axes Labels and Units:
- **X-axis (Time):** Labeled as \( t \), likely in seconds or milliseconds.
- **Y-axis (Voltage):** Labeled as \( V_{\text{load}} \), likely in volts.

Overall Behavior and Trends:
- The graph shows a periodic waveform with a sawtooth-like shape, indicating the ripple voltage in a power supply.
- There are two waveforms depicted:
1. **Solid Line:** Represents the output with no capacitor, showing a sharp drop to zero after each peak.
2. **Dashed Line:** Represents the output from a filter under load, which smooths the peaks and valleys.

Key Features and Technical Details:
- **Peak-to-Peak Ripple:** The vertical distance between the peaks and troughs of the dashed line waveform, labeled as "peak-to-peak ripple."
- The dashed line waveform indicates the effect of a capacitor in smoothing the ripple, not allowing the voltage to drop to zero.

Annotations and Specific Data Points:
- The graph is annotated with a label "peak-to-peak ripple" indicating the amplitude of the ripple voltage.
- Another annotation "output from filter, under load" indicates the smoothed waveform.
- "Output with no capacitor" label shows the unsmoothed waveform, emphasizing the effect of the capacitor in reducing the ripple.

Figure 1.61. Power-supply ripple calculation.
If you wanted to do the calculation without any approximation, you would use the exact exponential discharge formula. You would be misguided in insisting on that kind

[^24]of accuracy, though, for two reasons. (a) The discharge is an exponential only if the load is a resistance; many loads are not. In fact, the most common load, a voltage regulator, looks like a constant-current load. (b) Power supplies are built with capacitors with typical tolerances of $20 \%$ or more. Realizing the manufacturing spread, you design conservatively, allowing for the worst-case combination of component values.

In this case, viewing the initial part of the discharge as a ramp is in fact quite accurate, especially if the ripple is small, and in any case it errs in the direction of conservative design - it overestimates the ripple.

Exercise 1.20. Design a full-wave bridge rectifier circuit to deliver 10 V dc with less than $0.1 \mathrm{~V}(\mathrm{pp})$ ripple into a load drawing up to 10 mA . Choose the appropriate ac input voltage, assuming 0.6 V diode drops. Be sure to use the correct ripple frequency in your calculation.
image_name:Figure 1.62
description:The circuit is a full-wave bridge rectifier with a transformer, four diodes, and a smoothing capacitor. The output voltage Vdc is approximately the square root of 2 times the secondary RMS voltage of the transformer minus the diode drops.

Figure 1.62. Bridge rectifier circuit. The polarity marking and curved electrode indicate a polarized capacitor, which must not be allowed to charge with the opposite polarity.

### 1.6.4 Rectifier configurations for power supplies

#### A. Full-wave bridge

A dc power supply with the bridge circuit we just discussed looks as shown in Figure 1.62. In practice, you generally buy the bridge as a prepackaged module. The smallest ones come with maximum current ratings of 1 A average, with a selection of rated minimum breakdown voltages going from 100 V to 600 V , or even 1000 V . Giant bridge rectifiers are available with current ratings of 25 A or more.

#### B. Center-tapped full-wave rectifier

The circuit in Figure 1.63 is called a center-tapped fullwave rectifier. The output voltage is half what you get if you use a bridge rectifier. It is not the most efficient circuit in terms of transformer design, because each half of the secondary is used only half the time. To develop some intuition on this subtle point, consider two different configurations that produce the same rectified dc output voltage: (a) the circuit of Figure 1.63, and (b) the same transformer, this time with its secondary cut at the center tap and
rewired with the two halves in parallel, the resultant combined secondary winding connected to a full-wave bridge. Now, to deliver the same output power, each half winding in (a), during its conduction cycle, must supply the same current as the parallel pair in (b). But the power dissipated in the winding resistances goes like $I^{2} R$, so the power lost to heating in the transformer secondary windings reduced by a factor of 2 for the bridge configuration (b).

Here's another way to see the problem: imagine we use the same transformer as in (a), but for our comparison circuit we replace the pair of diodes with a bridge, as in Figure 1.62 , and we leave the center tap unconnected. Now, to deliver the same output power, the current through the winding during that time is twice what it would be for a true full-wave circuit. To expand on this subtle point: heating in the windings, calculated from Ohm's law, is $I^{2} R$, so you have four times the heating for half the time, or twice the average heating of an equivalent full-wave bridge circuit. You would have to choose a transformer with a current rating 1.4 (square root of 2) times as large compared with the (better) bridge circuit; besides costing more, the resulting supply would be bulkier and heavier.

Exercise 1.21. This illustration of $I^{2} R$ heating may help you understand the disadvantage of the center-tapped rectifier circuit. What fuse rating (minimum) is required for passing the current waveform shown in Figure 1.64, which has 1 amp average current? Hint: a fuse "blows out" by melting a metallic link $\left(I^{2} R\right.$ heating), for steady currents larger than its rating. Assume for this problem that the thermal time constant of the fusible link is much longer than the time scale of the square wave, i.e., that the fuse responds to the value of $I^{2}$ averaged over many cycles.

#### C. Split supply

A popular variation of the center-tapped full-wave circuit is shown in Figure 1.65. It gives you split supplies (equal plus and minus voltages), which many circuits need. It is an efficient circuit, because both halves of the input waveform are used in each winding section.
image_name:Figure 1.65
description:The circuit is a dual-polarity power supply using a center-tapped transformer and two diodes for full-wave rectification. The capacitor smooths the output voltage.

Figure 1.63. Full-wave rectifier using center-tapped transformer.
image_name:Figure 1.64
description:The graph in Figure 1.64 is a time-domain waveform illustrating the current (I) over time. The vertical axis represents the current in amperes (A), marked from 0 to 2.0 A. The horizontal axis represents time, with a noted interval of approximately 1 millisecond (ms) between the repeating waveform segments.

**Type of Graph and Function:**
This is a current-time waveform graph, likely depicting the behavior of current flow in a rectified circuit, possibly related to the dual-polarity power supply context.

**Axes Labels and Units:**
- **Vertical Axis (Y-axis):** Current (I) in amperes (A), ranging from 0 to 2.0 A.
- **Horizontal Axis (X-axis):** Time in milliseconds (ms), with a periodic interval of ~1 ms.

**Overall Behavior and Trends:**
The graph shows a rectangular waveform, indicating a discontinuous current flow with periodic peaks at 2.0 A and returns to 0 A. This suggests a pulsed current, typical of full-wave rectified outputs where the current flows only during certain periods.

**Key Features and Technical Details:**
- The waveform is consistent and periodic with a square shape, indicating a regular on-off pattern of current flow.
- The current reaches a peak of 2.0 A before dropping back to 0 A, highlighting the discontinuous nature of the current flow.

**Annotations and Specific Data Points:**
- The waveform period is approximately 1 ms, which is critical for understanding the timing and frequency of the current pulses.
- The amplitude of the current is consistently 2.0 A during the 'on' phases of the waveform.

This graph effectively illustrates the concept of greater I²R heating with discontinuous current flow, as indicated in the context, which is relevant to the efficiency and thermal considerations in power supply circuits.

Figure 1.64. Illustrating greater $I^{2} R$ heating with discontinuous current flow.
image_name:Figure 1.65. Dual-polarity (split) supply
description:
[
name: Transformer, type: Transformer, ports: {In1: ac_in, In2: GND, Out1: N1, Out2: N2}
name: D1, type: Diode, ports: {Na: N1, Nc: N3}
name: D2, type: Diode, ports: {Na: N2, Nc: N3}
name: D3, type: Diode, ports: {Na: N4, Nc: N2}
name: D4, type: Diode, ports: {Na: N4, Nc: N1}
name: C1, type: Capacitor, ports: {Np: +V, Nn: ground}
name: C2, type: Capacitor, ports: {Np: ground, Nn: -V}
]
extrainfo:The circuit is a dual-polarity (split) power supply, using a bridge rectifier configuration to convert AC input to dual DC outputs, +V and -V, with a common ground.

Figure 1.65. Dual-polarity (split) supply.
image_name:Figure 1.66
description:The circuit is a dual-polarity (split) power supply, using a bridge rectifier configuration to convert AC input to dual DC outputs, +V and -V, with a common ground.

Figure 1.66. Voltage doubler.

#### D. Voltage multipliers

The circuit shown in Figure 1.66 is called a voltage doubler. Think of it as two half-wave rectifier circuits in series. It is officially a full-wave rectifier circuit because both halves of the input waveform are used - the ripple frequency is twice the ac frequency $(120 \mathrm{~Hz}$ for the 60 Hz line voltage in the United States).

Variations of this circuit exist for voltage triplers, quadruplers, etc. Figure 1.67 shows doubler, tripler, and quadrupler circuits that let you ground one side of the transformer. You can extend this scheme as far as you want, producing what's called a Cockcroft-Walton generator; these are used in arcane applications (such as particle accelerators) and in everyday applications (such as image intensifiers, air ionizers, laser copiers, and even bug zappers) that require a high dc voltage but hardly any current.

### 1.6.5 Regulators

By choosing capacitors that are sufficiently large, you can reduce the ripple voltage to any desired level. This bruteforce approach has three disadvantages.
image_name:A. doubler
description:
[
name: Transformer, type: Transformer, ports: {In1: ac_in, In2: GND, Out1: N1, Oou2: GND}
name: D1, type: Diode, ports: {Na: N1, Nc: N2}
name: D2, type: Diode, ports: {Na: GND, Nc: N1}
name: C1, type: Capacitor, ports: {Np: N1, Nn: GND}
name: C2, type: Capacitor, ports: {Np: N2, Nn: GND}
]
extrainfo:The circuit is a voltage doubler configuration using a transformer, diodes, and capacitors to convert AC input to a higher DC output voltage.
image_name:B. tripler
description:
[
name: Transformer, type: Transformer, ports: {In1: AC_IN1, In2: AC_IN2, Out1: N1, Oou2: GND}
name: D1, type: Diode, ports: {Na: N1, Nc: N2}
name: D2, type: Diode, ports: {Na: N3, Nc: N1}
name: C1, type: Capacitor, ports: {Np: N1, Nn: GND}
name: C2, type: Capacitor, ports: {Np: N2, Nn: N3}
]
extrainfo:This is a voltage tripler circuit, which multiplies the input AC voltage by three to produce a higher DC output voltage. It consists of a transformer, two diodes, and two capacitors, configured to increase the voltage through successive rectification and charge storage.
image_name:C. quadrupler
description:
[
name: Transformer, type: Transformer, ports: {In1: ac_in, In2: GND, Out1: N1, Oou2: GND}
name: D1, type: Diode, ports: {Na: N1, Nc: N2}
name: C1, type: Capacitor, ports: {Np: N1, Nn: GND}
name: D2, type: Diode, ports: {Na: N2, Nc: N3}
name: C2, type: Capacitor, ports: {Np: N2, Nn: N4}
name: D3, type: Diode, ports: {Na: N4, Nc: N5}
name: C3, type: Capacitor, ports: {Np: N3, Nn: GND}
name: D4, type: Diode, ports: {Na: N5, Nc: Vout}
name: C4, type: Capacitor, ports: {Np: N5, Nn: N6}
name: D5, type: Diode, ports: {Na: N6, Nc: Vout}
name: C5, type: Capacitor, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit shown is a voltage quadrupler, which is a type of voltage multiplier circuit. It uses diodes and capacitors to increase the AC input voltage to a higher DC output voltage, approximately four times the peak input AC voltage. This type of circuit is often used in applications where a high DC voltage is required from a low AC input voltage.

Figure 1.67. Voltage multipliers; these configurations don't require a floating voltage source.

- The required capacitors may be prohibitively bulky and expensive.
- The very short interval of current flow during each cycle $^{31}$ (only very near the top of the sinusoidal waveform) produces more $I^{2} R$ heating.
- Even with the ripple reduced to negligible levels, you still have variations of output voltage that are due to other causes, e.g., the dc output voltage will be roughly proportional to the ac input voltage, giving rise to fluctuations caused by input line voltage variations. In addition, changes in load current will still cause the output voltage to change because of the finite internal resistances of the transformer, diode, etc. In other words, the Thévenin equivalent circuit of the dc power supply has $R>0$.
A better approach to power-supply design is to use enough capacitance to reduce ripple to low levels (perhaps

[^25]image_name:Figure 1.68
description:
[
name: T1, type: Transformer, ports: {In1: Vin, In2: GND, Out1: N1, Out2: N2}
name: D1, type: Diode, ports: {Na: N1, Nc: GND}
name: D2, type: Diode, ports: {Na: N2, Nc: GND}
name: D3, type: Diode, ports: {Na: GND, Nc: N1}
name: D4, type: Diode, ports: {Na: GND, Nc: N2}
name: C1, type: Capacitor, ports: {Np: N3, Nn: GND}
name: Regulator, type: Other, ports: {N1: N3, N2: GND, N3: Vout}
]
extrainfo:The circuit is a linear regulated DC power supply with a bridge rectifier and smoothing capacitor.

Figure 1.68. Regulated dc power supply.
$10 \%$ of the dc voltage), then use an active feedback circuit to eliminate the remaining ripple. Such a feedback circuit "looks at" the output, making changes in a controllable series resistor (a transistor) as necessary to keep the output voltage constant (Figure 1.68). This is known as a "linear regulated dc power supply." ${ }^{32}$

These voltage regulators are used almost universally as power supplies for electronic circuits. Nowadays complete voltage regulators are available as inexpensive ICs (priced under \$1). A power supply built with a voltage regulator can be made easily adjustable and self-protecting (against short circuits, overheating, etc.), with excellent properties as a voltage source (e.g., internal resistance measured in milliohms). We will deal with regulated dc power supplies in Chapter 9.

### 1.6.6 Circuit applications of diodes

#### A. Signal rectifier

There are other occasions when you use a diode to make a waveform of one polarity only. If the input waveform isn't a sinewave, you usually don't think of it as a rectification in the sense of a power supply. For instance, you might want a train of pulses corresponding to the rising edge of a square wave. The easiest way is to rectify the differentiated wave (Figure 1.69). Always keep in mind the 0.6 V (approximately) forward drop of the diode. This circuit, for instance, gives no output for square waves smaller than 0.6 V pp . If this is a problem, there are various tricks to circumvent this limitation. One possibility is to use hot carrier diodes (Schottky diodes), with a forward drop of about 0.25 V .

A possible circuit solution to this problem of finite diode drop is shown in Figure 1.70. Here $D_{1}$ compensates $D_{2}$ 's forward drop by providing 0.6 V of bias to hold $D_{2}$ at the threshold of conduction. Using a diode $\left(D_{1}\right)$ to provide the bias (rather than, say, a voltage divider) has several

[^26]image_name:Figure 1.69
description:
[
name: C, type: Capacitor, value: C, ports: {Np: Vin, Nn: N1}
name: R1, type: Resistor, value: R1, ports: {N1: N1, N2: GND}
name: D1, type: Diode, ports: {Na: N1, Nc: N2}
name: R2, type: Resistor, value: R2, ports: {N1: N2, N2: GND}
]
extrainfo:The circuit is a signal rectifier applied to a differentiator output, compensating the forward voltage drop of a diode.

Figure 1.69. Signal rectifier applied to differentiator output.
image_name:Figure 1.69
description:
[
name: C, type: Capacitor, value: 100pF, ports: {Np: Vin, Nn: N1}
name: R1, type: Resistor, value: 1.0k, ports: {N1: N1, N2: GND}
name: R2, type: Resistor, value: 1.0k, ports: {N1: N2, N2: GND}
name: R3, type: Resistor, value: 1.0k, ports: {N1: +5V, N2: N1}
name: D1, type: Diode, ports: {Na: N1, Nc: GND}
name: D2, type: Diode, ports: {Na: N1, Nc: N2}
]
extrainfo:The circuit is a signal rectifier applied to a differentiator output, compensating the forward voltage drop of a diode. It uses a diode (D1) for rectification and another diode (D2) for compensation. The resistors R1 and R3 create a voltage divider to apply a +0.6V bias to the diode D1. The circuit compensates for changes in the diode's forward voltage drop due to temperature variations.

Figure 1.70. Compensating the forward voltage drop of a diode signal rectifier.
advantages: (a) there is nothing to adjust, (b) the compensation will be nearly perfect, and (c) changes of the forward drop (e.g., with changing temperature) will be compensated properly. Later we will see other instances of matched-pair compensation of forward drops in diodes, transistors, and FETs. It is a simple and powerful trick.

#### B. Diode gates

Another application of diodes, which we will recognize later under the general heading of logic, is to pass the higher of two voltages without affecting the lower. A good example is battery backup, a method of keeping something running (e.g, the "real-time clock" chip in a computer, which keeps a running count of date and time) that must continue running even when the device is switched off. Figure 1.71 shows a circuit that does the job. The battery does nothing until the +5 V power is switched off; then it takes over without interruption.

#### C. Diode clamps

Sometimes it is desirable to limit the range of a signal (i.e., prevent it from exceeding certain voltage limits) somewhere in a circuit. The circuit shown in Figure 1.72 will accomplish this. The diode prevents the output from exceeding about +5.6 V , with no effect on voltages less than that (including negative voltages); the only limitation is that the input must not go so negative that the reverse breakdown voltage of the diode is exceeded (e.g., -75 V for a 1N4148). The series resistor limits the diode current during
image_name:Figure 1.71. Diode OR gate: battery backup
description:
[
name: D1, type: Diode, ports: {Na: +3V, Nc: V+}
name: D2, type: Diode, ports: {Na: +5V, Nc: V+}
name: Lithium Coin Cell, type: VoltageSource, value: +3V, ports: {Np: +3V, Nn: GND}
]
extrainfo:This circuit is a diode OR gate used for battery backup in real-time clock applications. It ensures that the real-time clock receives power from either a +3V lithium coin cell or a +5V source, depending on availability. The diodes prevent reverse current flow, ensuring that the highest available voltage powers the clock.

Figure 1.71. Diode OR gate: battery backup. The real-time clock chips are specified to operate properly with supply voltages from +1.8 V to +5.5 V . They draw a paltry $0.25 \mu \mathrm{~A}$, which calculates to a 1-million-hour life (a hundred years) from a standard CR2032 coin cell!
image_name:Figure 1.72. Diode voltage clamp.
description:
[
name: 1.0k, type: Resistor, value: 1.0k, ports: {N1: in, N2: out}
name: 1N4148, type: Diode, ports: {Na: +5V, Nc: out}
]
extrainfo:The circuit is a diode voltage clamp with a 1.0k resistor in series with the input and a diode connected to a +5V source to clamp the output voltage.

Figure 1.72. Diode voltage clamp.
image_name:Figure 1.72. Diode voltage clamp.
description:
[
name: R, type: Resistor, value: R, ports: {N1: signal_in, N2: out}
name: 2.0k, type: Resistor, value: 2.0k, ports: {N1: +15V, N2: out}
name: 1.0k, type: Resistor, value: 1.0k, ports: {N1: out, N2: GND}
name: Diode, type: Diode, ports: {Na: out, Nc: out}
]
extrainfo:The circuit is a voltage clamp with a resistor R in series with the input signal. A diode is connected at the output node to clamp the voltage. The output is further connected to a voltage divider formed by 2.0k and 1.0k resistors, with a +15V supply and ground.

Figure 1.73. Voltage divider providing clamping voltage.
clamping action; however, a side effect is that it adds $1 \mathrm{k} \Omega$ of series resistance (in the Thévenin sense) to the signal, so its value is a compromise between maintaining a desirable low source (Thévenin) resistance and a desirable low clamping current. Diode clamps are standard equipment on all inputs in contemporary CMOS digital logic. Without them, the delicate input circuits are easily destroyed by static electricity discharges during handling.

Exercise 1.22. Design a symmetrical clamp, i.e., one that confines a signal to the range -5.6 to +5.6 V .

A voltage divider can provide the reference voltage for a clamp (Figure 1.73). In this case you must ensure that the resistance looking into the voltage divider $\left(R_{\mathrm{vd}}\right)$ is small compared with $R$ because what you have looks as shown
image_name:Figure 1.74
description:
[
name: R_VD, type: Resistor, value: 667Ω, ports: {N1: +5V, N2: D1_anode}
name: R, type: Resistor, value: R, ports: {N1: signal_in, N2: out}
name: Diode, type: Diode, ports: {Na: D1_anode, Nc: out}
]
extrainfo:The circuit is a clamping circuit designed to confine the signal to a specific voltage range using a voltage divider and diode. The reference voltage is +5V, and the resistor R_VD sets the clamp level.

Figure 1.74. Clamping to voltage divider: equivalent circuit.
image_name:Figure 1.74
description:
[
name: R1, type: Resistor, value: 1.0k, ports: {N1: in, N2: out}
name: R2, type: Resistor, value: 667Ω, ports: {N1: out, N2: +5.6V}
name: +5.6V, type: VoltageSource, value: +5.6V, ports: {Np: +5.6V, Nn: out}
]
extrainfo:The circuit is a clamping circuit designed to confine the signal to a specific voltage range using a voltage divider and diode. The reference voltage is +5.6V, and the resistor R2 sets the clamp level.

Figure 1.75. Poor clamping: voltage divider not stiff enough.
image_name:Figure 1.76
description:The graph in Figure 1.76 is a time-domain waveform depicting the output of a clamping circuit when a triangle-wave input is applied. The horizontal axis represents time, while the vertical axis represents voltage. The graph is linear in scale.

The waveform shows how the clamping circuit affects the input signal. The input is a triangle wave, characterized by its linear rise and fall. However, due to the clamping action, the positive peaks of the waveform are limited to a specific voltage level, labeled as \( V_{clamp} \). This indicates the maximum voltage level the circuit allows during the positive cycle.

The waveform starts at zero, rises linearly until it reaches \( V_{clamp} \), where it becomes flat, indicating that the voltage is clamped. After the clamping period, the waveform descends linearly back to zero and continues into the negative cycle without clamping, showing the full negative swing of the triangle wave.

Key features of the graph include:
- The clamping level \( V_{clamp} \), which is the maximum voltage reached during the positive cycle.
- A flat section at the top of the waveform indicating the clamping action.
- The waveform resumes its triangular shape during the negative cycle, unaffected by clamping.

Overall, the graph effectively illustrates the clamping effect on a triangle wave, showing how the circuit confines the signal to a specified voltage range during the positive cycle.

Figure 1.76. Clamping waveform for circuit of Figure 1.73.
in Figure 1.74 when the voltage divider is replaced with its Thévenin equivalent circuit. When the diode conducts (input voltage exceeds clamp voltage), the output is really just the output of a voltage divider, with the Thévenin equivalent resistance of the voltage reference as the lower resistor (Figure 1.75). So, for the values shown, the output of the clamp for a triangle-wave input would look as shown in Figure 1.76. The problem is that the voltage divider doesn't provide a stiff reference, in the language of electronics. A stiff voltage source is one that doesn't bend easily, i.e., it has low internal (Thévenin) resistance.

In practice, the problem of finite impedance of the voltage-divider reference can be easily solved by use of a transistor or an op-amp. This is usually a better solution than using very small resistor values, because it doesn't consume large currents, yet it provides a voltage reference with a Thévenin resistance of a few ohms or less. Furthermore, there are other ways to construct a clamp, using an op-amp as part of the clamp circuit. You will see these methods in Chapter 4.

Alternatively, a simple way to stiffen the clamp circuit of Figure 1.73, for time-varying signals only, is to add a socalled bypass capacitor across the lower ( $1 \mathrm{k} \Omega$ ) resistor. To understand this fully we need to know about capacitors in
image_name:Figure 1.77. dc restoration
description:
[
name: C, type: Capacitor, value: C, ports: {Np: 0, Nn: 1}
name: D1, type: Diode, ports: {Na: 1, Nc: GND}
]
extrainfo:The circuit is a DC restoration circuit using a capacitor and a diode. The input signal is AC coupled through the capacitor, and the diode clamps the signal to ground, restoring the DC level.
image_name:Figure 1.78. Diode limiter
description:
[
name: C, type: Capacitor, value: C, ports: {Np: Vin, Nn: N1}
name: D1, type: Diode, ports: {Na: N1, Nc: GND}
]
extrainfo:The circuit is a diode limiter with a capacitor coupling the input to the diode. The capacitor blocks DC, allowing AC signals to pass. The diode clamps the voltage to the ground level, limiting the output voltage swing.

Figure 1.77. dc restoration.
image_name:Figure 1.78. Diode limiter
description:
[
name: R, type: Resistor, value: R, ports: {N1: in, N2: N1}
name: D1, type: Diode, ports: {Na: N1, Nc: GND}
name: D2, type: Diode, ports: {Na: GND, Nc: N1}
]
extrainfo:The circuit is a diode limiter. The resistor R connects the input to node N1. Diode D1 is forward-biased when the input voltage exceeds a certain level, clamping the voltage to ground. Diode D2 is reverse-biased and clamps negative voltages to ground. This limits the voltage swing at the output.

Figure 1.78. Diode limiter.
the frequency domain, a subject we'll take up shortly. For now we'll simply say that you can put a capacitor across the 1 k resistor, and its stored charge acts to maintain that point at constant voltage. For example, a $15 \mu \mathrm{~F}$ capacitor to ground would make the divider look as if it had a Thévenin resistance of less than $10 \Omega$ for frequencies above 1 kHz . (You could similarly add a bypass capacitor across $D_{1}$ in Figure 1.70.) As we'll learn, the effectiveness of this trick decreases at low frequencies, and it does nothing at dc.

One interesting clamp application is "dc restoration" of a signal that has been ac coupled (capacitively coupled). Figure 1.77 shows the idea. This is particularly important for circuits whose inputs look like diodes (e.g., a transistor with grounded emitter, as we'll see in the next chapter); otherwise an ac-coupled signal will just fade away, as the coupling capacitor charges up to the signal's peak voltage.

#### D. Limiter

One last clamp circuit is shown in Figure 1.78. This circuit limits the output "swing" (again, a common electronics term) to one diode drop in either polarity, roughly $\pm 0.6 \mathrm{~V}$. That might seem awfully small, but if the next stage is an amplifier with large voltage amplification, its input will always be near 0 V ; otherwise the output is in "saturation" (e.g., if the next stage has a gain of 1000 and operates from $\pm 15 \mathrm{~V}$ supplies, its input must stay in the range $\pm 15 \mathrm{mV}$ in order for its output not to saturate). Figure 1.79 shows what a limiter does to oversize sinewaves and spikes. This clamp circuit is often used as input protection for a highgain amplifier.

#### E. Diodes as nonlinear elements

To a good approximation the forward current through a diode is proportional to an exponential function of the
image_name:Figure 1.79 A
description:**Type of Graph and Function:**
The graph labeled "Figure 1.79 A" is a time-domain waveform illustrating the effect of a limiter on a sinusoidal input signal. It shows how large-amplitude sine waves are clipped when they exceed certain voltage thresholds.

**Axes Labels and Units:**
The horizontal axis represents time, though it is not explicitly labeled with units. The vertical axis represents voltage in volts, with specific clipping levels indicated at +0.6V and -0.6V.

**Overall Behavior and Trends:**
The graph depicts a sinusoidal waveform, described by the equation \( V = A \sin \omega t \), where \( A \) is the amplitude and \( \omega \) is the angular frequency. The sine wave is symmetrical around the time axis, but when it exceeds the voltage levels of +0.6V and -0.6V, the waveform is clipped, resulting in a flattened top and bottom.

**Key Features and Technical Details:**
- **Clipping Levels:** The sine wave is clipped at +0.6V and -0.6V, preventing the amplitude from exceeding these levels.
- **Clipped Waveform:** The previously smooth peaks and troughs are now flat, indicating the limiter's effect in preventing the waveform from exceeding the specified voltage limits.
- **Gradient:** The slope of the waveform at the point of clipping is marked as \( \frac{dV}{dt} = \omega A \), indicating the rate of change of voltage at the clipping points.

**Annotations and Specific Data Points:**
- The graph highlights the clipping action with a circle around the clipped portion of the sine wave, showing the transition from the natural sinusoidal shape to the clipped form.
- An annotation indicates the mathematical representation of the slope at the clipping points, providing insight into the waveform's behavior at those instances.

This graph effectively demonstrates how a limiter can protect subsequent stages in an electronic circuit by preventing excessive voltage levels, thereby avoiding saturation and potential damage.
image_name:Figure 1.79 B
description:Figure 1.79 B is a detailed view of a waveform that illustrates the limiting behavior of a circuit on a sine wave. This graph is a time-domain waveform, showing how an input sine wave is altered by a limiter.

1. **Axes Labels and Units:**
- The horizontal axis represents time, though it is not explicitly labeled with units.
- The vertical axis represents voltage, with specific limits indicated at +0.6V and -0.6V.

2. **Overall Behavior and Trends:**
- The graph shows a portion of a sine wave that is being limited. The sine wave would naturally continue beyond the +0.6V and -0.6V thresholds, but the limiter flattens the waveform at these points.
- The waveform starts to curve sharply as it approaches these voltage limits, indicating the effect of the limiter.

3. **Key Features and Technical Details:**
- The slope of the waveform is denoted as dV/dt = ωA, suggesting the rate of change of voltage with respect to time is proportional to the product of angular frequency (ω) and amplitude (A).
- The waveform is clipped at +0.6V and -0.6V, which are the key limiting values.
- There is a smooth transition around these limits, indicating a soft limiting action rather than hard clipping.

4. **Annotations and Specific Data Points:**
- The graph includes dashed lines showing the ideal continuation of the sine wave without limiting.
- The specific voltage levels of +0.6V and -0.6V are annotated, showing where the limiting occurs.

This detailed view helps to understand how a limiter modifies the waveform by preventing it from exceeding certain voltage thresholds, thereby protecting subsequent stages in a circuit from saturation.
image_name:Figure 1.79 C
description:Figure 1.79 C illustrates the behavior of a limiting circuit on a spike waveform. The graph is a time-domain waveform showing how the circuit clamps voltage spikes.

**Axes Labels and Units:**
- The horizontal axis represents time, although specific units are not labeled on the graph.
- The vertical axis represents voltage, with significant markers at +0.6V and -0.6V, indicating the clamping levels.

**Overall Behavior and Trends:**
- The waveform exhibits a sharp spike that is significantly limited by the circuit.
- The spike initially rises sharply, but the limiter restricts its peak to approximately +0.6V.
- Similarly, any negative excursions are clamped at -0.6V.
- The waveform shows a quick return to baseline after the spike, suggesting effective clamping action.

**Key Features and Technical Details:**
- The graph shows a single prominent spike that is limited to the voltage levels of +0.6V and -0.6V.
- The waveform before and after the spike is relatively flat, indicating no significant signal activity outside the spike.

**Annotations and Specific Data Points:**
- There are dashed lines indicating the peak of the spike, which align with the +0.6V and -0.6V clamping levels.
- The waveform illustrates the limiting function of the circuit, preventing any voltage beyond the specified clamping levels.

Figure 1.79. A. Limiting large-amplitude sinewaves; B. details; and C. spikes.
image_name:Figure 1.80
description:
[
name: I_in, type: CurrentSource, value: I_in, ports: {Np: Vin, Nn: Vout}
name: D1, type: Diode, ports: {Na: Vout, Nc: GND}
]
extrainfo:The circuit is a logarithmic converter using a diode's nonlinear V-I characteristics to produce an output voltage proportional to the logarithm of the input current I_in.

Figure 1.80. Exploiting the diode's nonlinear $V-I$ curve: logarithmic converter.
voltage across it at a given temperature (for a discussion of the exact law, see $\S 2.3 .1$ ). So you can use a diode to generate an output voltage proportional to the logarithm of a current (Figure 1.80). Because $V$ hovers in the region of 0.6 V , with only small voltage changes that reflect input current variations, you can generate the input current with a resistor if the input voltage is much larger than a diode drop (Figure 1.81).

In practice, you may want an output voltage that isn't offset by the 0.6 V diode drop. In addition, it would be nice to have a circuit that is insensitive to changes in temperature (a silicon diode's voltage drop decreases approximately $2 \mathrm{mV} /{ }^{\circ} \mathrm{C}$ ). The method of diode drop compensation is helpful here (Figure 1.82). $R_{1}$ makes $D_{2}$ conduct, holding
image_name:Figure 1.81. Approximate log converter.
description:
[
name: R, type: Resistor, value: R, ports: {N1: Vin, N2: Vout}
name: Diode1, type: Diode, ports: {Na: Vout, Nc: GND}
]
extrainfo:The circuit is an approximate log converter. The input voltage (Vin) is much larger than the diode drop, and the diode is used for compensation. The diode's voltage drop decreases approximately 2 mV/°C with temperature changes.

Figure 1.81. Approximate log converter.
image_name:Figure 1.81. Approximate log converter.
description:
[
name: R, type: Resistor, value: R, ports: {N1: Vin, N2: B}
name: D1, type: Diode, ports: {Na: B, Nc: A}
name: D2, type: Diode, ports: {Na: GND, Nc: A}
name: R1, type: Resistor, value: R1, ports: {N1: A, N2: -V}
]
extrainfo:The circuit is an approximate log converter. It uses two diodes, D1 and D2, for temperature compensation. The input voltage Vin is much larger than the diode drop, and the diode's voltage drop decreases approximately 2 mV/°C with temperature changes. Point A is at about -0.6 V, and point B is near ground, making the input current proportional to Vin. The resistor R1 should be chosen to ensure proper operation.

Figure 1.82. Diode drop compensation in the logarithmic converter.
point $A$ at about -0.6 V . Point $B$ is then near ground (making $I_{\text {in }}$ accurately proportional to $V_{\text {in }}$, incidentally). As long as the two (identical) diodes are at the same temperature, there is good cancellation of the forward drops, except, of course, for the difference owing to input current through $D_{1}$, which produces the desired output. In this circuit, $R_{1}$ should be chosen so that the current through $D_{2}$ is significantly larger than the maximum input current in order to keep $D_{2}$ in conduction.

In Chapter $2 x$ we will examine better ways of constructing logarithmic converter circuits, along with careful methods of temperature compensation. With such methods it is possible to construct logarithmic converters accurate to a few percent over six decades or more of input current. A better understanding of diode and transistor characteristics, along with an understanding of op-amps, is necessary first. This section is meant to serve only as an introduction for things to come.

### 1.6.7 Inductive loads and diode protection

What happens if you open a switch that is providing current to an inductor? Because inductors have the property

$$
V=L d I / d t
$$

it is not possible to turn off the current suddenly, because that would imply an infinite voltage across the inductor's terminals. What happens instead is that the voltage across the inductor rises abruptly and keeps rising until it forces current to flow. Electronic devices controlling inductive
image_name:Figure 1.83. Inductive "kick."
description:
[
name: +20V, type: VoltageSource, value: +20V, ports: {Np: +20V, Nn: A}
name: A-B, type: Inductor, ports: {N1: A, N2: B}
]
extrainfo:The circuit demonstrates an inductive 'kick' when the switch is opened, causing a high voltage spike across the inductor.

Figure 1.83. Inductive "kick."
image_name:Figure 1.83. Inductive "kick."
description:
[
name: L1, type: Inductor, value: L1, ports: {N1: +, N2: C}
name: D1, type: Diode, ports: {Na: C, Nc: +}
name: I_on, type: CurrentSource, value: I_on, ports: {Np: +, Nn: GND}
name: S1, type: Switch, ports: {N1: C, N2: GND}
]
extrainfo:The circuit demonstrates an inductive 'kick' when the switch is opened, causing a high voltage spike across the inductor. The diode is used to prevent damage by providing a path for the current when the switch is turned off.

Figure 1.84. Blocking inductive kick.
loads can be easily damaged, especially the component that "breaks down" in order to satisfy the inductor's craving for continuity of current. Consider the circuit in Figure 1.83 . The switch is initially closed, and current is flowing through the inductor (which might be a relay, as described later). When the switch is opened, the inductor tries to keep current flowing from $A$ to $B$, as it had been. In other words, it tries to make current flow out of $B$, which it does by forcing $B$ to a high positive voltage (relative to $A$ ). In a case like this, in which there's no connection to terminal $B$, it may go 1000 V positive before the switch contact "blows over." This shortens the life of the switch and also generates impulsive interference that may affect other circuits nearby. If the switch happens to be a transistor, it would be an understatement to say that its life is shortened; its life is ended.

The best solution usually is to put a diode across the inductor, as in Figure 1.84. When the switch is on, the diode is back-biased (from the dc drop across the inductor's winding resistance). At turn-off the diode goes into conduction, putting the switch terminal a diode drop above the positive supply voltage. The diode must be able to handle the initial diode current, which equals the steady current that had been flowing through the inductor; something like a 1N4004 is fine for nearly all cases.

The only disadvantage of this simple protection circuit is that it lengthens the decay of current through the inductor, because the rate of change of inductor current
image_name:Figure 1.85
description:
[
name: L1, type: Inductor, value: L1, ports: {N1: N1, N2: N2}
name: R1, type: Resistor, value: 100Ω, ports: {N1: N2, N2: N3}
name: C1, type: Capacitor, value: 0.05μF, ports: {Np: N3, Nn: N2}
]
extrainfo:The circuit is an RC snubber circuit used for suppressing inductive kickback. It consists of an inductor L1, a resistor R1, and a capacitor C1 connected in parallel to the inductor.

Figure 1.85. $R C$ "snubber" for suppressing inductive kick.
is proportional to the voltage across it. For applications in which the current must decay quickly (high-speed actuators or relays, camera shutters, magnet coils, etc.), it may be better to put a resistor across the inductor, choosing its value so that $V_{\text {supply }}+I R$ is less than the maximum allowed voltage across the switch. For the fastest decay with a given maximum voltage, a zener with series diode (or other voltage-clamping device) can be used instead, giving a linear-like ramp-down of current rather than an exponential decay (see discussion in Chapter 1x).

For inductors driven from ac (transformers, ac relays), the diode protection just described will not work, because the diode will conduct on alternate half-cycles when the switch is closed. In that case a good solution is an $R C$ "snubber" network (Figure 1.85). The values shown are typical for small inductive loads driven from the ac powerline. Such a snubber should be included in all instruments that run from the ac powerline, because the power transformer is inductive. ${ }^{33}$

An alternative to the $R C$ snubber is the use of a bidirectional zener-like voltage-clamping element. Among these the most common are the bidirectional "TVS" (transient voltage suppressor) zener and the metal-oxide varistor ("MOV"); the latter is an inexpensive device that looks something like a disc ceramic capacitor and behaves electrically like a bidirectional zener diode. Both classes are designed for transient voltage protection, are variously available at voltage ratings from 10 to 1000 volts, and can handle transient currents up to thousands of amperes (see Chapter $9 x$ ). Including a transient suppressor (with appropriate fusing) across the ac powerline terminals makes good sense in a piece of electronic equipment, not only to prevent inductive spike interference to other nearby instruments but also to prevent occasional large powerline spikes from damaging the instrument itself.

### 1.6.8 Interlude: inductors as friends

Lest we leave the impression that inductance and inductors are things only to be feared, let's look at the circuit in

[^27]Figure 1.86. The goal is to charge up the capacitor from a source of dc voltage $V_{\text {in }}$. In the top circuit (Figure 1.86A) we've done it the conventional way, with a series resistor to limit the peak current demanded from the voltage source. OK, it does work - but it has a drawback that can be serious, namely that half the energy is lost as heat in the resistor. By contrast, in the circuit with the inductor (Figure 1.86 B ) no energy is lost (assuming ideal components); and, as a bonus, the capacitor gets charged to twice the input voltage. The output-voltage waveform is a sinusoidal half-cycle at the resonant frequency $f=1 / 2 \pi \sqrt{L C}$, a topic we'll see soon (§1.7.14). ${ }^{34,35}$
image_name:Figure 1.86 A
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: R, type: Resistor, value: R, ports: {N1: Vin, N2: V(t)}
name: C, type: Capacitor, value: C, ports: {Np: V(t), Nn: GND}
]
extrainfo:This circuit is a simple RC charging circuit where the capacitor charges through the resistor from the voltage source Vin. The voltage across the capacitor is labeled as V(t).
image_name:Figure 1.86 B
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: R, type: Resistor, value: R, ports: {N1: Vin, N2: V(t)}
name: C, type: Capacitor, value: C, ports: {Np: V(t), Nn: GND}
]
extrainfo:The circuit is a basic RC charging circuit where the capacitor C is charged through the resistor R from the voltage source Vin. The voltage across the capacitor is labeled V(t).
image_name:Figure 1.87
description:The image shows an electrical circuit diagram labeled as Figure 1.87. The circuit consists of a voltage source labeled \( V_{in} \), a resistor labeled \( R \), and a capacitor labeled \( C \). The voltage across the capacitor is denoted as \( V(t) \). The circuit is arranged in series with the voltage source connected to the resistor, which in turn is connected to the capacitor. The circuit also includes a switch symbol before the resistor, indicating that the circuit can be opened or closed at this point. The entire circuit is grounded at both the voltage source and the bottom of the capacitor.

A.
image_name:A
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: R, type: Resistor, value: R, ports: {N1: Vin, N2: V(t)}
name: C, type: Capacitor, value: C, ports: {Np: V(t), Nn: GND}
]
extrainfo:The circuit is an RC series circuit with a switch, voltage source, resistor, and capacitor. The current through the resistor decreases exponentially, and the voltage across the capacitor increases over time.
image_name:I
description:The diagram labeled "I" consists of two parts, each depicting a circuit and its corresponding graphs.

### Part A:
1. **Circuit Description**:
- The circuit includes a voltage source labeled \( V_{in} \), a resistor \( R \), and a capacitor \( C \) connected in series. A switch is placed before the resistor, and the entire circuit is grounded at both the voltage source and the capacitor.

2. **Graph Description**:
- **Current Graph (Top Right)**:
- **Type**: Exponential decay curve.
- **Axes**: The vertical axis represents current \( I \) and the horizontal axis represents time \( t \).
- **Behavior**: The current starts at a maximum value of \( V_{in}/R \) and decays exponentially towards zero.
- **Voltage Graph (Bottom Right)**:
- **Type**: Exponential growth curve.
- **Axes**: The vertical axis represents voltage \( V \) and the horizontal axis represents time \( t \).
- **Behavior**: The voltage across the capacitor starts at zero and increases exponentially, approaching \( V_{in} \).

### Part B:
1. **Circuit Description**:
- The circuit includes a voltage source \( V_{in} \), an inductor \( L \), a diode \( D \), and a capacitor \( C \). The components are connected in series, with the diode oriented to allow current flow towards the capacitor, and the circuit is grounded at both the voltage source and the capacitor.

2. **Graph Description**:
- **Current Graph (Top Right)**:
- **Type**: Oscillatory curve.
- **Axes**: The vertical axis represents current \( I \) and the horizontal axis represents time \( t \).
- **Behavior**: The current increases to a peak and then decreases, indicating oscillation with a peak at time \( t_f \).
- **Voltage Graph (Bottom Right)**:
- **Type**: Step change.
- **Axes**: The vertical axis represents voltage \( V \) and the horizontal axis represents time \( t \).
- **Behavior**: The voltage across the capacitor jumps to \( 2V_{in} \) and stabilizes, suggesting a doubling effect due to the inductor and diode arrangement.
image_name:V
description:### Description of the Function Graph 'V'

Type of Graph and Function:
The graph appears to represent the time-domain behavior of an RC charging circuit. It consists of two plots: one for current (I) and one for voltage (V) across the capacitor as functions of time (t).

Axes Labels and Units:
- The vertical axis of the current plot is labeled "I" and represents current. It does not specify units, but it is implied to be in amperes (A).
- The vertical axis of the voltage plot is labeled "V" and represents voltage, likely in volts (V).
- The horizontal axis for both plots is labeled "t" and represents time, presumably in seconds (s).

Overall Behavior and Trends:
- **Current (I) Plot:**
- The current starts at a maximum value of \( \frac{V_{in}}{R} \) and exponentially decays to zero as time progresses. This behavior is typical of an RC charging circuit, where the current decreases as the capacitor charges.
- **Voltage (V) Plot:**
- The voltage across the capacitor starts at zero and exponentially increases, approaching \( V_{in} \) asymptotically. This reflects the charging of the capacitor over time.

Key Features and Technical Details:
- **Current (I) Plot:**
- Initial current value is \( \frac{V_{in}}{R} \), indicating Ohm's Law application at the start.
- Exponential decay is characteristic of the charging process, with no oscillations or overshoot.
- **Voltage (V) Plot:**
- The voltage follows an exponential rise, with no oscillations or overshoot, typical for a simple RC charging circuit.
- The asymptotic approach towards \( V_{in} \) indicates the capacitor is reaching full charge.

Annotations and Specific Data Points:
- The current plot has a dashed line indicating the initial current value \( \frac{V_{in}}{R} \).
- The voltage plot has a dashed line indicating the final voltage value \( V_{in} \) that the capacitor approaches.

This description provides a comprehensive understanding of the graph's representation of an RC circuit's charging behavior, emphasizing the exponential nature of the current decay and voltage rise over time.

B.
image_name:Figure 1.87
description:The graph in Figure 1.87 is a frequency response plot illustrating the equalization of a loudspeaker, often referred to as a "boom box." This is a Bode plot, where the x-axis represents frequency on a logarithmic scale ranging from 20 Hz to 20 kHz, and the y-axis shows relative response on a linear scale.

Axes Labels and Units:
- **X-axis (Frequency):** Logarithmic scale, marked at key points such as 20 Hz, 200 Hz, 2 kHz, and 20 kHz.
- **Y-axis (Relative Response):** Linear scale, indicating the loudspeaker's response at various frequencies.

Overall Behavior and Trends:
- The solid line represents the frequency response of the speaker. It shows a peak in response around the middle frequencies (around 200 Hz to 2 kHz), indicating that the speaker naturally amplifies these frequencies more than others.
- The response decreases at both the low end (infrasonic) and the high end (ultrasonic) of the frequency spectrum.

Key Features and Technical Details:
- **Lowest Note on Piano (A0):** Marked at 27.5 Hz, near the low-frequency end of the graph.
- **Middle C:** Marked around 261.6 Hz, aligning with the peak of the speaker's response.
- **Highest Note on Piano (C8):** Marked at 4.2 kHz, near the high-frequency end.
- The dashed line represents a compensating filter designed to flatten the speaker's response across the audible range, suggesting equalization to achieve a more balanced sound output.

Annotations and Specific Data Points:
- The graph includes annotations for significant musical notes like the lowest and highest notes on a piano and middle C.
- The compensating filter is intended to counteract the speaker's natural frequency response, as indicated by the dashed line, which shows a more uniform response across frequencies.

This graph effectively demonstrates the need for equalization in audio systems to ensure a consistent sound quality across different frequencies, particularly for devices like boom boxes that may have inherent frequency biases.

Figure 1.87. Example of frequency analysis: "boom box" loudspeaker equalization. The lowest and highest piano notes, called A0 and C8, are at 27.5 Hz and 4.2 kHz ; they are four octaves below A440 and four octaves above middle C, respectively.

## 1.7 Impedance and reactance

Warning: this section is somewhat mathematical; you may wish to skip over the mathematics, but be sure to pay attention to the results and graphs.

Circuits with capacitors and inductors are more complicated than the resistive circuits we talked about earlier, in that their behavior depends on frequency: a "voltage divider" containing a capacitor or inductor will have a frequency-dependent division ratio. In addition, circuits containing these components (known collectively as reactive components) "corrupt" input waveforms such as square waves, as we saw earlier.

However, both capacitors and inductors are linear devices, meaning that the amplitude of the output waveform, whatever its shape, increases exactly in proportion to the input waveform's amplitude. This linearity has many consequences, the most important of which is probably the following: the output of a linear circuit, driven with a sinewave at some frequency $f$, is itself a sinewave at the same frequency (with, at most, changed amplitude and phase).

Because of this remarkable property of circuits containing resistors, capacitors, and inductors (and, later, linear amplifiers), it is particularly convenient to analyze any such circuit by asking how the output voltage (amplitude and phase) depends on the input voltage for sinewave input at a single frequency, even though this may not be the intended use. A graph of the resulting frequency response, in which the ratio of output to input is plotted for each sinewave frequency, is useful for thinking about many kinds of

[^28]Figure 1.86. Resonant charging is lossless (with ideal components) compared with the $50 \%$ efficiency of resistive charging. Charging is complete after $t_{\mathrm{f}}$, equal to a half-cycle of the resonant frequency. The series diode terminates the cycle, which would otherwise continue to oscillate between 0 and $2 V_{\text {in }}$.
waveforms. As an example, a certain "boom-box" loudspeaker might have the frequency response shown in Figure 1.87, in which the "output" in this case is of course sound pressure, not voltage. It is desirable for a speaker to have a "flat" response, meaning that the graph of sound pressure versus frequency is constant over the band of audible frequencies. In this case the speaker's deficiencies can be corrected by the introduction of a passive filter with the inverse response (as shown) within the amplifiers of the radio.

As we will see, it is possible to generalize Ohm's law, replacing the word "resistance" with "impedance," in order to describe any circuit containing these linear passive devices (resistors, capacitors, and inductors). You could think of the subject of impedance (generalized resistance) as Ohm's law for circuits that include capacitors and inductors.

Some terminology: impedance $(\mathbf{Z})$ is the "generalized resistance"; inductors and capacitors, for which the voltage and current are always $90^{\circ}$ out of phase, are reactive; they have reactance $(X)$. Resistors, with voltage and current always in phase, are resistive; they have resistance ( $R$ ). In general, in a circuit that combines resistive and reactive components, the voltage and current at some place will have some in-between phase relationship, described by a complex impedance: impedance $=$ resistance + reactance, or $\mathbf{Z}=R+j X$ (more about this later). ${ }^{36}$ However, you'll see statements like "the impedance of the capacitor at this frequency is . . ." The reason you don't have to use the word "reactance" in such a case is that impedance covers everything. In fact, you frequently use the word "impedance" even when you know it's a resistance you're talking about; you say "the source impedance" or "the output impedance" when you mean the Thévenin equivalent resistance of some source. The same holds for "input impedance."

In all that follows, we will be talking about circuits driven by sinewaves at a single frequency. Analysis of circuits driven by complicated waveforms is more elaborate, involving the methods we used earlier (differential equations) or decomposition of the waveform into sinewaves (Fourier analysis). Fortunately, these methods are seldom necessary.

### 1.7.1 Frequency analysis of reactive circuits

Let's start by looking at a capacitor driven by a sinewave voltage source $V(t)=V_{0} \sin \omega t$ (Figure 1.88). The current

[^29]is
$$
I(t)=C \frac{d V}{d t}=C \omega V_{0} \cos \omega t,
$$
i.e., a current of amplitude $\omega C V_{0}$, with its phase leading the input voltage by $90^{\circ}$. If we consider amplitudes only, and disregard phases, the current is
$$
I=\frac{V}{1 / \omega C}
$$
(Recall that $\omega=2 \pi f$.) It behaves like a frequencydependent resistance $R=1 / \omega C$, but in addition the current is $90^{\circ}$ out of phase with the voltage (Figure 1.89).
image_name:Figure 1.88
description:
[
name: V(t), type: VoltageSource, value: V0sinωt, ports: {Np: Vin, Nn: GND}
name: C, type: Capacitor, value: C, ports: {Np: Vin, Nn: GND}
]
extrainfo:The circuit consists of a sinusoidal voltage source driving a capacitor, resulting in a current that leads the voltage by 90 degrees.

Figure 1.88. A sinusoidal ac voltage drives a capacitor.
image_name:Figure 1.89
description:The graph in Figure 1.89 consists of two sinusoidal waveforms plotted against time \( t \). The upper waveform represents the current \( I \), while the lower waveform represents the voltage \( V \). Both axes are labeled with \( t \) for time, although no specific units or scales are provided, suggesting a generic representation.

Type of Graph and Function:
- This is a time-domain waveform graph showing sinusoidal functions.

Axes Labels and Units:
- The horizontal axis represents time \( t \).
- The vertical axes represent current \( I \) and voltage \( V \) respectively.

Overall Behavior and Trends:
- Both waveforms are sinusoidal, indicating periodic behavior.
- The current waveform \( I \) leads the voltage waveform \( V \) by \( 90^{\circ} \). This phase difference is characteristic of a capacitive circuit where the current leads the voltage.

Key Features and Technical Details:
- The waveforms are smooth and continuous, with no abrupt changes or discontinuities.
- Each waveform crosses the time axis at regular intervals, indicating zero crossings.
- The peaks and troughs of the current waveform occur earlier in time compared to the voltage waveform, illustrating the phase lead.

Annotations and Specific Data Points:
- No specific numerical values or markers are provided on the graph.
- The graph visually demonstrates the concept of phase shift in capacitive circuits, where the current leads the voltage by \( 90^{\circ} \).

Figure 1.89. Current in a capacitor leads the sinusoidal voltage by $90^{\circ}$.

For example, a $1 \mu \mathrm{~F}$ capacitor put across the 115 volts (rms) 60 Hz powerline draws a current of rms amplitude:

$$
I=\frac{115}{1 /\left(2 \pi \times 60 \times 10^{-6}\right)}=43.4 \mathrm{~mA}(\mathrm{rms})
$$

Soon enough we will complicate matters by explicitly worrying about phase shifts and the like - and that will get us into some complex algebra that terrifies beginners (often) and mathophobes (always). Before we do that, though, this is a good time to develop intuition about the frequencydependent behavior of some basic and important circuits that use capacitors, ignoring for the time being the troublesome fact that, when driven with a sinusoidal signal, currents and voltages in a capacitor are not in phase.

As we just saw, the ratio of magnitudes of voltage to
current, in a capacitor driven at a frequency $\omega$, is just

$$
\frac{|V|}{|I|}=\frac{1}{\omega C}
$$

which we can think of as a sort of "resistance" - the magnitude of the current is proportional to the magnitude of the applied voltage. The official name for this quantity is reactance, with the symbol $X$, thus $X_{\mathrm{C}}$ for the reactance of a capacitor. ${ }^{37}$ So, for a capacitor,

$$
\begin{equation*}
X_{\mathrm{C}}=\frac{1}{\omega C} \tag{1.26}
\end{equation*}
$$

This means that a larger capacitance has a smaller reactance. And this makes sense, because, for example, if you double the value of a capacitor, it takes twice as much current to charge and discharge it through the same voltage swing in the same time (recall $I=C d V / d t$ ). For the same reason the reactance decreases as you increase the frequency - doubling the frequency (while holding $V$ constant) doubles the rate of change of voltage and therefore requires that you double the current, thus half the reactance.

So, roughly speaking, we can think of a capacitor as a "frequency-dependent resistor." Sometimes that's good enough, sometimes it isn't. We'll look at a few circuits in which this simplified view gets us reasonably good results, and provides nice intuition; later we'll fix it up, using the correct complex algebra, to get a precise result. (Keep in mind that the results we are about to get are approximate; we're lying to you - but it's a small lie, and anyway we'll tell the truth later. In the meantime we'll use the weird symbol $\asymp$ instead of = in all such "approximate equations," and we'll flag the equation as approximate.)
image_name:Figure 1.90. Lowpass filter
description:
[
name: Vin, type: VoltageSource, ports: {Np: Vin, Nn: GND}
name: R, type: Resistor, value: R, ports: {N1: Vin, N2: Vout}
name: C, type: Capacitor, value: C, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is a simple RC lowpass filter where the resistor R and capacitor C form a frequency-dependent voltage divider. It allows low frequencies to pass while attenuating high frequencies. The input is Vin and the output is Vout.

Figure 1.90. Lowpass filter.

#### A. RC lowpass filter (approximate)

The circuit in Figure 1.90 is called a lowpass filter, because it passes low frequencies and blocks high frequencies. If you think of it as a frequency-dependent voltage divider, this makes sense: the lower leg of the divider (the capacitor) has a decreasing reactance with increasing frequency, so the ratio of $V_{\text {out }} / V_{\text {in }}$ decreases accordingly:

[^30]image_name:Figure 1.91
description:The graph in Figure 1.91 consists of two plots, each illustrating different aspects of the frequency response of an RC lowpass filter.

1. **Type of Graph and Function:**
- The lower plot is a Bode plot, showing the frequency response of the filter. It displays both approximate and exact results for the transfer function \( \frac{V_{\text{out}}}{V_{\text{in}}} \) as a function of normalized frequency \( \frac{f}{f_0} \).
- The upper plot shows the percentage error between the approximate and exact results.

2. **Axes Labels and Units:**
- **Lower Plot:**
- The x-axis is labeled \( f/f_0 \), representing the normalized frequency on a logarithmic scale.
- The y-axis is labeled \( V_{\text{out}}/V_{\text{in}} \), representing the normalized output voltage.
- **Upper Plot:**
- The x-axis is the same as the lower plot, \( f/f_0 \).
- The y-axis is labeled \(% \text{ error}\), representing the percentage error.

3. **Overall Behavior and Trends:**
- **Lower Plot:**
- The solid line represents the exact result, while the dashed line represents the approximate solution.
- At low frequencies (\( f/f_0 < 1 \)), the lowpass filter maintains a high output (close to 1), while the highpass filter's output is low.
- At high frequencies (\( f/f_0 > 1 \)), the lowpass filter's output decreases, and the highpass filter's output increases, approaching 1.
- **Upper Plot:**
- The percentage error is low at both extremes of the frequency range and peaks around \( f/f_0 = 1 \).

4. **Key Features and Technical Details:**
- The crossover point where \( V_{\text{out}}/V_{\text{in}} \) for the lowpass and highpass filters is 0.5 occurs at \( f/f_0 = 1 \).
- The maximum percentage error is approximately -30% around \( f/f_0 = 1 \).

5. **Annotations and Specific Data Points:**
- The lower plot is annotated with 'approx' and 'exact' to distinguish between the approximate and exact curves.
- The terms 'highpass' and 'lowpass' indicate the respective regions where each filter type dominates.

Overall, the graph clearly illustrates the behavior of an RC lowpass filter, highlighting the differences between approximate and exact calculations and their respective errors across a range of frequencies.

Figure 1.91. Frequency response of single-section $R C$ filters, showing the results both of a simple approximation that ignores phase (dashed curve), and the exact result (solid curve). The fractional error (i.e., dashed/solid) is plotted above.

$$
\begin{equation*}
\frac{V_{\text {out }}}{V_{\text {in }}} \asymp \frac{X_{\mathrm{C}}}{R+X_{\mathrm{C}}}=\frac{1 / \omega C}{R+1 / \omega C}=\frac{1}{1+\omega R C} \quad \text { (approximate!) } \tag{1.27}
\end{equation*}
$$

We've plotted that ratio in Figure 1.91 (and also that of its cousin, the highpass filter), along with their exact results that we'll understand soon enough in §1.7.8.

You can see that the circuit passes low frequencies fully (because at low frequencies the capacitor's reactance is very high, so it's like a divider with a smaller resistor atop a larger one) and that it blocks high frequencies. In particular, the crossover from "pass" to "block" (often called the breakpoint) occurs at a frequency $\omega_{0}$ at which the capacitor's reactance $\left(1 / \omega_{0} C\right)$ is equal to the resistance $R: \omega_{0}=$ $1 / R C$. At frequencies well beyond the crossover (where the product $\omega R C \gg 1$ ), the output decreases inversely with increasing frequency; that makes sense because the reactance of the capacitor, already much smaller than $R$, continues dropping as $1 / \omega$. It's worth noting that, even with our "ignoration of phase shifts," the equation (and graph) for the ratio of voltages is quite accurate at both low and high frequencies and is only modestly in error around the crossover
frequency, where the correct ratio is $V_{\text {out }} / V_{\text {in }}=1 / \sqrt{2} \approx$ 0.7 , rather than the 0.5 that we got. ${ }^{38}$
image_name:Figure 1.92. Highpass filter
description:
[
name: C, type: Capacitor, value: C, ports: {Np: Vin, Nn: Vout}
name: R, type: Resistor, value: R, ports: {N1: Vout, N2: GND}
]
extrainfo:This is an RC highpass filter. It passes high frequencies and blocks low frequencies.

Figure 1.92. Highpass filter.

#### B. RC highpass filter (approximate)

You get the reverse behavior (pass high frequencies, block low) by interchanging $R$ and $C$, as in Figure 1.92. Treating it as a frequency-dependent voltage divider, and ignoring phase shifts once again, we get (see Figure 1.91)

$$
\begin{equation*}
\frac{V_{\text {out }}}{V_{\text {in }}} \asymp \frac{R}{R+X_{C}}=\frac{R}{R+1 / \omega C}=\frac{\omega R C}{1+\omega R C} \quad \text { (approximate!) } \tag{1.28}
\end{equation*}
$$

High frequencies (above the same crossover frequency as before, $\omega \gg \omega_{0}=1 / R C$ ) pass through (because the capacitor's reactance is much smaller than $R$ ), whereas frequencies well below the crossover are blocked (the capacitor's reactance is much larger than $R$ ). As before, the equation and graph are accurate at both ends, and only modestly in error at the crossover, where the correct ratio is, again, $V_{\text {out }} / V_{\text {in }}=1 / \sqrt{2}$.

#### C. Blocking capacitor

Sometimes you want to let some band of signal frequencies pass through a circuit, but you want to block any steady dc voltage that may be present (we'll see how this can happen when we learn about amplifiers in the next chapter). You can do the job with an $R C$ highpass filter if you choose the crossover frequency correctly: a highpass filter always blocks dc, so what you do is choose component values so that the crossover frequency is below all frequencies of interest. This is one of the more frequent uses of a capacitor and is known as a dc blocking capacitor.

For instance, every stereo audio amplifier has all its inputs capacitively coupled, because it doesn't know what dc level its input signals might be riding on. In such a coupling application you always pick $R$ and $C$ so that all frequencies of interest (in this case, 20 Hz to 20 kHz ) are passed

[^31]without loss (attenuation). That determines the product $R C: R C>1 / \omega_{\min }$, where for this case you might choose $f_{\min } \approx 5 \mathrm{~Hz}$, and so $R C=1 / \omega_{\min }=1 / 2 \pi f_{\min } \approx 30 \mathrm{~ms}$.
image_name:Figure 1.93
description:
[
name: pre-amp, type: OpAmp, value: pre-amp, ports: {InP: Vin, InN: GND, Out: N1}
name: C, type: Capacitor, value: 3.3µF, ports: {Np: N1, Nn: N2}
name: R, type: Resistor, value: 10k, ports: {N1: N2, N2: GND}
name: amplifier, type: OpAmp, value: amplifier, ports: {InP: N2, InN: GND, Out: Vout}
]
extrainfo:The circuit is a high-pass filter with a cutoff frequency of approximately 5 Hz, using a pre-amplifier, a coupling capacitor, and a resistor to block DC components.

Figure 1.93. "Blocking capacitor": a highpass filter for which all signal frequencies of interest are in the passband.

You've got the product, but you still have to choose individual values for $R$ and $C$. You do this by noticing that the input signal sees a load equal to $R$ at signal frequencies (where $C$ 's reactance is small - it's just a piece of wire there), so you choose $R$ to be a reasonable load, i.e., not so small that it's hard to drive, and not so large that the circuit is prone to signal pickup from other circuits in the box. In the audio business it's common to see a value of $10 \mathrm{k} \Omega$, so we might choose that value, for which the corresponding $C$ is $3.3 \mu \mathrm{~F}$ (Figure 1.93). The circuit connected to the output should have an input resistance much greater than $10 \mathrm{k} \Omega$, to avoid loading effects on the filter's output; and the driving circuit should be able to drive a $10 \mathrm{k} \Omega$ load without significant attenuation (loss of signal amplitude) to prevent circuit loading effects by the filter on the signal source. It's worth noting that our approximate model, ignoring phase shifts, is perfectly adequate for blocking capacitor design; that is because the signal band is fully in the passband, where the effects of phase shifts are negligible.

In this section we've been thinking in the frequency domain (sinewaves of frequency $f$ ). But it's useful to think in the time domain, where, for example, you might use a blocking capacitor to couple pulses, or square waves. In such situations you encounter waveform distortion, in the form of "droop" and overshoot (rather than the simple amplitude attenuation and phase shift you get with sinusoidal waves). Thinking in the time domain, the criterion you use to avoid waveform distortion in a pulse of duration $T$ is that the time constant $\tau=R C \gg T$. The resulting droop is approximately $T / \tau$ (followed by a comparable overshoot at the next transition).

You often need to know the reactance of a capacitor at a given frequency (e.g., for design of filters). Figure 1.100 in §1.7.8 provides a very useful graph covering large ranges
of capacitance and frequency, giving the value of $X_{C}=$ $1 / 2 \pi f C$.

#### D. Driving and loading RC filters

This example of an audio-blocking capacitor raised the issue of driving and loading $R C$ filter circuits. As we discussed in $\S 1.2 .5 \mathrm{~A}$, in the context of voltage dividers, you generally like to arrange things so that the circuit being driven does not significantly load the driving resistance (Thévenin equivalent source resistance) of the signal source.

The same logic applies here, but with a generalized kind of resistance that includes the reactance of capacitors (and inductors), known as impedance. So a signal source's impedance should generally be small compared with the impedance of the thing being driven. ${ }^{39}$ We'll have a precise way of talking about impedance shortly, but it's correct to say that, apart from phase shifts, the impedance of a capacitor is equal to its reactance.

What we want to know, then, are the input and output impedances of the two simple $R C$ filters (lowpass and highpass). This sounds complicated, because there are four impedances, and they all vary with frequency. However, if you ask the question the right way, the answer is simple, and the same in all cases!

First, assume that in each case the right thing is being done to the other end of the filter: when we ask the input impedance, we assume the output drives a high impedance (compared with its own); and when we ask the output impedance, we assume the input is driven by a signal source of low internal (Thévenin) impedance. Second, we dispose of the variation of impedances with frequency by asking only for the worst-case value; that is, we care what only the maximum output impedance of a filter circuit may be (because that is the worst for driving a load), and we care about only the minimum input impedance (because that is the hardest to drive).

Now the answer is astonishingly simple: in all cases the worst-case impedance is just $R$.
Exercise 1.23. Show that the preceding statement is correct.
So, for example, if you want to hang an $R C$ lowpass filter onto the output of an amplifier whose output resistance is $100 \Omega$, start with $R=1 \mathrm{k}$, then choose $C$ for the breakpoint you want. Be sure that whatever loads the output has an input impedance of at least 10k. You can't go wrong.

Exercise 1.24. Design a two-stage "bandpass" $R C$ filter, in which

[^32]the first stage is highpass with a breakpoint of 100 Hz , and the second stage is lowpass with a breakpoint of 10 kHz . Assume the input signal source has an impedance of $100 \Omega$. What is the worstcase output impedance of your filter, and therefore what is the minimum recommended load impedance?

### 1.7.2 Reactance of inductors

Before we embark on a fully correct treatment of impedance, replete with complex exponentials and the like, let's use our approximation tricks to figure out the reactance of an inductor.

It goes as before: we imagine an inductor $L$ driven by a sinusoidal voltage source of angular frequency $\omega$ such that a current $I(t)=I_{0} \sin \omega t$ is flowing. ${ }^{40}$ Then the voltage across the inductor is

$$
V(t)=L \frac{d I(t)}{d t}=L \omega I_{0} \cos \omega t
$$

And so the ratio of magnitudes of voltage to current - the resistance-like quantity called reactance - is just

$$
\frac{|V|}{|I|}=\frac{L \omega I_{0}}{I_{0}}=\omega L
$$

So. for an inductor,

$$
\begin{equation*}
X_{\mathrm{L}}=\omega L \tag{1.29}
\end{equation*}
$$

Inductors, like capacitors, have a frequency-dependent reactance; however, here the reactance increases with increasing frequency (the opposite of capacitors, where it decreases with increasing frequency). So, in the simplest view, a series inductor can be used to pass dc and low frequencies (where its reactance is small) while blocking high frequencies (where its reactance is high). You often see inductors used this way, particularly in circuits that operate at radio frequencies; in that application they're sometimes called chokes.

### 1.7.3 Voltages and currents as complex numbers

At this point it is necessary to get into some complex algebra; you may wish to skip over the math in some of the following sections, taking note of the results as we derive them. A knowledge of the detailed mathematics is not necessary for understanding the remainder of the book. Very little mathematics will be used in later chapters. The section ahead is easily the most difficult for the reader with little mathematical preparation. Don't be discouraged!

As we've just seen, there can be phase shifts between

[^33]the voltage and current in an ac circuit being driven by a sinewave at some frequency. Nevertheless, as long as the circuit contains only linear elements (resistors, capacitors, inductors), the magnitudes of the currents everywhere in the circuit are still proportional to the magnitude of the driving voltage, so we might hope to find some generalization of voltage, current, and resistance in order to rescue Ohm's law. Evidently a single number won't suffice to specify the current, say, at some point in the circuit, because we must somehow have information about both the magnitude and phase shift.

Although we can imagine specifying the magnitudes and phase shifts of voltages and currents at any point in the circuit by writing them out explicitly, e.g., $V(t)=$ $23.7 \sin (377 t+0.38)$, it turns out that we can meet our requirements more simply by using the algebra of complex numbers to represent voltages and currents. Then we can simply add or subtract the complex number representations, rather than laboriously having to add or subtract the actual sinusoidal functions of time themselves. Because the actual voltages and currents are real quantities that vary with time, we must develop a rule for converting from actual quantities to their representations, and vice versa. Recalling once again that we are talking about a single sinewave frequency, $\omega$, we agree to use the following rules.

1. Voltages and currents are represented by the complex quantities $\mathbf{V}$ and $\mathbf{I}$. The voltage $V_{0} \cos (\omega t+\phi)$ is to be represented by the complex number $V_{0} e^{j \phi}$. Recall that $e^{j \phi}=\cos \phi+j \sin \phi$, where $j=\sqrt{-1}$.
2. We obtain actual voltages and currents by multiplying their complex number representations by $e^{j \omega t}$ and then taking the real part: $V(t)=\mathscr{R} e\left(\mathbf{V} e^{j \omega t}\right), I(t)=$ $\mathscr{R} e\left(\mathbf{I}^{j \omega t}\right)$.

In other words,

| circuit voltage versus time |  | complex number representation |
| :---: | :---: | :---: |
| $V_{0} \cos (\omega t+\phi)$ |  | $V_{0} e^{j \phi}=a+j b$ |
|  | multiply by $e^{j \omega t}$ and take real part |  |

(In electronics, the symbol $j$ is used instead of $i$ in the exponential in order to avoid confusion with the symbol $i$ meaning small-signal current.) Thus, in the general case, the actual voltages and currents are given by

$$
\begin{aligned}
V(t) & =\mathscr{R e} e\left(\mathbf{V} e^{j \omega t}\right) \\
& =\mathscr{R} e(\mathbf{V}) \cos \omega t-\mathscr{I} m(\mathbf{V}) \sin \omega t
\end{aligned}
$$

$$
\begin{aligned}
I(t) & =\mathscr{R} e\left(\mathbf{I} e^{j \omega t}\right) \\
& =\mathscr{R} e(\mathbf{I}) \cos \omega t-\mathscr{I} m(\mathbf{I}) \sin \omega t .
\end{aligned}
$$

For example, a voltage whose complex representation is

$$
\mathbf{V}=5 j
$$

corresponds to a (real) voltage versus time of

$$
\begin{aligned}
V(t) & =\mathscr{R} e[5 j \cos \omega t+5 j(j) \sin \omega t] \\
& =-5 \sin \omega t \text { volts. }
\end{aligned}
$$

### 1.7.4 Reactance of capacitors and inductors

With this convention we can apply complex Ohm's law correctly to circuits containing capacitors and inductors, just as for resistors, once we know the reactance of a capacitor or inductor. Let's find out what these are. We begin with a simple (co)sinusoidal voltage $V_{0} \cos \omega t$ applied across a capacitor:

$$
V(t)=\mathscr{R} e\left(V_{0} e^{j \omega t}\right) .
$$

Then, using $I=C(d V(t) / d t)$, we obtain

$$
\begin{aligned}
I(t) & =-V_{0} C \omega \sin \omega t=\mathscr{R} e\left(\frac{V_{0} e^{j \omega t}}{-j / \omega C}\right), \\
& =\mathscr{R} e\left(\frac{V_{0} e^{j \omega t}}{\mathbf{Z}_{\mathrm{C}}}\right)
\end{aligned}
$$

i.e., for a capacitor

$$
\mathbf{Z}_{\mathrm{C}}=-j / \omega C \quad\left(=-j X_{\mathrm{C}}\right) ;
$$

$\mathbf{Z}_{\mathrm{C}}$ is the impedance of a capacitor at frequency $\omega$; it is equal in magnitude to the reactance $X_{C}=1 / \omega C$ that we found earlier, but with a factor of $-j$ that accounts for the $90^{\circ}$ leading phase shift of current versus voltage. As an example, a $1 \mu \mathrm{~F}$ capacitor has an impedance of $-2653 j \Omega$ at 60 Hz , and $-0.16 j \Omega$ at 1 MHz . The corresponding reactances are $2653 \Omega$ and $0.16 \Omega .{ }^{41}$ Its reactance (and also its impedance) at dc is infinite.

If we did a similar analysis for an inductor, we would find

$$
\mathbf{Z}_{\mathrm{L}}=j \omega L \quad\left(=j X_{\mathrm{L}}\right) .
$$

A circuit containing only capacitors and inductors always has a purely imaginary impedance, meaning that the voltage and current are always $90^{\circ}$ out of phase - it is purely reactive. When the circuit contains resistors, there is also

[^34]a real part to the impedance. The term "reactance" in that case means the imaginary part only.

### 1.7.5 Ohm's law generalized

With these conventions for representing voltages and currents, Ohm's law takes a simple form. It reads simply

$$
\begin{aligned}
\mathbf{I} & =\mathbf{V} / \mathbf{Z} \\
\mathbf{V} & =\mathbf{I Z}
\end{aligned}
$$

where the voltage represented by $\mathbf{V}$ is applied across a circuit of impedance $\mathbf{Z}$, giving a current represented by $\mathbf{I}$. The complex impedance of devices in series or parallel obeys the same rules as resistance:

$$
\begin{align*}
& \mathbf{Z}=\mathbf{Z}_{\mathbf{1}}+\mathbf{Z}_{\mathbf{2}}+\mathbf{Z}_{\mathbf{3}}+\cdots \quad \text { (series) }  \tag{1.30}\\
& \mathbf{Z}=\frac{1}{\frac{1}{\mathbf{Z}_{1}}+\frac{1}{\mathbf{Z}_{\mathbf{2}}}+\frac{1}{\mathbf{Z}_{3}}+\cdots} \quad \text { (parallel) } \tag{1.31}
\end{align*}
$$

Finally, for completeness we summarize here the formulas for the impedance of resistors, capacitors, and inductors:

$$
\begin{array}{ll}
\mathbf{Z}_{\mathrm{R}}=R & (\text { (resistor) } \\
\mathbf{Z}_{\mathrm{C}}=-j / \omega C=1 / j \omega C & \text { (capacitor) }  \tag{1.32}\\
\mathbf{Z}_{\mathrm{L}}=j \omega L & \text { (inductor) }
\end{array}
$$

With these rules we can analyze many ac circuits by the same general methods we used in handling dc circuits, i.e., application of the series and parallel formulas and Ohm's law. Our results for circuits such as voltage dividers will look nearly the same as before. For multiply-connected networks we may have to use Kirchhoff's laws, just as with dc circuits, in this case using the complex representations for $V$ and $I$ : the sum of the (complex) voltage drops around a closed loop is zero, and the sum of the (complex) currents into a point is zero. The latter rule implies, as with dc circuits, that the (complex) current in a series circuit is the same everywhere.

Exercise 1.25. Use the preceding rules for the impedance of devices in parallel and in series to derive the formulas (1.17) and (1.18) for the capacitance of two capacitors (a) in parallel and (b) in series. Hint: in each case, let the individual capacitors have capacitances $C_{1}$ and $C_{2}$. Write down the impedance of the parallel or series combination; then equate it to the impedance of a capacitor with capacitance $C$. Then find $C$.

Let's try out these techniques on the simplest circuit imaginable, an ac voltage applied across a capacitor, which we looked at earlier, in §1.7.1. Then, after a brief look at power in reactive circuits (to finish laying the groundwork),
we'll analyze (correctly, this time) the simple but extremely important and useful $R C$ lowpass and highpass filter circuits.

Imagine putting a $1 \mu \mathrm{~F}$ capacitor across a 115 volts (rms) 60 Hz powerline. What current flows? Using complex Ohm's law, we have

$$
\mathbf{Z}=-j / \omega C
$$

Therefore, the current is given by

$$
\mathbf{I}=\mathbf{V} / \mathbf{Z}
$$

The phase of the voltage is arbitrary, so let us choose $\mathbf{V}=$ $A$, i.e., $V(t)=A \cos \omega t$, where the amplitude $A=115 \sqrt{2} \approx$ 163 volts. Then

$$
\mathbf{I}=j \omega C A \approx-0.061 \sin \omega t
$$

The resulting current has an amplitude of 61 mA ( 43 mA rms) and leads the voltage by $90^{\circ}$. This agrees with our previous calculation. More simply, we could have noticed that the impedance of the capacitor is negative imaginary, so whatever the absolute phase of $V$, the phase of $I_{\text {cap }}$ must lead by $90^{\circ}$. And in general the phase angle between current and voltage, for any two-terminal $R L C$ circuit, is equal to the angle of the (complex) impedance of that circuit.

Note that if we wanted to know just the magnitude of the current, and didn't care what the relative phase was, we could have avoided doing any complex algebra: if

$$
\mathbf{A}=\mathbf{B} / \mathbf{C}
$$

then

$$
A=B / C
$$

where $A, B$, and $C$ are the magnitudes of the respective complex numbers; this holds for multiplication, also (see Exercise 1.18). Thus, in this case,

$$
I=V / Z=\omega C V
$$

This trick, which we used earlier (because we didn't know any better), is often useful.

Surprisingly, there is no power dissipated by the capacitor in this example. Such activity won't increase your electric bill; you'll see why in the next section. Then we will go on to look at circuits containing resistors and capacitors with our complex Ohm's law.

Exercise 1.26. Show that, if $\mathbf{A}=\mathbf{B C}$, then $A=B C$, where $A, B$, and $C$ are magnitudes. Hint: represent each complex number in polar form, i.e., $\mathbf{A}=A e^{i \theta}$.
image_name:Figure 1.94
description:The graph in Figure 1.94 is a time-domain waveform illustrating the relationship between voltage \( V(t) \) and current \( I(t) \) across a capacitor in an AC circuit. The graph is plotted with time \( t \) on the horizontal axis, marked with points A, B, C, and D, and the vertical axis representing the magnitude of \( V(t) \) and \( I(t) \). The units for the axes are not specified, but the graph is likely using standard units such as volts for voltage and amperes for current.

The key feature of this graph is the phase relationship between the voltage and current waveforms. The voltage \( V(t) \) is shown as a sinusoidal wave, and the current \( I(t) \) is also sinusoidal but leads the voltage by a phase shift of \( 90^{\circ} \). This phase shift is typical of capacitive circuits, where the current waveform reaches its peak values before the voltage waveform does.

The graph shows periodic oscillations, with both \( V(t) \) and \( I(t) \) having the same frequency but differing in phase. The current \( I(t) \) waveform crosses zero before the voltage \( V(t) \) waveform, indicating the leading phase. The points A, B, C, and D likely denote specific time intervals or significant points in the cycle, such as zero crossings or peak values, although their exact significance is not detailed in the image.

Overall, the graph effectively demonstrates the concept that in a purely capacitive AC circuit, the power delivered over a full cycle is zero due to the phase difference, which results in energy being alternately stored and released by the capacitor without net consumption.

Figure 1.94. The power delivered to a capacitor is zero over a full sinusoidal cycle, owing to the $90^{\circ}$ phase shift between voltage and current.

### 1.7.6 Power in reactive circuits

The instantaneous power delivered to any circuit element is always given by the product $P=V I$. However, in reactive circuits where $V$ and $I$ are not simply proportional, you can't just multiply their amplitudes together. Funny things can happen; for instance, the sign of the product can reverse over one cycle of the ac signal. Figure 1.94 shows an example. During time intervals $A$ and $C$, power is being delivered to the capacitor (albeit at a variable rate), causing it to charge up; its stored energy is increasing (power is the rate of change of energy). During intervals $B$ and $D$, the power delivered to the capacitor is negative; it is discharging. The average power over a whole cycle for this example is in fact exactly zero, a statement that is always true for any purely reactive circuit element (inductors, capacitors, or any combination thereof). If you know your trigonometric integrals, the next exercise will show you how to prove this.

Exercise 1.27. Optional exercise: prove that a circuit whose current is $90^{\circ}$ out of phase with the driving voltage consumes no power, averaged over an entire cycle.

How do we find the average power consumed by an arbitrary circuit? In general, we can imagine adding up little pieces of VI product, then dividing by the elapsed time. In other words,

$$
\begin{equation*}
P=\frac{1}{T} \int_{0}^{T} V(t) I(t) d t \tag{1.33}
\end{equation*}
$$

where $T$ is the time for one complete cycle. Luckily, that's almost never necessary. Instead, it is easy to show that the average power is given by

$$
\begin{equation*}
P=\mathscr{R} e\left(\mathbf{V} \mathbf{I}^{*}\right)=\mathscr{R} e\left(\mathbf{V}^{*} \mathbf{I}\right), \tag{1.34}
\end{equation*}
$$

where $\mathbf{V}$ and $\mathbf{I}$ are complex rms amplitudes (and an asterisk means complex conjugate - see the math review, Appendix A, if this is unfamiliar).

Let's take an example. Consider the preceding circuit, with a 1 volt (rms) sinewave driving a capacitor. We'll do everything with rms amplitudes, for simplicity. We have

$$
\begin{aligned}
\mathbf{V} & =1 \\
\mathbf{I} & =\frac{\mathbf{V}}{-j / \omega C}=j \omega C \\
P & =\mathscr{R} e\left(\mathbf{V I}^{*}\right)=\mathscr{R} e(-j \omega C)=0 .
\end{aligned}
$$

That is, the average power is zero, as stated earlier.
image_name:Figure 1.95
description:
[
name: V0 cos ωt, type: VoltageSource, value: V0 cos ωt, ports: {Np: Vin, Nn: GND}
name: C, type: Capacitor, value: C, ports: {Np: Vin, Nn: Vout}
name: R, type: Resistor, value: R, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit is a series RC circuit driven by an AC voltage source V0 cos ωt. The current I flows through the capacitor C and resistor R in series. The average power in the circuit is calculated as P = V0^2 R / (R^2 + (1/ω^2 C^2)).

Figure 1.95. Power and power factor in a series $R C$ circuit.
As another example, consider the circuit shown in Figure 1.95. Our calculations go like this:

$$
\begin{aligned}
\mathbf{Z} & =R-\frac{j}{\omega C} \\
\mathbf{V} & =V_{0} \\
\mathbf{I} & =\frac{\mathbf{V}}{\mathbf{Z}}=\frac{V_{0}}{R-(j / \omega C)}=\frac{V_{0}[R+(j / \omega C)]}{R^{2}+\left(1 / \omega^{2} C^{2}\right)} \\
P & =\mathscr{R} e\left(\mathbf{V I}^{*}\right)=\frac{V_{0}^{2} R}{R^{2}+\left(1 / \omega^{2} C^{2}\right)}
\end{aligned}
$$

(In the third line we multiplied numerator and denominator by the complex conjugate of the denominator in order to make the denominator real.) The calculated power ${ }^{42}$ is less than the product of the magnitudes of $\mathbf{V}$ and $\mathbf{I}$. In fact, their ratio is called the power factor:

$$
\begin{aligned}
|\mathbf{V}||\mathbf{I}| & =\frac{V_{0}^{2}}{\left[R^{2}+\left(1 / \omega^{2} C^{2}\right)\right]^{1 / 2}} \\
\text { power factor } & =\frac{\text { power }}{|\mathbf{V}||\mathbf{I}|} \\
& =\frac{R}{\left[R^{2}+\left(1 / \omega^{2} C^{2}\right)\right]^{1 / 2}}
\end{aligned}
$$

[^35]in this case. The power factor is the cosine of the phase angle between the voltage and the current, and it ranges from 0 (purely reactive circuit) to 1 (purely resistive). A power factor of less than 1 indicates some component of reactive current. ${ }^{43}$ It's worth noting that the power factor goes to unity, and the dissipated power goes to $V^{2} / R$, in the limit of large capacitance (or of high frequency), where the reactance of the capacitor becomes much less than $R$.

Exercise 1.28. Show that all the average power delivered to the preceding circuit winds up in the resistor. Do this by computing the value of $V_{R}^{2} / R$. What is that power, in watts, for a series circuit of a $1 \mu \mathrm{~F}$ capacitor and a 1.0 k resistor placed across the 115 volt (rms), 60 Hz powerline?

Power factor is a serious matter in large-scale electrical power distribution, because reactive currents don't result in useful power being delivered to the load, but cost the power company plenty in terms of $I^{2} R$ heating in the resistance of generators, transformers, and wiring. Although residential users are billed only for "real" power $\left[\mathscr{R} e\left(\mathbf{V I}^{*}\right)\right]$, the power company charges industrial users according to the power factor. This explains the capacitor yards that you see behind large factories, built to cancel the inductive reactance of industrial machinery (i.e., motors).

Exercise 1.29. Show that adding a series capacitor of value $C=$ $1 / \omega^{2} L$ makes the power factor equal 1.0 in a series $R L$ circuit. Now do the same thing, but with the word "series" changed to "parallel."

### 1.7.7 Voltage dividers generalized

Our original voltage divider (Figure 1.6) consisted of a pair of resistors in series to ground, input at the top and output at the junction. The generalization of that simple resistive divider is a similar circuit in which either or both resistors are replaced with a capacitor or inductor (or a more complicated network made from $R, L$, and $C$ ), as in Figure 1.96. In general, the division ratio $V_{\text {out }} / V_{\text {in }}$ of such a divider is not constant, but depends on frequency (as we have already seen, in our approximate treatment of the lowpass and highpass filters in §1.7.1). The analysis is straightforward:

$$
\begin{aligned}
\mathbf{I} & =\frac{\mathbf{V}_{\text {in }}}{\mathbf{Z}_{\text {total }}} \\
\mathbf{Z}_{\text {total }} & =\mathbf{Z}_{1}+\mathbf{Z}_{2}
\end{aligned}
$$

[^36]image_name:Figure 1.96
description:
[
name: Z1, type: Other, ports: {N1: Vin, N2: X1}
name: Z2, type: Other, ports: {N1: X1, N2: GND}
]
extrainfo:The circuit is a generalized voltage divider with two impedances Z1 and Z2. Vin is the input voltage, Vout is taken from the node between Z1 and Z2, and the lower end of Z2 is connected to ground.

Figure 1.96. Generalized voltage divider: a pair of arbitrary impedances.

$$
\mathbf{V}_{\mathrm{out}}=\mathbf{I} \mathbf{Z}_{2}=\mathbf{V}_{\mathrm{in}} \frac{\mathbf{Z}_{2}}{\mathbf{Z}_{1}+\mathbf{Z}_{2}}
$$

Rather than worrying about this result in general, let's look at some simple (but very important) examples, beginning with the $R C$ highpass and lowpass filters we approximated earlier.

### 1.7.8 RC highpass filters

We've seen that by combining resistors with capacitors it is possible to make frequency-dependent voltage dividers, owing to the frequency dependence of a capacitor's impedance $\mathbf{Z}_{\mathrm{C}}=-j / \omega C$. Such circuits can have the desirable property of passing signal frequencies of interest while rejecting undesired signal frequencies. In this subsection and the next we revisit the simple lowpass and highpass $R C$ filters, correcting the approximate analysis of $\S 1.7 .1$; though simple, these circuits are important and widely used. Chapter 6 and Appendix E describe filters of greater sophistication.

Referring back to the classic $R C$ highpass filter (Figure 1.92), we see that the complex Ohm's law (or the complex voltage-divider equation) gives

$$
\mathbf{V}_{\text {out }}=\mathbf{V}_{\text {in }} \frac{R}{R-j / \omega C}=\mathbf{V}_{\text {in }} \frac{R(R+j / \omega C)}{R^{2}+\left(1 / \omega^{2} C^{2}\right)}
$$

(For the last step, multiply top and bottom by the complex conjugate of the denominator.) Most often we don't care about the phase of $V_{\text {out }}$, just its amplitude:

$$
\begin{aligned}
V_{\text {out }} & =\left(\mathbf{V}_{\text {out }} \mathbf{V}_{\text {out }}^{*}\right)^{1 / 2} \\
& =\frac{R}{\left[R^{2}+\left(1 / \omega^{2} C^{2}\right)\right]^{1 / 2}} V_{\text {in }}
\end{aligned}
$$

Note the analogy to a resistive divider, where

$$
V_{\text {out }}=\frac{R_{2}}{R_{1}+R_{2}} V_{\text {in }}
$$

Here the impedance of the series $R C$ combination
image_name:Figure 1.97. Input impedance of unloaded highpass filter.
description:
[
name: C, type: Capacitor, value: C, ports: {Np: Vin, Nn: X}
name: R, type: Resistor, value: R, ports: {N1: X, N2: Vout}
]
extrainfo:This is a high-pass filter circuit consisting of a series capacitor and a parallel resistor.

Figure 1.97. Input impedance of unloaded highpass filter.
image_name:Figure 1.98. Impedance of series R C.
description:The graph in Figure 1.98 represents a phasor diagram depicting the impedance of a series RC circuit. The x-axis is labeled as the real part of the impedance, denoted by \( R \), while the y-axis represents the imaginary part of the impedance, denoted by \( jZ \). The graph uses a complex plane to illustrate the total impedance \( Z_{\text{total}} \) as a vector.

Type of Graph and Function:
This is a phasor diagram, a type of polar plot used to represent complex numbers, specifically the impedance in this case.

Axes Labels and Units:
- **X-axis (Real part):** Labeled as \( R \) (resistance component of the impedance).
- **Y-axis (Imaginary part):** Labeled as \( -j/\omega C \) (reactance component of the impedance).
- The units are typically ohms (Ω), although not explicitly mentioned.

Overall Behavior and Trends:
The vector \( Z_{\text{total}} \) is shown pointing from the origin to a point defined by the real component \( R \) and the imaginary component \( -j/\omega C \). This vector forms an angle \( \phi \) with the real axis, indicating the phase difference between the voltage and current through the RC circuit.

Key Features and Technical Details:
- **Vector Magnitude:** The magnitude of the total impedance \( |Z_{\text{total}}| \) is calculated using the formula \( \sqrt{R^2 + \frac{1}{\omega^2 C^2}} \).
- **Phase Angle:** The phase angle \( \phi \) is determined by \( \tan^{-1}\left(\frac{-1/\omega C}{R}\right) \), which indicates the phase shift introduced by the circuit.
- **Impedance Components:** The total impedance \( Z_{\text{total}} \) is expressed as \( R - j/\omega C \), showing both the resistive and reactive components.

Annotations and Specific Data Points:
- The diagram includes annotations for the vector components and the angle \( \phi \).
- The formulas for calculating the magnitude and phase angle are provided, highlighting the mathematical relationships involved in analyzing the circuit's impedance.

Figure 1.98. Impedance of series $R C$.
image_name:Figure 1.99
description:The graph in Figure 1.99 is a Bode plot depicting the frequency response of a highpass filter. The plot shows the relationship between the frequency \( \omega \) (on the x-axis) and the gain \( \frac{V_{\text{out}}}{V_{\text{in}}} \) (on the y-axis). The x-axis is labeled \( \omega \) and represents frequency, while the y-axis is labeled \( \frac{V_{\text{out}}}{V_{\text{in}}} \) and represents the gain, which is dimensionless. The scale of the x-axis is logarithmic, which is typical for Bode plots, although this is not explicitly marked on the graph.

Overall Behavior and Trends:
The graph shows that at low frequencies, the gain is low, approaching zero as \( \omega \) approaches zero. As the frequency increases, the gain increases. This behavior is characteristic of a highpass filter, which attenuates low-frequency signals and allows high-frequency signals to pass through.

Key Features and Technical Details:
- **Cutoff Frequency:** The graph highlights a critical point at \( \omega_{3\text{dB}} = \frac{1}{RC} \), which is the cutoff frequency where the gain is reduced by 3 dB from its maximum value. This point is marked on the graph and indicates the frequency at which the output power drops to half of the input power.
- **Slope:** Below the cutoff frequency, the graph shows a linear increase in gain, which is proportional to \( \omega \). This is indicated by the dashed line that shows the slope of the gain increase.
- **Asymptotic Behavior:** As the frequency continues to increase beyond the cutoff frequency, the gain approaches a maximum value of 1.0, indicating that the filter allows these frequencies to pass through with minimal attenuation.

Annotations and Specific Data Points:
- The graph includes a marker at the \(-3\text{dB}\) point, which is a standard reference in filter design to identify the cutoff frequency.
- An annotation indicates that the gain \( \frac{V_{\text{out}}}{V_{\text{in}}} \) is proportional to \( \omega \) at frequencies below the cutoff, reinforcing the characteristic behavior of a highpass filter.

Figure 1.99. Frequency response of highpass filter. The corresponding phase shift goes smoothly from $+90^{\circ}$ (at $\omega=0$ ), through $+45^{\circ}$ (at $\omega_{3 \mathrm{~dB}}$ ), to $0^{\circ}$ (at $\omega=\infty$ ), analogous to the lowpass filter's phase shift (Figure 1.104).
(Figure 1.97) is as shown in Figure 1.98. So the "response" of this circuit, ignoring phase shifts by taking magnitudes of the complex amplitudes, is given by

$$
\begin{align*}
V_{\text {out }} & =\frac{R}{\left[R^{2}+\left(1 / \omega^{2} C^{2}\right)\right]^{1 / 2}} V_{\mathrm{in}} \\
& =\frac{2 \pi f R C}{\left[1+(2 \pi f R C)^{2}\right]^{1 / 2}} V_{\mathrm{in}} \tag{1.35}
\end{align*}
$$

and looks as shown in Figure 1.99 (and earlier in Figure 1.91).

Note that we could have gotten this result immediately by taking the ratio of the magnitudes of impedances, as in Exercise 1.26 and the example immediately preceding it; the numerator is the magnitude of the impedance of the lower leg of the divider $(R)$, and the denominator is the magnitude of the impedance of the series combination of $R$ and $C$.

As we noted earlier, the output is approximately equal to the input at high frequencies (how high? $\omega \gtrsim 1 / R C$ ) and goes to zero at low frequencies. The highpass filter is
image_name:A
description:The graph labeled 'A' is a plot depicting the reactance of inductors and capacitors as a function of frequency. This graph is a type of Bode plot, which is commonly used to illustrate how the impedance of these components varies with frequency.

1. **Axes Labels and Units:**
- The x-axis represents frequency, ranging from 10 Hz to 1 GHz, with each major division marking a decade (logarithmic scale).
- The y-axis represents reactance, ranging from 10 Ohms to 1 Mega Ohm, also on a logarithmic scale.

2. **Overall Behavior and Trends:**
- The graph shows a series of diagonal lines, each representing a specific value of inductance or capacitance.
- For capacitors, the reactance decreases with increasing frequency, represented by downward sloping lines.
- For inductors, the reactance increases with increasing frequency, represented by upward sloping lines.

3. **Key Features and Technical Details:**
- The graph includes several diagonal lines labeled with component values, such as 1 pF, 10 nF, 100 µF for capacitors and 10 nH, 1 mH, 100 H for inductors.
- These lines intersect at various points, indicating the frequency at which the reactance equals a specific value.
- The plot provides a visual representation of how component values affect the reactance at different frequencies.

4. **Annotations and Specific Data Points:**
- The lines are annotated with standard component values, making it easy to determine the reactance of a specific component at a given frequency.
- The gridlines and annotations help in quickly identifying the reactance values for common component values across different frequencies.

This graph is useful for engineers and designers who need to understand how different components will behave in AC circuits over a range of frequencies. It serves as a quick reference to estimate the impedance of inductors and capacitors without complex calculations.
image_name:B
description:The graph labeled 'B' is a detailed plot of reactance versus frequency, focusing on a single decade from a larger range. This plot is likely a Smith chart or a similar impedance/reactance chart used for analyzing the behavior of inductors and capacitors over a specified frequency range.

1. **Type of Graph and Function:**
- This is a reactance chart, typically used to examine how the reactance of capacitors and inductors changes with frequency. It is a type of logarithmic plot where reactance is plotted against frequency.

2. **Axes Labels and Units:**
- The x-axis represents frequency, labeled from 1 to 10, likely in a logarithmic scale corresponding to a single decade (e.g., 1 Hz to 10 Hz, 10 Hz to 100 Hz, etc.).
- The y-axis represents reactance, with values ranging from 1 to 10, also on a logarithmic scale.

3. **Overall Behavior and Trends:**
- The graph shows diagonal lines representing constant capacitance and inductance values. These lines help visualize how reactance changes across different frequencies for specific component values.
- As frequency increases, the reactance of inductors generally increases, while the reactance of capacitors decreases.

4. **Key Features and Technical Details:**
- Lines are labeled with standard component values (e.g., 0.22, 0.33, 0.47, 0.68, 1.0, 1.5, 2.2, 3.3, 4.7, 6.8, 10.0), indicating either capacitance in microfarads or inductance in microhenries.
- The chart includes annotations for specific values of capacitors and inductors, such as 'C = 1.0' and 'L = 1.0', showing the intersection points where these values are applicable.

5. **Annotations and Specific Data Points:**
- The graph is marked with diagonal grids, each representing a specific component value, allowing for easy determination of reactance at a given frequency.
- This detailed view allows engineers to quickly assess the reactance for standard EIA "E6" component values within a particular frequency decade, aiding in component selection and circuit design.

Figure 1.100. A: Reactance of inductors and capacitors versus frequency; all decades are identical, except for scale. B: A single decade from part A expanded, with standard $20 \%$ component values (EIA "E6") shown.
very common; for instance, the input to the oscilloscope can be switched to "ac coupling." That's just an $R C$ highpass filter with the bend at about 10 Hz (you would use ac coupling if you wanted to look at a small signal riding on a large dc voltage). Engineers like to refer to the -3 dB "breakpoint" of a filter (or of any circuit that behaves like a filter). In the case of the simple $R C$ high-pass filter, the -3 dB breakpoint is given by

$$
f_{3 \mathrm{~dB}}=1 / 2 \pi R C
$$

You often need to know the impedance of a capacitor at a given frequency (e.g., for the design of filters).
image_name:Figure 1.101
description:
[
name: C1, type: Capacitor, value: 0.01uF, ports: {Np: Vin, Nn: X1}
name: R1, type: Resistor, value: 1.0k, ports: {N1: X1, N2: GND}
]
extrainfo:This is an RC high-pass filter with a cutoff frequency of approximately 15.9 kHz.

Figure 1.101. Highpass filter example.
Figure 1.100 provides a very useful graph covering large ranges of capacitance and frequency, giving the value of $|\mathbf{Z}|=1 / 2 \pi f C$.

As an example, consider the filter shown in Figure 1.101. It is a highpass filter with the 3 dB point ${ }^{44}$ at 15.9 kHz . The impedance of a load driven by it should be much larger than 1.0 k in order to prevent circuit loading effects on the filter's output, and the driving source should be able to drive a 1.0 k load without significant attenuation (loss of signal amplitude) in order to prevent circuit loading effects by the filter on the signal source (recall §1.7.1D for worst-case source and load impedances of $R C$ filters).

### 1.7.9 RC lowpass filters

Revisiting the lowpass filter, in which you get the opposite frequency behavior by interchanging $R$ and $C$ (Figure 1.90, repeated here as Figure 1.102), we find the accurate result

$$
\begin{equation*}
V_{\mathrm{out}}=\frac{1}{\left(1+\omega^{2} R^{2} C^{2}\right)^{1 / 2}} V_{\mathrm{in}} \tag{1.36}
\end{equation*}
$$

as seen in Figure 1.103 (and earlier in Figure 1.91). The 3 dB point is again at a frequency ${ }^{45} f=1 / 2 \pi R C$. Lowpass filters are quite handy in real life. For instance, a lowpass filter can be used to eliminate interference from nearby radio and television stations $(0.5-800 \mathrm{MHz})$, a problem that plagues audio amplifiers and other sensitive electronic equipment.
image_name:Figure 1.102
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: R, type: Resistor, value: R, ports: {N1: Vin, N2: Vout}
name: C, type: Capacitor, value: C, ports: {Np: Vout, Nn: GND}
]
extrainfo:This is a simple RC low-pass filter circuit. The input voltage is applied across the resistor, and the output is taken across the capacitor. The filter allows low-frequency signals to pass while attenuating high-frequency signals.

Figure 1.102. Lowpass filter.

Exercise 1.30. Show that the preceding expression for the response of an $R C$ lowpass filter is correct.

44 One often omits the minus sign when referring to the -3 dB point.
${ }^{45}$ As mentioned in $\S 1.7 .1 \mathrm{~A}$, we often like to define the breakpoint frequency $\omega_{0}=1 / R C$, and work with frequency ratios $\omega / \omega_{0}$. Then a useful form for the denominator in eq'n 1.36 is $\sqrt{1+\left(\omega / \omega_{0}\right)^{2}}$. The same applies to eq'n 1.35 , where the numerator becomes $\omega / \omega_{0}$.
image_name:Figure 1.103
description:The graph shown is a Bode plot representing the frequency response of an RC lowpass filter.

1. **Type of Graph and Function:**
- This is a Bode plot, specifically showing the magnitude response of the filter.

2. **Axes Labels and Units:**
- The horizontal axis is labeled as \( \omega \), representing the angular frequency in radians per second.
- The vertical axis is labeled as \( \frac{V_{\text{out}}}{V_{\text{in}}} \), indicating the ratio of the output voltage to the input voltage, which is a dimensionless gain.
- The scale appears to be logarithmic, as is typical for Bode plots, though not explicitly marked.

3. **Overall Behavior and Trends:**
- The graph starts at a normalized gain of 1.0 at low frequencies, indicating that the output voltage is equal to the input voltage.
- As frequency increases, the gain decreases, following a smooth, downward slope.
- The curve shows an exponential decay in gain as the frequency increases, typical of a lowpass filter.

4. **Key Features and Technical Details:**
- The cutoff frequency, where the gain drops by 3 dB, is marked on the graph as \( \omega_{3\text{dB}} = 1/RC \).
- Beyond this point, the gain decreases proportionally to \( 1/\omega \), as indicated by the annotation \( \frac{V_{\text{out}}}{V_{\text{in}}} \propto 1/\omega \).

5. **Annotations and Specific Data Points:**
- The -3 dB point is explicitly marked on the graph, indicating the cutoff frequency where the output power is half of the input power.
- The graph does not specify exact numerical values for \( R \) or \( C \), but these would determine the exact location of the cutoff frequency.

Figure 1.103. Frequency response of lowpass filter.

The lowpass filter's output can be viewed as a signal source in its own right. When driven by a perfect ac voltage (zero source impedance), the filter's output looks like $R$ at low frequencies (the perfect signal source can be replaced with a short, i.e., by its small-signal source impedance, for the purpose of impedance calculations). It drops to zero impedance at high frequencies, where the capacitor dominates the output impedance. The signal driving the filter sees a load of $R$ plus the load resistance at low frequencies, dropping to just $R$ at high frequencies. As we remarked in §1.7.1D, the worst-case source impedance and the worstcase load impedance of an $R C$ filter (lowpass or highpass) are both equal to $R$.
image_name:Figure 1.104
description:**Type of Graph and Function:**
The graph is a Bode plot representing the phase response of a lowpass filter. It shows how the phase shift of the filter's output signal varies with frequency.

**Axes Labels and Units:**
- The horizontal axis represents the normalized frequency \( f/f_c \), where \( f_c \) is the cutoff frequency. The scale is logarithmic, ranging from \( 0.1f_c \) to \( 10f_c \).
- The vertical axis represents the phase shift in degrees, ranging from 0° to -90°.

**Overall Behavior and Trends:**
The phase shift starts at approximately 0° at low frequencies (\( 0.1f_c \)), decreases steadily through the cutoff frequency \( f_c \), and approaches -90° at high frequencies (\( 10f_c \)). The transition from 0° to -90° occurs smoothly, with the steepest part of the curve centered around the cutoff frequency.

**Key Features and Technical Details:**
- At \( 0.1f_c \), the phase shift is approximately -5.7°.
- At the cutoff frequency \( f_c \), the phase shift is -45°, which is a significant marker for lowpass filters.
- At \( 10f_c \), the phase shift approaches -90°.
- The phase shift is within 6° of its asymptotic values both at low and high frequencies.

**Annotations and Specific Data Points:**
- The graph includes a table listing specific values of \( f/f_c \) and the corresponding phase shifts \( \phi \):
- \( f/f_c = 0.1 \), \( \phi = -5.7° \)
- \( f/f_c = 0.2 \), \( \phi = -11.3° \)
- \( f/f_c = 0.25 \), \( \phi = -14° \)
- \( f/f_c = 0.5 \), \( \phi = -26.5° \)
- \( f/f_c = 1.0 \), \( \phi = -45° \)
- The phase shift formula is given as \( \phi = -\tan^{-1}(f/f_c) \).

image_name:Figure 1.104
description:**Type of Graph and Function:**
The graph is a Bode plot representing the frequency response of a lowpass filter. It consists of two parts: amplitude response and phase response. The amplitude response is shown in the provided image.

**Axes Labels and Units:**
- The vertical axis represents the amplitude ratio \( \frac{V_{out}}{V_{in}} \) on a logarithmic scale.
- The horizontal axis represents the normalized frequency \( \frac{f}{f_c} \) also on a logarithmic scale, where \( f_c \) is the cutoff frequency.

**Overall Behavior and Trends:**
- At low frequencies (\( f < f_c \)), the amplitude ratio is approximately constant at 1, indicating no attenuation.
- As the frequency approaches the cutoff frequency \( f_c \), the amplitude begins to decrease.
- Beyond the cutoff frequency, the amplitude decreases at a rate of \(-20\) dB per decade, which corresponds to a slope of \(-6\) dB per octave or \( \sim 1/f \).

**Key Features and Technical Details:**
- The amplitude at the cutoff frequency \( f_c \) is approximately 0.707, which corresponds to the \(-3\) dB point, a standard characteristic of a lowpass filter.
- The slope of the graph beyond \( f_c \) is annotated as \(-20\) dB/decade and \(-6\) dB/octave, indicating the rate of attenuation.

**Annotations and Specific Data Points:**
- The graph includes annotations for the slope of the amplitude response beyond the cutoff frequency, specifying \(-6\) dB/octave and \(-20\) dB/decade.
- The point at \( f_c \) is marked with an amplitude of 0.707, highlighting the \(-3\) dB point.

Figure 1.104. Frequency response (phase and amplitude) of lowpass filter plotted on logarithmic axes. Note that the phase shift is $-45^{\circ}$ at the -3 dB point and is within $6^{\circ}$ of its asymptotic value for a decade of frequency change.

In Figure 1.104, we've plotted the same lowpass filter response with logarithmic axes, which is a more common way that it's done. You can think of the vertical axis as decibels, and the horizontal axis as octaves (or decades). On such a plot, equal distances correspond to equal ratios. We've also plotted the phase shift, using a linear vertical axis (degrees) and the same logarithmic frequency axis. This sort of plot is good for seeing the detailed response even when it is greatly attenuated (as at right); we'll see a number of such plots in Chapter 6, when we treat active filters. Note that the filter curve plotted here becomes a straight line at large attenuations, with a slope of $-20 \mathrm{~dB} /$ decade (engineers prefer to say " $-6 \mathrm{~dB} /$ octave"). Note also that the phase shift goes smoothly from $0^{\circ}$ (at frequencies well below the breakpoint) to $-90^{\circ}$ (well above it), with a value of $-45^{\circ}$ at the -3 dB point. A rule of thumb for single-section $R C$ filters is that the phase shift is $\approx 6^{\circ}$ from its asymptotic value at $0.1 f_{3 \mathrm{~dB}}$ and at $10 f_{3 \mathrm{~dB}}$.

Exercise 1.31. Prove the last assertion.
An interesting question is the following: is it possible to make a filter with some arbitrary specified amplitude response and some other arbitrary specified phase response? Surprisingly, the answer is no: the demands of causality (i.e., that response must follow cause, not precede it) force a relationship between phase and amplitude response of realizable analog filters (known officially as the KramersKronig relation).

### 1.7.10 RC differentiators and integrators in the frequency domain

The $R C$ differentiator that we saw in $\S 1.4 .3$ is exactly the same circuit as the highpass filter in this section. In fact, it can be considered as either, depending on whether you're thinking of waveforms in the time domain or response in the frequency domain. We can restate the earlier timedomain condition for its proper operation ( $\left.d V_{\text {out }} \ll d V_{\text {in }}\right)$ in terms of the frequency response: for the output to be small compared with the input, the signal frequency (or frequencies) must be well below the 3 dB point. This is easy to check: suppose we have the input signal $V_{\text {in }}=\sin \omega t$. Then, using the equation we obtained earlier for the differentiator output, we have

$$
V_{\mathrm{out}}=R C \frac{d}{d t} \sin \omega t=\omega R C \cos \omega t
$$

and so $d V_{\text {out }} \ll d V_{\text {in }}$ if $\omega R C \ll 1$, i.e., $R C \ll 1 / \omega$. If the input signal contains a range of frequencies, this must hold for the highest frequencies present in the input.

The $R C$ integrator (§1.4.4) is the same circuit as the lowpass filter; by similar reasoning, the criterion for a good integrator is that the lowest signal frequencies must be well above the 3 dB point.

### 1.7.11 Inductors versus capacitors

Instead of capacitors, inductors can be combined with resistors to make lowpass (or highpass) filters. In practice, however, you rarely see RL lowpass or highpass filters. The reason is that inductors tend to be more bulky and expensive and perform less well (i.e., they depart further from the ideal) than capacitors (see Chapter $1 x$ ). If you have a choice, use a capacitor. One important exception to this general statement is the use of ferrite beads and chokes in high-frequency circuits. You just string a few beads here and there in the circuit; they make the wire interconnections slightly inductive, raising the impedance at very high frequencies and preventing oscillations, without the added series resistance you would get with an $R C$ filter. An $R F$ choke is an inductor, usually a few turns of wire wound on a ferrite core, used for the same purpose in RF circuits. Note, however, that inductors are essential components in (a) $L C$ tuned circuits (\$1.7.14), and (b) switch-mode power converters (§9.6.4).

### 1.7.12 Phasor diagrams

There's a nice graphical method that can be helpful when we are trying to understand reactive circuits. Let's take an example, namely, the fact that an $R C$ filter attenuates 3 dB at a frequency $f=1 / 2 \pi R C$, which we derived in $\S 1.7 .8$. This is true for both highpass and lowpass filters. It is easy to get a bit confused here, because at that frequency the reactance of the capacitor equals the resistance of the resistor; so you might at first expect 6 dB attenuation (a factor of $1 / 2$ in voltage). That is what you would get, for example, if you were to replace the capacitor with a resistor of the same impedance magnitude. The confusion arises because the capacitor is reactive, but the matter is clarified by a phasor diagram (Figure 1.105). The axes are the real (resistive) and imaginary (reactive) components of the impedance. In a series circuit like this, the axes also represent the (complex) voltage, because the current is the same everywhere. So for this circuit (think of it as an $R C$ voltage divider) the input voltage (applied across the series $R C$ pair) is proportional to the length of the hypotenuse, and the output voltage (across $R$ only) is proportional to the length of the $R$ leg of the triangle. The diagram represents the situation at the frequency where the capacitor's reactance equals $R$,
i.e., $f=1 / 2 \pi R C$, and shows that the ratio of output voltage to input voltage is $1 / \sqrt{2}$, i.e., -3 dB .
image_name:Figure 1.105
description:The diagram labeled "Figure 1.105" is a phasor diagram representing a low-pass RC filter at the -3 dB point. This type of diagram is used to visualize the relationship between the resistive and reactive components of the filter at a specific frequency.

1. **Type of Graph and Function:**
- The diagram is a phasor diagram, which is a graphical representation of the magnitude and phase relationship between the components of an AC circuit. It is specifically used here to illustrate the behavior of a low-pass RC filter at the cutoff frequency.

2. **Axes Labels and Units:**
- The vertical axis is labeled 'Z' representing impedance. The horizontal axis shows the real component 'R', and the vertical component is labeled '-j/ωC', representing the imaginary part of the impedance due to the capacitive reactance.

3. **Overall Behavior and Trends:**
- The phasor diagram shows a right triangle formed by the resistive component (R) on the horizontal axis and the capacitive reactance (-j/ωC) on the vertical axis. The hypotenuse represents the total impedance at the cutoff frequency, where the magnitude is \( R\sqrt{2} \).

4. **Key Features and Technical Details:**
- At the -3 dB point, the angle between the total impedance vector and the resistive component is 45 degrees, indicating a phase shift of 45 degrees from input to output.
- The length of the resistive component (R) is equal to the length of the capacitive reactance (\(-j/ωC\)), showing that the reactance equals the resistance at this frequency.
- The overall impedance magnitude is \( R\sqrt{2} \), which corresponds to the condition where the output voltage is \( 1/\sqrt{2} \) times the input voltage, confirming the -3 dB point.

5. **Annotations and Specific Data Points:**
- The diagram is annotated with the angle of 45 degrees, emphasizing the phase shift.
- The phasor arrows are clearly marked to show the relationship between the resistive and reactive components of the circuit at the cutoff frequency.

$R C$ filter at -3 dB point
A.
image_name:Phasor diagram for lowpass filter at 3 dB point
description:The diagram is a phasor diagram representing a lowpass filter at the -3 dB point. It visually depicts the relationship between the resistive and reactive components of the circuit. The diagram consists of a horizontal line labeled with vectors representing resistive elements. There are two arrows pointing to the right, each labeled 'R', indicating resistive components. Additionally, there is an arrow pointing to the left labeled '2R', which likely represents the reactive component's impedance at the cutoff frequency. The vertical axis is marked as 'Z', indicating impedance.

This phasor diagram is used to illustrate the phase shift and amplitude relationship at the cutoff frequency, where the output voltage is reduced to 1/√2 of the input voltage, equivalent to a -3 dB point. The phase shift at this point is 45 degrees, as indicated by the angle between the vectors. The diagram helps in understanding the amplitude and phase relationships in RC circuits, specifically at the cutoff frequency, where the impedance magnitude is R√2.

resistive divider:
$R_{1}=R_{2}=R \quad(-6 \mathrm{~dB})$
B.

Figure 1.105. Phasor diagram for lowpass filter at 3 dB point.

The angle between the vectors gives the phase shift from input to output. At the 3 dB point, for instance, the output amplitude equals the input amplitude divided by the square root of 2 , and it leads by $45^{\circ}$ in phase. This graphical method makes it easy to read off amplitude and phase relationships in $R L C$ circuits. You can use it, for example, to get the response of the highpass filter that we previously derived algebraically.

Exercise 1.32. Use a phasor diagram to derive the response of an $R C$ high-pass filter: $V_{\text {out }}=V_{\text {in }} R / \sqrt{R^{2}+\left(1 / \omega^{2} C^{2}\right)}$.

Exercise 1.33. At what frequency does an $R C$ lowpass filter attenuate by 6 dB (output voltage equal to half the input voltage)? What is the phase shift at that frequency?

Exercise 1.34. Use a phasor diagram to obtain the lowpass filter response previously derived algebraically.

In the next chapter (§2.2.8) we'll see a nice example of phasor diagrams in connection with a constant-amplitude phase-shifting circuit.

### 1.7.13 "Poles" and decibels per octave

Look again at the response of the $R C$ lowpass filter (Figures 1.103 and 1.104). Far to the right of the "knee" the output amplitude is dropping proportional to $1 / f$. In one octave (as in music, one octave is twice the frequency) the output amplitude will drop to half, or -6 dB ; so a simple $R C$ filter has a $6 \mathrm{~dB} /$ octave falloff. You can make filters with several $R C$ sections; then you get 12 dB /octave (two $R C$ sections), $18 \mathrm{~dB} /$ octave (three sections), and so on. This is the usual way of describing how a filter behaves beyond the cutoff. Another popular way is to say a "three-pole filter," for instance, meaning a filter with three $R C$ sections (or one that behaves like one). (The word "pole" derives from a method of analysis that is beyond the scope of this book and that involves complex
transfer functions in the complex frequency plane, known by engineers as the " $s$-plane." This is discussed in the advanced volume, in Chapter $1 x$.)

A caution on multistage filters: you can't simply cascade several identical filter sections in order to get a frequency response that is the concatenation of the individual responses. The reason is that each stage will load the previous one significantly (since they're identical), changing the overall response. Remember that the response function we derived for the simple $R C$ filters was based on a zero-impedance driving source and an infinite-impedance load. One solution is to make each successive filter section have much higher impedance than the preceding one. A better solution involves active circuits like transistor or operational amplifier (op-amp) interstage "buffers," or active filters. These subjects will be treated in Chapters 2-4, 6 , and 13 .

### 1.7.14 Resonant circuits

When capacitors are combined with inductors or are used in special circuits called active filters, it is possible to make circuits that have very sharp frequency characteristics (e.g., a large peak in the response at a particular frequency), compared with the gradual characteristics of the $R C$ filters we've seen so far. These circuits find applications in various audio and RF devices. Let's now take a quick look at $L C$ circuits (there will be more on them, and active filters, in Chapter 6 and in Appendix E).

#### A. Parallel and series LC circuits

image_name:Figure 1.106
description:
[
name: R, type: Resistor, value: R, ports: {N1: Vin, N2: Vout}
name: L, type: Inductor, value: L, ports: {N1: Vout, N2: GND}
name: C, type: Capacitor, value: C, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is an LC resonant bandpass filter with a resistor R at the input. It filters signals based on frequency, allowing signals at the resonant frequency to pass while attenuating others.

Figure 1.106. $L C$ resonant circuit: bandpass filter.

First, consider the circuit shown in Figure 1.106. The impedance of the $L C$ combination at frequency $f$ is just

$$
\begin{aligned}
\frac{1}{\mathbf{Z}_{\mathrm{LC}}} & =\frac{1}{\mathbf{Z}_{\mathrm{L}}}+\frac{1}{\mathbf{Z}_{\mathrm{C}}}=\frac{1}{j \omega L}-\frac{\omega C}{j} \\
& =j\left(\omega C-\frac{1}{\omega L}\right)
\end{aligned}
$$

i.e.,

$$
\mathbf{Z}_{\mathrm{LC}}=\frac{j}{(1 / \omega L)-\omega C}
$$

In combination with $R$ it forms a voltage divider. Because of the opposite behaviors of inductors and capacitors, the impedance of the parallel $L C$ goes to infinity at the resonant frequency

$$
\begin{equation*}
f_{0}=1 / 2 \pi \sqrt{L C} \tag{1.37}
\end{equation*}
$$

(i.e., $\omega_{0}=1 / \sqrt{L C}$ ), giving a peak in the response there. The overall response is as shown in Figure 1.107.
image_name:frequency domain
description:The graph in Figure 1.107 is a frequency response plot for a parallel LC "tank" circuit, which is a type of Bode plot. The x-axis represents frequency \( f \), while the y-axis represents the ratio of output voltage to input voltage \( \frac{V_{out}}{V_{in}} \). The scale on the x-axis is linear, and the y-axis is dimensionless, ranging from 0 to 1.

Overall Behavior and Trends:
The graph shows a prominent peak at the resonant frequency \( f_0 = \frac{1}{2\pi\sqrt{LC}} \). This peak indicates the point where the impedance of the parallel LC circuit becomes infinite, resulting in maximum voltage output relative to input. The response curve is symmetrical around this peak, showing a sharp rise and fall, characteristic of high-Q resonant circuits.

Key Features and Technical Details:
- **Resonant Frequency \( f_0 \):** The peak occurs at this frequency, where the impedance is at its maximum.
- **Bandwidth \( \Delta f_{3dB} \):** The bandwidth is marked around the peak, showing the frequency range over which the output is within 3 dB of the peak value.
- **Quality Factor \( Q \):** Defined as \( Q = \frac{f_0}{\Delta f_{3dB}} \), it indicates the sharpness of the peak.

Annotations and Specific Data Points:
- The graph includes annotations for \( \Delta f_{3dB} \) and the quality factor \( Q \), highlighting the relationship between these parameters and the resonant frequency.

#### Inset: Time Domain Behavior
The inset shows the time-domain response of the circuit, illustrating a damped oscillation or "ringing" following an input voltage step or pulse. It indicates the decay of oscillations to 61% in energy (or 37% in voltage), which corresponds to the exponential decay characteristic of such circuits.
image_name:time domain
description:The provided graph consists of two parts: a frequency domain plot and an inset showing a time-domain waveform.

**1. Frequency Domain Plot:**
- **Type of Graph:** This is a frequency response plot of a parallel LC "tank" circuit.
- **Axes Labels and Units:**
- The vertical axis represents the ratio of output voltage to input voltage \( \frac{V_{out}}{V_{in}} \), with a scale from 0 to 1.
- The horizontal axis represents frequency \( f \), with a marker at the resonant frequency \( f_0 = \frac{1}{2\pi\sqrt{LC}} \).
- **Overall Behavior and Trends:**
- The graph shows a pronounced peak at the resonant frequency \( f_0 \), indicating maximum impedance and a sharp increase in the voltage ratio.
- The response decreases symmetrically on either side of the peak, showing typical bandpass filter behavior.
- **Key Features and Technical Details:**
- The peak represents the resonant frequency where the impedance is highest.
- The bandwidth \( \Delta f_{3dB} \) is marked around the peak, indicating the frequency range where the response is within 3 dB of the peak value.
- The quality factor \( Q \) is given by \( Q = \frac{f_0}{\Delta f_{3dB}} \), illustrating the sharpness of the peak.

**2. Time Domain Waveform (Inset):**
- **Type of Graph:** This is a time-domain waveform showing the response of the circuit to a voltage step or pulse.
- **Axes Labels and Units:**
- The horizontal axis represents time \( t \).
- **Overall Behavior and Trends:**
- The waveform shows a damped oscillation or "ringing" effect following the input step.
- The amplitude of the oscillations decreases over time, indicating energy loss.
- **Key Features and Technical Details:**
- Annotations indicate that the energy decays to 61% (\( 1/e \) in energy) and the voltage to 37% (\( 1/e \) in voltage) over time.
- The waveform's decay rate and oscillation frequency are characteristic of the LC circuit's resonant behavior.

Figure 1.107. Frequency response of parallel $L C$ "tank" circuit. The inset shows the time-domain behavior: a damped oscillation ("ringing") waveform following an input voltage step or pulse.

In practice, losses in the inductor and capacitor limit the sharpness of the peak, but with good design these losses can be made very small. Conversely, a $Q$-spoiling resistor is sometimes added intentionally to reduce the sharpness of the resonant peak. This circuit is known simply as a parallel $L C$ resonant circuit (or "tuned circuit," or "tank") and is used extensively in RF circuits to select a particular frequency for amplification (the $L$ or $C$ can be variable, so you can tune the resonant frequency). The higher the driving impedance, the sharper the peak; it is not uncommon to drive them with something approaching a current source, as you will see later. The quality factor $Q$ is a measure of the sharpness of the peak. It equals the resonant frequency divided by the width at the -3 dB points. For a parallel $R L C$ circuit, $Q=\omega_{0} R C,{ }^{46}$

Another variety of $L C$ circuit is the series $L C$ (Figure 1.108). By writing down the impedance formulas involved, and assuming that both the capacitor and inductor are ideal, i.e., that they have no resistive losses, ${ }^{47}$ you can convince yourself that the impedance of the $L C$ goes to zero

image_name:Figure 1.108
description:
[
name: Vin, type: VoltageSource, ports: {Np: Vin, Nn: GND}
name: R, type: Resistor, value: R, ports: {N1: Vin, N2: X1}
name: L, type: Inductor, value: L, ports: {N1: X1, N2: X2}
name: C, type: Capacitor, value: C, ports: {Np: X2, Nn: GND}
]
extrainfo:The circuit is a series LC notch filter. It uses a resistor, inductor, and capacitor to filter out signals at a specific frequency. The graph shows how reactance changes with frequency, indicating a sharp drop at the resonant frequency f0.
image_name:
description:The graph presented is a log-log plot showing the reactance of a series RLC circuit as a function of frequency. The x-axis represents the frequency normalized to the resonant frequency \( f_0 \), ranging from \( 0.1f_0 \) to \( 10f_0 \). The y-axis represents the normalized reactance \( X/X_0 \), with a scale from 0.1 to 10.

Type of Graph and Function:
This is a frequency response graph typically used in analyzing RLC circuits, specifically showing how reactance varies with frequency.

Axes Labels and Units:
- **X-axis:** Frequency \( f \) (normalized to \( f_0 \))
- **Y-axis:** Reactance \( X/X_0 \) (dimensionless ratio)
- Both axes use a logarithmic scale.

Overall Behavior and Trends:
- The reactance of the inductor \( L \) decreases with increasing frequency, following a downward slope.
- The reactance of the capacitor \( C \) increases with increasing frequency, showing an upward slope.
- The combined reactance of the RLC circuit (labeled \( RLC \)) exhibits a notch at the resonant frequency \( f_0 \), where the impedance is minimized.

Key Features and Technical Details:
- At the resonant frequency \( f_0 \), the reactance of the series RLC circuit drops significantly, indicating a sharp notch filter behavior.
- Two quality factor (\( Q \)) curves are shown: one for \( Q = 20 \) and another for \( Q = \infty \). The \( Q = \infty \) curve shows a deeper and sharper notch, indicating an ideal scenario with no resistive losses.
- The \( Q = 20 \) curve is broader, illustrating the effect of finite resistance, which causes the notch to be less pronounced.

Annotations and Specific Data Points:
- The graph includes annotations for the inductor \( L \), capacitor \( C \), and the combined RLC reactance.
- The dashed line at \( f_0 \) highlights the frequency where the notch occurs.
- The behavior of the reactance around \( f_0 \) is critical for understanding the filtering characteristics of the circuit.

Figure 1.108. $L C$ notch filter ("trap"). The inductive and capacitive reactances behave as shown, but the opposite sign of their complex impedances causes the series impedance to plummet. For ideal components the reactance of the series $L C$ goes completely to zero at resonance; for real-world components the minimum is non-zero, and usually dominated by the inductor.
image_name:Phase shift
description:The graph consists of two plots, depicting the frequency and phase response of a series LC trap circuit.

1. **Type of Graph and Function:**
- The top plot is a phase shift graph, while the bottom plot is a frequency response graph. Both are related to a series LC notch filter.

2. **Axes Labels and Units:**
- **Top Plot (Phase Shift):**
- The vertical axis is labeled "Phase shift" and is measured in degrees, ranging from -90° to 90°.
- The horizontal axis represents frequency (f) but lacks specific units, indicating a general frequency sweep.
- **Bottom Plot (Frequency Response):**
- The vertical axis is labeled "V_out / V_in," representing the ratio of output to input voltage, ranging from 0 to 1.
- The horizontal axis is labeled as frequency (f) with a linear scale, with the resonant frequency marked as \( f_0 = 1/(2\pi\sqrt{LC}) \).

3. **Overall Behavior and Trends:**
- **Top Plot (Phase Shift):**
- The phase shift starts at 0° at low frequencies, decreases sharply to around -90° at the resonant frequency, and then rapidly increases, peaking slightly above 90° before settling back to 0° at high frequencies.
- **Bottom Plot (Frequency Response):**
- The response shows a clear notch at the resonant frequency \( f_0 \), where the output/input ratio drops significantly, indicating minimal signal transmission at this frequency.

4. **Key Features and Technical Details:**
- **Top Plot (Phase Shift):**
- A sharp phase transition occurs at the resonant frequency, typical for resonant circuits. The phase change is abrupt, moving from negative to positive values.
- **Bottom Plot (Frequency Response):**
- The notch depth and width indicate the circuit's ability to "trap" or attenuate signals at \( f_0 \). The quality factor \( Q = 3 \) suggests moderate selectivity and bandwidth.

5. **Annotations and Specific Data Points:**
- The resonant frequency \( f_0 \) is clearly marked on the frequency axis, serving as a reference point for both plots.
- The quality factor \( Q = 3 \) is annotated on the frequency response plot, providing insight into the sharpness of the notch.

Overall, the graph effectively illustrates the phase and frequency characteristics of a series LC trap, emphasizing its role in attenuating signals at its resonant frequency.
image_name:Vout/Vin
description:The graph titled "Vout/Vin" is a Bode plot, which consists of two parts: the magnitude response and the phase response of a series LC notch filter, also known as a "trap." This plot illustrates the behavior of the filter around its resonant frequency.

1. **Magnitude Response (Vout/Vin):**
- **Type of Graph:** The lower part of the plot shows the magnitude response of the filter.
- **Axes Labels and Units:** The x-axis represents frequency \( f \) in hertz on a linear scale, and the y-axis represents the magnitude ratio \( \frac{V_{out}}{V_{in}} \), ranging from 0 to 1.
- **Overall Behavior and Trends:** The magnitude response exhibits a sharp dip at the resonant frequency \( f_0 = \frac{1}{2\pi\sqrt{LC}} \), indicating that the filter attenuates signals at this frequency. The response is symmetric around \( f_0 \).
- **Key Features and Technical Details:** At resonance, the magnitude drops to a minimum value, indicating the "trap" effect where the filter effectively shorts the signal to ground. The quality factor \( Q \) is given as 3, which affects the sharpness of the notch.

2. **Phase Response:**
- **Type of Graph:** The upper part of the plot shows the phase response of the filter.
- **Axes Labels and Units:** The x-axis is the same as the magnitude plot, representing frequency \( f \) in hertz. The y-axis represents phase shift in degrees, ranging from -90° to 90°.
- **Overall Behavior and Trends:** The phase response shows an abrupt change at the resonant frequency \( f_0 \), typical of resonant circuits. The phase shifts from approximately -90° to 90° as the frequency passes through \( f_0 \).
- **Key Features and Technical Details:** The phase shift is most pronounced at resonance, indicating a rapid transition in phase, which is characteristic of series resonant circuits.

Figure 1.109. Frequency and phase response of the series $L C$ trap. The phase changes abruptly at resonance, an effect seen in other resonator types (see for example Figure 7.36).
at resonance $\left(f_{0}=1 / 2 \pi \sqrt{L C}\right)$. Such a circuit is a "trap" for signals at or near the resonant frequency, shorting them to ground. Again, this circuit finds application mainly in RF circuits. Figure 1.109 shows what the response looks like. The $Q$ of a series $R L C$ circuit is $Q=\omega_{0} L / R .^{48}$ To see the impact of increasing $Q$, look at the accurate plots of tank and notch response in Figure 1.110.

[^38]image_name:Figure 1.110
description:The graph in Figure 1.110 illustrates the frequency response of an LC tank circuit (dotted curves) and an LC trap circuit (solid curves) for various values of the quality factor, \(Q\). The x-axis is labeled 'Normalized Frequency (f/f_0)' and ranges from 0 to 2, representing the frequency normalized by the resonant frequency \(f_0\). The y-axis is labeled \(V_{out}/V_{in}\) and ranges from 0 to 1, indicating the ratio of output voltage to input voltage.

1. **Type of Graph and Function:**
- The graph is a frequency response plot, showing both tank and trap responses for different quality factors.

2. **Axes Labels and Units:**
- **X-axis:** Normalized Frequency \((f/f_0)\), no units, ranging from 0 to 2.
- **Y-axis:** \(V_{out}/V_{in}\), unitless ratio, ranging from 0 to 1.

3. **Overall Behavior and Trends:**
- For the tank circuit (dotted curves): The response shows a peak at \(f/f_0 = 1\), with the peak becoming sharper and higher as \(Q\) increases. This indicates a stronger resonance effect with higher \(Q\).
- For the trap circuit (solid curves): The response shows a notch at \(f/f_0 = 1\), with the notch becoming deeper and narrower as \(Q\) increases, effectively shorting the resonant frequency to ground.

4. **Key Features and Technical Details:**
- For \(Q = 1\): The tank circuit shows a broad peak, while the trap circuit shows a shallow notch.
- For \(Q = 3\): The tank circuit's peak becomes more pronounced, and the trap circuit's notch becomes deeper.
- For \(Q = 10\): The tank circuit exhibits a sharp, high peak, and the trap circuit shows a very deep and narrow notch.
- The curves demonstrate how increasing the quality factor \(Q\) enhances the selectivity of both the tank and trap circuits.

5. **Annotations and Specific Data Points:**
- The graph includes annotations for \(Q = 1\), \(Q = 3\), and \(Q = 10\) on both sets of curves to indicate the respective quality factors.

This graph effectively illustrates the impact of the quality factor \(Q\) on the frequency response of LC tank and trap circuits, emphasizing the trade-off between bandwidth and selectivity.

Figure 1.110. Response of $L C$ tank (dotted curves) and trap (solid curves) for several values of quality factor, $Q$.

Exercise 1.35. Find the response ( $V_{\text {out }} / V_{\text {in }}$ versus frequency) for the series $L C$ trap circuit in Figure 1.108.

These descriptions of $L C$ resonant circuits are phrased in terms of frequency response, i.e., in the frequency domain. In the time domain you're generally interested in a circuit's response to pulses, or steps; there you see the sort of behavior shown in the inset of Figure 1.107, an $L C$ circuit with $Q=20$. The signal voltage falls to $1 / e(37 \%)$ in $Q / \pi$ cycles; the stored energy (proportional to $v^{2}$ ) falls to $1 / e(61 \%$ in amplitude) in $Q / 2 \pi$ cycles. You may prefer to think in radians: the energy falls to $1 / e$ in $Q$ radians, and the voltage falls to $1 / e$ in $2 Q$ radians. $L C$ resonant circuits are not unique in providing highly frequency-selective circuit behavior; alternatives include quartz-crystal, ceramic, and surface acoustic-wave (SAW) resonators; transmission lines; and resonant cavities.

### 1.7.15 LC filters

By combining inductors with capacitors you can produce filters (lowpass, highpass, bandpass) with far sharper behavior in frequency response than you can with a filter made from a simple $R C$, or from any number of cascaded $R C$ sections. We'll see more of this, and the related topic of active filters, in Chapter 6. But it's worth admiring now how well this works, to appreciate the virtue of the humble inductor (an often-maligned circuit component).

As an example, look at Figure 1.111, a photograph of a "mixer-digitizer" circuit board that we built for a project some years back (specifically, a radio receiver with 250 million simultaneous channels). There's lots of stuff on the board, which has to frequency-shift and digitize three
image_name:Figure 1.111
description:The image depicts a circuit board labeled as a "mixer-digitizer," designed for a radio receiver with 250 million simultaneous channels. This board is complex and contains various components essential for frequency conversion and digitization.

1. **Identification of Components and Structure:**
- The board prominently features six LC lowpass filters, which are essential for the frequency conversion process. One of these filters is highlighted within an oval.
- Each lowpass filter consists of three inductors, identifiable as square metal cans, and four capacitors, which are shiny, oblong components.
- Other visible components include numerous integrated circuits (ICs) arranged in rows, likely serving various signal processing functions.
- The board also includes connectors for RF input and digital outputs.

2. **Connections and Interactions:**
- The RF input is labeled, indicating where the radio frequency signals enter the board.
- The digital outputs are labeled, showing where the processed signals are output from the board.
- The LC lowpass filters are part of the signal path, designed to cut off frequencies above 1.0 MHz, preventing aliasing in the digitization process.
- PCB traces connect various components, facilitating the flow of signals across the board.

3. **Labels, Annotations, and Key Features:**
- The image includes annotations such as "RF input," "digital outputs," and "LC lowpass filter," which help identify the main functional areas of the board.
- The board is densely populated, indicating a high level of integration and complexity necessary for handling multiple RF bands and converting them to digital signals.
- The layout suggests a focus on efficient signal processing and noise reduction, crucial for maintaining signal integrity in radio frequency applications.

Figure 1.111. There are six $L C$ lowpass filters on this circuit board, part of the process of frequency conversion and digitizing for which this "mixer-digitizer" was designed.

RF bands; its design could occupy a book chapter. For now just gaze at the lumpy filter in the oval (there are five more on the board), comprising three inductors (the square metal cans) and four capacitors (the pairs of shiny oblongs). It's a lowpass filter, designed to cut off at 1.0 MHz ; it prevents 'aliases" in the digitized output, a subject we'll visit in Chapter 13.

How well does it work? Figure 1.112 shows a "frequency sweep," in which a sinewave input goes from 0 Hz to 2 MHz as the trace goes from left to right across the screen. The sausage shapes are the "envelope" of the sinewave output, here comparing the $L C$ filter with an $R C$ lowpass filter with the same 1 MHz cutoff $(1 \mathrm{k} \Omega$ and 160 pF ). The $L C$ wins, hands down. The $R C$ is pathetic by comparison. It's not even good English to call 1 MHz its "cutoff": it hardly cuts anything off.

### 1.7.16 Other capacitor applications

In addition to their uses in filters, resonant circuits, differentiators, and integrators, capacitors are needed for several other important applications. We treat these in detail later in the book, mentioning them here only as a preview.

#### A. Bypassing

The impedance of a capacitor decreases with increasing frequency. This is the basis of another important application: bypassing. There are places in circuits where you want to allow a dc voltage, but you don't want signals present. Placing a capacitor across that circuit element (usually a resistor) will help to kill any signals there. You choose the (noncritical) capacitor value so that its
image_name:Figure 1.112
description:The graph depicted in Figure 1.112 is a frequency response plot comparing two types of lowpass filters: a 7-section LC lowpass filter and an RC lowpass filter, both with a 1 MHz cutoff frequency. The x-axis represents input frequency, measured in megahertz (MHz), ranging from 0 to 2 MHz. The y-axis, although not explicitly labeled, likely represents amplitude or gain, as is typical in such plots.

The graph displays two distinct regions, one for each filter type. The LC lowpass filter is shown in the upper part of the graph, while the RC lowpass filter is in the lower part. The dark outline in each region indicates the amplitude envelope of a fast swept sinewave, which creates a 'sandpaper' appearance due to the digital oscilloscope capture.

For the LC lowpass filter, the amplitude remains relatively high and stable up to the cutoff frequency of 1 MHz, beyond which it sharply decreases, indicating the filter's effectiveness in attenuating higher frequencies. The RC lowpass filter, in contrast, shows a more gradual decrease in amplitude as frequency increases, starting from a lower frequency. This behavior reflects the typical performance of RC filters, which have a more gradual roll-off compared to LC filters.

Both filters show significant attenuation beyond the 1 MHz cutoff frequency, but the LC filter demonstrates a steeper roll-off, implying better high-frequency rejection. This characteristic makes the LC filter more efficient for applications requiring sharper cutoff characteristics.

Figure 1.112. Frequency sweep of the $L C$ lowpass filter shown in Figure 1.111 compared with an $R C$ lowpass filter with the same 1 MHz cutoff frequency. The dark outline is the amplitude envelope of the fast swept sinewave, which achieves a sandpaper appearance in this digital 'scope capture.
impedance at signal frequencies is small compared with what it is bypassing. You will see much more of this in later chapters.

#### B. Power-supply filtering

We saw this application in $\S 1.6 .3$, to filter the ripple from rectifier circuits. Although circuit designers often call them filter capacitors, this is really a form of bypassing, or energy storage, with large-value capacitors; we prefer the term storage capacitor. And these capacitors really are large - they're the big shiny round things you see inside most electronic instruments. We'll get into dc powersupply design in detail in Chapter 9.

#### C. Timing and waveform generation

As we've seen, a capacitor supplied with a constant current charges up with a ramp waveform. This is the basis of ramp and sawtooth generators, used in analog function generators, oscilloscope sweep circuits, analog-digital converters, and timing circuits. $R C$ circuits are also used for timing, and they form the basis of delay circuits (monostable multivibrators). These timing and waveform applications are important in many areas of electronics and will be covered in Chapters 3, 6, 10, and 11.

### 1.7.17 Thévenin's theorem generalized

When capacitors and inductors are included, Thévenin's theorem must be restated: any two-terminal network of resistors, capacitors, inductors, and signal sources is equivalent to a single complex impedance in series with a single signal source. As before, you find the (complex) impedance
and the signal source (waveform, amplitude, and phase) from the open-circuit output voltage and the short-circuit output current.

## 1.8 Putting it all together - an AM radio

In our circuit course we tie together the topics of this chapter by hooking up a simple AM radio. The signal that's transmitted is a sinewave at the station's frequency in the AM band $(520-1720 \mathrm{kHz})$, with its amplitude varied ("modulated") according to the audio waveform (Figure 1.113). In other words, an audio waveform described by some function $f(t)$ would be transmitted as a RF signal $[A+f(t)] \sin 2 \pi f_{\mathrm{c}}$; here $f_{\mathrm{c}}$ is the station's "carrier" frequency, and the constant $A$ is added to the audio waveform so that the coefficient $[A+f(t)]$ is never negative.
image_name:Figure 1.113
description:The graph depicted in Figure 1.113 is a time-domain waveform illustrating an amplitude-modulated (AM) radio signal. The x-axis represents time (t), while the y-axis represents amplitude, though specific units are not labeled. The graph combines two waveforms: a high-frequency radiofrequency (RF) carrier wave and a lower-frequency audio waveform.

1. **Type of Graph and Function:**
- The graph is a time-domain representation of an AM signal, showcasing the modulation process.

2. **Axes Labels and Units:**
- The x-axis is labeled as time (t), though no specific time units are provided.
- The y-axis represents amplitude, but it is not explicitly labeled with units.

3. **Overall Behavior and Trends:**
- The graph shows a high-frequency RF carrier wave (~1 MHz) whose amplitude is modulated by a lower-frequency audio signal (20 Hz to 5 kHz).
- The carrier wave appears as a series of rapid oscillations, while the envelope formed by these oscillations follows the slower variations of the audio waveform.
- The envelope does not cross zero due to the DC offset applied to the audio waveform.

4. **Key Features and Technical Details:**
- The RF carrier frequency is approximately 1 MHz, characterized by very rapid oscillations.
- The audio waveform envelope varies between 20 Hz and 5 kHz, modulating the amplitude of the carrier.
- The graph illustrates how the amplitude of the carrier wave changes in accordance with the audio signal.

5. **Annotations and Specific Data Points:**
- Annotations indicate the frequency range of the audio waveform (20 Hz to 5 kHz) and the RF carrier frequency (~1 MHz).
- The modulation process is visually represented by the changing amplitude of the RF wave, corresponding to the shape of the audio signal envelope.

Figure 1.113. An AM signal consists of an RF carrier ( $\sim 1 \mathrm{MHz}$ ) whose amplitude is varied by the audio-frequency signal (speech or music; audible frequencies up to $\sim 5 \mathrm{kHz}$ ). The audio waveform is dc offset so that the envelope does not cross zero.

At the receiver end (that's $u s!$ ) the task is to select this station (among many) and somehow extract the modulating envelope, which is the desired audio signal. Figure 1.114 shows the simplest AM radio; it is the "crystal set" of yesteryear. It's really quite straightforward: the parallel $L C$ resonant circuit is tuned to the station's frequency by the variable capacitor $C_{1}$ (§1.7.14); the diode $D$ is a half-wave rectifier (§1.6.2), which (if ideal) would pass only the positive half-cycles of the modulated carrier; and $R_{1}$ provides a light load, so that the rectified output follows the halfcycles back down to zero. We're almost done. We add small capacitor $C_{2}$ to prevent the output from following the fast half-cycles of carrier (it's a storage capacitor, §1.7.16B), choosing the time constant $R_{1} C_{2}$ to be long compared with a carrier period $(\sim 1 \mu \mathrm{~s})$, but short compared with the period of the highest audio frequency ( $\sim 200 \mu \mathrm{~s}$ ).

Figures 1.115 and 1.116 show what you see when you probe around with a 'scope. The bare antenna shows plenty of low-frequency pickup (mostly 60 Hz ac powerline), and a tiny bit of signal from all the AM stations at once. But
image_name:Figure 1.114
description:
[
name: C1, type: Capacitor, value: C1, ports: {Np: X, Nn: GND}
name: L, type: Inductor, value: L, ports: {N1: X, N2: GND}
name: D, type: Diode, ports: {Na: X, Nc: Y}
name: R1, type: Resistor, value: R1, ports: {N1: Y, N2: GND}
name: C2, type: Capacitor, value: C2, ports: {Np: Y, Nn: GND}
name: Audio Amplifier, type: OpAmp, ports: {InP: Y, InN: GND, OutP: Speaker}
]
extrainfo:This is a simple AM receiver circuit. The LC circuit (C1 and L) is used to tune to the desired AM station frequency. The diode D acts as a demodulator, picking off the positive envelope of the AM signal. The resistor R1 and capacitor C2 form a low-pass filter to smooth the signal, and the audio amplifier boosts the audio signal to drive the speaker.

Figure 1.114. The simplest AM receiver. Variable capacitor $C_{1}$ tunes the desired station, diode $D$ picks off the positive envelope (smoothed by $R_{1} C_{2}$ ), and the resulting weak audio signal is amplified to drive the loudspeaker, loudly.
when you connect it to the $L C$ resonant circuit, all the lowfrequency stuff disappears (because the $L C$ looks like a very low impedance, Figure 1.107) and it sees only the selected AM station. What's interesting here is that the amplitude of the selected station is much larger with the $L C$ attached than with nothing connected to the antenna: that's because the resonant circuit's high $Q$ is storing energy from multiple cycles of the signal. ${ }^{49}$
image_name:Figure 1.115
description:The graph in Figure 1.115 consists of two time-domain waveforms displayed vertically. The top waveform represents the signal observed at point \( X \) from a bare antenna (open-circuit), while the bottom waveform shows the signal with an \( LC \) resonant circuit connected to the antenna.

Axes Labels and Units:
- **Vertical Axis:** Voltage in volts, with a scale of 1 V/division.
- **Horizontal Axis:** Time in milliseconds, with a scale of 4 ms/division.

Overall Behavior and Trends:
- **Top Waveform (Bare Antenna):**
- The waveform is relatively smooth and appears as a continuous band with slight undulations. This indicates the presence of low-frequency noise or 'junk' that is not filtered out.
- The signal amplitude is relatively small compared to the bottom waveform.

- **Bottom Waveform (Antenna with \( LC \) Circuit):**
- The waveform exhibits a much larger amplitude, indicating a stronger signal reception.
- The low-frequency components are significantly reduced, resulting in a more defined and sharper appearance. This is due to the \( LC \) circuit filtering out low-frequency noise and enhancing the amplitude of the selected AM station.

Key Features and Technical Details:
- The top waveform shows a lower signal amplitude and more noise, reflecting the lack of filtering.
- The bottom waveform demonstrates the effect of the \( LC \) resonant circuit, which enhances the radiofrequency signal by storing energy from multiple cycles, as indicated by the increased amplitude and reduced noise.

Annotations and Specific Data Points:
- The graph is annotated with labels indicating the conditions for each waveform ('antenna (open-circuit)' and 'antenna (parallel \( LC \) to ground)').
- The \( \sim 1 \) MHz radiofrequency carrier is not explicitly visible as a distinct waveform but is represented by the solid filled areas due to the single-shot trace nature of the observation.

Figure 1.115. Observed waveforms at point " $X$ " from the bare antenna (top) and with the $L C$ connected. Note that the low-frequency junk disappears and that the radio signal gets larger. These are single-shot traces, in which the $\sim 1 \mathrm{MHz}$ radiofrequency carrier appears as a solid filled area. Vertical: $1 \mathrm{~V} / \mathrm{div}$; horizontal: $4 \mathrm{~ms} / \mathrm{div}$.

The audio amplifier is fun, too, but we're not ready for it. We'll see how to make one of those in Chapter 2 (with discrete transistors), and again in Chapter 4 (with operational amplifiers, the Lego ${ }^{\text {TM }}$ block of analog design).

[^39]image_name:point 'X'
description:The graph titled "point 'X'" displays two separate waveform traces. These traces are time-domain waveforms illustrating the behavior of a radiofrequency signal at point 'X'. Each waveform is captured as a single-shot trace, showing how the signal changes over time.

1. **Type of Graph and Function:**
- The graph is a time-domain waveform, capturing the voltage signal over time.

2. **Axes Labels and Units:**
- The vertical axis represents voltage with a scale of $1 \mathrm{~V} / \mathrm{div}$.
- The horizontal axis represents time with a scale of $4 \mathrm{~ms} / \mathrm{div}$.

3. **Overall Behavior and Trends:**
- The top waveform at point 'X' demonstrates a consistent oscillatory pattern, indicating the presence of a radiofrequency carrier. The oscillations are regular and exhibit a high frequency, consistent with a $\sim 1 \mathrm{MHz}$ carrier.
- The waveform shows periodic peaks and troughs, suggesting a stable oscillation without significant amplitude modulation.

4. **Key Features and Technical Details:**
- The waveform is characterized by its high-frequency oscillations, which fill the area between the peaks and troughs, appearing as a solid filled area due to the rapid oscillations.
- No significant amplitude changes or distortion are observed, indicating a stable carrier signal.

5. **Annotations and Specific Data Points:**
- The graph does not have specific annotations or markers for data points, but the consistent oscillatory pattern is a key feature.

This description of point 'X' provides insight into the stable nature of the radiofrequency signal, as captured in the waveform traces.
image_name:point 'Y'
description:The graph displays two sets of time-domain waveforms observed at point 'Y'. The vertical axis represents voltage with a scale of 1 V per division, and the horizontal axis represents time with a scale of 1 ms per division.

**Upper Waveform (R1 only):**
- This waveform shows the signal observed at point 'Y' with only resistor R1 in the circuit.
- The waveform features a filled solid area indicating a strong presence of a radiofrequency carrier around 1 MHz.
- The waveform exhibits a periodic pattern with noticeable oscillations.
- The amplitude of the waveform appears relatively consistent throughout, with no significant peaks or valleys.

**Lower Waveform (R1 + C2):**
- This waveform shows the signal at point 'Y' with both resistor R1 and smoothing capacitor C2 included.
- The waveform is offset for clarity and shows a more smoothed appearance compared to the upper waveform.
- There are noticeable peaks and valleys indicating the effect of the smoothing capacitor.
- The amplitude varies more significantly, with distinct peaks and troughs, suggesting a reduction in high-frequency noise or oscillations due to the capacitor.

Overall, the addition of the smoothing capacitor C2 results in a smoother, more stable waveform at point 'Y', reducing the high-frequency components and providing a clearer signal representation.

Figure 1.116. Observed waveforms at point " $Y$ " with $R_{1}$ only (top) and with smoothing capacitor $C_{2}$ included (bottom). The upper pair is a single-shot capture (with the $\sim 1 \mathrm{MHz}$ carrier appearing as solid black), and the lower pair is a separate single-shot capture, in which we have offset the rectified wave for clarity. Vertical: $1 \mathrm{~V} / \mathrm{div}$; horizontal: $1 \mathrm{~ms} / \mathrm{div}$.

And one amusing final note: in our class, we like to show the effect of probing point " X " with a length of BNC (bayonet Neill-Concelman) cable going to a 'scope input (that's how we start out, in the first week). When we do that, the cable's capacitance (about $30 \mathrm{pF} / \mathrm{ft}$ ) adds to $C_{1}$, lowering the resonant frequency and so tuning to a different station. If we choose right, it changes languages (from English to Spanish)! The students howl with laughter - a language-translating electronic component. Then we use an ordinary 'scope probe, with its $\sim 10 \mathrm{pF}$ of capacitance: no change of station, nor of language.

## 1.9 Other passive components

In the following subsections we would like to introduce briefly an assortment of miscellaneous but essential components. If you are experienced in electronic construction, you may wish to proceed to the next chapter.

### 1.9.1 Electromechanical devices: switches

These mundane but important devices seem to wind up in most electronic equipment. It is worth spending a few paragraphs on the subject (and there's more in Chapter 1x). Figures 1.117 and 1.118 show some common switch types.

#### A. Toggle switches

The simple toggle switch is available in various configurations, depending on the number of poles; Figure 1.119 shows the usual ones (SPST indicates a single-pole singlethrow switch, SPDT indicates a single-pole double-throw
image_name:Figure 1.117
description:The image labeled "Figure 1.117" showcases a diverse array of switches, each serving different purposes in electronic devices. The arrangement displays a variety of switch types, highlighting their structural differences and potential applications.

1. **Toggle Switches:**
- Located at the center foreground, these include both panel-mounting and PCB-mounting types. They have a lever that can be flipped to open or close the circuit. These are typically used for manual control of electronic devices, allowing for a simple on/off operation.

2. **Momentary-Contact (Pushbutton) Switches:**
- Positioned at the right side of the image, these switches include both panel-mounting and PCB-mounting designs. They are characterized by their temporary contact, meaning they only connect circuits while being pressed. This type is often used in applications like keyboards or reset buttons.

3. **Lever-Actuated Switches:**
- These switches are also visible and are actuated by a lever, providing a mechanical advantage to operate the switch. They are useful in environments where the switch needs to be operated by a machine or where manual force is minimized.

4. **Multipole Switches:**
- These are visible in the image, allowing multiple circuits to be controlled by a single switch. They are useful in complex devices where multiple functions need to be controlled simultaneously.

5. **Binary-Coded Thumbwheel Switches:**
- Located above the toggle switches, these are used for data entry in electronic devices. They allow users to set a binary code by rotating the wheels.

6. **Matrix-Encoded Hexadecimal Keypad:**
- Found to the left of the binary-coded switches, this keypad allows for hexadecimal input. It is typically used in devices requiring a compact input method for complex data.

7. **Rotary Switches:**
- Various types of rotary switches are present, which allow the user to select one of many different circuits by rotating the switch.

8. **Slide Switches:**
- These are small switches that slide from one position to another, often used in circuits requiring a small footprint and easy manual operation.

The image provides a comprehensive look at different switch types, each with unique mechanical structures and intended uses, reflecting their importance in electronic design and functionality.

Figure 1.117. Switch Smorgasbord. The nine switches at right are momentary-contact ("pushbutton") switches, including both panelmounting and PCB-mounting types (PCB, printed-circuit board). To their left are additional types, including lever-actuated and multipole styles. Above them are a pair of panel-mounting binary-coded thumbwheel switches, to the left of which is a matrix-encoded hexadecimal keypad. The switches at center foreground are toggle switches, in both panel-mounting and PCB-mounting varieties; several actuator styles are shown, including a locking variety (fourth from front) that must be pulled before it will switch. The rotary switches in the left column illustrate binary-coded types (the three in front and the larger square one), and the traditional multipole-multiposition configurable wafer switches.
image_name:Figure 1.118
description:The image titled "Figure 1.118" showcases a variety of board-mounted DIP switches organized into three distinct groups, each demonstrating different configurations and functionalities.

1. **Identification of Components and Structure:**
- **Left Group:** This group includes single-pole single-throw (SPST) switches. From front to back and left to right, the components are:
- A single station side-action toggle switch.
- A three-station side-action toggle switch.
- A two-station rocker switch.
- A single-station slide switch.
- An eight-station low-profile slide switch.
- A six-station rocker switch.
- Another eight-station slide switch and rocker switch.

2. **Middle Group:** This group consists of hexadecimal coded switches, which are crucial for applications requiring binary input or coding. The components include:
- A six-pin low-profile switch.
- A six-pin switch with top or side adjustability.
- A 16-pin switch with both true and complement coding options.

3. **Right Group:** This group contains very small switches, measuring 2 mm x 2 mm, suitable for compact spaces.

2. **Connections and Interactions:**
- These DIP switches are designed for mounting on printed circuit boards (PCBs) and are used to set configurations or control logic circuits. The pins visible on each switch allow for electrical connections to the PCB, enabling the flow of signals.
- The switches can be toggled to change the circuit path or configuration, often used in setting device parameters or modes.

3. **Labels, Annotations, and Key Features:**
- Each switch is labeled with numbers or letters to indicate the switch position or configuration setting. For instance, the left group has numbers indicating the station or switch sequence.
- The middle group switches are marked with hexadecimal codes, which are essential for digital applications requiring precise coding.
- The scale at the bottom right indicates that the size of the components is small, with a reference length of 1 cm, highlighting their suitability for compact electronic applications.

Overall, this image provides a comprehensive view of various DIP switches used in electronics, illustrating their design, functionality, and potential applications.

Figure 1.118. Board-mounted "DIP switches." Left group, front to back and left to right (all are SPST): single station side-action toggle; three-station side-action, two-station rocker, and single-station slide; eight-station slide (low-profile) and six-station rocker; eight-station slide and rocker. Middle group (all are hexadecimal coded): six-pin low-profile, six-pin with top or side adjust; 16-pin with true and complement coding. Right group: $2 \mathrm{~mm} \times 2 \mathrm{~mm}$ surface-mount header block with movable jumper ("shunt"), $0.1^{\prime \prime} \times 0.1^{\prime \prime}$ ( $2.54 \mathrm{~mm} \times 2.54 \mathrm{~mm}$ ) through-hole header block with shunts; 18-pin SPDT (common actuator); eight-pin dual SPDT slide and rocker; 16-pin quad SPDT slide (two examples).
switch, and DPDT indicates a double-pole double-throw switch). Toggle switches are also available with "center OFF" positions and with up to four poles switched simultaneously. Toggle switches are always "break before make," e.g., the moving contact never connects to both terminals in an SPDT switch.
image_name:Figure 1.119
description:
[
name: SPST, type: Switch, ports: {N1: Node1, N2: Node2}
name: SPDT, type: Switch, ports: {N1: Node3, N2: Node4, N3: Node5}
name: DPDT, type: Switch, ports: {N1: Node6, N2: Node7, N3: Node8, N4: Node9}
]
extrainfo:The diagram illustrates fundamental switch types including Single Pole Single Throw (SPST), Single Pole Double Throw (SPDT), and Double Pole Double Throw (DPDT). Each switch type is represented with its corresponding schematic symbol.

Figure 1.119. Fundamental switch types.
image_name:form A, NO
description:
[
name: form A, NO, type: Switch, ports: {N1: Node1, N2: Node2}
]
extrainfo:The diagram illustrates three types of switches: Form A (Normally Open), Form B (Normally Closed), and Form C (Single Pole Double Throw). Form A is used for normally open applications where the circuit is completed when the switch is activated. Form B is used for normally closed applications where the circuit is open when the switch is activated. Form C is a SPDT switch, which can connect a common terminal to either of two other terminals, labeled NO (Normally Open) and NC (Normally Closed).
image_name:form B, NC
description:
[
name: form B, NC, type: Diode, ports: {Na: Node1, Nc: Node2}
]
extrainfo:The diagram illustrates fundamental switch types including Single Pole Single Throw (SPST), Single Pole Double Throw (SPDT), and Double Pole Double Throw (DPDT). The focus is on the 'form B, NC' which is a normally closed diode configuration.
image_name:form C, SPDT
description:
[
name: form C, SPDT, type: Switch, ports: {N1: C, N2: NC, N3: NO}
]
extrainfo:The diagram illustrates different types of switches: Form A (Normally Open), Form B (Normally Closed), and Form C (Single Pole Double Throw). It highlights the schematic symbols for each switch type.

Figure 1.120. Momentary-contact (pushbutton) switches.

#### B. Pushbutton switches

Pushbutton switches are useful for momentary-contact applications; they are drawn schematically as shown in Figure 1.120 (NO and NC mean normally open and normally closed). For SPDT momentary-contact switches, the terminals must be labeled NO and NC, whereas for SPST types the symbol is self-explanatory. Momentary-contact switches are always "break before make." In the electrical (as opposed to electronic) industry, the terms form A, form B , and form C are used to mean SPST (NO), SPST (NC), and SPDT, respectively.

#### C. Rotary switches

Rotary switches are available with many poles and many positions, often as kits with individual wafers and shaft hardware. Both shorting (make-before-break) and nonshorting (break-before-make) types are available, and they can be mixed on the same switch. In many applications the shorting type is useful to prevent an open circuit between switch positions, because circuits can go amok with unconnected inputs. Nonshorting types are necessary if the separate lines being switched to one common line must not ever be connected to each other.

Sometimes you don't really want all those poles, you just want to know how many clicks (detents) the shaft has been turned. For that a common form of rotary switch en-
codes its position as a 4-bit binary quantity, thereby saving lots of wires (only five are needed: the four bits, and a common line). An alternative is the use of a rotary encoder, an electromechanical panel-mounting device that creates a sequence of $N$ pulse pairs for each full rotation of the knob. These come in two flavors (internally using either mechanical contacts or electro-optical methods), and typically provide from 16 to 200 pulse pairs per revolution. The optical varieties cost more, but they last forever.

#### D. PC-mounting switches

It's common to see little arrays of switches on printedcircuit (PC) boards, like the ones shown in Figure 1.118. They're often called DIP switches, referring to the integrated circuit dual in-line package that they borrow, though contemporary practice increasingly uses the more compact surface-mount technology (SMT) package. As the photograph illustrates, you can get coded rotary switches; and because these are used for set-and-forget internal settings, you can substitute a multipin header block, with little slideon "shunts" to make the connections.

#### E. Other switch types

In addition to these basic switch types, there are available various exotic switches such as Hall-effect switches, reed switches, proximity switches, etc. All switches carry maximum current and voltage ratings; a small toggle switch might be rated at 150 volts and 5 amps . Operation with inductive loads drastically reduces switch life because of arcing during turn-off. It's always OK to operate a switch below its maximum ratings, with one notable exception: since many switches rely on substantial current flow to clean away contact oxides, it's important to use a switch that is designed for "dry switching" when switching lowlevel signals, ${ }^{50}$ otherwise you'll get noisy and intermittent operation (see Chapter 1x).

#### F. Switch examples

As an example of what can be done with simple switches, let's consider the following problem: suppose you want to sound a warning buzzer if the driver of a car is seated and one of the car doors is open. Both doors and the driver's seat have switches, all normally open. Figure 1.121 shows a circuit that does what you want. If one or the other door is open (switch closed) AND the seat switch is closed, the buzzer sounds. The words OR and AND are used in a logic sense here, and we will see this example again in

[^40]image_name:Figure 1.121
description:
[
name: buzzer, type: Other, ports: {N1: +12V, N2: seat}
name: seat, type: Switch, ports: {N1: buzzer, N2: node1}
name: left door, type: Switch, ports: {N1: node1, N2: GND}
name: right door, type: Switch, ports: {N1: node1, N2: GND}
]
extrainfo:The circuit sounds the buzzer if the seat switch and either the left door or right door switch is closed, indicating a logic AND-OR operation.

Figure 1.121. Switch circuit example: open door warning.
Chapters 2, 3, and 10 when we talk about transistors and digital logic.

Figure 1.122 shows a classic switch circuit used to turn a ceiling lamp on or off from a switch at either of two entrances to a room.
image_name:Figure 1.122
description:
[
name: 115Vac, type: VoltageSource, value: 115Vac, ports: {Np: node1, Nn: node2}
name: Switch1, type: Switch, ports: {N1: node1, N2: node3}
name: Switch2, type: Switch, ports: {N1: node4, N2: node2}
name: Lamp, type: Other, ports: {N1: node3, N2: node4}
]
extrainfo:This is a classic three-way switch circuit used to control a lamp from two different switches. The lamp is powered by a 115Vac source. The circuit allows the lamp to be turned on or off from either switch.

Figure 1.122. Electrician's "three-way" switch wiring.

Exercise 1.36. Although few electronic circuit designers know how, every electrician can wire up a light fixture so that any of $N$ switches can turn it on or off. See if you can figure out this generalization of Figure 1.122. It requires two SPDT switches and $N-2$ DPDT switches.

### 1.9.2 Electromechanical devices: relays

Relays are electrically controlled switches. In the traditional electromechanical relay, a coil pulls in an armature (to close the contacts) when sufficient coil current flows. Many varieties are available, including "latching" and "stepping" relays. ${ }^{51}$ Relays are available with dc or ac

[^41]excitation, and coil voltages from 3 volts up to 115 volts (ac or dc) are common. "Mercury-wetted" and "reed" relays are intended for high-speed ( $\sim 1 \mathrm{~ms}$ ) applications, and giant relays intended to switch thousands of amps are used by power companies.

The solid-state relay (SSR) - consisting of a semiconductor electronic switch that is turned on by a LED - provides better performance and reliability than mechanical relays, though at greater cost. SSRs operate rapidly, without contact "bounce," and usually provide for smart switching of ac power (they turn on at the moment of zero voltage, and they turn off at the moment of zero current). Much more on these useful devices in Chapter 12.

As we'll learn, electrically controlled switching of signals within a circuit can be accomplished with transistor switches, without having to use relays of any sort (Chapters 2 and 3 ). The primary uses of relays are in remote switching and high-voltage (or high-current) switching, where it is important to have complete electrical isolation between the control signal and the circuit being switched.

### 1.9.3 Connectors

Bringing signals in and out of an instrument, routing signal and dc power around between the various parts of an instrument, providing flexibility by permitting circuit boards and larger modules of the instrument to be unplugged (and replaced) - these are the functions of the connector, an essential ingredient (and usually the most unreliable part) of any piece of electronic equipment. Connectors come in a bewildering variety of sizes and shapes. ${ }^{52}$ Figures 1.123 , 1.124 , and 1.125 give some idea of the variety.

#### A. Single-wire connectors

The simplest kind of connector is the simple pin jack or banana jack used on multimeters, power supplies, etc. It is handy and inexpensive, but not as useful as the shieldedcable or multiwire connectors you often need. The humble binding post is another form of single-wire connector, notable for the clumsiness it inspires in those who try to use it.

#### B. Shielded-cable connectors

To prevent capacitive pickup, and for other reasons we'll go into in Appendix H, it is usually desirable to pipe signals around from one instrument to another in shielded coaxial cable. The most popular connector is the BNC type that

[^42]image_name:Figure 1.123. Rectangular connectors
description:The image titled "Figure 1.123. Rectangular connectors" displays a diverse assortment of multipin electrical connectors, showcasing their variety in structure and application. The components are organized neatly, demonstrating different types of connectors commonly used in electronics.

1. **Identification of Components and Structure:**
- **Multipin Nylon Power Connectors:** Located at the lower left, these are often referred to as Molex-type connectors. They are characterized by their white or translucent plastic casing and multiple pins for connecting wires.
- **Dual-row Box Headers:** Positioned above the nylon connectors, these have a $0.1^{\prime \prime}$ spacing and are shown with and without latch ejectors. Some have Wire-Wrap® and right-angle tails, indicating their use in PCB applications.
- **D-sub Connectors:** These are visible in the center and right sections, recognizable by their D-shaped metal shields and multiple pins or sockets. They are used for connecting serial devices.
- **USB Connectors:** Located at the right side, these have the familiar flat, rectangular shape used for standard USB connections.
- **Terminal Blocks:** Visible in the top section, these are used for secure wire connections and feature screw terminals for wire attachment.

2. **Connections and Interactions:**
- The connectors are designed for various applications, including power delivery, data transmission, and signal routing. The multipin configurations allow for multiple connections in a single unit, facilitating organized and efficient wiring.
- The dual-row box headers are typically used on PCBs to connect external wires or ribbon cables, providing a stable and reliable connection.
- D-sub connectors are often used for serial communication, allowing multiple lines of data to be transmitted simultaneously.

3. **Labels, Annotations, and Key Features:**
- The image includes a scale marker indicating a length of 1 cm, providing context for the size of the connectors.
- The connectors are shown in various forms, including some with attached cables and others with exposed pins, highlighting their versatility in different applications.
- The variety of connectors illustrates the wide range of available options for specific electronic needs, from simple power connections to complex data interfaces.

Figure 1.123. Rectangular connectors. The variety of available multipin connectors is staggering. Here is a collection of common specimens: the five connectors at lower left are multipin nylon power connectors (sometimes called Molex-type for historical reasons). Above them are four dual-row box headers ( $0.1^{\prime \prime}$ spacing, shown with and without latch ejectors, and also with Wire-Wrap ${ }^{\circledR}$ and right-angle tails), and to their right an open ("unshrouded") $0.1^{\prime \prime}$ dual-row header, along with a pair of dual-row headers of finer pitch ( 2 mm and 1.27 mm ). These dual-row male connectors mate with insulation displacement connectors (IDC) such as the one shown attached to a short length of ribbon cable (just above the unshrouded header). Just below the ribbon are shown single-row $0.1^{\prime \prime}$ headers, with mating shells (AMP MODU) that accept individual wire leads. At bottom right are several terminal blocks used for power wiring, and four "Faston"type crimpable spade lugs. Above them are USB connectors, and to their left are the common RJ-45 and RJ-11 modular telephone/data connectors. The popular and reliable D-subminiature connectors are at center, including (right to left) a pair of 50-pin micro-D (cable plug, PCB socket), the 9-pin D-sub, 26-pin high-density, and a pair of 25 -pin D-subs (one IDC). Above them are (right to left) a 96 -pin VME backplane connector, a 62-pin card-edge connector with solder tails, a "Centronics-type" connector with latching bail, and a card-edge connector with ribbon IDC. At top left is a miscellany - a mating pair of "GR-type" dual banana connectors, a mating pair of Cinch-type connectors, a mating pair of shrouded Winchester-type connectors with locking jackscrews, and (to their right) a screw-terminal barrier block. Not shown here are the really tiny connectors used in small portable electronics (smartphones, cameras, etc); you can see a fine example in Figure 1.131.
adorns most instrument front panels. It connects with a quarter-turn twist and completes both the shield (ground) circuit and inner conductor (signal) circuit simultaneously. Like all connectors used to mate a cable to an instrument, it comes in both panel-mounting and cable-terminating varieties.

Among the other connectors for use with coaxial cable are the TNC ("threaded Neill-Concelman," a close cousin of the BNC, but with threaded outer shell), the highperformance but bulky type N, the miniature SMA and SMB, the subminiature LEMO and SMC, and the highvoltage MHV and SHV. The so-called phono jack used in audio equipment is a nice lesson in bad design, because the
inner (signal) conductor mates before the shield (ground) when you plug it in; furthermore, the design of the connector is such that both shield and center conductor tend to make poor contact. You've undoubtedly heard the results! Not to be outdone, the television industry has responded with its own bad standard, the type-F coax "connector," which uses the unsupported inner wire of the coax as the pin of the male plug, and a shoddy arrangement to mate the shield. ${ }^{53}$

We hereby induct these losers into the Electronic

[^43]image_name:Figure 1.124. Circular connectors
description:The image shows a collection of circular connectors, arranged in three rows, showcasing various types of multipin and non-radio frequency connectors. Each connector is paired with its corresponding panel-mounting receptacle on the left side.

1. **Top Row (Left to Right):**
- **MS-type (MIL-C-5015) Rugged Connector:** This is a robust connector available in numerous configurations, designed for military and industrial applications. It features a circular shape with multiple pins and a threaded coupling mechanism for secure connections.
- **High-Current 'Supericon':** This connector is designed to handle high currents, up to 50 amperes. It has a sturdy build and a large pin configuration to accommodate the high current flow.
- **Multipin Locking XLR:** Commonly used in audio and video applications, this connector has a locking mechanism to ensure a secure connection. It features multiple pins arranged in a circular pattern.

2. **Middle Row (Left to Right):**
- **Weatherproof Connector (Switchcraft EN3):** This connector is designed to withstand harsh environmental conditions. It has a protective cover and a sealing mechanism to prevent water ingress.
- **12 mm Video Connector (Hirose RM):** A small, circular connector used in video applications, known for its compact design and reliable performance.
- **Circular DIN and Mini-DIN Connectors:** These connectors are used for various electronic devices, including audio equipment and computer peripherals, featuring a distinctive circular layout with multiple pins.
- **4-Pin Microphone Connector:** Typically used in audio equipment, this connector has four pins and is designed for secure audio signal transmission.

3. **Bottom Row (Left to Right):**
- **Locking 6-Pin Connector (Lemo):** Known for its precision and reliability, this connector features a push-pull locking mechanism and is used in high-quality audio and video equipment.
- Various other connectors are shown, each with specific designs and pin configurations suited for different applications, such as power, audio, and video.

**Key Features:**
- The connectors vary in size, shape, and pin configuration, tailored for specific applications ranging from military and industrial to consumer electronics.
- Each connector is paired with a panel-mounting receptacle, highlighting the male and female parts of the connection.
- The image includes a scale for reference, indicating the connectors' relative sizes, with a 1 cm marker at the bottom right corner.

Figure 1.124. Circular connectors. A selection of multipin and other "non-RF" connectors; the panel-mounting receptacle is shown to the left of each cable-mounted plug. Top row, left to right: "MS"-type (MIL-C-5015) rugged connector (available in hundreds of configurations), high-current ( 50 A ) "Supericon," multipin locking XLR. Middle row: weatherproof (Switchcraft EN3), 12 mm video (Hirose RM), circular DIN, circular mini-DIN, 4-pin microphone connector. Bottom row: locking 6-pin (Lemo), microminiature 7-pin shielded (Microtech EP-7S), miniature 2-pin shrouded (Litton SM), 2.5 mm power, banana, pin jack.

Components Hall of Infamy, some charter members of which are shown in Figure 1.126.

#### C. Multipin connectors

Very frequently electronic instruments demand multiwire cables and connectors. There are literally dozens of different kinds. The simplest example is a three-wire "IEC" powerline cord connector. Among the more popular are the excellent type-D subminiature, the Winchester MRA series, the venerable MS type, and the flat ribbon-cable mass-termination connectors. These and others are shown in Figure 1.123.

Beware of connectors that can't tolerate being dropped on the floor (the miniature hexagon connectors are classic) or that don't provide a secure locking mechanism (e.g., the Jones 300 series).

#### D. Card-edge connectors

The most common method used to make connection to printed-circuit cards is the card-edge connector, which mates to a row of gold-plated contacts at the edge of the card; common examples are the motherboard connectors that accept plug-in computer memory modules. Card-edge connectors may have from 15 to 100 or more connections,
and they come with different lug styles according to the method of connection. You can solder them to a "motherboard" or "backplane," which is itself just another PCB containing the interconnecting wiring between the individual circuit cards. Alternatively, you may want to use edge connectors with standard solder-lug terminations, particularly in a system with only a few cards. A more reliable (though more costly) solution is the use of "two-part" PCB connectors, in which one part (soldered onto the board) mates with the other part (on a backplane, etc); an example is the widely used VME (VersaModule Eurocard) connector (upper right-hand corner of Figure 1.123).

### 1.9.4 Indicators

#### A. Meters

To read out the value of some voltage or current, you have a choice between the time-honored moving-pointer type of meter and digital-readout meters. The latter are more expensive and more accurate. Both types are available in a variety of voltage and current ranges. There are, in addition, exotic panel meters that read out such things as VUs (volume units, an audio dB scale), expanded-scale ac volts (e.g., 105 to 130 V ), temperature (from a thermocouple),
image_name:Figure 1.125
description:The image, titled "Figure 1.125," displays a variety of RF and shielded connectors arranged in a grid format. The connectors are organized in rows, with each row showcasing different types of connectors used for various applications. The connectors are primarily metallic and vary in size and design, indicating their specific uses for audio, RF, and high-voltage applications.

**Identification of Components and Structure:**
- **Top Row (Left to Right):**
- **Stereo Phone Jack:** A typical audio connector used for headphones and audio equipment.
- **Audio "XLR" Type:** Commonly used in professional audio and video equipment for balanced audio signals.
- **N and UHF (RF Connectors):** Used for connecting radio frequency signals, often found in telecommunications and broadcasting.

- **Second Row (Left to Right):**
- **BNC Connector:** A quick connect/disconnect RF connector used in television and other radio-frequency electronic equipment.
- **TNC Connector:** A threaded version of the BNC connector, providing better performance at microwave frequencies.
- **Type F Connector:** Commonly used for "over-the-air" terrestrial television, cable television, and universally for satellite television.
- **MHV and SHV (High Voltage):** Connectors designed to handle high voltage applications.

- **Third Row (Left to Right):**
- **2.5 mm Audio Connector:** A smaller version of the typical 3.5 mm audio jack, used in compact electronics.
- **3.5 mm Stereo Connector:** Widely used for audio connections in consumer electronics.
- **Improved 3.5 mm Stereo Connector:** An enhanced version of the standard 3.5 mm jack.
- **Phono (RCA Type):** Common in consumer electronics for audio and video signals.
- **LEMO Coaxial Connector:** Known for precision and reliability, used in various professional applications.

- **Bottom Row:**
- **SMA Connectors:** Includes panel jack and flexible coax plug, as well as board-mount jack and rigid coax plug, used for microwave applications.
- **SMB Connectors:** Smaller than SMA, used for applications requiring compactness and high performance.

**Connections and Interactions:**
Each connector is designed to interface with specific types of cables or equipment. The connectors may involve threaded or push-in mechanisms for secure attachment. The arrangement suggests a focus on providing a visual comparison of different connector types.

**Labels, Annotations, and Key Features:**
The image includes a scale marker indicating "1 cm" for size reference. The connectors are not individually labeled in the image, but their arrangement and design provide clues about their function and application. The connectors are displayed with both male and female parts, illustrating how they fit together in practical use.

Figure 1.125. RF and shielded connectors. The panel-mounting receptacle is shown to the left of each cable-mounted plug. Top row, left to right: stereo phone jack, audio "XLR" type; N and UHF (RF connectors). Second row down: BNC, TNC, type F; MHV and SHV (high voltage). Third row down: 2.5 mm ( $3 / 32^{\prime \prime}$ ) audio, 3.5 mm stereo, improved 3.5 mm stereo, phono ("RCA type"), LEMO coaxial. Bottom row: SMA (panel jack, flexible coax plug), SMA (board-mount jack, rigid coax plug), SMB; SC and ST (optical fiber).
percentage motor load, frequency, etc. Digital panel meters often provide the option of logic-level outputs, in addition to the visible display, for internal use by the instrument.

As a substitute for a dedicated meter (whether analog or digital), you increasingly see an LCD (liquid-crystal display) or LED panel with a meter-like pattern. This is flexible and efficient: with a graphic LCD display module (§12.5.3) you can offer the user a choice of "meters," according to the quantity being displayed, all under the control of an embedded controller (a built-in microprocessor; see Chapter 15).

#### B. Lamps, LEDs, and displays

Flashing lights, screens full of numbers and letters, eerie sounds - these are the stuff of science fiction movies, and except for the last, they form the subject of lamps and displays (see §12.5.3). Small incandescent lamps used to be standard for front-panel indicators, but they have been re-
placed with LEDs. The latter behave electrically like ordinary diodes, but with a forward voltage drop in the range of 1.5 to 2 volts (for red, orange, and some green LEDs; 3.6 V for blue ${ }^{54}$ and high-brightness green; see Figure 2.8). When current flows in the forward direction, they light up. Typically, 2 mA to 10 mA produces adequate brightness. LEDs are cheaper than incandescent lamps, they last pretty much forever, and they come in four standard colors as well as "white" (which is usually a blue LED with a yellow fluorescent coating). They come in convenient panel-mounting packages; some even provide built-in current limiting. ${ }^{55}$

LEDs can also be used for digital displays, for example

[^44]image_name:Figure 1.126
description:The image labeled "Figure 1.126" showcases a variety of electrical components that are generally advised against using, as per the context provided. The components are arranged in three rows, each containing different types of connectors, switches, and other elements.

1. **Top Row (Left to Right):**
- **Low-value wirewound potentiometer:** This component is circular with a metallic casing, typically used for adjusting resistance but not preferred due to its low value.
- **Type UHF connector:** A cylindrical connector often used for radio frequency applications, but not recommended here.
- **Electrical tape:** A roll of black tape, commonly used for insulation but discouraged in this context.

2. **Middle Row (Left to Right):**
- **Cinch-type connectors:** These are small, rectangular connectors with multiple pins, usually used for quick connections.
- **Microphone connector:** A cylindrical connector, possibly used for audio equipment, but not preferred.
- **Hexagon connectors:** These connectors have a hexagonal shape, used for specific types of connections that may not be reliable.

3. **Bottom Row (Left to Right):**
- **Slide switch:** A small switch used for turning circuits on or off, not recommended due to its construction.
- **Cheap IC socket (not "screw-machined"):** A socket for integrated circuits, noted for being inexpensive and less durable.
- **Type-F connector:** A coaxial RF connector, typically used for cable television, not advised here.
- **Open-element trimmer pot:** A small, adjustable resistor, exposed and prone to damage.
- **Phono connector:** Used for audio connections, but not preferred due to potential quality issues.

The components shown are generally considered outdated or unreliable for modern applications, and alternatives are likely suggested elsewhere in the context. The image serves as a visual guide to identify and avoid these components in electronic designs.

Figure 1.126. Components to avoid. We advise against using components like these, if you have a choice (see text if you need convincing!). Top row, left to right: low-value wirewound pot, type UHF connector, electrical tape ("just say no!"). Middle row: "cinchtype" connectors, microphone connector, hexagon connectors. Bottom row: slide switch, cheap IC socket (not "screw-machined"), type-F connector, open-element trimmer pot, phono connector.
as 7 -segment numeric displays or (for displaying letters as well as numbers - "alphanumeric") 16-segment displays or dot-matrix displays. However, if more than a few digits or characters need to be displayed, LCDs are generally preferred. These come in line-oriented arrays (e.g., 16 characters by 1 line, up to 40 characters by 4 lines), with a simple interface that permits sequential or addressable entry of alphanumeric characters and additional symbols. They are inexpensive, low power, and visible even in sunlight. Back-lighted versions work well even in subdued light, but are not low power. Much more on these (and other) optoelectronic devices in §12.5.

### 1.9.5 Variable components

#### A. Variable resistors

Variable resistors (also called volume controls, potentiometers, pots, or trimmers) are useful as panel controls or internal adjustments in circuits. A classic panel type is the 2-watt-type AB potentiometer; it uses the same basic material as the fixed carbon-composition resistor, with a rotatable "wiper" contact. Other panel types are available with ceramic or plastic resistance elements, with improved characteristics. Multiturn types ( 3,5 , or 10 turns) are available, with counting dials, for improved resolution and linearity. "Ganged" pots (several independent sections on one shaft) are also manufactured, although in limited variety, for applications that demand them. Figure 1.8 shows a representative selection of pots and trimmers.

For use inside an instrument, rather than on the front panel, trimmer pots come in single-turn and multiturn styles, most intended for printed-circuit mounting. These are handy for calibration adjustments of the "set-andforget" type. Good advice: resist the temptation to use lots of trimmers in your circuits. Use good design instead.
image_name:Figure 1.127
description:
[
name: Potentiometer, type: Resistor, ports: {N1: CCW, N2: CW}
]
extrainfo:The diagram shows a potentiometer, which is a three-terminal variable resistor, with terminals labeled CCW (counterclockwise) and CW (clockwise). The middle terminal is the adjustable wiper.

Figure 1.127. Potentiometer (three-terminal variable resistor).

The symbol for a variable resistor, or pot, is shown in Figure 1.127. Sometimes the symbols CW and CCW are used to indicate the clockwise and counterclockwise ends.

An all-electronic version of a potentiometer can be made with an array of electronic (transistor) switches that select a tap in a long chain of fixed resistors. As awkward as that may sound, it is a perfectly workable scheme when implemented as an IC. For example, Analog Devices, Maxim/Dallas Semiconductor, and Xicor make a series of "digital potentiometers" with up to 1024 steps; they come as single or dual units, and some of them are "nonvolatile," meaning that they remember their last setting even if power has been turned off. These find application in consumer electronics (televisions, stereos) where you want to adjust the volume from your infrared remote control, rather than by turning a knob; see $\S 3.4 .3 \mathrm{E}$.

One important point about variable resistors: don't attempt to use a potentiometer as a substitute for a precise resistor value somewhere within a circuit. This is tempting, because you can trim the resistance to the value you want. The trouble is that potentiometers are not as stable as good $(1 \%)$ resistors, and in addition they may not have good resolution (i.e., they can't be set to a precise value). If you must have a precise and settable resistor value somewhere, use a combination of a $1 \%$ (or better) precision resistor and a potentiometer, with the fixed resistor contributing most of the resistance. For example, if you need a 23.4 k resistor, use a $22.6 \mathrm{k} 1 \%$ fixed resistor (a standard value) in series with a 2 k trimmer pot. Another possibility is to use a series combination of several precision resistors, selecting the last (and smallest) resistor to give the desired series resistance.

As we'll see later (§3.2.7), it is possible to use FETs as voltage-controlled variable resistors in some applications. Another possibility is an "optophotoresistor" (§12.7). Transistors can be used as variable-gain amplifiers, again controlled by a voltage. Keep an open mind when design brainstorming.
image_name:Figure 1.128
description:
[
name: Variable Capacitor, type: Capacitor, value: Variable, ports: {Np: , Nn:}
]
extrainfo:The diagram shows the symbol for a variable capacitor, commonly used in RF circuits for tuning purposes.

Figure 1.128. Variable capacitor.

#### B. Variable capacitors

Variable capacitors are primarily confined to the smaller capacitance values (up to about 1000 pF ) and are commonly used in RF circuits. Trimmers are available for incircuit adjustments, in addition to the panel type for user tuning. Figure 1.128 shows the symbol for a variable capacitor.

Diodes operated with applied reverse voltage can be used as voltage-variable capacitors; in this application they're called varactors, or sometimes varicaps or epicaps. They're very important in RF applications, especially phase-locked loops, automatic frequency control (AFC), modulators, and parametric amplifiers.

#### C. Variable inductors

Variable inductors are usually made by arranging to move a piece of core material in a fixed coil. In this form they're available with inductances ranging from microhenrys to henrys, typically with a $2: 1$ tuning range for any given inductor. Also available are rotary inductors (coreless coils with a rolling contact). ${ }^{56}$

#### D. Variable transformers

Variable transformers are handy devices, especially the ones operated from the 115 volt ac line. They're usually configured as "autotransformers," which means that they have only one winding, with a sliding contact. They're also commonly called Variacs (the name given to them by General Radio), and they are made by Technipower, Superior Electric, and others. Figure 1.129 shows a classic unit from General Radio. Typically they provide 0 to 135 volts ac output when operated from 115 volts, and they come in current ratings from 1 amp to 20 amps or more. They're good for testing instruments that seem to be affected by powerline variations, and in any case to verify worst-case performance. Important Warning: don't forget that the output is not electrically isolated from the powerline, as it would be with a transformer!

[^45]image_name:Figure 1.129
description:The image shows a powerline variable transformer, commonly known as a "Variac," manufactured by General Radio. The device is depicted in two forms: one fully assembled and the other with its cover removed to reveal the internal components.

1. **Identification of Components and Structure:**
- The assembled unit features a robust metal casing with a handle for portability. The front panel of the device includes a large, central rotary dial marked with voltage levels ranging from 0 to 135 volts. This dial is used to adjust the output voltage.
- The internal view reveals a coil of wire wound around a toroidal core, which is the primary component of the autotransformer. The winding is connected to the rotary dial mechanism, allowing the user to select different tap points on the winding.

2. **Connections and Interactions:**
- The device is equipped with a standard power cord for connection to a 115-volt AC power source. The output voltage is controlled by rotating the dial, which adjusts the contact point on the coil, thereby varying the output voltage.
- The internal components show wiring connections that link the input and output terminals to the coil and the dial mechanism. These connections are crucial for the operation of the transformer, allowing the variable adjustment of voltage.

3. **Labels, Annotations, and Key Features:**
- The front panel is labeled with the manufacturer's name, "General Radio," and the type "WSMT3." It also includes a power switch labeled "ON" and a reset button.
- The dial is prominently marked with voltage levels, providing a visual indication of the selected output voltage.
- Important safety information is provided, warning that the output is not electrically isolated from the powerline, emphasizing the need for caution during use.

This device is particularly useful for testing and verifying the performance of electrical instruments under varying power conditions.

Figure 1.129. A powerline variable transformer ("Variac") lets you adjust the ac input voltage to something you are testing. Here a 5 A unit is shown, both clothed and undressed.

## 1.10 A parting shot: confusing markings and itty-bitty components

In our electronics course, ${ }^{57}$ and indeed in day-to-day electronics on the bench, we encounter a wonderful confusion of component markings. Capacitors in particular are just, well, perverse: they rarely bother specifying units (even though they span 12 orders of magnitude, picofarads to farads), and for ceramic SMT varieties they dispense with any markings whatsoever! Even worse, they are still caught up in the transition from printing the value as an integer (e.g., " 470 " meaning 470 pF ) versus using exponent notation (e.g., " 470 " meaning $47 \times 10^{0}$, i.e., 47 pF ). Figure 1.130 shows exactly that case! Another trap for the unwary (and sometimes the wary, as well) is the date-code gotcha: the 4-digit code (yydd) can masquerade as a part number, as in the four examples in the photo. And, as components become smaller and smaller, there's precious little room for all but the briefest of markings; so, following the pharmaceutical industry, manufacturers invent a short

[^46]image_name:Figure 1.130
description:The image titled "Figure 1.130" displays a collection of various electronic components, each with distinct markings and features. These components are laid out clearly to illustrate potential confusion in identifying them due to their markings.

1. **Identification of Components and Structure:**
- **Integrated Circuits (ICs):**
- There are three ICs visible. The first is marked with "S7426" and "M1406N." The second IC is labeled "9H26/74126" and "PCF7419." The third IC is marked with "UA7812" and "UC7924 FKOREA," indicating it might be a voltage regulator.
- **Resistors:**
- Two cylindrical resistors are shown, each with different markings. One is labeled "7321F" and "8502J," indicating potential resistance values.
- **Capacitors:**
- A small rectangular capacitor is marked "C105" and "470K," and a disc capacitor is labeled "470K Y5P."
- **Other Components:**
- A diode is visible, marked "18C," and another component is labeled "8001000 0.005%."

2. **Connections and Interactions:**
- The components are not connected in this image; they are displayed separately for identification purposes. There are no visible wiring or PCB traces indicating signal flow or circuit connections.

3. **Labels, Annotations, and Key Features:**
- The ICs have both part numbers and date codes, which can cause confusion as they might be mistaken for valid part numbers.
- The resistors and capacitors have markings that could represent either their values or part numbers, contributing to potential misidentification.
- The scale at the bottom right indicates a measurement of 1 cm, providing a reference for the size of the components.

Overall, the image serves as a visual representation of how similar markings on electronic components can lead to confusion, especially when part numbers and date codes are not clearly distinguished.

Figure 1.130. Confusion Central! The three ICs are each marked with both a part number (e.g., UA7812) and a "date code" (e.g., UC7924, signifying the 24th week of 1979). Unfortunately, both are perfectly valid part numbers (a +12 V or a -24 V regulator). The resistor pair (actually two views of identically marked resistors) suffers from the same problem: it could be $7.32 \mathrm{~K} \Omega \pm 1 \%$, or it could be $85.0 \mathrm{k} \Omega \pm 5 \%$ (it's the former, but who would know?). The pair of ceramic capacitors are both marked 470K (470,000 of something?), but, surprise, the " $K$ " means $10 \%$ tolerance; and, bigger surprise, the square cap is 47 pF , the round one is 470 pF . And what is one to make of a black box labeled 80K000 (pronounced "eighty-koooh"), or a diode with two cathodes (and no anode?), or a resistor with a single black band in the center?
alphanumeric code for each component. And that's all you get. For example, National's LMV981 op-amp comes in several 6-pin packages: the SOT23 is marked "A78A," the smaller SC70 says "A77," and the really tiny microSMD blurts out a single letter "A" (or "H" if it's free of lead). Not much to go on.

### 1.10.1 Surface-mount technology: the joy and the pain

While we're complaining, let's whine just a bit about the difficulty of prototyping circuits with tiny surface-mount components. From an electrical point of view they are excellent: low inductance, and compact. But they are nearly impossible to wire up in prototype breadboard fashion, in the way that was easy with "through-hole" (or "leaded" pronounced lee'-ded) components, such as resistors with axial leads (a wire sticking out each end), or integrated circuits in DIP (dual in-line) cases. Figure 1.131 gives
image_name:Figure 1.131
description:The image shows a close-up view of a corner of a cellphone circuit board, illustrating the complexity and miniaturization typical of surface-mount technology (SMT). The components visible on the board include small ceramic resistors and capacitors, which are rectangular and lack protruding leads, making them compact and suitable for high-density circuit designs.

Also present are integrated circuits (ICs) with ball-grid array (BGA) connections on their undersides. These ICs are identifiable by their black rectangular packages, and they rely on an array of tiny solder balls for electrical connections to the board, which are not visible in this view but are a key feature of BGA technology.

The circuit board also includes very small connectors, likely used for interfacing with components such as the antenna and display panel. These connectors are characterized by their fine pitch and compact design, allowing them to fit in the limited space available on the board.

Visible connections on the board include intricate printed circuit board (PCB) traces that link the various components, allowing for the flow of electrical signals and power throughout the circuit. These traces are thin lines etched onto the board's surface, forming the pathways for electrical currents.

The image includes a scale marker indicating a 1mm reference, emphasizing the small scale of the components involved. The presence of a human thumb in the image provides additional context for the size, highlighting the challenges of working with such small components during prototyping and manufacturing processes.

Figure 1.131. We're "all thumbs" when working with surfacemount technology (SMT). This is a corner of a cellphone circuit board, showing small ceramic resistors and capacitors, integrated circuits with ball-grid connecting dots on their undersides, and the Lilliputian connectors for the antenna and display panel. See also Figure 4.84.
image_name:Figure 1.132
description:The image labeled "Figure 1.132" showcases a comparison of surface-mount technology (SMT) components, highlighting their diminutive sizes. The components are lined up next to a 0.5mm mechanical pencil tip and a DIP-8 integrated circuit for scale.

1. **Identification of Components and Structure:**
- The image displays three groups of SMT components, labeled with their respective sizes: 01005 (0402 metric), 0201 (0603 metric), and 0402 (1005 metric). These represent different standard sizes of SMT resistors or capacitors, with the 01005 size being the smallest.
- A DIP-8 integrated circuit is visible at the top of the image, providing a familiar reference point for the size of the SMT components.

2. **Connections and Interactions:**
- The image does not depict any direct electrical connections or interactions between the components, as it is focused on illustrating the size differences.

3. **Labels, Annotations, and Key Features:**
- The components are clearly labeled with both their inch and metric sizes, providing a direct comparison of their physical dimensions.
- The presence of the 0.5mm mechanical pencil tip further emphasizes the minute scale of these components, illustrating the challenges faced during prototyping and manufacturing with such small parts.

Overall, the image effectively conveys the extreme miniaturization of modern electronic components and the associated challenges in handling and assembling them.

Figure 1.132. How small can these things get?! The "01005"-size SMT $\left(0.016^{\prime \prime} \times 0.008^{\prime \prime}\right.$, or $0.4 \mathrm{~mm} \times 0.2 \mathrm{~mm}$ ) represents the industry's greatest insult to the experimenter.
a sense of the scale of these little components, and Figure 1.132 displays the true horror of the tiniest of these the " 01005 "-size chip components ( 0402 metric) that measure $200 \mu \mathrm{~m} \times 400 \mu \mathrm{~m}$ : not much thicker than a human hair, and indistinguishable from dust!

Sometimes you can use little adapter carriers (from companies like Bellin Dynamic Systems, Capital Advanced Technologies, or Aries) to convert an SMT integrated circuit to a fake DIP. But the densest surface-mount
image_name:Figure 1.133
description:The image labeled Figure 1.133 showcases a variety of passive components typically used in surface-mount technology (SMT) packaging. These components are arranged in a grid-like fashion and vary significantly in size and function, illustrating the diversity of available SMT components.

1. **Identification of Components and Structure:**
- **Connectors and Headers:** There are several connectors and headers visible, characterized by their multiple pins and plastic housings. These components are used for establishing electrical connections between different parts of a circuit.
- **Switches and Buttons:** Small tactile switches and push buttons are present, identifiable by their distinct button-like tops.
- **Trimmer Potentiometers:** These are small adjustable resistors used for tuning and calibration purposes in circuits.
- **Inductors and Transformers:** Components with coiled wire visible, possibly inductors or small transformers, used for magnetic energy storage and transformation.
- **Resistors and Capacitors:** Small rectangular components, likely resistors and capacitors, are present. These are fundamental for controlling current flow and storing charge.
- **Crystals and Oscillators:** Some components may be quartz crystals or oscillators, used for frequency control in circuits.
- **Fuses and Protection Devices:** Small, cylindrical components that could be fuses, providing overcurrent protection.

2. **Connections and Interactions:**
- The components do not appear to be connected in this image, as it serves more as a display of available component types rather than an active circuit.
- In a real-world application, these components would be soldered onto a PCB with traces connecting them to form functional circuits.

3. **Labels, Annotations, and Key Features:**
- Some components have visible markings and labels, such as part numbers or value indicators (e.g., '50M', '101'). These labels are crucial for identifying the specific type and value of each component.
- The scale at the bottom right indicates a 1 cm reference, providing a sense of the actual size of these components, emphasizing their compactness, especially in comparison to traditional through-hole components.

Overall, this image provides a clear representation of the variety and miniaturization of components available in surface-mount technology, highlighting the complexity and precision required in modern electronics design.

Figure 1.133. A taste of the world of passive components in surface-mount packages: connectors, switches, trimmer pots, inductors, resistors, capacitors, crystals, fuses.... If you can name it, you can probably get it in SMT.
packages have no leads at all, just an array of bumps (up to several thousand!) on the underside; and these require serious "reflow" equipment before you can do anything with them. Sadly, we cannot ignore this disturbing trend, because the majority of new components are offered only in surface-mount packages. Woe to the lone basement experimenter-inventor! Figure 1.133 give a sense of the variety of passive component types that come in surfacemount configurations.

## Review of Chapter 1

An A-to-H summary of what we have learned in Chapter 1. This summary reviews basic principles and facts in Chapter 1, but it does not cover application circuit diagrams and practical engineering advice presented there.

### IfA. Voltage and Current.

Electronic circuits consist of components connected together with wires. Current $(I)$ is the rate of flow of charge through some point in these connections; it's measured in amperes (or milliamps, microamps, etc.). Voltage ( $V$ ) between two points in a circuit can be viewed as an applied driving "force" that causes currents to flow between them; voltage is measured in volts (or kilovolts, millivolts, etc.); see $\S 1.2 .1$. Voltages and currents can be steady (dc), or varying. The latter may be as simple as the sinusoidal alternating voltage (ac) from the wallplug, or as complex as a high-frequency modulated communications waveform, in which case it's usually called a signal (see T[B below). The algebraic sum of currents at a point in a circuit (a node) is zero (Kirchhoff's current law, KCL, a consequence of conservation of charge), and the sum of voltage drops going around a closed loop in a circuit is zero (Kirchhoff's voltage law, KVL, a consequence of the conservative nature of the electrostatic field).

### IB. Signal Types and Amplitude.

See §1.3. In digital electronics we deal with pulses, which are signals that bounce around between two voltages (e.g., +5 V and ground); in the analog world it's sinewaves that win the popularity contest. In either case, a periodic signal is characterized by its frequency $f$ (units of $\mathrm{Hz}, \mathrm{MHz}$, etc.) or, equivalently, period $T$ (units of $\mathrm{ms}, \mu \mathrm{s}$, etc.). For sinewaves it's often more convenient to use angular frequency (radians/s), given by $\omega=2 \pi f$.

Digital amplitudes are specified simply by the HIGH and Low voltage levels. With sinewaves the situation is more complicated: the amplitude of a signal $V(t)=V_{0} \sin \omega t$ can be given as (a) peak amplitude (or just "amplitude") $V_{0}$, (b) root-mean-square (rms) amplitude $V_{\mathrm{rms}}=V_{0} / \sqrt{2}$, or (c) peak-to-peak amplitude $V_{\mathrm{pp}}=2 V_{0}$. If unstated, a sinewave amplitude is usually understood to be $V_{\mathrm{rms}}$. A signal of rms amplitude $V_{\text {rms }}$ delivers power $P=V_{\mathrm{rms}}^{2} / R_{\text {load }}$ to a resistive load (regardless of the signal's waveform), which accounts for the popularity of rms amplitude measure.

Ratios of signal amplitude (or power) are commonly expressed in decibels $(\mathrm{dB})$, defined as $\mathrm{dB}=10 \log _{10}\left(P_{2} / P_{1}\right)$ or $20 \log _{10}\left(V_{2} / V_{1}\right)$; see $\S 1.3 .2$. An amplitude ratio of 10 (or power ratio of 100 ) is $20 \mathrm{~dB} ; 3 \mathrm{~dB}$ is a doubling of
power; 6 dB is a doubling of amplitude (or quadrupling of power). Decibel measure is also used to specify amplitude (or power) directly, by giving a reference level: for example, $-30 \mathrm{dBm}(\mathrm{dB}$ relative to 1 mW ) is $1 \mathrm{microwatt;}$ +3 dBVrms is a signal of 1.4 V rms amplitude ( 2 V peak, 4 Vpp ).

Other important waveforms are square waves, triangle waves, ramps, noise, and a host of modulation schemes by which a simple "carrier" wave is varied in order to convey information; some examples are AM and FM for analog communication, and PPM (pulse-position modulation) or QAM (quadrature-amplitude modulation) for digital communication.

### IC. The Relationship Between Current and Voltage.

This chapter concentrated on the fundamental, essential, and ubiquitous two-terminal linear devices: resistors, capacitors, and inductors. (Subsequent chapters deal with transistors - three-terminal devices in which a signal applied to one terminal controls the current flow through the other pair - and their many interesting applications. These include amplification, filtering, power conversion, switching, and the like.) The simplest linear device is the resistor, for which $I=V / R$ (Ohm's Law, see $\S 1.2 .2 \mathrm{~A}$ ). The term "linear" means that the response (e.g., current) to a combined sum of inputs (i.e., voltages) is equal to the sum of the responses that each input would produce: $I\left(V_{1}+V_{2}\right)=I\left(V_{1}\right)+I\left(V_{2}\right)$.

### ID. Resistors, Capacitors, and Inductors.

The resistor is clearly linear. But it is not the only linear two-terminal component, because linearity does not require $I \propto V$. The other two linear components are $c a$ pacitors (§1.4.1) and inductors (§1.5.1), for which there is a time-dependent relationship between voltage and current: $I=C d V / d t$ and $V=L d I / d t$, respectively. These are the time domain descriptions. Thinking instead in the frequency domain, these components are described by their impedances, the ratio of voltage to current (as a function of frequency) when driven with a sinewave (§1.7). A linear device, when driven with a sinusoid, responds with a sinusoid of the same frequency, but with changed amplitude and phase. Impedances are therefore complex, with the real part representing the amplitude of the response that is in-phase, and the imaginary part representing the amplitude of the response that is in quadrature $\left(90^{\circ}\right.$ out of phase). Alternatively, in the polar representation of complex impedance $\left(Z=|Z| e^{i \theta}\right)$, the magnitude $|Z|$ is the ratio of magnitudes $(|Z|=|V| /|I|)$ and the quantity $\theta$ is the phase shift between $V$ and $I$. The impedances of the three
linear 2-terminal components are $Z_{\mathrm{R}}=R, Z_{\mathrm{C}}=-j / \omega C$, and $Z_{\mathrm{L}}=j \omega L$, where (as always) $\omega=2 \pi f$; see $\S 1.7 .5$. Sinewave current through a resistor is in phase with voltage, whereas for a capacitor it leads by $90^{\circ}$, and for an inductor it lags by $90^{\circ}$.

### ПE. Series and Parallel.

The impedance of components connected in series is the sum of their impedances; thus $R_{\text {series }}=R_{1}+R_{2}+\cdots$, $L_{\text {series }}=L_{1}+L_{2}+\cdots, \quad$ and $\quad 1 / C_{\text {series }}=1 / C_{1}+1 / C_{2}+\cdots$. When connected in parallel, on the other hand, it's the admittances (inverse of impedance) that add. Thus the formula for capacitors in parallel looks like the formula for resistors in series, $C_{\mathrm{parallel}}=C_{1}+C_{2}+\cdots$; and vice versa for resistors and inductors, thus $1 / R_{\text {parallel }}=1 / R_{1}+1 / R_{2}+\cdots$. For a pair of resistors in parallel this reduces to $R_{\text {parallel }}=\left(R_{1} R_{2}\right) /\left(R_{1}+R_{2}\right)$. For example, two resistors of value $R$ have resistance $R / 2$ when connected in parallel, or resistance $2 R$ in series.

The power dissipated in a resistor $R$ is $P=I^{2} R=V^{2} / R$. There is no dissipation in an ideal capacitor or inductor, because the voltage and current are $90^{\circ}$ out of phase. See §1.7.6.

### ПF. Basic Circuits with R, L, and C.

Resistors are everywhere. They can be used to set an operating current, as for example when powering an LED or biasing a zener diode (Figure 1.16); in such applications the current is simply $I=\left(V_{\text {supply }}-V_{\text {load }}\right) / R$. In other applications (e.g., as a transistor's load resistor in an amplifier, Figure 3.29) it is the current that is known, and a resistor is used to convert it to a voltage. An important circuit fragment is the voltage divider (§1.2.3), whose unloaded output voltage (across $R_{2}$ ) is $V_{\text {out }}=V_{\text {in }} R_{2} /\left(R_{1}+R_{2}\right)$.

If one of the resistors in a voltage divider is replaced with a capacitor, you get a simple filter: lowpass if the lower leg is a capacitor, highpass if the upper leg is a capacitor (§§1.7.1 and 1.7.7). In either case the -3 dB transition frequency is at $f_{3 \mathrm{~dB}}=1 / 2 \pi R C$. The ultimate rolloff rate of such a "single-pole" lowpass filter is $-6 \mathrm{~dB} /$ octave, or $-20 \mathrm{~dB} /$ decade; i.e., the signal amplitude falls as $1 / f$ well beyond $f_{3 \mathrm{~dB}}$. More complex filters can be created by combining inductors with capacitors, see Chapter 6. A capacitor in parallel with an inductor forms a resonant circuit; its impedance (for ideal components) goes to infinity at the resonant frequency $f=1 /(2 \pi \sqrt{L C})$. The impedance of a series $L C$ goes to zero at that same resonant frequency. See §1.7.14.

Other important capacitor applications in this chapter (§1.7.16) include (a) bypassing, in which a capacitor's low
impedance at signal frequencies suppresses unwanted signals, e.g., on a dc supply rail; (b) blocking (§1.7.1C), in which a highpass filter blocks dc, but passes all frequencies of interest (i.e., the breakpoint is chosen below all signal frequencies); (c) timing (§1.4.2D), in which an $R C$ circuit (or a constant current into a capacitor) generates a sloping waveform used to create an oscillation or a timing interval; and (d) energy storage (§1.7.16B), in which a capacitor's stored charge $Q=C V$ smooths out the ripples in a dc power supply.

In later chapters we'll see some additional applications of capacitors: (e) peak detection and sample-and-hold (§§4.5.1 and 4.5.2), which capture the voltage peak or transient value of a waveform, and (f) the integrator (§4.2.6), which performs a mathematical integration of an input signal.

### ๆG. Loading; Thévenin Equivalent Circuit.

Connecting a load (e.g., a resistor) to the output of a circuit (a "signal source") causes the unloaded output voltage to drop; the amount of such loading depends on the load resistance, and the signal source's ability to drive it. The latter is usually expressed as the equivalent source impedance (or Thévenin impedance) of the signal. That is, the signal source is modeled as a perfect voltage source $V_{\text {sig }}$ in series with a resistor $R_{\text {sig }}$. The output of the resistive voltage divider driven from an input voltage $V_{\mathrm{in}}$, for example, is modeled as a voltage source $V_{\text {sig }}=V_{\text {in }} R_{2} /\left(R_{1}+R_{2}\right)$ in series with a resistance $R_{\mathrm{sig}}=R_{1} R_{2} /\left(R_{1}+R_{2}\right)$ (which is just $\left.R_{1} \| R_{2}\right)$. So the output of a $1 \mathrm{k} \Omega-1 \mathrm{k} \Omega$ voltage divider driven by a 10 V battery looks like 5 V in series with $500 \Omega$.

Any combination of voltage sources, current sources, and resistors can be modeled perfectly by a single voltage source in series with a single resistor (its "Thévenin equivalent circuit"), or by a single current source in parallel with a single resistor (its "Norton equivalent circuit"); see Appendix D. The Thévenin equivalent source and resistance values are found from the open-circuit voltage and short-circuit current as $V_{\mathrm{Th}}=V_{\mathrm{oc}}, R_{\mathrm{Th}}=V_{\mathrm{oc}} / I_{\mathrm{sc}}$; and for the Norton equivalent they are $I_{\mathrm{N}}=I_{\mathrm{sc}}, R_{\mathrm{N}}=V_{\mathrm{oc}} / I_{\mathrm{sc}}$.

Because a load impedance forms a voltage divider with the signal's source impedance, it's usually desirable for the latter to be small compared with any anticipated load impedance (§1.2.5A). However, there are two exceptions: (a) a current source has a high source impedance (ideally infinite), and should drive a load of much lower impedance; and (b) signals of high frequency (or fast risetime), traveling through a length of cable, suffer reflections unless the load impedance equals the so-called "characteristic impedance" $Z_{0}$ of the cable (commonly $50 \Omega$ ), see Appendix H .

### IH. The Diode, a Nonlinear Component.

There are important two-terminal devices that are not linear, notably the diode (or rectifier), see §1.6. The ideal diode conducts in one direction only; it is a "one-way valve." The onset of conduction in real diodes is roughly at 0.5 V in the "forward" direction, and there is some small leakage current in the "reverse" direction, see Figure 1.55 . Useful diode circuits include power-supply rectification (conversion of ac to dc, §1.6.2), signal rectification (§1.6.6A), clamping (signal limiting, §1.6.6C), and gating (§1.6.6B). Diodes are commonly used to prevent polarity
reversal, as in Figure 1.84; and their exponential current versus applied voltage can be used to fashion circuits with logarithmic response (§1.6.6E).

Diodes specify a maximum safe reverse voltage, beyond which avalanche breakdown (an abrupt rise of current) occurs. You don't go there! But you can (and should) with a zener diode (§1.2.6A), for which a reverse breakdown voltage (in steps, going from about 3.3 V to 100 V or more) is specified. Zeners are used to establish a voltage within a circuit (Figure 1.16), or to limit a signal's swing.
