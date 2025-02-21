# CHAPTER4 OPERATIONAL AMPLIFIERS

## 4.1 Introduction to op-amps - the "perfect component"

In the previous three chapters we learned about circuit design with "discrete components," both active and passive. Our basic building blocks were transistors, both bipolar (BJT) and field-effect (FET), along with the resistors, capacitors, and other components that are needed to set bias, couple and block signals, create load impedances, and so on.

With those tools we have gone quite far. We've learned how to design simple power supplies, signal amplifiers and followers, current sources, dc and differential amplifiers, analog switches, power drivers and regulators, and even some rudimentary digital logic.

But we've also learned to struggle with imperfections. Voltage amplifiers suffer from nonlinearity (a groundedemitter amplifier with a 1 mV input signal has $\sim 1 \%$ distortion), which you can trade off against voltage gain (by adding emitter degeneration); differential amplifiers have input unbalance, typically tens of millivolts (with bipolar transistors), ten times more with discrete junction-FETs (JFETs); in bipolar design you have to worry about input current (often substantial), and the ever-present $V_{\mathrm{BE}}$ and its variation with temperature; in FET design you trade absence of input current for unpredictability of $V_{G S}$; and so on.

We've seen hints that things can be better, in particular the remarkable linearizing effects of negative feedback (\$2.5.3), and its ability to make overall circuit performance less dependent on component imperfections. It is negative feedback that gives the emitter-degenerated amplifier its linearity advantage over the grounded-emitter amplifier (at the cost of voltage gain). And in the high-loop-gain limit, negative feedback promises circuit performance largely independent of transistor imperfections.

Promised, but not yet delivered: the high-gain amplifier blocks we need to get high loop gain in a feedback arrangement still involve substantial design efforts - the hallmark of complex circuits implemented with discrete (as opposed to integrated) components.

With this chapter we enter the promised land! The opamp is, essentially, a "perfect part": a complete integrated amplifier gain block, best thought of as a dc-coupled differential amplifier with single-ended output, and with extraordinarily high gain. It also excels in precise input symmetry and nearly zero input current. Op-amps are designed as "gain engines" for negative feedback, with such high gain that the circuit performance is set almost entirely by the feedback circuitry. Op-amps are small and inexpensive, and they should be the starting point for nearly every analog circuit you design. In most op-amp circuit designs we're in the regime where they are essentially perfect: with them we will learn to build nearly perfect amplifiers, current sources, integrators, filters, regulators, current-tovoltage converters, and a host of other modules.

Op-amps are our first example of integrated circuits many individual circuit elements, such as transistors and resistors, fabricated and interconnected on a single "chip" of silicon. ${ }^{1}$ Figure 4.1 shows some IC op-amp packaging schemes.

### 4.1.1 Feedback and op-amps

We first met negative feedback in Chapter 2, where we saw that the process of coupling the output back, in such a way as to cancel some of the input signal, improved characteristics such as linearity, flatness of response, and predictability. As we saw quantitatively, the more negative feedback that is used, the less the resultant amplifier characteristics depend on the characteristics of the open-loop (no-feedback) amplifier, ultimately depending only on the properties of the feedback network itself. Operational amplifiers are typically used in this high-loop-gain limit, with open-loop voltage gain (no feedback) of a million or so.

A feedback network can be frequency-dependent, to produce an equalization amplifier (for example the

[^16]image_name:Figure 4.1
description:The image, labeled "Figure 4.1," displays a variety of operational amplifier (op-amp) packages. These packages are common in electronic circuits and vary in size, pin count, and form factor.

1. **Identification of Components and Structure:**
- **Top Row:**
- The left component is a 14-pin plastic dual in-line package (DIP) labeled "M8640 LF347N." This package is characterized by two parallel rows of pins.
- The right component is an 8-pin plastic DIP labeled "MB1AB LF412CN," smaller in size compared to the 14-pin DIP.

2. **Middle Row:**
- The left component is a 14-pin thin-shrink small-outline package (TSSOP), labeled "LMX429 EUD 008." This package is slimmer and more compact than the DIP packages.
- The middle component is an 8-pin small-outline package (SO8) labeled "LF412 X4MSC." This is a surface-mount package with pins extending from the sides.
- The right component is an 8-pin TSSOP, labeled "4422 3K," similar to the SO8 but slightly smaller.

3. **Bottom Row:**
- The left component is a 5-pin small-outline transistor package (SOT23), labeled "ADML." It is one of the smallest packages shown and typically used for transistors or small ICs.
- The middle component is a 6-ball chip-scale package (CSP), shown from both top and bottom views. This package is extremely compact, with solder balls on the bottom for mounting.
- The right component is a 5-pin SC package, labeled "AADI," another small package similar to the SOT23.

4. **Connections and Interactions:**
- The image does not explicitly show connections or interactions between these components, as it is primarily focused on illustrating the variety of package types.

5. **Labels, Annotations, and Key Features:**
- Each component is labeled with a part number or identifier, which helps in identifying the specific model and type of op-amp or IC.
- A scale is provided at the bottom right, indicating a 1 cm reference, which helps in understanding the relative sizes of the components.

This image serves to showcase the diversity of op-amp packaging, highlighting how different designs suit various applications and space constraints in electronic devices.

Figure 4.1. Op-amps (and other linear ICs) come in a bewildering variety of "packages," most of which are represented in this photograph. Top row, left to right: 14-pin plastic dual in-line package (DIP), 8-pin plastic DIP ("mini-DIP"). Middle row: 14-pin thin-shrink small-outline package (TSSOP), 8-pin small-outline package (SO8), 8-pin TSSOP (" $\mu \mathrm{MAX}$ "). Bottom row: 5 -pin small-outline transistor package (SOT23), 6-ball chip-scale package (CSP - top and bottom views), 5 -pin SC-70. The 14-pin packages hold quad opamps (i.e., four independent op-amps), the 8 -pin packages hold duals, and the rest are singles. (TSSOP and smaller packages courtesy of Travis Eichhorn, Maxim Semiconductor.)
treble and bass "tone control" stage of amplification that you find in most audio systems); or it can be amplitudedependent, producing a nonlinear amplifier (a popular example is a logarithmic amplifier, built with feedback that exploits the logarithmic $V_{\mathrm{BE}}$ versus $I_{\mathrm{C}}$ of a diode or transistor). It can be arranged to produce a current source (nearinfinite output impedance) or a voltage source (near-zero output impedance), and it can be connected to generate very high or very low input impedance. Speaking in general terms, the property that is sampled to produce feedback is the property that is improved. Thus, if you feed back a signal proportional to the output current, you will generate a good current source.

As we remarked in $\S 2.5 .1$, feedback can be arranged intentionally to be positive, for example to make an oscillator, or, as we'll see later, to make a Schmitt trigger circuit. That's the good kind of positive feedback. The bad kind occurs, uninvited (and unwelcome), when a negativefeedback circuit is burdened with sufficient accumulated phase shifts at some frequency to produce overall positive feedback, and oscillations. This can occur for a variety of reasons. We'll discuss this important subject, and see how to prevent unwanted oscillations by frequency compensation, the topic of $\S 4.9$ at the end of the chapter.
image_name:Figure 4.2. Op-amp symbol.
description:
[
name: A1, type: OpAmp, value: A1, ports: {InP: InP, InN: InN, Out: Out}
]
extrainfo:The diagram shows a basic operational amplifier symbol with one positive input, one negative input, and a single output.

Figure 4.2. Op-amp symbol.

Having made these general comments, we now look at a few feedback examples with op-amps.

### 4.1.2 Operational amplifiers

The operational amplifier is a very high-gain dc-coupled differential amplifier with a single-ended output. You can think of the classic long-tailed pair (§2.3.8) with its two inputs and single output as a prototype, although real opamps have much higher gain (typically $10^{5}$ to $10^{6}$ ) and lower output impedance, and they allow the output to swing through most or all of the supply range (you often use a split supply, for example $\pm 5 \mathrm{~V}$ ). Operational amplifiers are available in literally thousands of types, with the universal symbol shown in Figure 4.2, where the $(+)$ and $(-)$ inputs do as expected: the output goes positive when the noninverting input $(+)$ goes more positive than the inverting input $(-)$, and vice versa. The $(+)$ and $(-)$ symbols don't mean that you have to keep one positive with respect to the other, or anything like that; they just tell you the relative phase of the output (which is important to keep negative feedback negative). Using the words "noninverting" and "inverting," rather than "plus" and "minus" helps avoid confusion. Power-supply connections are frequently not displayed, and there is no ground terminal. Operational amplifiers have enormous voltage gain, and they are never (well, hardly ever) used without feedback. Think of an opamp as fodder for feedback. The open-loop gain is so high that, for any reasonable closed-loop gain, the characteristics depend on only the feedback network. Of course, at some level of scrutiny this generalization must fail. We will start with a naïve view of op-amp behavior and fill in some of the finer points later, when we need to.

There are literally thousands of different op-amps available, offering various performance tradeoffs that we will explain later (look ahead to Tables 4.2a,b, 5.5, or 8.3 if you want to see a small sample of what's available). A very good all-around performer is the popular LF411 ("411" for short), originally introduced by National Semiconductor. Like many op-amps, it is a wee beastie packaged in the so-called mini-DIP (dual in-line package) or SOIC (smalloutline IC), and it looks as shown in Figure 4.3. It is inexpensive (less than \$1) and easy to use; it comes in an improved grade (LF411A) and also in a version containing
image_name:Figure 4.3
description:The image labeled "Figure 4.3" depicts two types of integrated circuit (IC) packages: the mini-DIP (dual in-line package) and the SOIC (small-outline IC). The larger component on the left is the LF411CN, which is a mini-DIP package. It has eight pins protruding from the bottom, four on each side, and is rectangular in shape. The dimensions are marked as 3/8 inches in width and 1/4 inch in height. The package is labeled with the part number "LF411CN" and a manufacturing code "NSC ≈ 8926."

The smaller component on the right is the LF412, which is in an SOIC package. This package is more compact, measuring 4mm in width and 3mm in height. It also has eight pins, but they are arranged in a more compact manner suitable for surface mounting on a printed circuit board (PCB). The package is labeled with "LF412 XAMSC."

Both components are operational amplifiers (op-amps), with the LF411 being a single op-amp and the LF412 being a dual op-amp, meaning it contains two independent op-amps in one package. The image illustrates the physical differences between the packaging types, highlighting the mini-DIP's suitability for through-hole mounting and the SOIC's suitability for surface mounting. There are no visible connections or annotations indicating specific wiring or circuit configurations in this diagram.

Figure 4.3. Mini-DIP and SOIC packages.
image_name:Figure 4.4. Pin connections for LF411 op-amp in 8-pin DIP.
description:
[
name: LF411, type: OpAmp, value: LF411, ports: {InP: 3, InN: 2, OutP: 6, OutN: , Vdd: 7, -Vdd: 4}
]
extrainfo:The diagram shows the pin configuration for the LF411 op-amp in an 8-pin DIP package. Pin 1 and Pin 5 are for offset null adjustment. Pin 8 is not connected. Pin 2 is the inverting input, Pin 3 is the non-inverting input, Pin 6 is the output, Pin 7 is the positive supply voltage, and Pin 4 is the negative supply voltage.

Figure 4.4. Pin connections for LF411 op-amp in 8-pin DIP.
two independent op-amps (LF412, called a "dual" opamp). We will adopt the LF411/LF412 throughout this chapter as our "standard" op-amp, and we recommend it (or perhaps the versatile LMC6482) as a good starting point for your circuit designs.

Inside the 411 is a piece of silicon containing 24 transistors (21 BJTs, 3 FETs), 11 resistors, and 1 capacitor. (You can look ahead to Figure 4.43 on page 243 to see a simplified circuit diagram of its innards.) The pin connections are shown in Figure 4.4. The dot in the upper-lefthand corner, or notch at the end of the package, identifies the end from which to begin counting the pin numbers. As with most electronic packages, you count pins counterclockwise, viewing from the top. The "offset null" terminals (also known as "balance" or "trim") have to do with correcting (externally) the small asymmetries that are unavoidable when making the op-amp. More about this later in the chapter.

### 4.1.3 The golden rules

Here are the simple rules for working out op-amp behavior with external negative feedback. They're good enough for almost everything you'll ever do.
image_name:Figure 4.5. Inverting amplifier
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: in, N2: A}
name: R2, type: Resistor, value: R2, ports: {N1: A, N2: out}
name: A1, type: OpAmp, value: A1, ports: {InP: B, InN: A, OutP: out, OutN: ''}
]
extrainfo:The circuit is an inverting amplifier with a gain of G = -R2/R1 and an input impedance of Zin = R1. The op-amp is configured with negative feedback to stabilize the gain.

Figure 4.5. Inverting amplifier.
First, the op-amp voltage gain is so high that a fraction of a millivolt between the input terminals will swing the output over its full range, so we ignore that small voltage and state golden rule I.
I. The output attempts to do whatever is necessary to make the voltage difference between the inputs zero.

Second, op-amps draw very little input current (about 50 pA for the inexpensive JFET-input LF411, and often less than a picoamp for MOSFET-input types); we round this off, stating golden rule II.
II. The inputs draw no current.

One important note of explanation: golden rule I doesn't mean that the op-amp actually changes the voltage at its inputs. It can't do that. (How could it, and be consistent with golden rule II?) What it does is "look" at its input terminals and swing its output terminal around so that the external feedback-network brings the input differential to zero (if possible).

These two rules get you quite far. We illustrate with some basic and important op-amp circuits, and these will prompt a few cautions listed in §4.2.7.

## 4.2 Basic op-amp circuits

### 4.2.1 Inverting amplifier

Let's begin with the circuit shown in Figure 4.5. The analysis is simple, if you remember your golden rules.

1. Point $B$ is at ground, so rule I implies that point $A$ is also.
2. This means that (a) the voltage across $R_{2}$ is $V_{\text {out }}$ and (b) the voltage across $R_{1}$ is $V_{\text {in }}$.
3. So, using rule II, we have $V_{\text {out }} / R_{2}=-V_{\text {in }} / R_{1}$.

In other words, the voltage gain ( $G_{V} \equiv V_{\text {out }} / V_{\text {in }}$ ) is

$$
\begin{equation*}
G_{V}=-R_{2} / R_{1} \tag{4.1}
\end{equation*}
$$

Later you will see that it's sometimes better not to ground $B$ directly, but through a resistor - but don't worry about that now.
image_name:Figure 4.6. Noninverting amplifier
description:
[
name: A1, type: OpAmp, value: A1, ports: {InP: in, InN: A, OutP: out, OutN:}
name: R1, type: Resistor, value: R1, ports: {N1: A, N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: A, N2: out}
]
extrainfo:The circuit is a noninverting amplifier with a voltage gain G = 1 + R2/R1. The input impedance Zin is infinite.

Figure 4.6. Noninverting amplifier.

Our analysis seems almost too easy! In some ways it obscures what is actually happening. To understand how feedback works, just imagine some input level, say +1 volt. For concreteness, imagine that $R_{1}$ is 10 k and $R_{2}$ is 100 k . Now, suppose the output decides to be uncooperative, and sits at zero volts. What happens? $R_{1}$ and $R_{2}$ form a voltage divider, holding the inverting input at +0.91 volts. The op-amp sees an enormous input unbalance, forcing the output to go negative. This action continues until the output is at the required -10.0 volts, at which point both opamp inputs are at the same voltage, namely ground. Similarly, any tendency for the output to go more negative than -10.0 volts will pull the inverting input below ground, forcing the output voltage to rise.

What is the input impedance? Simple. Point $A$ is always at zero volts (it's called a virtual ground). So $Z_{\text {in }}=R_{1}$. At this point you don't yet know how to figure the output impedance; for this circuit, it's a fraction of an ohm.

Note that this analysis is true even for dc - it's a dc amplifier. So if you have a signal source that has a dc offset from ground (collector of a previous stage, for instance), you may want to use a coupling capacitor (sometimes called a blocking capacitor, since it blocks dc but couples the signal). For reasons you will see later (having to do with departures of op-amp behavior from the ideal), it is usually a good idea to use a blocking capacitor if you're interested only in ac signals anyway.

This circuit is known as an inverting amplifier. Its one undesirable feature is the low input impedance, particularly for amplifiers with large (closed-loop) voltage gain, where $R_{1}$ tends to be rather small. That is remedied in the next circuit (Figure 4.6).

### 4.2.2 Noninverting amplifier

Consider Figure 4.6. Again, the analysis is simplicity itself:

$$
V_{A}=V_{\mathrm{in}}
$$

But $V_{A}$ comes from a voltage divider: $V_{A}=V_{\text {out }} R_{1} /\left(R_{1}+\right.$ $R_{2}$ ). Set $V_{A}=V_{\text {in }}$, and you get a voltage gain of

$$
\begin{equation*}
G_{V}=1+R_{2} / R_{1} \tag{4.2}
\end{equation*}
$$

This is a noninverting amplifier. In the approximation we are using, the input impedance is infinite (with the JFETinput 411 it would be $10^{12} \Omega$ or more; a BJT-input op-amp will typically exceed $10^{8} \Omega$ ). The output impedance is still a fraction of an ohm. As with the inverting amplifier, a detailed look at the voltages at the inputs will convince you that it works as advertised.
image_name:Figure 4.7A
description:
[
name: C1, type: Capacitor, value: 0.1μF, ports: {Np: in, Nn: InP(A1)}
name: R1, type: Resistor, value: 100k, ports: {N1: InP(A1), N2: GND}
name: R2, type: Resistor, value: 18k, ports: {N1: InN(A1), N2: out}
name: R1, type: Resistor, value: 2k, ports: {N1: InN(A1), N2: GND}
name: A1, type: OpAmp, ports: {InP: InP(A1), InN: InN(A1), OutP: out, OutN: ''}
]
extrainfo:The circuit is an AC-coupled noninverting amplifier with a voltage gain of 10 and a low-frequency 3 dB point of 16 Hz.
image_name:Figure 4.7B
description:
[
name: C1, type: Capacitor, value: 4.7μF, ports: {Np: X1, Nn: GND}
name: R1, type: Resistor, value: 2k, ports: {N1: in, N2: X1}
name: A1, type: OpAmp, value: A1, ports: {InP: in, InN: X1, OutP: out, OutN:}
name: R2, type: Resistor, value: 18k, ports: {N1: X1, N2: out}
]
extrainfo:This circuit is an ac-coupled noninverting amplifier. It uses an operational amplifier (A1) with a gain set by resistors R1 and R2. The capacitor C1 provides ac coupling, blocking dc signals. The gain is determined by the ratio of R2 to R1. The circuit is designed for ac signals, with a focus on maintaining gain stability at different frequencies.

Figure 4.7. Amplifiers for ac signals: A. ac-coupled noninverting amplifier, B. blocking capacitor rolls off the gain to unity at dc.

#### A. An ac amplifier

The basic noninverting amplifier, like the inverting amplifier earlier, is a dc amplifier. If the signal source is accoupled, you must provide a return to ground for the (very small) input current, as in Figure 4.7A. The component values shown give a voltage gain of 10 and a low-frequency 3 dB point of 16 Hz .

If only ac signals are being amplified, it is often a good idea to "roll off" the gain to unity at dc, especially if the amplifier has large voltage gain, to reduce the effects of finite "input offset voltage" (§4.4.1A). The circuit in Figure 4.7 B has a low-frequency 3 dB point of 17 Hz , the frequency at which the impedance of the capacitor $C_{1}$ equals $R_{1}$, or 2.0 k . Note the large capacitor value required. For noninverting amplifiers with high gain, the capacitor in this ac amplifier configuration may be undesirably large. In that
image_name:Figure 4.8. Op-amp follower
description:
[
name: OpAmp, type: OpAmp, ports: {InP: in, InN: out, OutP: out}
]
extrainfo:The circuit is an op-amp follower configuration with a gain (G) of 1.0, infinite input impedance (Zin), and zero output impedance (Zout).

Figure 4.8. Op-amp follower.
case it may be preferable to omit the capacitor and trim the offset voltage to zero, as we will discuss later. An alternative is to raise $R_{1}$ and $R_{2}$, perhaps using a $T$ network for the latter (Figure 4.66 on page 259).

In spite of its desirable high input impedance, the noninverting amplifier configuration is not necessarily to be preferred over the inverting amplifier configuration in all circumstances. As we will see later, the inverting amplifier puts less demand on the op-amp, and therefore gives somewhat better performance. In addition, its virtual ground provides a handy way to combine several signals without interaction. Finally, if the circuit in question is driven from the (stiff) output of another op-amp, it makes no difference whether the input impedance is 10 k (say) or infinity, because the previous stage has no trouble driving it in either case.

### 4.2.3 Follower

Figure 4.8 shows the op-amp version of an emitter follower. It is simply a noninverting amplifier with $R_{1}$ infinite and $R_{2}$ zero (gain $=1$ ). An amplifier of unity gain is sometimes called a buffer because of its isolating properties (high input impedance, low output impedance).

### 4.2.4 Difference amplifier

The circuit in Figure 4.9A is a difference amplifier (sometimes called a differential amplifier) with gain $R_{2} / R_{1}$. This circuit requires precise resistor matching to achieve high common-mode rejection ratios (CMRR). You may be lucky and find a batch of $100 \mathrm{k} 0.01 \%$ resistors at an electronics flea market or surplus outlet; otherwise you can buy precision resistor arrays, with close matching of ratios and temperature coefficients. ${ }^{2}$ All your difference amplifiers

[^17]image_name:A
description:
[
name: V1, type: VoltageSource, ports: {Np: V1, Nn: GND}
name: V2, type: VoltageSource, ports: {Np: V2, Nn: GND}
name: R1a, type: Resistor, value: R1, ports: {N1: V1, N2: InN(A1)}
name: R1b, type: Resistor, value: R1, ports: {N1: V2, N2: InP(A1)}
name: R2a, type: Resistor, value: R2, ports: {N1: InN(A1), N2: Vout}
name: R2b, type: Resistor, value: R2, ports: {N1: InP(A1), N2: GND}
name: A1, type: OpAmp, value: A1, ports: {InP: InP(A1), InN: InN(A1), OutP: Vout, OutN: GND}
]
extrainfo:The circuit is a classic difference amplifier with gain R2/R1, used to amplify the difference between two input voltages V2 and V1. It requires precise resistor matching to achieve high common-mode rejection ratios (CMRR). The output voltage Vout is given by the formula Vout = (R2/R1) * (V2 - V1).
image_name:B
description:
[
name: R1, type: Resistor, value: 25k, ports: {N1: in(-), N2: InN(A1)}
name: R2, type: Resistor, value: 25k, ports: {N1: sense, N2: InN(A1)}
name: R1, type: Resistor, value: 25k, ports: {N1: in(+), N2: InP(A1)}
name: R2, type: Resistor, value: 25k, ports: {N1: ref, N2: InP(A1)}
name: A1, type: OpAmp, value: INA105, ports: {InP: InP(A1), InN: InN(A1), OutP: output}
]
extrainfo:This is an integrated difference amplifier circuit using the INA105 op-amp. The resistors are precisely matched to 25k ohms for high accuracy. The circuit provides differential amplification with inputs labeled as in(-) and in(+), and outputs the amplified difference to the output node. The sense and ref nodes allow for additional connections or adjustments.

Figure 4.9. Classic difference amplifier: A. Op-amp with matched resistor ratios. B. Integrated version, with uncommitted "sense" and "reference" pins. In the best grade (INA105A) the resistor ratio is matched to better than $0.01 \%$, with a temperature coefficient better than $5 \mathrm{ppm} /{ }^{\circ} \mathrm{C}$.
will have unity gain, but that's easily remedied with further (single-ended) stages of gain. If you can't find good resistors (or even if you can!), you should know that you can buy this circuit as a convenient packaged difference amplifier, with well-matched resistors; examples are the INA105 or AMP03 $(G=1)$, INA106 ( $G=10$ or 0.1 ), and INA117 or AD629 ( $G=1$ with input dividers; input signals to $\pm 200 \mathrm{~V}$ ) from TI/Burr-Brown and Analog Devices (many more are listed in Table 5.7 on page 353). The unitygain INA105 configuration is shown in Figure 4.9B, with its uncommitted "sense" and "reference" pins. You get the classic difference amplifier by connecting sense to the output and ref to ground. But the additional flexibility lets you make all sorts of nifty circuits, such as a precision unitygain inverter, noninverting gain-of-2 amplifier, and noninverting gain-of-0.5 amplifier. We treat difference amplifiers in greater detail in $\S 5.14$.

Exercise 4.1. Show how to make these three circuits with an INA105.

There are, in addition, more sophisticated differential amplifier configurations, known officially as "instrumentation amplifiers"; they are discussed in detail in $\S \S 5.15$ and 5.16, along with a listing in Table 5.8 on page 363.
formance: their best resistor arrays specify worst-case ratio tracking to $0.001 \%$, and tracking temperature coefficient (tempco) to $\pm 0.1 \mathrm{ppm} /{ }^{\circ} \mathrm{C}$.
image_name:Figure 4.10
description:
[
name: A1, type: OpAmp, value: A1, ports: {InP: Vin, InN: GND, OutP: load, OutN:}
name: R, type: Resistor, value: R, ports: {N1: Vin, N2: GND}
]
extrainfo:The circuit is a basic op-amp current source with a floating load. The current through the load is I_load = Vin/R.

Figure 4.10. Basic op-amp current source (floating load). $V_{\text {in }}$ might come from a voltage divider, or it could be a signal that varies with time.
image_name:Figure 4.11
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: V+, N2: Vin}
name: R2, type: Resistor, value: R2, ports: {N1: Vin, N2: V-}
name: R, type: Resistor, value: R, ports: {N1: Vin, N2: GND}
name: OpAmp, type: OpAmp, value: OpAmp, ports: {InP: Vin, InN: GND, OutP: load, OutN:}
name: V+, type: VoltageSource, value: V+, ports: {Np: V+, Nn: com}
name: V-, type: VoltageSource, value: V-, ports: {Np: com, Nn: V-}
name: Load, type: Other, ports: {N1: load, N2: GND}
]
extrainfo:The circuit is a current source with a grounded load and floating power supply. The current through the load is given by I_load = Vin/R = (V+ + R2)/(R(R1 + R2)). The op-amp provides feedback to maintain the desired current through the load.

Figure 4.11. Current source with grounded load and floating power supply.

### 4.2.5 Current sources

The circuit in Figure 4.10 approximates an ideal current source, without the $V_{\mathrm{BE}}$ offset of a transistor current source. Negative feedback results in $V_{\text {in }}$ at the inverting input, producing a current $I=V_{\text {in }} / R$ through the load. The major disadvantage of this circuit is the "floating" load (neither side grounded). You couldn't generate a usable sawtooth wave with respect to ground with this current source, for example. One solution is to float the whole circuit (power supplies and all) so that you can ground one side of the load (Figure 4.11). The circuit in the box is the previous current source, with its power supplies shown explicitly. $R_{1}$ and $R_{2}$ form a voltage divider to set the current. If this circuit seems confusing, it may help to remind yourself that "ground" is a relative concept. Any one point in a circuit could be called ground. This circuit is useful for generating currents into a load that is returned to ground, but it has the disadvantage that the control input is now floating, so you cannot program the output current with an in-
put voltage referenced to ground. In addition, you've got to make sure that the floating power supply is truly floating - for example, you'd have trouble making a microamp dc current source this way if you tried to use a standard wall-plug-powered dc power supply, because capacitance between windings in its transformer would introduce reactive currents, at the 60 Hz line frequency, that might well exceed the desired microamp output current; one possible solution would be to use batteries. Some other approaches to this problem are presented in Chapter 9 (§9.3.14) in the discussion of constant-current power supplies. ${ }^{3}$

#### A. Current sources for loads returned to ground

With an op-amp and external transistor it is possible to make a simple high-quality current source for a load returned to ground; a little additional circuitry makes it possible to use a programming input referenced to ground (Figure 4.12). In the first circuit, feedback forces a voltage $V_{\mathrm{CC}}-V_{\mathrm{in}}$ across $R$, giving an emitter current (and therefore an output current) $I_{E}=\left(V_{\mathrm{CC}}-V_{\mathrm{in}}\right) / R$. There are no $V_{\mathrm{BE}}$ offsets, or their variations with temperature, with $I_{\mathrm{C}}$, with $V_{\mathrm{CE}}$, etc., to worry about. The current source is imperfect (ignoring op-amp errors: $I_{\mathrm{B}}, V_{\mathrm{OS}}$ ) only insofar as the small base current may vary somewhat with $V_{\mathrm{CE}}$ (assuming the op-amp draws no input current), not too high a price to pay for the convenience of a grounded load; a Darlington for $Q_{1}$ would reduce this error considerably. This error comes about, of course, because the op-amp stabilizes the emitter current, whereas the load sees the collector current. A variation of this circuit, using a MOSFET instead of a bipolar transistor, avoids this problem altogether, since FETs draw no dc gate current (but large power MOSFETs have plenty of input capacitance, which can cause problems; see the comment at the end of this subsection).

With this circuit the output current is proportional to the voltage drop below $V_{\mathrm{CC}}$ applied to the op-amp's noninverting input; in other words, the programming voltage is referenced to $V_{\mathrm{CC}}$, which is fine if $V_{\text {in }}$ is a fixed voltage generated by a voltage divider, but an awkward situation if an external input is to be used. This is remedied in the second circuit, in which a similar current source with an npn transistor is used to convert an input voltage (referenced to ground) to a $V_{\mathrm{CC}}$-referenced input to the final current

[^18]image_name:A
description:
[
name: A1, type: OpAmp, value: A1, ports: {InP: Vin, InN: x1, OutP: x1, OutN:}
name: Q1, type: NPN, ports: {C: Vcc, B: x1, E: GND}
name: R1, type: Resistor, value: R1, ports: {N1: Vin, N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: Vin, N2: GND}
name: R, type: Resistor, value: R, ports: {N1: Vcc, N2: x1}
name: Load, type: Resistor, ports: {N1: x1, N2: GND}
]
extrainfo:Circuit A is a current source for grounded loads, using an op-amp A1 and an NPN transistor Q1. The load current I_load is given by (Vcc - Vin) / R.
image_name:B
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: GND, N2: InN(A1)}
name: R2, type: Resistor, value: R2, ports: {N1: InP(A2), N2: GND}
name: R3, type: Resistor, value: R3, ports: {N1: +Vcc, N2: InN(A2)}
name: A1, type: OpAmp, value: A1, ports: {InP: InP(A1), InN: InN(A1), Out: Out(A1)}
name: A2, type: OpAmp, value: A2, ports: {InP: InP(A2), InN: InN(A2), Out: Out(A2)}
name: Q1, type: NPN, ports: {C: Out(A1), B: InN(A1), E: GND}
name: Q2, type: PMOS, ports: {S: +Vcc, D: Out(A2), G: InN(A2)}
name: Vin, type: VoltageSource, value: Vin, ports: {Np: InP(A1), Nn: GND}
]
extrainfo:The circuit diagram B is a current source for grounded loads that converts an input voltage referenced to ground to a Vcc-referenced input. It uses an NPN transistor (Q1) and a PMOS transistor (Q2) controlled by two op-amps (A1 and A2) to achieve this conversion. The current output (I_out) is determined by the resistors R1, R2, and R3, and the input voltage Vin.

Figure 4.12. Current sources for grounded loads that don't require a floating power supply. The op-amps may need to have rail-to-rail input and output capability (RRIO); see text.
source; for the latter we've used a $p$-channel MOSFET for variety (and to eliminate the small base-current error you get with bipolar transistors). Op-amps and transistors are inexpensive. Don't hesitate to use a few extra components to improve performance or convenience in circuit design.

One important note about these circuits: at low output currents the voltage across the emitter (or source) resistors may be quite small, which means that the op-amps must be able to operate with their inputs near or at the positive supply voltage. For example, in the circuit of Figure 4.12B $\mathrm{IC}_{2}$ needs to operate with its inputs close to the positive supply rail. Don't assume that a given op-amp will do this, without explicit permission from the datasheet! The LF411's datasheet waffles a bit on this, but grudgingly admits that it will work, albeit with degraded performance, with the inputs at the positive rail. (It will not, however, work down to the negative rail; but with $\mathrm{IC}_{1}$ powered from split supply voltages there's no problem there.) By contrast, opamps like the LMC7101 or LMC6482 guarantee proper
image_name:Figure 4.13
description:
[
name: D1, type: Diode, value: LM385-1.2, ports: {Na: Vcc, Nc: GND}
name: R1, type: Resistor, value: 100k, ports: {N1: GND, N2: InP(A1)}
name: R2, type: Resistor, value: 100k, ports: {N1: InP(A1), N2: Vin}
name: R3, type: Resistor, value: 3.3k, ports: {N1: Vcc, N2: InN(A1)}
name: R4, type: Resistor, value: 1.0Ω, ports: {N1: Vcc, N2: x1}
name: R5, type: Resistor, value: 33, ports: {N1: x1, N2: x2}
name: C1, type: Capacitor, value: 1nF, ports: {Np: InN(A1), Nn: Out(A1)}
name: A1, type: OpAmp, ports: {InP: InP(A1), InN: InN(A1), OutP: Out(A1)}
name: Q1, type: PMOS, ports: {S: Vcc, D: x1, G: Out(A1)}
name: Q2, type: NPN, ports: {C: x1, B: x2, E: Iout}
]
extrainfo:The circuit is a FET-bipolar current source suitable for high currents, utilizing an op-amp (A1) to control the PMOS (Q1) and NPN (Q2) transistors. The output current Iout ranges from 0 to 1.2A. The LM385-1.2 diode is used for voltage reference.

Figure 4.13. FET-bipolar current source suitable for high currents.
operation all the way to (and a bit beyond) the positive rail (see the "Swing to supplies?" column in Table 4.2a on page 271). Alternatively, the op-amp could be powered from a separate $V_{+}$voltage higher than $V_{\mathrm{CC}}$.
Exercise 4.2. What is the output current in the last circuit for a given input voltage $V_{\text {in }}$ ? (Did we get it right in the figure?)

Figure 4.13 shows an interesting variation on the op-amp-transistor current source. Although you can get plenty of current with a simple power MOSFET, the high interelectrode capacitances of high-current FETs may cause problems. When a relatively low-current MOSFET ${ }^{4}$ is combined with a high-current $n p n$ power transistor, this circuit has the advantage of zero base current error (which you get with FETs) along with much smaller input capacitance. In this circuit, which is analogous to the "complementary Darlington" (or Sziklai circuit; see §2.4.2A), bipolar transistor $Q_{2}$ kicks in when the output current exceeds about 20 mA .

Lest we leave the wrong impression, we emphasize that the simpler MOSFET-only circuit (in the manner of Figure 4.12B) is a preferable configuration, given the major drawback of power BJTs, namely their susceptibility to "second breakdown" and consequent limit on safe operating area (as we saw in $\S 3.5 .1 \mathrm{~B}$, see particularly Figure 3.95). Big power MOSFETs have large input capacitance, so in such a circuit you should use a network like Figure 4.13's $R_{3} C_{1}$ to prevent oscillation.

#### B. Howland current source

Figure 4.14 shows a nice "textbook" current source. If the resistors are chosen so that $R_{3} / R_{2}=R_{4} / R_{1}$, then it can be shown that $I_{\text {load }}=-V_{\text {in }} / R_{2}$.

Exercise 4.3. Show that the preceding result is correct.

[^19]image_name:Figure 4.14. Howland current source
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: Vin, N2: InN(A1)}
name: R2, type: Resistor, value: R2, ports: {N1: InP(A1), N2: GND}
name: R3, type: Resistor, value: R3, ports: {N1: Out(A1), N2: InP(A1)}
name: R4, type: Resistor, value: R4, ports: {N1: InN(A1), N2: Out(A1)}
name: A1, type: OpAmp, value: A1, ports: {InP: InP(A1), InN: InN(A1), OutP: Out(A1), OutN: ''}
]
extrainfo:The circuit is a Howland current source. The resistor ratios must be precisely matched for it to function as an ideal current source. The output current is given by I_out = -Vin/R2. The output impedance is affected by any mismatch in resistor ratios.

Figure 4.14. Howland current source.

This sounds great, but there's a hitch: the resistor ratios must be matched exactly; otherwise it isn't a perfect current source. Even so, its performance is limited by the op-amp's common-mode rejection ratio (CMRR, §2.3.8). For large output currents the resistors must be small, and the compliance is limited. Also, at high frequencies (where the loop gain is low, as we'll learn shortly) the output impedance can drop from the desired value of infinity to as little as a few hundred ohms (the op-amp's open-loop output impedance). These drawbacks limit the applicability of this clever circuit.

You can convert this circuit into a noninverting current source by grounding $R_{1}$ (where $V_{\text {in }}$ is shown) and applying the control input voltage $V_{\text {in }}$ instead to $R_{2}$.

Figure 4.15 is a nice improvement on the Howland circuit, because the output current is sourced through a sense resistor $R_{\mathrm{S}}$ whose value you can choose independently of the matched resistor array (with resistor pairs $R_{1}$ and $R_{2}$ ). The best way to understand this circuit is to think of $\mathrm{IC}_{1}$ as a difference amplifier whose output sense and reference connections sample the drop across $R_{\mathrm{S}}$ (i.e., the current); the latter is buffered by follower $\mathrm{IC}_{2}$ so there is no current error.

For this configuration you can exploit the internal precision matched resistors in an integrated difference amplifier: use something like an INA106 for $R_{1}, R_{2}$, and $\mathrm{IC}_{1}$, wired "backwards" (for $G=0.1$ ) to reduce the drop across the sense resistor. See $\S 5.14$ and Table 5.7 on page 353.

### 4.2.6 Integrators

Op-amps allow you to make nearly perfect integrators, without the restriction that $V_{\text {out }} \ll V_{\text {in }}$. Figure 4.16 shows how it's done. Input current $V_{\text {in }} / R$ flows through $C$. Because the inverting input is a virtual ground, the output voltage is given by

$$
V_{\mathrm{in}} / R=-C\left(d V_{\text {out }} / d t\right)
$$

image_name:Figure 4.15. Bipolarity current source-sink
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: Vin, N2: InP(A2)}
name: R2, type: Resistor, value: R2, ports: {N1: InP(A2), N2: InN(A1)}
name: Rs, type: Resistor, value: Rs, ports: {N1: Out(A2), N2: Iout}
name: A1, type: OpAmp, value: A1, ports: {InP: InP(A1), InN: InN(A1), OutP: Out(A1), OutN: GND}
name: A2, type: OpAmp, value: A2, ports: {InP: InP(A2), InN: GND, OutP: Out(A2), OutN: GND}
]
extrainfo:This circuit is a bipolar current source-sink configuration using two op-amps. The output current Iout is determined by the equation Iout = (R2/R1) * (Vin/Rs).

GND.
Figure 4.15. Bipolarity current source-sink.
image_name:Figure 4.16. Integrator
description:
[
name: R, type: Resistor, value: R, ports: {N1: Vin, N2: InN(A1)}
name: C, type: Capacitor, value: C, ports: {Np: InN(A1), Nn: Vout}
name: A1, type: OpAmp, value: A1, ports: {InP: GND, InN: InN(A1), OutP: Vout, OutN: GND}
]
extrainfo:This circuit is an integrator using an operational amplifier (OpAmp), a resistor (R), and a capacitor (C). The output voltage Vout is determined by the integral of the input voltage Vin, following the equation Vout(t) = -1/(RC) * integral(Vin(t) dt) + const.

Figure 4.16. Integrator.
or

$$
\begin{equation*}
V_{\text {out }}(t)=-\frac{1}{R C} \int V_{\text {in }}(t) d t+\text { const. } \tag{4.3}
\end{equation*}
$$

The input can, of course, be a current, in which case $R$ is omitted.

As an example, if we choose $R=1 \mathrm{M}$ and $C=0.1 \mu \mathrm{~F}$ in this circuit, then a constant dc input of +1 V produces $1 \mu \mathrm{~A}$ of current into the summing junction, hence an output voltage that is ramping downward at $d V_{\text {out }} / d t=-V_{\text {in }} / R C=$ $-10 \mathrm{~V} / \mathrm{s}$. To say it algebraically, for a constant $V_{\text {in }}$ or con$\operatorname{stant} I_{\text {in }}$,

$$
\Delta V_{\mathrm{out}}=-\frac{V_{\mathrm{in}}}{R C} \Delta t=-\frac{I_{\mathrm{in}}}{C} \Delta t
$$

We rigged up the integrator of Figure 4.16, with $R=1 \mathrm{M} \Omega$ and $C=1 \mathrm{nF}$, and drove it with the simple test waveform shown in Figure 4.17. Without having taken a math class, the thing knows calculus!

Sharp-eyed readers may have noticed that this circuit doesn't have any feedback at dc, and so there's no way for it to have a stable quiescent point: for any nonzero input voltage $V_{\text {in }}$, the output is going somewhere! As we'll see shortly, even with $V_{\text {in }}$ exactly at zero volts, the output tends to wander off, owing to op-amp imperfections (non-zero input current, and "offset voltage"). These latter problems can be minimized by careful choice of op-amp and circuit values; but even so you usually have to provide some way to reset the integrator. Figure 4.18 shows how this is commonly done, either with a reset switch (both discrete JFET and integrated CMOS analog switch examples are shown)
image_name:Figure 4.17. Integrator waveforms
description:The graph titled "Figure 4.17. Integrator waveforms" displays time-domain waveforms for an integrator circuit. It consists of two plots: an input and an output waveform.

1. **Type of Graph and Function:**
- This is a time-domain waveform graph depicting the behavior of an integrator circuit.

2. **Axes Labels and Units:**
- The horizontal axis represents time, with a scale of 10 milliseconds per division.
- The vertical axis for the input waveform is labeled as "input" with a scale of 0.5 volts per division.
- The vertical axis for the output waveform is labeled as "output" with a scale of 5 volts per division.

3. **Overall Behavior and Trends:**
- **Input Waveform:** The input shows a step-like behavior, with initial low voltage, followed by a rise, a plateau, a drop, and another rise.
- **Output Waveform:** The output demonstrates integration of the input signal. It starts at a low level, rises linearly corresponding to the positive step in the input, reaches a peak, then decreases with a negative slope during the input plateau, and rises again with the final input rise.

4. **Key Features and Technical Details:**
- The output waveform integrates the input signal, resulting in a linear increase or decrease in voltage corresponding to the positive or negative steps in the input.
- The output voltage changes are significantly larger in magnitude than the input changes, reflecting the integrative function of the circuit.
- The waveform shows characteristic integration behavior with smooth transitions and slopes correlating to the input signal changes.

5. **Annotations and Specific Data Points:**
- There are no specific annotations or markers on the graph, but the division scales provide reference points for measuring voltage and time changes.
- The graph effectively illustrates how the integrator circuit responds to step changes in the input signal.

Figure 4.17. Integrator waveforms. The output can go anywhere it wants to, unlike our simple $R C$ "integrator" of §1.4.4. Horizontal: $10 \mathrm{~ms} / \mathrm{div}$.
or with a large-value feedback resistor across the integrating capacitor. Closing a reset switch ${ }^{5}$ (Figures 4.18A,B) zeroes the integrator by rapidly discharging the capacitor, while allowing perfect integration when open. The use of a feedback resistor (Figure 4.18D) produces stable biasing by restoring feedback at dc (where the circuit behaves like a high-gain inverting amplifier), but the effect is to roll off the integrator action at very low frequencies, $f<1 / R_{f} C$. An additional series analog switch at the input (Figure 4.18C) lets you control the intervals during which the integrator is active; when that switch is open the integrator output is frozen at its last value.

You don't have to worry about zeroing the integrator, of course, if it's part of a larger circuit that does the right thing. We'll see a beautiful example shortly (§4.3.3), namely an elegant triangle-wave generator, in which an untamed integrator is just what you want.

This first look at the op-amp integrator assumes that the op-amp is perfect, in particular that (a) the inputs draw no current, and (b) the amplifier is balanced with both inputs at precisely the same voltage. When our op-amp honeymoon is over we'll see that real op-amps do have some input current (called "bias current," $I_{\mathrm{B}}$ ), and that they exhibit some voltage imbalance (called "offset voltage," $V_{\mathrm{OS}}$ ). These imperfections are not large - bias currents of picoamps are routine, as are offset voltages of less than a millivolt - but they can cause problems with circuits like integrators, in which the effect of a small error grows with time. We'll deal with these essential topics later in the chapter (§4.4), after you're comfortable with the basics.

[^20]image_name:A.
description:
[
name: JFET, type: Other, ports: {N1: InN1(A1), N2: Out(A1)}
name: C, type: Capacitor, value: C, ports: {Np: InN1(A1), Nn: Out(A1)}
name: A1, type: OpAmp, value: A1, ports: {InP: GND, InN: InN(A1), OutP: Out(A1), OutN:}
name: R, type: Resistor, value: R, ports: {N1: InN(A1), N2: InN1(A1)}
]
extrainfo:The circuit is an op-amp integrator with a reset switch using a JFET for resetting. It integrates the input signal at InN(A1) and provides the integrated output at Out(A1). The op-amp is configured for positive output only.
image_name:B.
description:
[
name: JFET, type: Other, ports: {N1: InN(A1), N2: Out(A1), N3: reset}
name: C, type: Capacitor, value: C, ports: {Np: InN(A1), Nn: Out(A1)}
name: A1, type: OpAmp, value: A1, ports: {InP: GND, InN: InN(A1), OutP: Out(A1)}
name: R, type: Resistor, value: R, ports: {N1: InN(A1), N2: InN(A1)}
]
extrainfo:Circuit B is an op-amp integrator with a reset switch. The input is connected to the inverting terminal of the op-amp through a resistor R, and a capacitor C is connected between the inverting terminal and the output. A JFET switch is used to reset the integrator. The non-inverting terminal is grounded.
image_name:C.
description:
[
name: C, type: Capacitor, value: 1µF, ports: {Np: Out(A1), Nn: InN(A1)}
name: A1, type: OpAmp, value: A1, ports: {InP: GND, InN: InN(A1), OutP: Out(A1), OutN:}
name: R1, type: Resistor, value: R1, ports: {N1: InN(A1), N2: Load}
name: R2, type: Resistor, value: 10M, ports: {N1: InN(A1), N2: Out(A1)}
]
extrainfo:The circuit is an op-amp integrator with a feedback capacitor and a resistor network for input and feedback. It includes a load resistor and uses a 1µF capacitor for integration. The op-amp is configured with one input grounded.
image_name:D.
description:
[
name: JFET, type: Other, ports: {N1: Out(A1), N2: InN(A1)}
name: C, type: Capacitor, value: C, ports: {Np: Out(A1), Nn: InN(A1)}
name: A1, type: OpAmp, value: A1, ports: {InP: GND, InN: InN(A1), OutP: Out(A1), OutN: GND}
name: R, type: Resistor, value: R, ports: {N1: InN(A1), N2: LOAD}
name: R1, type: Resistor, value: R1, ports: {N1: InN(A1), N2: LOAD}
name: R2, type: Resistor, value: 10M, ports: {N1: InN(A1), N2: Out(A1)}
]
extrainfo:The circuit diagram D is an op-amp integrator with a reset switch. It includes an op-amp A1, a capacitor C, resistors R1 and R2, and a load resistor. The JFET is used for resetting the integrator. The circuit is designed to integrate the input signal at InN(A1) and produce an output at Out(A1). The presence of a large resistor R2 (10M) suggests a feedback path for stability or biasing.

Figure 4.18. Op-amp integrators with reset switches.

### 4.2.7 Basic cautions for op-amp circuits

- In all op-amp circuits, golden rules I and II (§4.1.3) are obeyed only if the op-amp is in the active region, i.e., inputs and outputs are not saturated at one of the supply voltages.

For instance, overdriving one of the amplifier configurations will cause output clipping at output swings near $V_{\mathrm{CC}}$ or $V_{\mathrm{EE}}$. During clipping, the inputs will no longer be maintained at the same voltage. The op-amp output cannot swing beyond the supply voltages (typically it can swing only to within 2 V of the supplies, though certain op-amps are designed to swing all the way to one supply or the other, or to both; the latter are known as "rail-torail output" op-amps). Likewise, the output compliance of an op-amp current source is set by the same limitation.

The current source with floating load (Figure 4.10), for instance, can put a maximum of $V_{\mathrm{CC}}-V_{\text {in }}$ across the load in the "normal" direction (current in the same direction as applied voltage) and $V_{\text {in }}-V_{\mathrm{EE}}$ in the reverse direction. ${ }^{6}$

- The feedback must be arranged so that it is negative. This means (among other things) that you must not mix up the inverting and noninverting inputs. We'll learn later that you can get yourself into similar problems if you rig up a feedback network that has lots of phase shift at some frequency.
- There must always be feedback at dc in an op-amp circuit. Otherwise the op-amp is guaranteed to go into saturation.

For instance, we were able to put a capacitor from the feedback network to ground in the noninverting amplifier (to reduce gain to 1 at dc, Figure 4.7B), but we could not similarly put a capacitor in series between the output and the inverting input. Likewise, an integrator will ultimately saturate without some additional circuitry such as a reset switch.

- Some op-amps have a relatively small maximum differential-input voltage limit. The maximum voltage difference between the inverting and noninverting inputs may be limited to as little as 5 volts in either polarity. Breaking this rule will cause large input currents to flow, with degradation or destruction of the op-amp.
- Op-amps are high-gain devices, often having plenty of gain even at radiofrequencies, where the inductances in the power-rail wiring can lead to instabilities in the amplifiers. We solve this issue with mandatory (we mean it!) bypass capacitors on the op-amp supply rails. ${ }^{7}$ Note: The figures in this chapter and elsewhere (and generally in the real world) do not show bypass capacitors, for simplicity. You have been warned.

We take up some more issues of this type in $\S 4.4$, and again in Chapter 5 in connection with precision circuit design.
${ }^{6}$ The load could be rather strange, e.g., it might contain batteries, requiring the reverse sense of voltage to get a forward current; the same thing might happen with an inductive load driven by changing currents.
${ }^{7}$ When we were young we were taught that each op-amp needed its own set of bypass capacitors. But with experience we've come to realize that one pair of capacitors can work to stabilize nearby op-amps. Furthermore, local wiring inductance with multiple sets of bypass capacitors can lead to resonances, which allow one op-amp to interfere with another. For example, if $L=25 \mathrm{nH}$ and $C=0.01 \mu \mathrm{~F}$, then $f_{\mathrm{LC}}=10 \mathrm{MHz}$, and $X_{\mathrm{LC}}=1.6 \Omega$. The impedance peak at resonance will be $Q$ times higher. You can solve this problem by adding an additional parallel lossy bypass capacitor, such as a small electrolytic. Its equivalent series resistance, of order $0.5 \Omega$ or more, acts to damp the resonant $Q$.

## 4.3 An op-amp smorgasbord

In the following examples we skip the detailed analysis, leaving that fun for the reader.

### 4.3.1 Linear circuits

#### A. Optional inverter

The circuits in Figure 4.19 let you invert, or amplify without inversion, by flipping a switch. The voltage gain is either +1 or -1 , depending on the switch position. The "switches" can be CMOS analog switches ${ }^{8}$, which let you control the sense of inversion with a (digital) signal. The clever variation of Figure 4.20 lets you vary the gain continuously from follower to inverter. And when the pot $R_{1}$ is at mid-position, the circuit does nothing at all!

Exercise 4.4. Show that the circuits in Figure 4.19 work as advertised.
image_name:Figure 4.19
description:
[
name: R1, type: Resistor, value: 10.0k, ports: {N1: in, N2: InN(A1)}
name: R2, type: Resistor, value: 10.0k, ports: {N1: InP(A1), N2: out}
name: A1, type: OpAmp, value: A1, ports: {InP: InP(A1), InN: InN(A1), OutP: out, OutN: GND}
name: SW1, type: Switch, ports: {N1: InN(A1), N2: W1}
name: W1, type: Switch, ports: {N1: W1, N2: InP(A1)}
name: W2, type: Switch, ports: {N1: W1, N2: GND}
name: S1, type: Switch, ports: {N1: W1, N2: 5k}
]
extrainfo:The circuit in Figure 4.19 allows switching between follower and inverter configurations. Circuit A uses switches to toggle between follower and inverter modes. Circuit B adds a potentiometer to adjust the gain continuously between follower and inverter modes.
image_name:Figure 4.20
description:
[
name: R1, type: Resistor, value: 10.0k, ports: {N1: in, N2: InN(A1)}
name: R2, type: Resistor, value: 10.0k, ports: {N1: InN(A1), N2: out}
name: A1, type: OpAmp, value: A1, ports: {InP: InP(A1), InN: InN(A1), OutP: out, OutN:}
name: SW1, type: Switch, ports: {N1: InP(A1), N2: W1}
name: W1, type: Switch, ports: {N1: W1, N2: in}
name: W2, type: Switch, ports: {N1: W1, N2: GND}
name: S1, type: Switch, ports: {N1: W1, N2: 5k}
]
extrainfo:The circuit in Figure 4.20 allows for a continuously adjustable gain from +1 to -1. The switch SW1 selects between follower and inverter modes. The potentiometer (5k) adjusts the gain.

Figure 4.19. Optional inverters; $G= \pm 1.0$
image_name:Figure 4.19. Optional inverters; $G= \pm 1.0$
description:
[
name: R1, type: Resistor, value: 10k, ports: {N1: in, N2: InN(A1)}
name: R2, type: Resistor, value: 10k, ports: {N1: InN(A1), N2: out}
name: A1, type: OpAmp, value: A1, ports: {InP: GND, InN: InN(A1), OutP: out, OutN: ''}
]
extrainfo:The circuit is an op-amp inverter with optional gain settings of +1 or -1, controlled by the configuration of resistors and the op-amp. The input is connected through R1 to the inverting input of the op-amp, and feedback is provided through R2. The non-inverting input is grounded.

Figure 4.20. Follower-to-inverter: continuously adjustable gain from $G=+1$ to $G=-1$.

[^21]image_name:Figure 4.21
description:
[
name: A1, type: OpAmp, value: A1, ports: {InP: InP(A1), InN: GND, OutP: Out(A1), OutN:}
name: LOAD, type: Capacitor, value: 0.1uF, ports: {Np: LOAD, Nn: InP(A1)}
name: X1, type: Capacitor, value: 0.1uF, ports: {Np: X1, Nn: GND}
name: R1, type: Resistor, value: 1M, ports: {N1: InP(A1), N2: X1}
name: R2, type: Resistor, value: 1M, ports: {N1: Out(A1), N2: X1}
]
extrainfo:The circuit is an op-amp follower with bootstrap configuration. It uses a capacitor to bootstrap the input impedance, improving the performance of the op-amp with AC-coupled inputs.

Figure 4.21. Op-amp follower with bootstrap.

#### B. Follower with bootstrap

As with transistor amplifiers, the bias path can compromise the high input impedance you would otherwise get with an op-amp, particularly with ac-coupled inputs, for which a resistor to ground is mandatory. If that is a problem, the bootstrap circuit shown in Figure 4.21 is a possible solution. As in the transistor bootstrap circuit (\$2.4.3), the $0.1 \mu \mathrm{~F}$ capacitor makes the upper 1 M resistor look like a high-impedance current source to input signals. The lowfrequency rolloff for this circuit will begin at about 10 Hz , dropping at 12 dB per octave for frequencies somewhat below this. ${ }^{9}$ This circuit may exhibit some frequency peaking, analogous to the Sallen-and-Key circuit of §4.3.6; this can be tamed by adding a resistor of $1-10 \mathrm{k}$ in series with the feedback capacitor.

The very low input current (and therefore high input impedance) of FET-input op-amps generally make bootstrapping unnecessary; you can use 10 M or larger resistors for the input bias path in ac-coupled amplifiers.

#### C. Ideal current-to-voltage converter

Remember that the humble resistor is the simplest $I$-to- $V$ converter. However, it has the disadvantage of presenting a nonzero impedance to the source of input current; this can be fatal if the device providing the input current has very little compliance or does not produce a constant current as the output voltage changes. A good example is a photovoltaic cell, a diode junction that has been optimized as a light detector. Even the garden-variety signal diodes you use in circuits have a small photovoltaic effect (there are amusing stories of bizarre circuit behavior finally traced to this effect). Figure 4.22 shows the good way to convert current to voltage while holding the input strictly at ground. The inverting input is a virtual ground; this is fortunate, because a photovoltaic diode can generate only a few tenths

[^22]image_name:Figure 4.22 Photodiode amplifier
description:
[
name: Rf, type: Resistor, value: 1M, ports: {N1: Vout, N2: InN(A1)}
name: A1, type: OpAmp, ports: {InP: GND, InN: InN(A1), OutP: Vout}
name: D1, type: Diode, ports: {Na: InN(A1), Nc: GND}
]
extrainfo:The circuit is a photodiode amplifier with a transresistance configuration. It converts the current from the photodiode into a voltage output, where Vout = Rf * ID = 1 volt/μA.

Figure 4.22. Photodiode amplifier.
of a volt. This particular circuit has an output of 1 volt per microamp of input current. (With BJT-input op-amps you sometimes see a resistor connected between the noninverting input and ground; its function will be explained shortly in connection with op-amp shortcomings.)

Of course, this transresistance configuration can be used equally well for devices that source their current from some positive excitation voltage, such as $V_{\mathrm{CC}}$. Photodiodes and phototransistors (both devices that source current from a positive supply when exposed to light) are often used this way (Figure 4.23). The photodiode has lower photocurrent, but excels in linearity and speed; very fast photodiodes can operate at gigahertz speeds. By contrast, the phototransistor has a considerably higher photocurrent (owing to transistor beta, which boosts the native collector-to-base photocurrent), with poorer linearity and speed. You can even get photo-Darlingtons, which extend this trend.

In real-world applications it is usually necessary to include a small capacitor across the feedback resistor, to ensure stability (i.e., prevent oscillation or ringing). This is because the capacitance of the detector, in combination with the feedback resistor, forms a lowpass filter; the resulting lagging phase shift at high frequencies, combined with the op-amp's own lagging phase shift (see §4.9.3), can add up to $180^{\circ}$, thus producing overall positive feedback, and thus oscillation. We treat this interesting problem in some detail in Chapter $4 x$ ("Transresistance amplifiers"); be sure to read that section carefully if you are building amplifiers for photodiodes. (And analogous stability problems occur, for similar reasons, when you drive capacitive loads with op-amps; see §4.6.1B).

Exercise 4.5. Use a 411 and a 1 mA (full scale) meter to construct a "perfect" current meter (i.e., one with zero input impedance) with 5 mA full scale. Design the circuit so that the meter will never be driven more than $\pm 150 \%$ full scale. Assume that the 411 output can swing to $\pm 13$ volts ( $\pm 15 \mathrm{~V}$ supplies) and that the meter has $500 \Omega$ internal resistance.
image_name:A
description:
[
name: Q, type: NPN, ports: {C: +15, B: NC, E: InN(A1)}
name: Rf, type: Resistor, value: 100k, ports: {N1: InN(A1), N2: Out(A1)}
name: A1, type: OpAmp, ports: {InP: GND, InN: InN(A1), Out: Vout}
]
extrainfo:The circuit in diagram A is a phototransistor amplifier with reverse bias. It uses an NPN phototransistor (Q) with a collector connected to +15V, an emitter connected to the inverting input of an op-amp (A1), and a feedback resistor (Rf) of 100k ohms. The op-amp is configured as an inverting amplifier with the non-inverting input grounded. The output is taken from the op-amp's output terminal.
image_name:B
description:
[
name: Q, type: NPN, ports: {C: V+, B: NC, E: InP(A1)}
name: A1, type: OpAmp, ports: {InP: InP(A1), InN: GND, OutP: +Vout}
name: RL, type: Resistor, value: RL, ports: {N1: InP(A1), N2: GND}
]
extrainfo:Diagram B features a photodiode amplifier circuit. The phototransistor Q is reverse-biased, and the load resistor RL is used to convert the photocurrent into a voltage that is amplified by the op-amp A1. The output is taken at +Vout.
image_name:C
description:
[
name: Q, type: NPN, ports: {C: V+, B: NC, E: InP(A1)}
name: RL, type: Resistor, value: RL, ports: {N1: InP(A1), N2: GND}
name: A1, type: OpAmp, value: A1, ports: {InP: InP(A1), InN: GND, OutP: Vout}
]
extrainfo:This circuit is a phototransistor amplifier with a load resistor RL driving a voltage follower configuration using an op-amp A1. The phototransistor Q is used to convert light into an electrical signal, which is then amplified by the op-amp. The output is taken from the op-amp's output terminal, Vout.
image_name:D
description:
[
name: Q, type: NPN, ports: {C: +15, B: NC, E: InN(A1)}
name: Rf, type: Resistor, value: 100k, ports: {N1: InN(A1), N2: -Vout}
name: A1, type: OpAmp, ports: {InP: GND, InN: InN(A1), OutP: -Vout, OutN: GND}
]
extrainfo:This circuit is a phototransistor amplifier with reverse bias. The phototransistor Q is used to convert light into a current, which is then amplified by the op-amp A1. The resistor Rf provides feedback to the op-amp, controlling the gain of the amplifier. The output voltage is inverted, as indicated by the -Vout label.

Figure 4.23. Photodiode amplifiers with reverse bias: A. Phototransistor; note base terminal is not used. B. Photodiode. C. Phototransistor used as photodiode; for variety we show it current sinking. D. Phototransistor with load resistor driving voltage follower.

#### D. Summing amplifier

The circuit shown in Figure 4.24 is just a variation of the inverting amplifier. Point $X$ is a virtual ground, so the input current is $V_{1} / R_{1}+V_{2} / R_{2}+V_{3} / R_{3}$. With equal resistor values you get $V_{\text {out }}=-\left(V_{1}+V_{2}+V_{3}\right)$. Note that the inputs can be positive or negative. Also, the input resistors need not be equal; if they're unequal, you get a weighted sum. For instance, you could have four inputs, each of which is +1 volt or zero, representing binary values $1,2,4$, and 8 . By using input resistors of $10 \mathrm{k}, 5 \mathrm{k}, 2.5 \mathrm{k}$, and 1.25 k , you will get a negative output in volts equal to the binary count input. This scheme can be easily expanded to several dig-
image_name:Figure 4.24. Summing amplifier
description:
[
name: R1, type: Resistor, value: 10k, ports: {N1: V1, N2: X}
name: R2, type: Resistor, value: 10k, ports: {N1: V2, N2: X}
name: R3, type: Resistor, value: 10k, ports: {N1: V3, N2: X}
name: Rf, type: Resistor, value: 10k, ports: {N1: X, N2: Vout}
name: A1, type: OpAmp, value: A1, ports: {InP: GND, InN: X, OutP: Vout, OutN: ''}
]
extrainfo:This is a summing amplifier circuit. The output voltage Vout is given by the equation Vout = -Rf * (V1/R1 + V2/R2 + V3/R3), where Rf is the feedback resistor and R1, R2, R3 are the input resistors.

Figure 4.24. Summing amplifier.
its. It is the basis of digital-to-analog conversion, although a different input circuit (an $R-2 R$ ladder) is usually used.

Exercise 4.6. Show how to make a two-digit digital-to-analog converter (DAC) by appropriately scaling the input resistors in a summing amplifier. The digital input represents two digits, each consisting of four lines that represent the values $1,2,4$, and 8 for the respective digits. An input line is either at +1 volt or at ground, i.e., the eight input lines represent $1,2,4,8,10,20,40$, and 80 . With $\pm 15 \mathrm{~V}$ supplies, the op-amp's outputs generally cannot swing beyond $\pm 13$ volts; you will have to settle for an output in volts equal to one-tenth the value of the input number.

#### E. Power booster

For high output current, a power transistor follower can be hung on an op-amp output (Figure 4.25). In this case a noninverting amplifier has been drawn, though a follower can be added to any op-amp configuration. Notice that feedback is taken from the emitter; thus feedback enforces the desired output voltage in spite of the $V_{\mathrm{BE}}$ drop. This circuit has the usual problem that the follower output can only source current. As with transistor circuits, the remedy is a push-pull booster (Figure 4.26). We'll see later that the limited speed with which the op-amp can move its output (slew rate) seriously limits the speed of this booster in the crossover region, creating distortion. For slow-speed applications you don't need to bias the push-pull pair into quiescent conduction, because feedback will take care of most of the crossover distortion. Complete power booster ICs are available, e.g. the LT1010 and BUF633/4. These
image_name:Figure 4.25
description:
[
name: A1, type: OpAmp, value: A1, ports: {InP: Vin, InN: GND, OutP: X1, OutN:}
name: Q1, type: NPN, ports: {C: Vcc, B: X1, E: Vout}
name: 1.10k, type: Resistor, value: 1.10k, ports: {N1: Vin, N2: GND}
name: 10.0k, type: Resistor, value: 10.0k, ports: {N1: Vin, N2: X1}
name: 1k, type: Resistor, value: 1k, ports: {N1: X1, N2: Vout}
]
extrainfo:The circuit is a single-ended emitter follower using an op-amp and an NPN transistor to boost the op-amp output current. The gain of the circuit is 10.
image_name:Figure 4.26
description:
[
name: A1, type: OpAmp, value: A1, ports: {InP: Vin, InN: GND, OutP: output, OutN:}
name: Q1, type: NPN, ports: {C: Vcc, B: output, E: GND}
name: R1, type: Resistor, value: 1.10k, ports: {N1: Vin, N2: GND}
name: R2, type: Resistor, value: 10.0k, ports: {N1: Vin, N2: output}
name: R3, type: Resistor, value: 1k, ports: {N1: output, N2: GND}
]
extrainfo:The circuit shown in Figure 4.26 is a push-pull follower that boosts op-amp output current, both sourcing and sinking. It includes an NPN transistor Q1 for current boosting with a gain of 10 as indicated.

Figure 4.25. Single-ended emitter follower boosts op-amp output current (sourcing only).
image_name:Figure 4.26
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: LOAD, N2: InN(A1)}
name: R2, type: Resistor, value: R2, ports: {N1: Out(A1), N2: output}
name: A1, type: OpAmp, value: A1, ports: {InP: GND, InN: InN(A1), OutP: Out(A1), OutN: GND}
name: Q1, type: NPN, ports: {C: +VCC, B: Out(A1), E: output}
name: Q2, type: PNP, ports: {C: output, B: Out(A1), E: -VEE}
]
extrainfo:The circuit is a push-pull follower that boosts op-amp output current, both sourcing and sinking. It includes an NPN transistor Q1 and a PNP transistor Q2 for current boosting. The op-amp A1 controls the transistors to drive the output.

Figure 4.26. Push-pull follower boosts op-amp output current, both sourcing and sinking. You commonly see a small resistor ( $\sim 100 \Omega$ ) connected between the bases and emitters to reduce crossover nonlinearity by maintaining feedback throughout the signal swing. See Figure 2.71 for improved output-stage biasing.
are unity-gain push-pull amplifiers capable of 200 mA of output current, and operation to $20-100 \mathrm{MHz}$ (see $\S 5.8 .4$, and also the discussion (and table) of unity-gain buffers in Chapter $4 x$.); they are carefully biased for low open-loop crossover distortion, and include on-chip protection (current limit, and often thermal shutdown as well). As long as you ensure that the op-amp driving them has significantly less bandwidth, you can include them inside the feedback loop without any worries. ${ }^{10}$

#### Feedback and the push-pull booster

The push-pull booster circuit illustrates nicely the linearizing effect of negative feedback. We hooked up an LF411 op-amp as a noninverting unity-gain follower, driving a BJT push-pull output stage, and we loaded the output with a $10 \Omega$ resistor to ground. Figure 4.27 shows the output signals at the op-amp and at the load, with an input sinewave of 1 V amplitude at 125 Hz . For the upper pair of traces we (foolishly) took the feedback from the op-amp's output, which produced a fine replica of the input signal; but the load sees severe crossover distortion (from the $2 V_{\mathrm{BE}}$ dead zone). With the feedback coming from the push-pull output (where the load is connected) we get what we want, as seen in the lower pair of traces. The op-amp cleverly creates an exaggerated waveform to drive the push-pull follower, with precisely the right shape to compensate for the crossover.

Figure 4.28 shows what these waveforms look like when we try driving an actual loudspeaker, a load that is more complicated than a resistor (because it's both a "motor" and a "generator," it exhibits resonances and other nasty properties; it's also got a reactive crossover network, and

[^23]image_name:Figure 4.27
description:Figure 4.27 presents a time-domain waveform graph, illustrating the effect of feedback on crossover distortion in a push-pull follower circuit. The graph is divided into two sections, each showing waveforms with different feedback configurations.

1. **Axes Labels and Units:**
- The vertical axis represents voltage, with a scale of 1 V per division.
- The horizontal axis represents time, with a scale of 2 ms per division.

2. **Overall Behavior and Trends:**
- The upper pair of traces shows waveforms with feedback from the op-amp. The op-amp trace exhibits an exaggerated waveform, which is more pronounced at the peaks and troughs. This compensates for the crossover distortion by adjusting the shape of the waveform.
- The lower pair of traces shows waveforms with feedback from the load. Here, the waveforms are more symmetrical and smoother, indicating that feedback from the load reduces distortion more effectively.

3. **Key Features and Technical Details:**
- In both sections, two waveforms are shown: one labeled 'op-amp' and the other 'load.'
- The 'op-amp' waveform in the upper section has sharper peaks and troughs, while the 'load' waveform is more rounded.
- In the lower section, both waveforms are smoother, with reduced distortion, indicating effective feedback from the load.

4. **Annotations and Specific Data Points:**
- Annotations indicate the source of feedback ('feedback from op-amp' and 'feedback from load').
- The waveforms demonstrate the op-amp's ability to adjust its output to minimize distortion, particularly when feedback is derived from the load.

This graph effectively demonstrates how feedback can be used to mitigate crossover distortion in a push-pull follower circuit, with feedback from the load providing a more linear response than feedback from the op-amp alone.

Figure 4.27. Feedback cures crossover distortion in the push-pull follower. Vertical: $1 \mathrm{~V} / \mathrm{div}$; horizontal: $2 \mathrm{~ms} /$ div.
image_name:Figure 4.27
description:The graph in Figure 4.27 is a time-domain waveform illustrating how feedback impacts crossover distortion in a push-pull follower circuit. The graph is divided into two main sections: one showing feedback from the op-amp and the other showing feedback from the load.

1. **Type of Graph and Function:**
- The graph is a time-domain waveform plot, displaying voltage over time.

2. **Axes Labels and Units:**
- The vertical axis represents voltage, scaled at $1 \mathrm{~V} / \mathrm{div}$.
- The horizontal axis represents time, scaled at $2 \mathrm{~ms} / \mathrm{div}$.

3. **Overall Behavior and Trends:**
- In the section labeled "feedback from op-amp," the waveform shows noticeable distortion around the zero-crossing points, indicating significant crossover distortion.
- In the section labeled "feedback from load," the waveform is more linear and symmetrical, with reduced distortion at the zero-crossing points, demonstrating the effectiveness of feedback in mitigating distortion.

4. **Key Features and Technical Details:**
- The top waveform ("op-amp") in both sections shows more distortion compared to the bottom waveform ("load").
- The distortion is characterized by flat spots or kinks around the zero-crossing points in the "feedback from op-amp" section.
- In contrast, the "feedback from load" section shows smoother transitions through zero, indicating a more linear response.

5. **Annotations and Specific Data Points:**
- The waveforms are annotated with labels "op-amp" and "load," highlighting the source of feedback.
- The graph effectively demonstrates the improvement in linearity and reduction in distortion when feedback is taken from the load rather than directly from the op-amp.

Figure 4.28. Same as Figure 4.27, but loaded with a loudspeaker of $6 \Omega$ nominal impedance.
an inductive coil to propel the cone). Once again, the magic of feedback does the job, this time with an op-amp output that is charmingly unsymmetrical. ${ }^{11}$

#### F. Power supply

An op-amp can provide the gain for a feedback voltage regulator (Figure 4.29). The op-amp compares a sample of the output with the zener reference, changing the drive to the Darlington "pass transistor" as needed. This circuit supplies a stable 10 volt output ("regulated"), at up to 1 amp load current. Some notes about this circuit:

[^24]image_name:Figure 4.29. Voltage regulator
description:
[
name: Q1, type: NPN, ports: {C: Vin, B: Out(A1), E: Vin}
name: Q2, type: NPN, ports: {C: Vout, B: Vin, E: Vin}
name: A1, type: OpAmp, value: A1, ports: {InP: InP(A1), InN: InN(A1), OutP: Out(A1), OutN: GND}
name: D1, type: Diode, ports: {Na: InP(A1), Nc: GND}
name: CC, type: Capacitor, value: CC, ports: {Np: Out(A1), Nn: GND}
name: 10k, type: Resistor, value: 10k, ports: {N1: Vin, N2: InP(A1)}
name: 4.42k, type: Resistor, value: 4.42k, ports: {N1: Vout, N2: InN(A1)}
name: 5.62k, type: Resistor, value: 5.62k, ports: {N1: InN(A1), N2: GND}
]
extrainfo:This circuit is a voltage regulator using an op-amp to control a Darlington pair for stable output. The op-amp compares a sampled output with a zener reference and adjusts the drive to the pass transistor. It provides a regulated 10V output with up to 1A load current.

Figure 4.29. Voltage regulator.

- The voltage divider that samples the output could be a potentiometer, for adjustable output voltage.
- For reduced ripple at the zener, the 10 k resistor should be replaced with a current source. Another approach is to bias the zener from the output; that way you take advantage of the regulator you have built. Caution: when using this trick, you must analyze the circuit carefully to be sure it will start up when power is first applied.
- We used a rail-to-rail op-amp, which can swing its output to the positive rail, ${ }^{12}$ so that the input voltage can go as low as +12 V without putting the Darlington pass transistor into saturation. With a 411, by contrast, you would have to allow another $1.5-2 \mathrm{~V}$ of margin, because the opamp's output cannot get closer than that to the positive supply rail.
- The circuit as drawn could be damaged by a temporary short circuit across the output, because the op-amp would attempt to drive the Darlington pair into heavy conduction. Regulated power supplies should always have circuitry to limit "fault" current (see §9.1.1C for more details).
- Without the "compensation capacitor" $C_{\mathrm{C}}$ the circuit would likely oscillate when the dc output is bypassed (as it would be when powering a circuit) because of the additional lagging phase shift. Capacitor $C_{\mathrm{C}}$ ensures stability into a capacitive load, a subject we'll visit in $\S \S 4.6 .1 \mathrm{~B}$, 4.6.2, and 9.1.1C.
- Integrated circuit voltage regulators are available in tremendous variety, from the time-honored 723 to the

12 Our suggested LT1637 is a 44-volt "over-the-top" op-amp that exhibits strikingly higher input-bias currents when its input is near the positive rail (as much as $I_{\mathrm{B}}=20 \mu \mathrm{~A}$, about 100 times its normal bias current). The LT1677, with $I_{\mathrm{B}}=0.2 \mu \mathrm{~A}$, might be a better choice.
convenient 3-terminal adjustable regulators with internal current limit and thermal shutdown (see §9.3). These devices, complete with temperature-compensated internal voltage reference and pass transistor, are so easy to use that you will almost never use a general-purpose op-amp as a regulator. The exception might be to generate a stable voltage within a circuit that already has a stable powersupply voltage available.

In Chapter 9 we discuss voltage regulators and power supplies in detail, including special ICs intended for use as voltage regulators.

### 4.3.2 Nonlinear circuits

#### A. Comparator - an introduction

It is quite common to want to know which of two signals is larger, or to know when a given input signal exceeds a predetermined voltage. For instance, the usual method of generating triangle waves is to supply positive or negative currents into a capacitor, reversing the polarity of the current when the amplitude reaches a preset peak value. Another example is a digital voltmeter. In order to convert a voltage to a number, the unknown voltage is applied to one input of a comparator, with a linear ramp (capacitor + current source) applied to the other. A digital counter counts cycles of an oscillator during the time that the ramp is less than the unknown voltage and displays the result when equality of amplitudes is reached. The resultant count is proportional to the input voltage. This is called single-slope integration; in most sophisticated instruments a dual-slope integration is used (Chapter 13).

The simplest form of comparator is a high-gain differential amplifier, made either with transistors or with an opamp (Figure 4.30). In this circuit there's no feedback - the op-amp goes into positive or negative saturation according to the difference of the input voltages. Because of the enormous voltage gain of op-amps (typically $10^{5}-10^{6}$ ), the inputs will have to be equal to within a fraction of a millivolt in order for the output not to be saturated. Although an ordinary op-amp can be used as a comparator (and frequently is), there are special ICs intended for use as comparators. They let you set the output voltage levels independently of the voltages used to power the comparator (e.g., you can have output levels of 0 V and +5 V from a comparator powered from $\pm 15 \mathrm{~V}$ ); and they are generally much faster, because they are not trying to be op-amps, i.e., linear amplifiers intended for use with negative feedback. We'll talk about them in detail in Chapter 12 (§§12.1.7 and 12.3, and Table 12.2).

Figure 4.30. Comparator: an op-amp without feedback.
image_name:Figure 4.31
description:The graph in Figure 4.31 is a time-domain waveform depicting the behavior of a comparator without hysteresis when subjected to a noisy input signal.

1. **Type of Graph and Function:**
- The graph is a time-domain waveform showing the relationship between the input signal and the output of a comparator.

2. **Axes Labels and Units:**
- The x-axis represents time, though specific units are not provided.
- The y-axis for the top part of the graph shows voltage levels of the input signal and the trigger point. The y-axis for the bottom part shows the comparator output, typically switching between two discrete levels (e.g., 0 and 1 or low and high).

3. **Overall Behavior and Trends:**
- The input signal is noisy, with fluctuations around a central trend. This noise causes multiple crossings over the trigger point.
- The output waveform shows multiple transitions, corresponding to the input signal crossing the trigger point due to its noise.

4. **Key Features and Technical Details:**
- The input signal fluctuates around a trigger point, which is a horizontal line indicating the voltage at the other input of the comparator.
- The output signal exhibits multiple transitions, switching states each time the input crosses the trigger point.
- This behavior illustrates the lack of hysteresis, leading to instability in the output as the input signal noise causes repeated triggering.

5. **Annotations and Specific Data Points:**
- The graph includes annotations for the 'input' and 'trigger point' on the input waveform and 'output' on the output waveform.
- No specific numerical values or units are provided for the voltages or time intervals.

Figure 4.31. Comparator without hysteresis produces multiple transitions from noisy input signal.
image_name:A
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: V+, N2: InN(A1)}
name: R2, type: Resistor, value: R2, ports: {N1: InN(A1), N2: GND}
name: A1, type: OpAmp, value: A1, ports: {InP: InP(A1), InN: InN(A1), OutP: Out(A1)}
name: R1, type: Resistor, value: 10k, ports: {N1: +10, N2: InN(A1)}
name: R2, type: Resistor, value: 10k, ports: {N1: InN(A1), N2: GND}
name: R3, type: Resistor, value: 100k, ports: {N1: Out(A1), N2: InP(A1)}
name: A1, type: OpAmp, value: A1, ports: {InP: InP(A1), InN: InN(A1), OutP: Out(A1)}
]
extrainfo:Diagram A shows a comparator without hysteresis, resulting in multiple transitions due to input noise. Diagram B shows a Schmitt trigger configuration with positive feedback, preventing multiple transitions.
image_name:B
description:
[
name: R1, type: Resistor, value: 10k, ports: {N1: V+, N2: InN(A1)}
name: R2, type: Resistor, value: 10k, ports: {N1: InN(A1), N2: GND}
name: R3, type: Resistor, value: 100k, ports: {N1: Out(A1), N2: InP(A1)}
name: A1, type: OpAmp, value: A1, ports: {InP: InP(A1), InN: InN(A1), OutP: Out(A1)}
]
extrainfo:This circuit is a Schmitt trigger configuration using positive feedback to prevent multiple output transitions. The resistors R1 and R2 form a voltage divider providing a reference voltage at the inverting input of the op-amp. R3 provides positive feedback from the output to the non-inverting input, creating hysteresis.

Figure 4.32. Positive feedback prevents multiple comparator transitions. A. Comparator without feedback. B. Schmitt trigger configuration uses positive feedback to prevent multiple output transitions. Special comparator ICs are generally preferable, and are drawn with the same symbol.

#### B. Schmitt trigger

The simple comparator circuit in Figure 4.30 has two disadvantages. For a very slowly varying input, the output swing can be rather slow. Worse still, if the input is noisy, the output may make several transitions as the input passes through the trigger point (Figure 4.31). Both these problems can be remedied by use of positive feedback (Figure 4.32). The effect of $R_{3}$ is to make the circuit have two thresholds, depending on the output state. In the example shown, the threshold when the output is at ground (input high) is 4.76 volts, whereas the threshold with the output at +5 volts is 5.0 volts. A noisy input is less likely to produce multiple triggering (Figure 4.33). Furthermore, the positive feedback ensures a rapid output transition, regardless of the speed of the input waveform. (A small "speed-up" capacitor of $10-100 \mathrm{pF}$ is often connected across $R_{3}$ to enhance switching speed still further.) This configuration is known
image_name:Figure 4.33
description:The graph in Figure 4.33 illustrates the behavior of a Schmitt trigger, demonstrating how hysteresis can stabilize a noise-prone comparator. The graph features two main plots: the input voltage waveform and the corresponding output voltage waveform.

1. **Type of Graph and Function:**
- The graph is a time-domain waveform illustrating the input-output relationship of a Schmitt trigger.

2. **Axes Labels and Units:**
- The vertical axis represents voltage in volts. The input voltage is marked with specific thresholds at +4.76 volts (low threshold) and +5.0 volts (high threshold).
- The output voltage is indicated with two levels: 0 volts and +5 volts.
- The horizontal axis represents time, although specific units or scales are not provided.

3. **Overall Behavior and Trends:**
- The input waveform is a noisy signal fluctuating around the threshold levels. It shows random variations typical of noise.
- The output waveform is a square wave, which switches between 0 volts and +5 volts. The transitions occur when the input crosses the threshold levels.

4. **Key Features and Technical Details:**
- The Schmitt trigger's hysteresis is evident, as the output changes state only when the input crosses the specified thresholds.
- The high threshold is at +5.0 volts, and the low threshold is at +4.76 volts. This difference introduces hysteresis, preventing false triggering due to noise.
- The output remains at +5 volts when the input exceeds the high threshold and switches to 0 volts when the input drops below the low threshold.

5. **Annotations and Specific Data Points:**
- The thresholds are clearly marked on the input waveform, illustrating the hysteresis band.
- The output waveform is shown in a binary form, emphasizing the clear and rapid transitions between states, which is a characteristic of the Schmitt trigger's design to handle noisy inputs effectively.

Figure 4.33. Hysteresis tames noise-prone comparator.
image_name:Figure 4.34
description:The graph shown is a transfer function for a Schmitt trigger, illustrating the relationship between the input voltage and the output voltage. This is a piecewise linear graph with hysteresis, which is typical for a Schmitt trigger.

1. **Type of Graph and Function:**
- This is a transfer function graph, specifically for a Schmitt trigger, showing how the output voltage changes in response to the input voltage.

2. **Axes Labels and Units:**
- The horizontal axis represents the input voltage, labeled as "input," with units likely in volts. The scale is linear and ranges from below 4.0 to above 5.0 volts.
- The vertical axis represents the output voltage, labeled as "output," with units also in volts. The scale is linear and shows two discrete levels: 0 volts and +5 volts.

3. **Overall Behavior and Trends:**
- The graph displays a hysteresis loop, indicating that the output voltage depends not only on the current input voltage but also on the input voltage's history.
- As the input voltage increases past approximately 5.0 volts, the output switches from 0 volts to +5 volts.
- As the input voltage decreases past approximately 4.0 volts, the output switches from +5 volts back to 0 volts.
- This behavior creates a rectangular loop in the graph, characteristic of hysteresis.

4. **Key Features and Technical Details:**
- The key feature of this graph is the hysteresis, which provides noise immunity by requiring a significant change in input voltage to switch states, thus avoiding false triggering from noise.
- The thresholds for switching are approximately 4.0 volts for the transition from high to low output and 5.0 volts for the transition from low to high output.

5. **Annotations and Specific Data Points:**
- The graph includes arrows indicating the direction of the transitions, emphasizing the hysteresis effect.
- The clear distinction between the two output states (+5 volts and 0 volts) is marked, showing the binary nature of the output in response to varying input levels.

Figure 4.34. Output versus input ("transfer function") for Schmitt trigger.
as a Schmitt trigger, a function that we saw earlier in a discrete transistor implementation (Figure 2.13).

The output depends both on the input voltage and on its recent history, an effect called hysteresis. This can be illustrated with a diagram of output versus input, as in Figure 4.34. The design procedure is easy for Schmitt triggers that have a small amount of hysteresis. Use the circuit of Figure 4.32B. First choose a resistive divider ( $R_{1}$, $R_{2}$ ) to put the threshold at approximately the right voltage; if you want the threshold near ground, just use a single resistor from noninverting input to ground. Next, choose the (positive) feedback resistor $R_{3}$ to produce the required hysteresis, noting that the hysteresis equals the output swing, attenuated by a resistive divider formed by $R_{3}$ and $R_{1} \| R_{2}$. Finally, if you are using a comparator with "open-collector" output, you must add an output pullup resistor small enough to ensure a nearly full supply swing, taking account of the loading by $R_{3}$ (read about comparator outputs in $\S 12.3$, and see Table 12.2). For the case in which you want thresholds symmetrical about ground, connect an offsetting resistor of appropriate value from the noninverting input to the negative supply. You may wish to scale all resistor values to keep the output current and impedance levels within a reasonable range.

#### C. Power-switching driver

The output of a comparator or Schmitt trigger switches abruptly between high and low voltages; it's not a continuous (or "linear") signal. You might want to use its output to turn a substantial load on or off. Examples might be a relay, laser, or motor.
image_name:A
description:
[
name: A, type: OpAmp, ports: {InP: In1(A), InN: In2(A), OutP: Out(A), OutN: , Vdd: , -Vdd:}
name: R, type: Resistor, value: 1k, ports: {N1: Out(A), N2: base}
name: PI, type: Diode, ports: {Na: base, Nc: GND}
name: M1, type: NPN, ports: {C: +Vcc, B: base, E: GND}
]
extrainfo:This is a power-switching driver circuit using an op-amp and an NPN transistor. The op-amp output drives the base of the NPN transistor through a resistor, with a diode for reverse protection. The configuration allows for driving a load connected to Vcc.
image_name:B
description:
[
name: A1, type: OpAmp, value: A1, ports: {InP: In1(A1), InN: In2(A1), OutP: Out(A1), OutN: , Vdd: +15, -Vdd: -15}
name: M1, type: NMOS, ports: {S: GND, D: load, G: Out(A1)}
name: load, type: Resistor, ports: {N1: load, N2: +VDD}
]
extrainfo:This circuit diagram is a power-switching driver using an op-amp and an NMOS transistor. It is designed to control a load by switching it on or off using the output of the op-amp. The op-amp is powered by dual supply rails (+15V and -15V). The NMOS transistor (IRF520) acts as a switch, controlled by the op-amp output, to connect the load to ground. The load is connected between the drain of the NMOS and a positive supply voltage (+VDD).

Figure 4.35. Power switching with an op-amp; A. With bipolar npn; note base current limit and reverse protection, B. With power MOSFET; note simplified drive circuit.

For loads that are either on or off, a switching transistor can be driven from a comparator or op-amp. Figure 4.35A shows how. Note the diode to prevent reverse base-emitter breakdown (op-amps powered from dual supply rails easily swing more than the -6 V base-emitter breakdown voltage); it would be omitted if the op-amp's negative supply were no more than -5 V . The TIP3055 is a jellybean classic power transistor for noncritical high-current applications, though you'll find plenty of variety of available types with improved maximum voltage, current, power dissipation, and speed (see the listing in Table 2.2 on page 106). A Darlington can be used if currents greater than about 1 amp need to be driven.

In general, however, you're better off using an $n$-channel power MOSFET, in which case you can dispense with the resistor and diode altogether (Figure 4.35B). The IRF520 ${ }^{13}$ is a near-classic - but the variety of readily available power MOSFETs is overwhelming (see Table 3.4); in general you trade off high breakdown voltage against low ONresistance.

When switching external loads, don't forget to include a reverse diode if the load is inductive (§1.6.7).

[^25]image_name:Figure 4.36
description:
[
name: A1, type: OpAmp, value: A1, ports: {InP: Vin, InN: InN(A1), OutP: Out(A1), OutN:}
name: D1, type: Diode, ports: {Na: Out(A1), Nc: Vout}
name: R, type: Resistor, value: 10k, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit is a simple active half-wave rectifier using an op-amp and a diode. The op-amp is configured with a diode in the feedback loop to rectify the input signal. The resistor R provides a path to ground for the output.

Figure 4.36. Simple active half-wave rectifier.
image_name:Figure 4.37
description:The graph in Figure 4.37 is a time-domain waveform illustrating the effect of finite slew rate on a simple active rectifier. The graph has two main waveforms: the input signal and the op-amp output.

**Axes Labels and Units:**
- The vertical axis represents voltage, labeled from \(V_{EE}\) to \(V_{CC}\), with 0 volts marked in the middle.
- The horizontal axis represents time, although specific units are not provided, it is implied to be a continuous waveform.

**Overall Behavior and Trends:**
- The input waveform is shown as a dashed line, oscillating symmetrically around the 0-volt line, indicating an AC signal.
- The op-amp output, represented by a solid line, follows the input waveform closely when the input is positive, but deviates when the input is negative, due to the rectification process.

**Key Features and Technical Details:**
- The graph highlights the effect of the op-amp's finite slew rate on the rectification process. When the input signal is positive, the op-amp output follows it closely, but there is a noticeable delay and smoothing effect due to the slew rate limitation.
- A critical feature noted is the '1 diode drop' annotation, indicating the voltage drop across the diode when the input is positive. This is typical in diode-based rectifiers, but the op-amp compensates for this drop, allowing the output to closely follow the input.
- The op-amp output waveform is slightly smoothed compared to the input, especially at the peaks, due to the finite slew rate and the diode's presence in the feedback loop.

**Annotations and Specific Data Points:**
- The graph is annotated with 'op-amp output' and 'input' to distinguish between the two waveforms.
- The '1 diode drop' annotation is positioned at the peak of the positive cycle, indicating the voltage difference caused by the diode.

Overall, the graph demonstrates how the active rectifier circuit effectively rectifies the input signal with minimal voltage drop across the diode, but also highlights the impact of the op-amp's finite slew rate on the output waveform's fidelity.

Figure 4.37. Effect of finite slew rate on the simple active rectifier.

#### D. Active rectifier

Rectification of signals smaller than a diode drop cannot be done with a simple diode-resistor combination. As usual, op-amps come to the rescue, in this case by putting a diode in the feedback loop (Figure 4.36). For $V_{\text {in }}$ positive, the diode provides negative feedback; the circuit's output follows the input, coupled by the diode, but without a $V_{\mathrm{BE}}$ drop. For $V_{\text {in }}$ negative, the op-amp goes into negative saturation and $V_{\text {out }}$ is at ground. $R$ could be chosen smaller for lower output impedance, with the tradeoff of higher opamp output current. A better solution is to use an op-amp follower at the output, as shown, to produce very low output impedance regardless of the resistor value.

There is a problem with this circuit that becomes serious with high-speed signals. Because an op-amp cannot swing its output infinitely fast, the recovery from negative saturation (as the input waveform passes through zero from below) takes some time, during which the output is incorrect. It looks something like the curve shown in Figure 4.37. The output (heavy trace) is an accurate rectified version of the input (light trace), except for a short time interval after the input rises through zero volts. During that interval the op-amp output is racing up from saturation near $-V_{E E}$, so the circuit's output is still at ground. A general-purpose opamp like the 411 has a slew rate (maximum rate at which the output can change) of $15 \mathrm{~V} / \mu \mathrm{s}$; recovery from negative saturation therefore takes about $1 \mu \mathrm{~s}$ (when operating from $\pm 15 \mathrm{~V}$ supplies), which may introduce significant output
image_name:Figure 4.38
description:
[
name: R1, type: Resistor, value: 10k, ports: {N1: Vin, N2: InN(A1)}
name: R2, type: Resistor, value: 10k, ports: {N1: Out(A1), N2: InN(A1)}
name: D1, type: Diode, ports: {Na: Out(A1), Nc: Vout}
name: D2, type: Diode, ports: {Na: InN(A1), Nc: Out(A1)}
name: A1, type: OpAmp, value: A1, ports: {InP: GND, InN: InN(A1), OutP: Out(A1), OutN: GND}
name: A2, type: OpAmp, value: A2, ports: {InP: Vout, InN: GND, Out: Vout}
]
extrainfo:The circuit is an improved active half-wave rectifier. It uses two diodes and two op-amps to rectify the input signal. D1 and D2 control the feedback and output clamping, while A2 buffers the output.

Figure 4.38. Improved active half-wave rectifier.
error for fast signals. A circuit modification improves the situation considerably (Figure 4.38).
$D_{1}$ makes the circuit a unity-gain inverter for negative input signals. $D_{2}$ clamps the op-amp's output at one diode drop below ground for positive inputs, and since $D_{1}$ is then back-biased, $V_{\text {out }}$ sits at ground. The improvement comes because the op-amp's output swings only two diode drops as the input signal passes through zero. Because the opamp output has to slew only about 1.2 volts instead of $V_{\mathrm{EE}}$ volts, the "glitch" at zero crossings is reduced more than 10 -fold. This rectifier is inverting, incidentally. If you require a noninverted output, attach a unity-gain inverter to the output.

The performance of these circuits is improved if you choose an op-amp with a high slew rate. Slew rate also influences the performance of the other op-amp applications we've discussed, for instance the simple voltage amplifier circuits. Shortly we'll take a closer look at the ways in which real op-amps depart from the ideal - input current, offset voltage, bandwidth and slew rate, and so on - because you need to know about those limitations if you want to design good circuits. With that knowledge we'll also look at some active full-wave rectifier circuits to complement these half-wave rectifiers. ${ }^{14}$ First, though, we'd like to demonstrate some of the fun of designing with op-amps by showing a few real-world circuit examples.

### 4.3.3 Op-amp application: triangle-wave oscillator

These op-amp circuit fragments that we've been exploring - amplifiers, integrators, Schmitt triggers, etc. - are interesting enough; but the real excitement in circuit design comes when you creatively put pieces together to make a complete "something." A nice example that we can handle now is a triangle-wave oscillator. Unlike any other circuits so far, this one has no input signal; instead it creates an output signal, in this case a symmetrical triangle wave of

[^26]1 volt amplitude. As a by-product you also get a square wave, for free. (We'll see many more examples of oscillators in Chapter 7).

The idea is first to use an integrator (with a constantdc input voltage) to generate a ramp; we need to turn the ramp around when it reaches its $\pm 1 \mathrm{~V}$ limits, so we let the integrator output (the ramp) drive a Schmitt trigger, with thresholds at $\pm 1 \mathrm{~V}$. The output of the Schmitt, then, is what ought to determine the direction of the ramp. Aha! Just use its output (which switches between the supply rail voltages) as the input to the integrator.

Figure 4.39 shows a circuit implementation. It's easiest to start with $\mathrm{IC}_{2}$, which is wired as a noninverting Schmitt trigger (it looks like an inverting amplifier, but it's not note that feedback goes to the non-inverting input), for a reason we'll see soon. This configuration is used less frequently than the conventional inverting circuit of Figure 4.32B, because of its lower input impedance (and substantial input current reversal at threshold). Importantly, the LMC6482 has rail-to-rail output swing, so with $\pm 5 \mathrm{~V}$ power supplies its thresholds are at $\pm 1 \mathrm{~V}$, set by a 5:1 ratio of $R_{3}$ to $R_{2}$.
image_name:Figure 4.39
description:
[
name: R1, type: Resistor, value: 124k, ports: {N1: GND, N2: Out(A1)}
name: R2, type: Resistor, value: 2.0k, ports: {N1: Out(A1), N2: InP(A2)}
name: R3, type: Resistor, value: 10.0k, ports: {N1: Out(A2), N2: InP(A2)}
name: C1, type: Capacitor, value: 0.01µF, ports: {Np: Out(A1), Nn: InN(A1)}
name: A1, type: OpAmp, value: A1, ports: {InP: Out(A2), InN: GND, OutP: Out(A1), OutN: GND}
name: A2, type: OpAmp, value: A2, ports: {InP: Out(A1), InN: GND, OutP: Out(A2), OutN: GND}
]
extrainfo:The circuit is a triangle-wave oscillator with a frequency of 1 kHz. The output voltage swings between +1V and -1V, with a rail-to-rail output swing provided by the LMC6482 op-amps. The frequency of oscillation is determined by the formula f = 1/(4R1C1) * (R3/R2).
image_name:Triangle-wave oscillator
description:The graph displays a triangle-wave oscillator circuit, utilizing operational amplifiers configured with specific resistor and capacitor values to generate a periodic waveform. The circuit diagram includes two operational amplifiers labeled A1 and A2, both part of LMC6482 ICs, with connections to resistors and a capacitor that define the waveform characteristics.

1. **Type of Graph and Function:**
- The graph represents a time-domain waveform of a triangle-wave oscillator circuit.

2. **Axes Labels and Units:**
- The axes are not explicitly labeled in the schematic, but the waveform is shown to oscillate between +1V and -1V, indicating voltage levels over time.
- The output frequency is specified as 1 kHz, suggesting a periodic time scale of 1 ms for a full cycle.

3. **Overall Behavior and Trends:**
- The waveform is a triangle wave with linear rising and falling edges, oscillating symmetrically between +1V and -1V.
- The circuit generates a consistent triangular waveform at a frequency of 1 kHz.

4. **Key Features and Technical Details:**
- The circuit uses a feedback loop to stabilize the waveform, with feedback going to the non-inverting input of A2.
- The resistors R2 and R3 set the output voltage levels, with a ratio that defines the thresholds at ±1V.
- The capacitor C1 (0.01 µF) and resistor R1 (124kΩ) are part of the integrator circuit, determining the rate of voltage change.
- The output of A2 provides a square wave at ±5V, which is used to drive the integrator A1, creating the triangle wave.
- The frequency of the oscillator is given by the formula \( f = \frac{1}{4R_1C_1}\frac{R_3}{R_2} \), which calculates to approximately 1 kHz with the given component values.

5. **Annotations and Specific Data Points:**
- The schematic includes annotations for the component values and the expected output waveform characteristics.
- The circuit outputs are clearly marked, showing both the triangle wave and the square wave outputs, with respective voltage levels and frequency noted.

Figure 4.39. Triangle-wave oscillator.

The Schmitt's $\pm 5 \mathrm{~V}$ output is the input to the integrator $\mathrm{IC}_{1}$. We chose $C_{1}$ to be a convenient value of $0.01 \mu \mathrm{~F}$, then calculated $R_{1}$ to ramp through 2 V in a half period $(0.5 \mathrm{~ms})$, using $5 \mathrm{~V} / R_{1}=I_{\mathrm{in}}=C_{1}[d V / d t]_{\mathrm{ramp}}$. The calculated resistor value of $125 \mathrm{k} \Omega$ (in the figure we show the nearest standard 1\% "E96" resistor value; see Appendix C) came out reasonable, given real-world op-amp characteristics, as we'll learn later in the chapter. If it hadn't, we would have changed $C_{1}$; this is typically how you get to your final circuit component values.

Exercise 4.7. Confirm that value of $R_{1}$ is correct, and that the Schmitt trigger thresholds are at $\pm 1 \mathrm{~V}$.

Now the reason for connecting $\mathrm{IC}_{2}$ as a noninverting Schmitt trigger becomes clear: if $\mathrm{IC}_{2}$ 's output is at -5 V , say, then the triangle wave is ramping upward toward the Schmitt's +1 V threshold, at which point the Schmitt's output will switch to +5 V , reversing the cycle. If we had instead used the more conventional inverting Schmitt configuration, the oscillator would not oscillate; in that case it would "latch up" at one limit, as you can verify by walking through one cycle of operation.

The expressions for output frequency and amplitude are shown in the figure. It's interesting to note that the frequency is independent of supply voltage; but if you alter the resistor ratio $R_{2} / R_{3}$ to change the output amplitude, you will also change the frequency. Sometimes it is good to develop algebraic expressions for circuit operation, to see such dependencies. Here's how it goes in this case:

$$
\begin{align*}
& \frac{d V}{d t}=\frac{I}{C}=\frac{V_{\mathrm{S}} / R_{1}}{C_{1}}, \\
& \text { so } \quad \Delta t=C_{1} \frac{R_{1}}{V_{\mathrm{S}}} \Delta V, \\
& \text { but } \Delta V=2 \frac{R_{2}}{R_{3}} V_{S} \text {, } \\
& \text { so } \quad \Delta t=2 C_{1} R_{1} \frac{R_{2}}{R_{3}}, \\
& \text { and so, finally, } \quad f=\frac{1}{2 \Delta t}=\frac{1}{4 R_{1} C_{1}} \frac{R_{3}}{R_{2}} \text {. } \tag{4.4}
\end{align*}
$$

Note how $V_{\mathrm{s}}$ cancelled in the fourth step, leading to an output frequency independent of supply voltage.

A warning: it's easy to be dazzled by the apparent power of mathematics and quickly to fall in love with "algebraic circuit design." Our stern advice in this matter (and you can quote us on it) is:

Resist the temptation to take refuge in equations as a substitute for understanding how a circuit really works.

### 4.3.4 Op-amp application: pinch-off voltage tester

Here's another nice application of op-amps: suppose you want to measure a batch of JFETs in order to put them into groups that are matched in pinch-off voltage $V_{\mathrm{GS}}$ (off) (sometimes called $V_{P}$, see $\S 3.1 .3$ ). This is useful because the large spread of specified $V_{\mathrm{P}}$ sometimes makes it difficult to design a good amplifier. ${ }^{15}$ We'll assume that you want to find the gate-source back-bias that results in a drain

[^27]image_name:Figure 4.40
description:
[
name: A1, type: OpAmp, value: A1, ports: {InP: GND, InN: Out(A1), OutP: Out(A1), OutN: , Vdd: V+, -Vdd: V-}
name: R1, type: Resistor, value: 100k, ports: {N1: Out(A1), N2: DUT_D}
name: C1, type: Capacitor, value: 100pF, ports: {Np: Out(A1), Nn: InN(A1)}
name: R2, type: Resistor, value: 10M, ports: {N1: InN(A1), N2: V-}
name: DUT, type: NMOS, ports: {S: GND, D: V+, G: DUT_D}
]
extrainfo:The circuit is a pinch-off voltage tester for n-channel JFETs. It uses an op-amp (LF411) to maintain a constant drain current of 1 μA for the JFET under test, with the drain at +10 V and the source grounded. The gate-source voltage at this condition is the pinch-off voltage.

Figure 4.40. Simple pinch-off voltage tester.
current of $1 \mu \mathrm{~A}$ with the drain at +10 V and the source grounded.

If you didn't know about op-amps, you could imagine (a) grounding the source, (b) hooking up a sensitive current meter from the drain to $\mathrm{a}+10 \mathrm{~V}$ supply, and then (c) adjusting the gate voltage with a variable negative supply to a value that produces $1 \mu \mathrm{~A}$ of measured drain current.

Figure 4.40 shows a better way. The device under test (you'll often see the acronym DUT) has its drain tied to +10 V ; but the source lead, instead of being grounded, is tied to the inverting input (virtual ground) of an op-amp whose noninverting input is grounded. The op-amp controls the gate voltage, thus holding the source at ground. Because the source is pulled down to -10 V through a 10 M resistor, the source current (and therefore the drain current) is $1 \mu \mathrm{~A}$. The op-amp's output is the same as the gate voltage, so the output of this circuit is the pinch-off voltage you wanted to know.

A few details:

- We chose power supply voltages of $\pm 10 \mathrm{~V}$ for the op-amp to make the rest of the circuit simpler, since we wanted to measure $V_{\mathrm{P}}$ with +10 V on the drain. That's OK , because most op-amps work well over a range of supply voltages (in fact, the trend is toward lower operating voltages, driven by the market for battery-powered consumer devices). But if you have only $\pm 15 \mathrm{~V}$ available, you would have to generate +10 V within your circuit, either with a voltage divider, a zener, or a 3-terminal voltage regulator (see Chapter 9).
- We put a 100 k resistor $\left(R_{1}\right)$ as protection in series with the gate to prevent any significant gate current from flowing during plug-in transients, etc. This can introduce a lagging phase shift around the loop at high frequencies (as can the rather large pull-down resistor $R_{2}$ ), so we added a small feedback capacitor $C_{1}$ to maintain stability.

We talk about this business of stability toward the end of the chapter, in §4.9.

- For this circuit to work properly, it's important that the op-amp's inverting input not load the source terminal, for example by drawing anything approaching a microamp of current. As we'll learn shortly, this is not always the case. For this example our general-purpose 411 op-amp, with its JFET input transistors, is fine (with input currents in the picoamperes); but an op-amp that uses bipolar transistors for its input stage would generally have input currents in the 10's to 100's of nanoamps, and should be avoided for a low-current application like this.
- The drain current at which pinch-off voltage is specified is not always $1 \mu \mathrm{~A}$. You'll see $V_{\mathrm{GS}(\text { off })}$ specified at values of drain current ranging from 1 nA to tens of microamps, depending on the size of the JFET, and the whim of the manufacturer. (In an informal survey of datasheets we found 1 nA to be the most popular, followed by $1 \mu \mathrm{~A}$, 10 nA , and 0.5 nA , with five other values used occasionally.) It would be easy to modify the circuit to accommodate higher test currents; but to go to 10 nA , say, you would need a $1 \mathrm{G} \Omega$ resistor for $R_{2}$ ! In that case a better solution is to return the pull-down resistor to a lower voltage, say -0.1 V , which you could generate with a voltage divider from the -10 V negative supply. You'd have to worry again about op-amp input currents with such a small test current.
Exercise 4.8. Show how to make the pinch-off tester operate from $\pm 15 \mathrm{~V}$ supplies, with the measurement still made at $V_{\mathrm{D}}=+10 \mathrm{~V}$; assume that the largest resistor value available is $10 \mathrm{M} \Omega$.

Exercise 4.9. Modify the pinch-off tester circuit of Figure 4.40 so that you can measure $V_{\mathrm{GS}}$ at three values of drain current, namely $1 \mu \mathrm{~A}, 10 \mu \mathrm{~A}$, and $100 \mu \mathrm{~A}$, by setting a 3-position switch. Assume that the largest resistor value you can conveniently get is $10 \mathrm{M} \Omega$.

Exercise 4.10. Now change the circuit so that it measures $V_{\mathrm{GS}(\mathrm{off})}$ at $I_{\mathrm{D}}=1 \mathrm{nA}$. Assume you can get $100 \mathrm{M} \Omega 5 \%$ resistors.

### 4.3.5 Programmable pulse-width generator

When triggered by a short input pulse, the circuit in Figure 4.41 generates an output pulse ${ }^{16}$ whose width is set by 10-turn pot $R_{1}$. Here's how it works.
$\mathrm{IC}_{1}, \mathrm{IC}_{2}$, and $Q_{1}$ form a current source that charges timing capacitor $C$, as we'll detail below. $\mathrm{IC}_{3}$ is a versatile timer IC, whose many exploits we will enjoy in Chapter 7. It holds $C$ discharged (through a saturated MOSFET

[^28]switch whose drain drives the DIS pin to ground) and simultaneously holds the output at ground, until it receives a negative-going trigger pulse at its TRIG input pin; at that point it releases DIS and switches its output to $V_{+}$, in this case +5 V .

The current source now charges $C$ with a positive-going ramp, according to $I=C d V / d t$. This continues until the capacitor voltage, which also drives $\mathrm{IC}_{3}$ 's TH input, reaches a voltage equal to $2 / 3$ of the supply voltage, $V_{\mathrm{TH}}=\frac{2}{3} V_{+}$; at this point $\mathrm{IC}_{3}$ abruptly pulls DIS back to ground, simultaneously switching its output to ground. This completes the cycle.

The current source is an elegant circuit. We want to source a current into the capacitor, with compliance from ground to at least $+3.3 \mathrm{~V}(2 / 3$ of $+5 \mathrm{~V})$, with linear control by a pot that returns to ground. For reasons we'll see presently, we want the programmed current proportional to the supply voltage $V_{+}$. In this circuit $Q_{1}$ is the current source, with $\mathrm{IC}_{2}$ controlling its base to hold its emitter at $+5 \mathrm{~V} . \mathrm{IC}_{1}$ is an inverting amplifier referenced to +5 V ; it pivots its output to a voltage that exceeds +5 V by an amount proportional to the current flowing through $R_{1}$ and $R_{2}$. That excess voltage appears across $R$, generating the output current. You'll know you understand how it works by doing the following problem.

Exercise 4.11. Calculate the current sourced by $Q_{1}$ by calculating the output voltage of IC ${ }_{1}$ as a function of $R_{\mathrm{X}}$ (the sum of $R_{1}$ and $R_{2}$ ), $R_{3}$, and $V_{+}$. Now use it to calculate the output pulse width, knowing that $\mathrm{IC}_{3}$ switches when the voltage at TH reaches $\frac{2}{3} V_{+}$.

This circuit is an illustration of the use of ratiometric techniques: for a given setting of $R_{1}$, both the capacitor charging current $I$ and the timer IC threshold voltage $V_{\mathrm{TH}}$ individually depend on supply voltage $V_{+}$; but their variation is such that the final pulse width $T$ does not depend on $V_{+}$. That is why the current source was designed with $I \propto V_{+}$. The use of ratiometric techniques is an elegant way to design circuits with excellent performance, often without requiring precise control of power-supply voltages.

### 4.3.6 Active lowpass filter

The simple $R C$ filters we saw back in Chapter 1 have a soft rolloff; that is, their response versus frequency does not progress sharply from a passband to a stopband. Perhaps surprisingly, this behavior cannot be remedied by simply cascading multiple stages, as we'll see in detail in Chapter 6 (and particularly in connection with active filters, §6.3). Much better filter performance can be achieved if
image_name:Figure 4.41. Pulse generator with programmable width.
description:
[
name: R1, type: Resistor, value: 10k, ports: {N1: GND, N2: Rx}
name: R2, type: Resistor, value: 1.0k, ports: {N1: Rx, N2: IC1_InN}
name: R3, type: Resistor, value: 1.0k, ports: {N1: IC1_Out, N2: IC1_InN}
name: R, type: Resistor, value: 15k, ports: {N1: IC1_Out, N2: Q1_C}
name: C, type: Capacitor, value: 0.1μF, ports: {Np: IC3_6, Nn: GND}
name: IC1, type: OpAmp, value: IC1, ports: {InP: V+, InN: IC1_InN, OutP: IC1_Out, OutN: , Vdd: , -Vdd:}
name: IC2, type: OpAmp, value: IC2, ports: {InP: IC1_Out, InN: trig_in, OutP: Q1_B, OutN: , Vdd: , -Vdd:}
name: IC3, type: Other, ports: {N1: IC3_2, N2: IC3_6, N3: IC3_3, N4: IC3_7, N5: IC3_8, N6: V+, N7: GND, N8: IC3_4}
name: Q1, type: NPN, ports: {C: Q1_C, B: Q1_B, E: GND}
]
extrainfo:The circuit is a pulse generator with programmable width, using op-amps and a 555 timer IC. The pulse width is determined by the equation T = (2/3) * RC * (Rx/R3), where Rx can vary between 1k to 11k, resulting in a pulse width range of 1ms to 11ms.

Figure 4.41. Pulse generator with programmable width.
you include both inductors and capacitors, or, equivalently, if you "activate" the filter design by using op-amps.

Figure 4.42 shows an example of a simple and even partly intuitive filter. This configuration is known as a Sallen-and-Key filter, after its inventors. The unity-gain amplifier can be an op-amp connected as a follower, or a unity-gain buffer IC, or just an emitter follower. This particular filter is a second-order lowpass filter. Note that it would be simply a pair of cascaded passive $R C$ lowpass filters, except for the fact that the bottom of the first capacitor is bootstrapped by the output. It is easy to see that at high frequencies (well beyond $f=1 / 2 \pi R C$ ) it falls off just like a cascaded $R C$, i.e., at $-12 \mathrm{~dB} /$ octave, because the output is essentially zero (and therefore the first capacitor's lower end is effectively grounded). As we lower the frequency and approach the passband, however, the bootstrap action tends to reduce the attenuation, thus giving a sharper "knee" to the curve of response versus frequency. We've plotted the response versus frequency, with three "tunings" of the $R$ and $C$ values. ${ }^{17}$

Of course, such hand-waving cannot substitute for honest analysis, which luckily has been done for a prodigious variety of nice filters. And contemporary generalpurpose SPICE-based analog simulation tools, or special filter analysis software, let you design and view filter response curves with relative ease.

[^29]image_name:A
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: input, N2: X1}
name: R2, type: Resistor, value: R2, ports: {N1: X1, N2: InP}
name: C1, type: Capacitor, value: C1, ports: {Np: X1, Nn: GND}
name: C2, type: Capacitor, value: C2, ports: {Np: InP, Nn: GND}
name: A1, type: OpAmp, value: A1, ports: {InP: InP, InN: InN, OutP: output}
]
extrainfo:This is a Sallen-and-Key active lowpass filter. The diagram shows a comparison of its frequency response with a cascade of two passive RC sections.
image_name:B
description:The graph labeled 'B' is a frequency response plot comparing a Sallen-and-Key active lowpass filter with a cascade of two passive RC sections.

1. **Type of Graph and Function:**
- The graph is a Bode plot, showing the gain of the filter as a function of frequency.

2. **Axes Labels and Units:**
- The x-axis represents frequency in hertz (Hz), and it is plotted on a logarithmic scale ranging from 10 Hz to 10 kHz.
- The y-axis represents gain in linear scale, ranging from 0.0 to 1.0.

3. **Overall Behavior and Trends:**
- The gain remains constant at 1.0 for low frequencies, indicating a flat response.
- As frequency increases, the gain begins to drop sharply, showing the lowpass filter behavior.
- The Sallen-and-Key filter shows a sharper roll-off compared to the passive RC sections.
- The knee of the curve, where the gain starts to decrease significantly, occurs around 1 kHz.

4. **Key Features and Technical Details:**
- The Sallen-and-Key filter provides a steeper roll-off, which is evident in the sharper decline in gain compared to the dashed line representing the two RC sections.
- The plot highlights the superior performance of the active filter in terms of selectivity and cutoff characteristics.

5. **Annotations and Specific Data Points:**
- The plot includes annotations indicating the comparison between the 'Sallen and Key' and '2 RC’s'.
- The Sallen-and-Key filter's sharper decline is highlighted with a solid line, while the two RC sections are represented by a dashed line.
- The significant change in gain around the 1 kHz mark is a critical point of interest, emphasizing the cutoff frequency.

Figure 4.42. Sallen-and-Key active lowpass filter: A. Schematic; B. frequency response, compared with a cascade of two passive $R C$ sections.

## 4.4 A detailed look at op-amp behavior

We've hinted that op-amps aren't perfect, and that the performance of circuits such as active rectifiers and Schmitt triggers is limited by op-amp speed, or "slew rate." For those applications a high-speed op-amp is often required.

But slew rate is just one of a half-dozen important parameters of op-amps, which include input offset voltage, input bias current, input common-mode range, noise, bandwidth, output swing, and supply voltage and current. To state the situation fairly, op-amps are remarkable devices, with nearideal performance for most applications you are likely to encounter. To put it quantitatively, think of the difficulty of designing, with discrete transistors and other components, a high-gain dc differential amplifier that has an input current less than a picoamp, an offset from perfect balance less than a millivolt, a bandwidth of several megahertz, and that operates with its inputs anywhere between the two supply voltages. You can get such an op-amp for a dollar; it comes in a tiny package measuring $1.5 \mathrm{~mm} \times 3 \mathrm{~mm}$, and it draws less than a milliamp.

But op-amps do have performance limitations - that's why there are literally thousands of available types - and in general you're faced with a tradeoff: you can get much lower bias current (for example), at the expense of offset voltage. A good understanding of op-amp limitations and their influence on circuit design and performance will help you choose your op-amps wisely and design with them effectively.

To motivate the subject, imagine that you've been asked to design a dc amplifier, so that small voltages $(0-10 \mathrm{mV})$ can be seen on a handsome analog meter scale. And it should have at least $10 \mathrm{M} \Omega$ input resistance, and be accurate to $1 \%$ or so. No problem, you say...I'll just use the non-inverting amplifier configuration (to get high input resistance), with lots of gain ( $\times 1000$, say, so 10 mV is amplified to 10 V ). Speed is not an issue, so you don't worry about slew rate. With supreme confidence you draw up the circuit (with an LF411 op-amp), your technician builds it, and $\ldots$ your boss fires you! The thing was a disaster: it read $20 \%$ of full-scale with no input attached, and it drifted like crazy when carried outside. It does work OK - as a paperweight. ${ }^{18}$

To get started, look at Figure 4.43, a simplified schematic of the LF411. Its circuit is relatively straightforward, in terms of the kinds of transistor circuits we discussed in the last two chapters. It has a JFET differential input stage, with current-mirror active load, buffered with an npn follower (to prevent loading of the high-gain input stage) driving a grounded-emitter npn stage (with currentsource active load). This drives the push-pull emitter follower output stage ( $Q_{7} Q_{8}$ ), with current-limiting circuitry

[^30]( $R_{5} Q_{9}$ and $R_{6} Q_{10}$ ) to protect against output short-circuit. ${ }^{19}$ The curious feedback capacitor $C_{\mathrm{C}}$ ensures stability; we'll learn about it later. This circuit displays the internal circuitry characteristic of the typical op-amp, and from it we can see how and why op-amp performance departs from ideal.

Exercise 4.12. Explain how the current-limiting circuitry in Figure 4.43 works. What is the maximum output current?

Exercise 4.13. Explain the function of the two diodes in the output stage.

Let's look at these problems, what the consequences are for circuit design, and what to do about it.
image_name:Figure 4.43
description:
[
name: Q1, type: PNP, ports: {C: input-, B: 150µA, E: GND}
name: Q2, type: PNP, ports: {C: input+, B: 150µA, E: GND}
name: Q3, type: NPN, ports: {C: GND, B: input-, E: R1-R2}
name: Q4, type: NPN, ports: {C: GND, B: input+, E: R3-R4}
name: Q5, type: NPN, ports: {C: CC, B: GND, E: R1-R2}
name: Q6, type: NPN, ports: {C: CC, B: GND, E: R3-R4}
name: Q7, type: NPN, ports: {C: +VCC, B: out, E: R5}
name: Q8, type: PNP, ports: {C: R6, B: out, E: -VEE}
name: Q9, type: NPN, ports: {C: +VCC, B: out, E: R5}
name: Q10, type: PNP, ports: {C: R6, B: out, E: -VEE}
name: R1, type: Resistor, value: 2k, ports: {N1: input-, N2: offset trim}
name: R2, type: Resistor, value: 2k, ports: {N1: offset trim, N2: GND}
name: R3, type: Resistor, value: 20k, ports: {N1: input+, N2: offset trim}
name: R4, type: Resistor, value: 20k, ports: {N1: offset trim, N2: GND}
name: R5, type: Resistor, value: 22Ω, ports: {N1: out, N2: -VEE}
name: R6, type: Resistor, value: 22Ω, ports: {N1: out, N2: -VEE}
name: CC, type: Capacitor, value: CC, ports: {Np: CC, Nn: GND}
name: 150µA, type: CurrentSource, value: 150µA, ports: {Np: +VCC, Nn: GND}
name: 150µA, type: CurrentSource, value: 150µA, ports: {Np: +VCC, Nn: GND}
]
extrainfo:The circuit is a simplified schematic of the LF411 op-amp, illustrating the internal structure and current-limiting features. It includes multiple transistors, resistors, and current sources, which contribute to the op-amp's non-ideal performance characteristics. The diodes in the output stage are likely used for protection or biasing.

Figure 4.43. Simplified schematic of the LF411 op-amp.

### 4.4.1 Departure from ideal op-amp performance

The ideal op-amp has these characteristics:

- Input current $=0$ (input impedance $=\infty$ ).
- $V_{\text {out }}=0$ when both inputs are at precisely the same voltage (zero "offset voltage").
- Output impedance $($ open loop $)=0$.
- Voltage gain $=\infty$.
- Common-mode voltage gain $=0$.

19 The LF411's detailed schematic reveals a more elaborate negative current-limit configuration; check it out on the datasheet, to see if you can understand how it works.

- Output can change instantaneously (infinite slew rate).
$\cdot$ Absence of added "noise."
All of these characteristics should be independent of temperature and supply voltage changes.

In the following paragraphs we describe how real opamps depart from these ideals. As you struggle through the fact-filled sections, you may want to refer to Table 4.1 to maintain perspective. Tables $4.2 \mathrm{a}, \mathrm{b}, 5.5$, and 8.3 may be helpful also, for seeing some actual numbers. And we'll revisit these in more detail in Chapter 5 ( $\S 5.7$ and 5.8) in connection with the design of precision circuits.

#### A. Input offset voltage

Op-amps don't have perfectly balanced input stages, owing to manufacturing variations. The problem is worse with FETs, with their poorer matching of input thresholds. If you connect the two op-amp inputs together to create exactly zero differential input signal, the output will usually saturate at either $V_{+}$or $V_{-}$(you can't predict which). The difference in input voltages necessary to bring the output to zero is called the input offset voltage, $V_{\mathrm{OS}}$ (it's as if there were a battery of that voltage in series with one of the inputs). Typical offset voltages are around 1 mV , but "precision" op-amps can have offset voltages as small as $10 \mu \mathrm{~V}$. Some op-amps make provision for trimming the input offset voltage to zero. For a 411 you attach a 10k pot between pins 1 and 5 ("offset trim" in Figure 4.43), with the wiper connected to $V_{\mathrm{EE}}$, and adjust for zero offset; the effect is to unbalance deliberately the current mirror to compensate for the offset.

#### B. Offset voltage drift

Of greater importance for precision applications is the drift of the input offset voltage with temperature and time, since any initial offset could be manually trimmed to zero. A 411 has a typical offset voltage of 0.8 mV ( 2 mV maximum), with a tempco of $\Delta V_{\mathrm{OS}} / \Delta T=7 \mu \mathrm{~V} /{ }^{\circ} \mathrm{C}$ and unspecified coefficient of offset drift with time. The OP177A, a precision op-amp, is laser-trimmed for a maximum offset of 10 mi crovolts, with a temperature coefficient of $0.1 \mu \mathrm{~V} /{ }^{\circ} \mathrm{C}(\max )$ and long-term drift of $0.2 \mu \mathrm{~V} /$ month (typical) - roughly a hundred times better in both offset and tempco.

#### C. Input current

The input terminals sink (or source, depending on the opamp type) a small current called the input bias current, $I_{\mathrm{B}}$, which is defined as half the sum of the input currents with the inputs tied together (the two input currents are approximately equal and are simply the base or gate currents of
the input transistors). For the JFET-input 411 the bias current is typically $50 \mathrm{pA}(200 \mathrm{pA} \max )$ at room temperature (but as much as 4 nA at $70^{\circ} \mathrm{C}$ ), while a typical BJT-input op-amp like the OP27 has a bias current of 15 nA , varying little with temperature. As a rough guide, BJT-input opamps have bias currents in the tens of nanoamps, whereas JFET-input op-amps have input currents in the tens of picoamps (i.e., 1000 times lower), and MOSFET-input opamps have input currents of typically a picoamp or less. Generally speaking, you can ignore input current with FET op-amps, but not with bipolar-input op-amps. ${ }^{20}$

The significance of input bias current is that it causes a voltage drop across the resistors of the feedback network, bias network, or source impedance. How small a resistor this restricts you to depends on the dc gain of your circuit and how much output variation you can tolerate. For example, an LF412's maximum input current of 200 pA means that you can tolerate resistances (seen from the input terminals) up to $\sim 5 \mathrm{M} \Omega$ before you have to worry about it at the 1 mV level.

We will see more about how this works later. If your circuit is an integrator, bias current produces a slow ramp even when there is no external input current to the integrator.

Op-amps are available with input bias currents down to a nanoamp or less for bipolar-transistor-input circuit types, or down to a fraction of a picoamp $\left(10^{-6} \mu \mathrm{~A}\right)$ for MOSFET-input circuit types. The very lowest bias currents are typified by the BJT-input LT1012, with a typical input current of 25 pA , the JFET-input OPA129, with an input current of 0.03 pA , and the MOSFET LMC6041, with an input current of 0.002 pA . At the other end, very fast BJT op-amps like the THS4011/21 ( $\sim 300 \mathrm{MHz}$ ) have input currents of $3 \mu \mathrm{~A}$. In general, BJT op-amps intended for highspeed operation have higher bias currents.

#### D. Input offset current

Input offset current is a fancy name for the difference of the input currents between the two inputs. Unlike input bias current, the offset current, $I_{\mathrm{OS}}$, is a result of manufacturing variations, since an op-amp's symmetrical input circuit would otherwise result in identical bias currents at the two inputs. The significance is that, even when it is driven by identical source impedances, the op-amp will see unequal voltage drops and hence a difference voltage between its inputs. You will see shortly how this influences design.

Typically, the offset current is somewhere between one-

[^31]Table 4.1 Op-amp Parameters ${ }^{a}$

| Parameter | bipolar (BJT) |  | JFET-input |  | cMOS |  | Units |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
|  | jellybean | premium | jellybean | premium | jellybean | premium |  |
| $V_{\text {os }}$ (max) | 3 | 0.025 | 2 | 0.1 | 2 | 0.1 | mV |
| TCV ${ }_{\text {os }}$ (max) | 5 | 0.1 | 20 | 1 | 10 | 3 | $\mu \mathrm{V} /{ }^{\circ} \mathrm{C}$ |
| image_name:I_B (typ)
description:The image shows the text 'I_B (typ)', which refers to the typical input bias current for an operational amplifier (op-amp). This parameter is part of a table comparing various op-amp parameters across different technologies such as bipolar (BJT), JFET-input, and CMOS. The table lists the typical input bias current values for jellybean and premium versions of each technology, measured at 25 degrees Celsius. The values are 50nA for bipolar jellybean, 25pA for bipolar premium, 50pA for JFET-input jellybean, 40fA for JFET-input premium, 1pA for CMOS jellybean, and 2fA for CMOS premium.
| 50nA | 25pA | 50pA | 40fA | 1pA | 2fA | @ $25^{\circ} \mathrm{C}$ |
| en (typ) | 10 | 1 | 20 | 3 | 30 | 7 | nV/VHz @ 1kHz |
| $f_{\text {T }}$ (typ) | 2 | 2000 | 5 | 400 | 2 | 10 | MHz |
| SR (typ) | 2 | 4000 | 15 | 300 | 5 | 10 | V/us |
| $V_{\text {S }}(\mathrm{min})^{\mathrm{b}}$ | 5 | 1.5 | 10 | 5 | 2 | 1 | V |
| $V_{\text {s }}(\max )^{\text {b }}$ | 36 | 44 | 36 | 36 | 15 | 15 | V |

Notes: (a) typical and "best" values of important op-amp performance parameters. (b) total supply: $V_{+}-V_{-}$.
Typical and "best" values of important op-amp performance parameters. In this chart we list values for run-of-the-mill ("jellybean") parts, and for the best op-amp you can get for each individual parameter. That is, you cannot get a single op-amp that has the combination of excellent performance shown in any of the "premium" columns. In this chart you can clearly see that bipolar op-amps excel in precision, stability, speed, wide supply voltage range, and noise, at the expense of bias current; JFET-input types are intermediate, with CMOS op-amps displaying the lowest bias current.
half and one-tenth the bias current. For the 411, $I_{\text {offset }}=$ 25 pA , typical. However, for bias-compensated op-amps (like the OPA177), the specified offset current and bias current are comparable, for reasons we'll see in the advanced Chapter 5.

#### E. Input impedance

Input impedance refers to the small-signal ${ }^{21}$ differential input resistance (impedance looking into one input, with the other input grounded), which is usually much less than the common-mode resistance (a typical input stage looks like a long-tailed pair with current source). For the FET-input 411 it is about $10^{12} \Omega$, whereas for BJT-input op-amps like the LT1013 it is about $300 \mathrm{M} \Omega$. Because of the input bootstrapping effect of negative feedback (it attempts to keep both inputs at the same voltage, thus eliminating most of the differential-input signal), $Z_{\text {in }}$ in practice is raised to very high values and usually is not as important a parameter as input bias current.

#### F. Common-mode input range

The inputs to an op-amp must stay within a certain voltage range, typically less than the full supply range, for proper operation. If the inputs go beyond this range, the gain of the op-amp may change drastically, even reversing sign! For a 411 operating from $\pm 15$ volt supplies, the guaranteed common-mode input range is $\pm 11$ volts minimum.

[^32]However, the manufacturer claims that the 411 will operate with common-mode inputs all the way to the positive supply, though performance may be degraded. Bringing either input down to the negative supply voltage causes the amplifier to go berserk, with symptoms like phase reversal ${ }^{22}$ and output saturation to the positive supply. From the circuit in Figure 4.43 you can see why the LF411 cannot possibly operate with input voltages to the negative rail, because that would put the source terminals of the input JFET pair below the negative rail, taking them out of the active region. This is discussed further in Chapter $4 x$, along with some good war stories.

There are many op-amps available with common-mode input ranges down to the negative supply, e.g., the bipolar LT1013 and the CMOS TLC2272 and LMC6082; these are often referred to as "single-supply op-amps" or "groundsensing op-amps" (see §4.6.3). There are also some opamps whose common-mode input range includes the positive supply, e.g., the JFET LF356. With the trend toward lower supply voltages for battery-powered equipment, opamp designers have come up with varieties that accommodate input signals over the full range between supply voltages; these are called rail-to-rail, because supply voltages

[^33]are often called supply rails. ${ }^{23}$ Examples are the CMOS LMC6482 and TLV2400 series, and the bipolar LM6132, LT1630, and LT6220 series. These have the additional nice feature of being able to swing their outputs all the way to the rails (see the subsection on output swing below). These would seem to be ideal op-amps; however, as we discuss in $\S \S 5.7,5.9$, and 5.10 , rail-to-rail op-amps typically make compromises that affect other characteristics, notably offset voltage, output impedance, and supply current. There are, in addition, a few (very few) op-amps that operate properly for input voltages above the positive rail (for example, the "over-the-top" LT1637, listed in Table 4.2a on page 271).

In addition to the operating common-mode range, there are maximum allowable input voltages beyond which damage will result. For the 411 they are $\pm 15$ volts (but not to exceed the negative supply voltage, if it is less).

#### G. Differential input range

Some bipolar op-amps allow only a limited voltage between the inputs, sometimes as small as $\pm 0.5$ volt, although most are more forgiving, permitting differential inputs nearly as large as the supply voltages. Exceeding the specified maximum can degrade or destroy the op-amp.

#### H. Output swing versus load resistance

The LF411, typical of many op-amps, cannot swing its output closer than a volt or two from either supply rail, even when lightly loaded ( $R_{L}>5 \mathrm{k}$, say). That's because the output stage is a push-pull emitter follower, so even a full rail-to-rail drive to its bases would leave the output a diode drop short of both rails; the drive circuitry has its own difficulties getting close to the rails as well, and the currentlimit sense resistors $R_{5}$ and $R_{6}$ impose an additional voltage drop, which accounts for the shortfall.

For low values of load resistance, the internal currentlimit circuit will set the maximum swing. For example, the 411 can swing its output to within about 2 volts of $V_{\mathrm{CC}}$ and $V_{\text {EE }}$ into load resistances greater than about 1 k . Load resistances significantly less than that will permit only a small swing. This is frequently shown on datasheets as a graph of peak-to-peak output voltage swing $V_{\mathrm{om}}$ as a function of

[^34]image_name:Figure 4.44
description:Figure 4.44 depicts a graph illustrating the relationship between the peak-to-peak output swing (Vpp) and the load resistance for an LF411 operational amplifier, with a supply voltage of ±15V. The graph is a plot with logarithmic scaling on the horizontal axis and linear scaling on the vertical axis.

1. **Type of Graph and Function:**
- The graph is a plot of peak-to-peak output voltage swing versus load resistance.
- It shows how the output swing changes with varying load resistance for the LF411 op-amp.

2. **Axes Labels and Units:**
- The horizontal axis represents the Load Resistance, measured in kilo-ohms (kΩ), with a logarithmic scale ranging from 0.1 kΩ to 10 kΩ.
- The vertical axis represents the Peak-to-Peak Output Swing, measured in volts (Vpp), with a linear scale ranging from 0 to 30 volts.

3. **Overall Behavior and Trends:**
- The graph shows a rapidly increasing trend at low load resistances, which gradually levels off as the resistance increases.
- For very low load resistances (below 1 kΩ), the peak-to-peak output swing is limited and starts at around 5 Vpp.
- As the load resistance increases, the output swing increases sharply and then begins to plateau, approaching a maximum value just below 30 Vpp.

4. **Key Features and Technical Details:**
- The curve exhibits a saturation behavior, where the output swing is significantly limited at lower resistances but stabilizes at higher resistances.
- The maximum output swing achievable is close to 30 Vpp for load resistances greater than approximately 3 kΩ.

5. **Annotations and Specific Data Points:**
- The graph includes an annotation indicating the op-amp model (LF411) and the supply voltage (Vs = ±15V).
- There are no specific data points or markers highlighted on the graph, but the trend is clear and well-defined.

Figure 4.44. Maximum peak-to-peak output swing versus load (LF411).
load resistance, or sometimes just a few values for typical load resistances. Figure 4.44 shows the datasheet's graph for the LF411. Many op-amps have asymmetrical output drive capability, with the ability to sink more current than they can source (or vice versa). For that reason you often see maximum output swing plotted, versus load current, as separate curves for output sourcing and sinking current into a load. Figure 4.45 shows such graphs for the LF411.

Some op-amps can produce output swings all the way down to the negative supply (e.g., the bipolar LT1013 and CMOS TLC2272), a particularly useful feature for circuits operated from a single positive supply, because output swings all the way to ground are then possible. Finally, opamps with CMOS transistor outputs in a common-source amplifier configuration ${ }^{24}$ (e.g., the LMC6xxx series) can swing all the way to both rails. For such op-amps a much more useful graph plots how close the output can get to each power-supply rail as a function of load current (both sourcing and sinking). An example is shown in Figure 4.46 for the CMOS rail-to-rail LMC6041. Note the effective use of log-log axes, so you can read off accurately the fact that this op-amp can swing to within 1 mV of the rails when supplying $10 \mu \mathrm{~A}$ of output current, and that its output resistance is approximately $80 \Omega$ (sinking) and $100 \Omega$ (sourcing). You can find bipolar op-amps that share this property, without the limited supply voltage range of the CMOS opamps (usually $\pm 8 \mathrm{~V}$ max), for example, the LM6132/42/52 family and the LT1636/7.

#### I. Output Impedance

Output impedance $R_{\mathrm{o}}$ means the op-amp's intrinsic output impedance without feedback (see Figure 2.90). For the 411 it is about $40 \Omega$, but with some low-power op-amps it can

[^35]image_name:Figure 4.45
description:The graph in Figure 4.45 is a plot showing the maximum output voltage (in volts) versus the output current (in milliamperes) for an LF411 operational amplifier. The graph is a line chart with two curves, representing the positive (sourcing) and negative (sinking) output capabilities of the op-amp.

1. **Type of Graph and Function:**
- This is a line graph depicting the relationship between output voltage and output current.

2. **Axes Labels and Units:**
- The x-axis is labeled "Output Current (±mA)" and ranges from 0 to 30 milliamperes.
- The y-axis is labeled "Maximum Output Voltage (±V)" and ranges from 0 to 15 volts.

3. **Overall Behavior and Trends:**
- Both curves start at around 15 volts when the output current is near zero.
- As the output current increases, the maximum output voltage decreases.
- The decrease is gradual until about 20 mA, where the rate of voltage drop increases sharply.

4. **Key Features and Technical Details:**
- The curves indicate the op-amp's ability to supply (source) or absorb (sink) current while maintaining a certain output voltage.
- The graph shows that the op-amp can maintain a higher voltage at lower currents, but as the current approaches 20 mA, the voltage capability significantly drops.
- The positive sourcing curve is slightly higher than the negative sinking curve, suggesting better performance in sourcing current.

5. **Annotations and Specific Data Points:**
- The graph includes annotations for the LF411 op-amp, with supply voltage \( V_S = \pm 15V \) and junction temperature \( T_J = 25^{\circ}C \).
- The curves are labeled "positive (sourcing)" and "negative (sinking)" to differentiate between the two modes of operation.

Figure 4.45. Maximum output voltage (both sourcing and sinking) versus load current (LF411). The maximum output current capability decreases by $\sim 25 \%$ at $T_{\mathrm{J}}=125^{\circ} \mathrm{C}$.
image_name:Figure 4.46
description:Figure 4.46 illustrates the maximum swing (ΔV from the respective rails) versus load current for a CMOS rail-to-rail output operational amplifier (op-amp). The graph is a logarithmic plot with both axes using a logarithmic scale.

**Axes Labels and Units:**
- The x-axis represents the output current in milliamperes (mA), ranging from 0.001 mA to 100 mA.
- The y-axis represents the voltage swing from the rail (ΔV) in volts (V), ranging from 0.0001 V to 10 V.

**Overall Behavior and Trends:**
- The graph features two primary curves: a solid curve for negative (sinking) current and a dashed curve for positive (sourcing) current.
- Both curves demonstrate an increasing trend, indicating that as the load current increases, the voltage swing from the rail also increases.

**Key Features and Technical Details:**
- The solid curve for negative (sinking) current shows a consistent increase across the entire range of output currents.
- The dashed curve for positive (sourcing) current deviates from the solid curve, particularly at lower currents, indicating a discrepancy between measured and datasheet values.

**Annotations and Specific Data Points:**
- The op-amp model is specified as LMC6041 with a supply voltage \( V_S = \pm 2.5V \).
- Annotations on the graph differentiate between the positive (sourcing) and negative (sinking) operation modes.
- The graph highlights the unreliability of the datasheet's sourcing curve, as evidenced by the dashed line deviating from the expected trend.

Figure 4.46. Maximum swing (as $\Delta \mathrm{V}$ from the respective rails) versus load current for a CMOS rail-to-rail output op-amp. The solid curves are measured values; you can't always trust datasheets in this case the datasheet's sourcing curve (dashed curve) is evidently in error.
be as high as several thousand ohms, a characteristic shared by some op-amps with rail-to-rail outputs. Feedback lowers the output impedance into insignificance (or raises it, for a current source), by a factor of the loop gain $A B$ (see $\S 2.5 .3 \mathrm{C}$ ); so what usually matters more is the maximum output current, with typical values of $\pm 20 \mathrm{~mA}$ or so (but much higher for the rarified group of "high current" opamps, see Table 4.2 b on page 272).

#### J. Voltage gain, bandwidth, and phase shift

Typically the voltage gain $A_{\mathrm{vo}}$ (sometimes called $A_{\mathrm{VOL}}, A_{\mathrm{V}}$, $G_{\mathrm{V}}$, or $G_{\mathrm{VOL}}$ ) at dc is 100,000 to $1,000,000$ (often specified
image_name:Figure 4.47
description:Figure 4.47 is a Bode plot that illustrates the gain versus frequency for the LF411 operational amplifier. The graph is plotted on logarithmic scales for both axes. The x-axis represents frequency in hertz (Hz), ranging from 1 Hz to 10 MHz, while the y-axis represents voltage gain in volts per volt (V/V), spanning from 0.1 to 1M.

The plot shows two distinct regions: the open-loop gain and the closed-loop gain. The open-loop gain starts at a high value of around 1,000,000 V/V (or 120 dB) at low frequencies and decreases steadily as frequency increases. This decline is linear on the logarithmic scale, indicating a constant rate of decrease in gain with increasing frequency. The gain eventually drops to unity gain (1 V/V) at the frequency denoted as \(f_T\), which is noted at approximately 10 MHz.

The closed-loop gain is depicted as a horizontal line at a much lower gain value, approximately 100 V/V, indicating that it remains constant across the frequency range until it intersects with the open-loop gain curve. This intersection occurs at the cutoff frequency \(f_{3dB}\), which is where the gain drops by 3 dB from its low-frequency value.

Key features of this graph include the labeling of the open-loop and closed-loop gain regions, the indication of the cutoff frequency \(f_{3dB}\), and the unity gain bandwidth \(f_T\). The annotations provide insight into the performance characteristics of the LF411, highlighting the frequency at which the operational amplifier transitions from high gain to unity gain, which is crucial for understanding its bandwidth capabilities and stability in various applications.

Figure 4.47. LF411 gain versus frequency ("Bode plot").
in decibels, thus 100 dB to 120 dB ), dropping to unity gain at a frequency (called $f_{\mathrm{T}}$, or sometimes gain-bandwidth product, GBW), most often in the range of 0.1 MHz to 10 MHz . This is usually given as a graph of open-loop voltage gain as a function of frequency, on which the $f_{\mathrm{T}}$ value is clearly seen; see, for example, Figure 4.47, which shows the curve for our favorite LF411.

For internally compensated op-amps this graph is simply a 6 dB /octave rolloff beginning at some fairly low frequency (for the 411 it begins at about 10 Hz ), an intentional characteristic necessary for stability, as we'll see in §4.9. This rolloff (the same as a simple $R C$ lowpass filter) results in a constant $90^{\circ}$ lagging phase shift from input to output (open-loop) at all frequencies above the beginning of the rolloff, increasing to $120^{\circ}$ to $160^{\circ}$ as the open-loop gain approaches unity. Because a $180^{\circ}$ phase shift at a frequency where the voltage gain equals 1 will result in positive feedback (oscillations), the term "phase margin" is used to specify the difference between the phase shift at $f_{\mathrm{T}}$ and $180^{\circ}$.

There's a price to pay for greater bandwidth $f_{\mathrm{T}}$, namely, higher transistor operating currents, and therefore higher op-amp supply currents. You can get op-amps with supply currents of less than $1 \mu \mathrm{~A}$, but they have $f_{\mathrm{T}}$ 's down around 10 kHz ! In addition to high supply currents, very fast opamps can have relatively high input bias currents, often more than a microamp, owing to their bipolar input stages operating at high collector current. Don't use fast op-amps if you don't need them - in addition to the drawbacks just mentioned, their high gain at high frequency makes it easier for your circuit to oscillate.
image_name:Figure 4.48
description:Figure 4.48 is a time-domain waveform graph illustrating the concept of slew rate in op-amps, specifically highlighting the maximum slew rate at the zero crossings of a sinewave. The graph plots voltage on the vertical axis, ranging from -14V to +14V, while the horizontal axis represents time.

The waveform shown is a sinusoidal signal, with zero crossings being the points where the waveform crosses the horizontal axis (time axis). The graph indicates two different slew rates: 1 V/µs and 3 V/µs, corresponding to maximum frequencies (f_max) of 11 kHz and 34 kHz, respectively. These slew rates are depicted at the zero crossings of the sinewave, where the rate of change of the voltage is at its maximum.

The annotations on the graph clearly mark these slew rates and their associated maximum frequencies, emphasizing that the maximum slew rate occurs at the zero crossings. The waveform demonstrates the limitations imposed by the slew rate, as the output waveform cannot change instantaneously and is limited by these rates as it crosses zero.

Overall, this graph visually conveys how the slew rate restricts the op-amp's ability to follow rapid changes in input, a critical consideration in high-frequency applications where the slew rate can limit performance.

Figure 4.48. The maximum slew rate of a sinewave, $\mathrm{SR}=2 \pi A f$, occurs at the zero crossings.

#### K. Slew rate

The op-amp "compensation" capacitance (discussed further in §4.9.2) and small internal drive currents act together to limit the rate at which the output can change, even when a large input unbalance occurs. This limiting speed is usually specified as slew rate or slewing rate (SR). For the 411 it is $15 \mathrm{~V} / \mu \mathrm{s}$; low-power op-amps typically have slew rates less than $1 \mathrm{~V} / \mu \mathrm{s}$, whereas a high-speed op-amp might slew at hundreds of volts per microsecond. The slew rate limits the amplitude of an undistorted sine-wave output swing above some critical frequency (the frequency at which the full supply swing requires the maximum slew rate of the op-amp), thus the "output voltage swing as a function of frequency" graph (seen in datasheets; see for example Figure 4.54). A sine wave of frequency $f$ hertz and amplitude $A$ volts requires a minimum SR of $2 \pi A f$ volts per second, with the peak slewing occurring at the zero crossings (Figure 4.48). Figure 4.49 shows a 'scope trace illustrating realworld "slew-rate distortion."

For externally compensated op-amps, the slew rate depends on the compensation network used. In general, it will be lowest for "unity-gain compensation," increasing to perhaps 30 times faster for $\times 100$ gain compensation. This is discussed further in $\S 4.9 .2 \mathrm{~B}$ and in Chapter $4 x .{ }^{25}$ As with gain-bandwidth product $f_{\mathrm{T}}$, higher SR op-amps run at higher supply currents.

An important note: slew rate is ordinarily specified for a unity-gain configuration (i.e., a follower) with a full-swing step input. So there's is a large differential drive at the opamp's input, which really gets the currents flowing in there. The slew rate will be considerably less for a small input, say 10 mV .

[^36]LT1013

Figure 4.49. Slew-rate-induced distortion. This scope trace of an LT1013 op-amp follower, for which the datasheet specifies a typical SR of $0.4 \mathrm{~V} / \mu \mathrm{s}$, shows the input and output waveforms for a sinewave whose peak SR is $0.6 \mathrm{~V} / \mu \mathrm{s}(A=6.0 \mathrm{~V}, f=15.4 \mathrm{kHz})$; also shown is a slower sinewave, which overlays its (identical) output $(A=6.0 \mathrm{~V}, f=11 \mathrm{kHz}$ : $\mathrm{SR}=0.4 \mathrm{~V} / \mu \mathrm{s})$. Scales: $2 \mathrm{~V} / \mathrm{div}, 10 \mu \mathrm{~s} / \mathrm{div}$.

#### L. Temperature dependence

Most of these parameters have some temperature dependence. However, this usually doesn't make any difference, since small variations in gain, for example, are almost entirely compensated by feedback. Furthermore, the variations of these parameters with temperature are typically small compared with the variations from unit to unit.

The exceptions are input offset voltage and input offset current; these input errors will matter, particularly if you've trimmed the offsets approximately to zero, and will cause drifts in the output. When high precision is important, a low-drift "instrumentation" op-amp should be used, with external loads kept above 10k to minimize the horrendous effects on input-stage performance caused by temperature gradients. We will have much more to say about this subject in Chapter 5.

#### M. Supply voltage and current

Traditionally, most op-amps were designed for $\pm 15 \mathrm{~V}$ power supplies, with a smattering of "single-supply" opamps that operated on single supplies (i.e., $+V$ and ground), typically from +5 V to +15 V . The traditional split-supply op-amps were somewhat flexible; for example, the third-generation LF411 accepts supplies from $\pm 5 \mathrm{~V}$ to $\pm 18 \mathrm{~V}$. Most of these early op-amps ran at supply currents of a few milliamps.

There has been an important trend to lower-current and especially lower-voltage operation to accommodate battery-powered equipment. So, for example, it is now common to see op-amps that operate with total supply voltages (the span from $V_{+}$to $V_{-}$) of 5 V , or even 3 V , and run on supply currents of $10 \mu \mathrm{~A}$ to $100 \mu \mathrm{~A}$. These are usually
image_name:Figure 4.50. Inverting amplifier
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: Vin, N2: InN}
name: R2, type: Resistor, value: R2, ports: {N1: Vout, N2: InN}
name: A1, type: OpAmp, value: A1, ports: {InP: GND, InN: InN, OutP: Vout, OutN: GND}
]
extrainfo:The circuit is an inverting amplifier with a gain of Gv = -R2/R1. The DC error is given by ΔVout = (1 + R2/R1)Vos + IBR2. The input is at the inverting terminal of the op-amp, and the output is at the op-amp's output terminal.

Figure 4.50. Inverting amplifier.
built with $100 \%$ CMOS circuitry, but there are some bipolar designs as well. These are usually rail-to-rail output stages - obviously such op-amps cannot afford the luxury of the "no-closer-than-2-volts-from-either-rail" mantra!

When considering these op-amps, watch out for unusually low maximum supply voltage restrictions. Many such op-amps are limited to as little as 10 V total supply (i.e., $\pm 5 \mathrm{~V}$ ), and an increasing number are limited to 5 volts or less. Also, note that an op-amp with microamp quiescent current will necessarily draw plenty of current if you ask it to supply that amount of current to an attached load; output current doesn't come out of thin air.

#### N. Miscellany: CMRR, PSRR, $e_{\mathrm{n}}, i_{\mathrm{n}}$

For completeness, we should mention here that op-amps are also limited in common-mode rejection ratio (CMRR) and power-supply rejection ratio (PSRR), i.e., their incomplete rejection of common-mode input variations and power-supply fluctuations. This becomes more important at high frequencies, where the loop gain is decreasing and where the compensation capacitor $C_{\mathrm{C}}$ couples negative-rail fluctuations into the signal chain.

In addition, op-amps are not noiseless - they introduce both voltage noise $\left(e_{\mathrm{n}}\right)$ and current noise $\left(i_{\mathrm{n}}\right)$ at their input. These become significant limitations primarily in connection with precision circuits and low-noise amplifiers, and they will be treated in Chapters 5 and 8.

### 4.4.2 Effects of op-amp limitations on circuit behavior

Let's go back and look at the inverting amplifier with these limitations in mind. We'll see how they affect performance, and we'll learn how to design effectively in spite of them. With the understanding we'll get from this example, you should be able to handle other op-amp circuits. Figure 4.50 shows the circuit again.
image_name:Figure 4.51
description:
[
name: A, type: OpAmp, value: A, ports: {InP: in, InN: InN, OutP: out, OutN: GND}
name: R1, type: Resistor, value: R1, ports: {N1: InN, N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: out, N2: InN}
]
extrainfo:The circuit is a non-inverting amplifier with a feedback network consisting of resistors R1 and R2. The gain is determined by the formula B = R1 / (R1 + R2).

Figure 4.51. Op-amp noninverting amplifier with finite open-loop gain.
image_name:A.
description:
[
name: A, type: OpAmp, value: A, ports: {InP: in, InN: InN, OutP: out, OutN: GND}
name: R1, type: Resistor, value: R1, ports: {N1: InN, N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: out, N2: InN}
]
extrainfo:The circuit is a non-inverting amplifier with a feedback network consisting of resistors R1 and R2. The gain is determined by the formula B = R1 / (R1 + R2). The input impedance Zin is R1 + R2/(1 + A) and the output impedance Zout is Z(open-loop)/(1 + A).
image_name:
description:
[
name: A, type: OpAmp, value: A, ports: {InP: GND, InN: InN, OutP: out, OutN: GND}
name: R1, type: Resistor, value: R1, ports: {N1: InN, N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: out, N2: InN}
]
extrainfo:The circuit is a non-inverting amplifier with a feedback network consisting of resistors R1 and R2. The gain is determined by the formula B = R1 / (R1 + R2). The input impedance is given as Zin = R1 + R2/(1+A) and the output impedance as Zout = Z(open-loop)/(1+A).

$\begin{array}{rr}\text { GMD } & Z_{\text {out }}=\frac{Z \text { (open-loop) }}{1+A B} \\ \text { B. } \quad\left(B=\frac{R_{1}}{R_{1}+R_{2}}\right)\end{array}$
Figure 4.52. Input and output impedances: A. transresistance amplifier, B. inverting voltage amplifier.

#### A. Open-loop gain

Finite open-loop gain affects bandwidth, input and output impedances, and linearity. We saw this earlier, in the context of discrete transistor amplifiers, when we introduced negative feedback in Chapter 2 (§2.5.3). That material forms an essential background to what follows here; be sure to review it if you are foggy on this stuff.

#### Bandwidth

Because of finite open-loop gain, the voltage gain of the amplifier with feedback (closed-loop gain) will begin dropping at a frequency where the open-loop gain approaches $R_{2} / R_{1}$ (Figure 4.47). For garden-variety op-amps like the 411, this means that you're dealing with a relatively lowfrequency amplifier; the open-loop gain is down to 100 at

40 kHz , and $f_{\mathrm{T}}$ is 4 MHz . Note that the closed-loop gain is always less than the open-loop gain, so the overall amplifier will exhibit a noticeable falloff of gain at a fraction of $f_{\mathrm{T}}$. Recall from Chapter 2 that the closed-loop gain of the noninverting amplifier in Figure 4.51 is given by

$$
G=\frac{A}{1+A B}
$$

where $B$ is the fraction of the output fed back, in this case $B=R_{1} /\left(R_{1}+R_{2}\right)$. The output will therefore be down 3 dB at the frequency where the magnitude of the loop gain $A B$ is unity (i.e., where the magnitude of the open-loop gain $A$ equals the desired closed-loop gain $1 / B$ ), approximately 40 kHz for the LF411. ${ }^{26}$

Back in $\S 4.2 .5$ we remarked that op-amp current sources rely on the op-amp's voltage gain (thus loop gain) to raise its inherently low output resistance $R_{\mathrm{o}}$ (of order $\sim 100 \Omega$, see Figure 5.20), and that the decrease of open-loop gain with increasing frequency degrades the current-source's output impedance. This can be made quantitative: $Z_{\text {out }}$ at increasing frequencies is of the form $R_{\mathrm{O}} \cdot f_{\mathrm{T}} / f$.

#### Output impedance

Finite loop gain also affects the input and output impedances of a closed-loop op-amp circuit. Feedback can extract a sample of the output voltage (e.g., the noninverting voltage amplifiers we've been considering) or the output current (e.g., an op-amp current source). For voltage feedback the op-amp's open-loop output impedance is lowered by a factor of $1+A B$, bringing typical open-loop output impedances of tens to hundreds of ohms down to milliohms (for large loop gain), but rising back up to openloop values as the loop gain falls to unity at higher frequencies.

This linear rise in closed-loop output impedance is nicely illustrated in Figure 4.53, adapted from the LT1055 datasheet. You can see how greater loop gain (feedback configured for lower closed-loop gain) produces correspondingly lower output impedance; and you can see the linear rise up to the op-amp's native $R_{\text {out }}$ (sometimes designated $r_{\mathrm{o}}$ ), here about $60 \Omega$. Note also that an impedance that rises linearly with frequency is like an inductor. And, in fact, that's just what the output looks like for signals in this frequency range. This can have important conse-

[^37]quences, for example, creating a series $L C$ resonant circuit when the op-amp's load is capacitive.

The effect of the lowered loop gain (at high frequencies) is to degrade the beneficial effects of negative feedback. So a voltage amplifier suffers from increased output impedance, as we've seen. And the reverse is true for an amplifier with feedback that senses output current: here feedback normally acts to raise the native output impedance by a factor of loop gain (that's good: you want high output impedance in a current source), which then drops back to its open-loop values as the loop gain falls. Some op-amps (most notably those with rail-to-rail outputs) use an output stage with intrinsically high output impedance; for these op-amps a high loop gain is essential to achieve low output impedance.
image_name:Figure 4.53
description:The graph in Figure 4.53 is a Bode plot that illustrates the closed-loop output impedance of an operational amplifier as a function of frequency. The x-axis represents frequency, measured in kilohertz (kHz), and is plotted on a logarithmic scale ranging from 0.1 kHz to 1000 kHz. The y-axis represents the closed-loop output impedance, measured in ohms (Ω), also on a logarithmic scale, ranging from 0.1 Ω to 100 Ω.

The graph displays three curves, each corresponding to different closed-loop gains (G_CL): 1, 10, and 100. These gains are annotated on each curve. The curves show how the closed-loop output impedance changes with frequency for each gain setting.

1. **Curve for G_CL = 1:** This curve starts at a low impedance and rises linearly with frequency, appearing as a straight line on the log-log plot. It behaves like an inductance of approximately 1.9 μH.

2. **Curve for G_CL = 10:** Similar to the previous curve, this linearly rising curve represents a higher inductance of approximately 19 μH.

3. **Curve for G_CL = 100:** This curve also rises linearly with frequency, showing an inductance of approximately 190 μH. It levels off at high frequencies, approaching the open-loop output resistance of the op-amp, noted as 60 Ω.

The behavior of these curves indicates that as the closed-loop gain increases, the effective inductance increases, and the closed-loop output impedance rises more sharply with frequency. However, at high frequencies, the impedance for each curve approaches the same open-loop resistance value, indicating the limit of the feedback's influence at these frequencies.

Figure 4.53. An op-amp's closed-loop output impedance rises approximately linearly with frequency over a large portion of its bandwidth, thus behaving like an inductance $L_{\text {out }} \approx r_{0} G_{\mathrm{CL}} / 2 \pi f_{\mathrm{T}}$. After the loop gain drops to unity, $Z_{\text {out }}$ looks like the op-amp's open-loop output resistance $r_{0}$. These curves were adapted from the LT1055 datasheet.

#### Input impedance

The input impedance of a noninverting amplifier is raised by a factor of $1+A B$ from its open-loop value, a matter usually of little consequence because of the high native input impedances of op-amps.

The inverting amplifier circuit is different from the noninverting circuit and has to be analyzed separately. It's best to think of it as a combination of an input resistor driving a shunt feedback stage (Figure 4.52). The shunt stage alone has its input at the "summing junction" (the inverting input of the amplifier), where the currents from feedback and input signals are combined (this amplifier connection is really a "transresistance" configuration; it converts a current
image_name:Figure 4.54
description:The graph in Figure 4.54 is a plot of the peak-to-peak output swing versus frequency for the LF411 operational amplifier. The x-axis represents frequency in hertz (Hz) on a logarithmic scale, ranging from 1 kHz to 10 MHz. The y-axis represents the peak-to-peak output swing in volts (V), ranging from 0 to 30 volts.

Overall Behavior and Trends:
- **Initial Flat Region:** At lower frequencies, approximately from 1 kHz to around 30 kHz, the peak-to-peak output swing remains constant at about 27 volts. This indicates that the amplifier can maintain its full output swing at these frequencies.
- **Roll-off Region:** Beyond approximately 30 kHz, the output swing begins to decrease. This decrease continues as the frequency increases, demonstrating a roll-off behavior.
- **High-Frequency Behavior:** At frequencies above 100 kHz, the output swing drops more significantly, following a trend that approximates a 1/f relationship. This indicates that the output capability of the amplifier diminishes as frequency increases.

Key Features and Technical Details:
- **Full-Power Bandwidth:** The point where the output begins to drop is labeled as the full-power bandwidth. This is related to the slew rate (SR) of the amplifier, which is given as 15 V/µs. The relationship is given by \( f = \frac{SR}{\pi A_{pp}} \), where \( A_{pp} \) is the peak-to-peak output.
- **Annotations:** The graph includes annotations such as the amplifier model (LF411), power supply voltage (\( V_S = \pm 15 \) V), load resistance (\( R_L = 2k\Omega \)), and the slew rate (SR = 15 V/µs).

### Observations:
- The amplifier maintains a high output swing at lower frequencies, which is ideal for applications requiring consistent output levels.
- The reduction in output swing at higher frequencies is typical for op-amps and is due to limitations in the slew rate, affecting the full-power bandwidth.
- This graph is useful for understanding the frequency limitations of the LF411 when used in applications requiring large output swings.

Figure 4.54. Peak-to-peak output swing versus frequency (LF411).
input to a voltage output). Feedback reduces the impedance looking into the summing junction, $R_{2}$, by a factor of $1+A$ (see if you can prove this). In cases of very high loop gain, the input impedance is reduced to a fraction of an ohm, a good characteristic for a current-input amplifier.

The classic op-amp inverting amplifier connection is a combination of a shunt feedback transresistance amplifier and a series input resistor, as in the figure. As a result, the input impedance equals the sum of $R_{1}$ and the impedance looking into the summing junction. For high loop gain, $R_{\text {in }}$ approximately equals $R_{1}$.

It is a straightforward exercise to derive an expression for the closed-loop voltage gain of the inverting amplifier with finite loop gain. The answer is

$$
\begin{equation*}
G=-A(1-B) /(1+A B) \tag{4.5}
\end{equation*}
$$

where $B$ is defined as before, $B=R_{1} /\left(R_{1}+R_{2}\right)$. In the limit of large open-loop gain $A, G=-1 / B+1$ (i.e., $G=$ $-R_{2} / R_{1}$ ).

Exercise 4.14. Derive the foregoing expressions for input impedance and gain of the inverting amplifier.

#### Linearity

In the limit of infinite loop gain, a feedback circuit's behavior depends on only the feedback network; the native nonlinearities of the op-amp (e.g., voltage dependence of gain, crossover distortion, and so on) are compensated by feedback. These defects reappear as loop gain is reduced, for example at higher frequencies. It is for this reason that you have to choose your op-amps with care, for example if you want to design low-distortion audio amplifier circuits. Op-amps intended for this sort of application have carefully designed output stages, and often they specify distor-
tion as a function of frequency and gain. An example is the excellent AD797, which specifies a maximum distortion of $0.0003 \%$ at 20 kHz and 3 V (rms) output.

#### B. Slew rate

Because of limited slew rate, the maximum undistorted sinewave output swing drops above a certain frequency. Figure 4.54 shows the curve for a 411 , with its $15 \mathrm{~V} / \mu \mathrm{s}$ slew rate. For slew rate $S$, the output amplitude is limited to $A(\mathrm{pp}) \leq S / \pi f$ for a sinewave of frequency $f$, thus explaining the $1 / f$ dropoff of the curve. The flat portion of the curve reflects the power-supply limits of output voltage swing. An easy formula to remember is ${ }^{27}$

$$
\begin{equation*}
S_{\min }=\omega A=2 \pi f A \tag{4.6}
\end{equation*}
$$

where $S_{\min }$ is the minimum required SR for a sinewave of amplitude $A$ (that's half the peak-to-peak amplitude: $A_{\mathrm{PP}}=$ $2 A$ ) and angular frequency $\omega$; recall that $\omega=2 \pi f$. As an aside, the slew-rate limitation of op-amps can be usefully exploited to filter sharp noise spikes from a desired signal, with a technique known as nonlinear lowpass filtering: if the slew rate is deliberately limited, the fast spikes can be dramatically reduced with little distortion of the underlying signal.

#### C. Output current

Because of limited output-current capability, an op-amp's output swing is reduced for small load resistances, as we saw in Figure 4.44. For precision applications it is a good idea to avoid large output currents in order to prevent onchip thermal gradients produced by excessive power dissipation in the output stage.

#### D. Offset voltage

Because of input offset voltage, a zero input produces an output ${ }^{28}$ of $V_{\text {out }}=G_{\mathrm{dc}} V_{\mathrm{OS}}=\left(1+R_{2} / R_{1}\right) V_{\mathrm{OS}}$. For an inverting amplifier with a voltage gain of 100 built with a 411, the output could be as large as $\pm 0.2$ volt when the input

[^38]is grounded ( $V_{\mathrm{OS}}=2 \mathrm{mV}$ max). Solutions: (a) If you don't need gain at dc, use a capacitor to drop the gain to unity at dc, as in Figure 4.7B. In this case you could do that by capacitively coupling the input signal. (b) Trim the voltage offset to zero with the manufacturer's recommended trimming network. (c) Use an op-amp with smaller $V_{\text {OS }}$. (d) Trim the voltage offset to zero with an external trimming network, as for example in §4.8.3 (see Figure 4.91).

#### E. Input bias current

Even with a perfectly trimmed op-amp (i.e., $V_{\mathrm{OS}}=0$ ), our inverting amplifier circuit will produce a nonzero output voltage when its input terminal is connected to ground. That is because the finite input bias current, $I_{\mathrm{B}}$, produces a voltage drop across the resistors, which is then amplified by the circuit's voltage gain. In this circuit the inverting input sees a driving impedance of $R_{1} \| R_{2}$, so the bias current produces a voltage $V_{\text {in }}=I_{\mathrm{B}}\left(R_{1} \| R_{2}\right)$, which is then amplified by the gain at dc, $1+R_{2} / R_{1}$ (see footnote 28); the result is an output error voltage of $V_{\text {out }}=I_{\mathrm{B}} R_{2}$.

With FET-input op-amps the effect is usually negligible, but the substantial input current of bipolar op-amps (and also current-feedback op-amps; see Chapter $4 x$ ) can cause real problems. For example, consider an inverting amplifier with $R_{1}=10 \mathrm{k}$ and $R_{2}=1 \mathrm{M}$; these are reasonable values for an audiofrequency inverting stage, where we might like to keep $Z_{\text {in }}$ at least 10 k . If we chose the low-noise bipolar NE5534 ( $I_{\mathrm{B}}=2 \mu \mathrm{~A}$, max), the output (for grounded input) could be as large as $100 \times 2 \mu \mathrm{~A} \times 9.9 \mathrm{k}$, or 1.98 volt $\left(G_{\mathrm{dc}} I_{\mathrm{B}} R_{\text {unbalance }}\right)$, which is unacceptable. By comparison, for our jellybean LF411 (JFET-input) op-amp, the corresponding worst-case output (for grounded input) is 0.2 mV ; for most applications this is negligible, and in any case is dwarfed by the $V_{\text {OS }}$-produced output error ( 200 mV , worstcase untrimmed, for the LF411).

There are several solutions to the problem of biascurrent errors. If you must use an op-amp with large bias current, it is a good idea to ensure that both inputs see the same dc driving resistance, as in Figure 4.55. In this case, 91 k is chosen as the parallel resistance of 100 k and 1 M . In addition, it is best to keep the resistance of the feedback network small enough so that bias current doesn't produce large offsets; typical values for the resistance seen from the op-amp inputs are 1 k to 100 k or so. A third cure involves reducing the gain to unity at dc, as in Figure 4.7B.

In most cases, though, the simplest solution is to use opamps with negligible input current. Op-amps with JFETor MOSFET-input stages generally have input currents in the picoamp range (watch out for its rapid rise versus temperature, though, roughly doubling every $10^{\circ} \mathrm{C}$ ),
image_name:Figure 4.55
description:
[
name: LOAD, type: Resistor, value: 100k, ports: {N1: LOAD, N2: InN(A1)}
name: 1M, type: Resistor, value: 1M, ports: {N1: InN(A1), N2: Vout}
name: 91k, type: Resistor, value: 91k, ports: {N1: InP(A1), N2: GND}
name: A1, type: OpAmp, value: A1, ports: {InP: InP(A1), InN: InN(A1), OutP: Vout, OutN: GND}
]
extrainfo:The circuit is a non-inverting amplifier using a bipolar op-amp. The input is connected through a 100k resistor, and feedback is provided by a 1M resistor. A 91k resistor is connected to the inverting input and ground.

Figure 4.55. With bipolar op-amps, use a compensation resistor to reduce errors caused by input bias current.
and many modern bipolar designs use superbeta transistors or bias-cancellation schemes to achieve bias currents nearly as low and decreasing slightly with temperature. With these op-amps, you can have the advantages of bipolar op-amps (precision, low noise) without the annoying problems caused by input current. For example, the precision low-noise bipolar OP177 has $I_{\mathrm{B}}<2 \mathrm{nA}$, and the bias-compensated bipolar LT1012 has $I_{\mathrm{B}}= \pm 25 \mathrm{pA}$ (typ). Among inexpensive FET op-amps, the JFET LF411 has $I_{\mathrm{B}}=50 \mathrm{pA}($ typ $)$, and the MOSFET TLC270 series, priced under a dollar, has $I_{\mathrm{B}}=1 \mathrm{pA}(\mathrm{typ})$.

#### F. Input offset current

As we just described, it is usually best to design circuits so that circuit impedances, combined with op-amp bias current, produce negligible errors. However, occasionally it may be necessary to use an op-amp with high bias current, or to deal with signals of extraordinarily high Thévenin impedances. Examples of high-bias-current amplifiers are current-feedback op-amps (e.g., the AD844), low-noise $\left(e_{n}\right)$ op-amps (e.g., the AD797), and wideband op-amps (e.g., the LM7171), each with input currents of several microamps.

In these cases the best you can do is to balance the dc driving resistances seen by the op-amp at its input terminals. There will still be some error at the output ( $G_{\mathrm{dc}} I_{\mathrm{offset}} R_{\mathrm{source}}$ ) that is due to unavoidable asymmetry in the op-amp input currents. In general, $I_{\text {offset }}$ is smaller than $I_{\text {bias }}$ by a factor of 2 to 20 (with bipolar op-amps generally showing better matching than FET op-amps).

#### G. Limitations imply tradeoffs

In the preceding paragraphs we discussed the effects of op-amp limitations, taking the example of the simple inverting voltage amplifier circuit. Thus, for example, opamp input current caused a voltage error at the output. In a different op-amp application you may get a different effect; for example, in an op-amp integrator circuit, a finite input current produces an output ramp (rather than a
constant) with zero applied input. As you become familiar with op-amp circuits you will be able to predict the effects of op-amp limitations in a given circuit and therefore choose which op-amp to use in a given application. In general, there is no "best" op-amp (even when price is no object): for example, op-amps with the very lowest input currents (MOSFET types) generally have larger voltage offsets and greater noise, and vice versa. Good circuit designers choose their components with the right tradeoffs to optimize performance, without going overboard on unnecessary "gold-plated" parts.

To help put this discussion of "op-amp realities" into perspective, you may want to look again at Table 4.1 on page 245 , where we've summarized the kinds of performance you can expect from op-amps that might be described as average, or "jellybean" (for example, the LF412 is a jellybean JFET op-amp), and from those that are among the best available ("premium") for each given parameter. Sadly, you can't get an op-amp that combines all the characteristics in a "premium" column; engineering is the art of compromise.

The limitations of op-amp performance we have talked about will have an influence on component values in nearly all circuits. For instance, the feedback resistors must be large enough so that they don't load the output significantly, but they must not be so large that input bias current produces sizable offsets. High impedances in the feedback network cause both loading effects, and destabilizing phase shifts, from stray capacitances; they also increase susceptibility to capacitive pickup of interfering signals. These tradeoffs typically dictate resistor values of 2 k to 100 k with general-purpose op-amps.

Similar sorts of tradeoffs are involved in almost all electronic design, including the simplest circuits constructed with transistors. For example, the choice of quiescent current in a transistor amplifier is limited at the high end by device dissipation, increased input current, excessive supply current, and reduced current gain, whereas the lower limit of operating current is limited by leakage current, reduced current gain, and reduced speed (from stray capacitance in combination with the high resistance values). For these reasons you typically wind up with collector currents in the range of a few tens of microamps to a few tens of milliamps (higher for power circuits, sometimes a bit lower in "micropower" applications), as mentioned in Chapter 2.

In later chapters we look more carefully at some of these problems in order to convey a good understanding of the tradeoffs involved.

Exercise 4.15. Draw a dc-coupled inverting amplifier with a gain
of 100 and $Z_{\text {in }}=10 \mathrm{k}$. Include compensation for input bias current and show offset voltage trimming network ( 10 k pot between pins 1 and 5 , wiper tied to $V_{-}$). Now add circuitry so that $Z_{\text {in }} \geq$ $10^{8} \Omega$.

### 4.4.3 Example: sensitive millivoltmeter

To put flesh on these bones, let's look at a very simple design example - a dc amplifier with lots of gain, high input impedance, and (for variety in today's too-digital world) an analog zero-center panel meter readout. We'll aim for $\pm 10 \mathrm{mV}$ full-scale sensitivity, and 10 megohms input impedance.

Figure 4.56 shows the initial design, where we assume we've got $\pm 5 \mathrm{~V}$ supplies available (more on this later), and we use a noninverting gain of 100 to produce a $\pm 1 \mathrm{~V}$ opamp output at fullscale. That drives a $100-0-100 \mu \mathrm{~A}$ zerocenter meter movement, which we decorate with a relabeled scale that reads " $-10 \mathrm{mV} \cdots 0 \cdots 10 \mathrm{mV}$."
image_name:Figure 4.56
description:
[
name: IC1, type: OpAmp, ports: {InP: Vin, InN: GND, OutP: Vout, Vdd: +5, -Vdd: -5}
name: 10M, type: Resistor, value: 10M, ports: {N1: Vin, N2: Vout}
name: 1k, type: Resistor, value: 1k, ports: {N1: GND, N2: Vout}
name: 99k, type: Resistor, value: 99k, ports: {N1: Vout, N2: InN}
name: 2k, type: Resistor, value: 2k, ports: {N1: Vout, N2: MeterCal}
name: 7.87k, type: Resistor, value: 7.87k, ports: {N1: MeterCal, N2: Meter}
name: 1100Ω, type: Resistor, value: 1100Ω, ports: {N1: Meter, N2: GND}
]
extrainfo:The circuit is a sensitive millivoltmeter with analog readout, designed for a ±10 mV full-scale sensitivity. It uses a noninverting gain of 100 with an op-amp to drive a zero-center meter movement. The circuit includes calibration for the meter scale.

Figure 4.56. Sensitive millivoltmeter with analog readout; see text for choice of $I_{1}$.

It looks simple, and it is. But it won't work well if we're not careful. Imagine we choose our default LF411 for IC $\mathrm{C}_{1}$, figuring that the low bias current of a JFET-input op-amp is just what we need. We short the input leads together and find to our horror that the meter reads way off center, as much as $\pm 2 \mathrm{mV}$. That's because the 411 has $V_{\mathrm{OS}}=2 \mathrm{mV}$ (max). Ideally we'd like the thing to read zero with the input leads shorted or open, where "zero" might realistically mean no more than $1 \%$ of the full-scale reading.

OK, we add an offset trimmer and adjust it until the output reads zero with shorted input. We leave it on the bench, go to lunch, then come back and find it now reads -0.2 mV with shorted input. That's because it sat in the sun, warmed up by $10^{\circ} \mathrm{C}$, and therefore drifted by $200 \mu \mathrm{~V}$ (the LF411 has a temperature coefficient of offset voltage $\mathrm{TCV}_{\mathrm{OS}}=20 \mu \mathrm{~V} /{ }^{\circ} \mathrm{C}$, max). Well, we won't use it in the sun!

So, we wait for it to cool down, and note with satisfaction that it reads zero again.

Now we go to test it on a voltage divider, but we find that when we remove the short (test leads open circuited) the meter reads +2 mV ! This time the problem is bias current, specified as 200 pA (max) at room temperature. That's not much current, but it develops $2000 \mu \mathrm{~V}$ across the 10 M input resistor, which the meter dutifully reports as an input.

We could solve the $V_{\mathrm{OS}}$ problem with a precision bipolar op-amp, but we'd be in worse trouble with $I_{\mathrm{B}}$. We need an op-amp with $V_{\mathrm{OS}}<100 \mu \mathrm{~V}$ and $I_{\mathrm{B}}<10 \mathrm{pA}$. The solution is a precision FET-input op-amp, for example, the OPA336 ( $125 \mu \mathrm{~V}$ untrimmed, and 10 pA ), which is just about good enough without trimming, and certainly fine if we're willing to trim the initial offset.

A better solution here is to use a "chopper" op-amp like the LTC1050C or AD8638 (see Table 5.6). These are sometimes called "zero-drift," or "auto-zeroing" amplifiers. We'll learn about them shortly, and in more detail in the next chapter; for now all you need to know is that they offer specifications like $V_{\mathrm{OS}}<5 \mu \mathrm{~V}$, $\mathrm{TC} V_{\mathrm{OS}}<0.05 \mu \mathrm{~V} /{ }^{\circ} \mathrm{C}$, and $I_{\mathrm{B}}<50 \mathrm{pA}$ (those are, in fact, the worst-case specs for the LTC1050 in its inexpensive C-suffix grade).

A final thought: having a calibration adjustment is OK if you're building just a few of these things. But in production it would be nice to avoid manual calibration steps. An elegant circuit solution that circumvents calibration is to use a current-sensing resistor on the low side of the meter. We include this feature when we revisit this example early in Chapter 5 (§5.2), in a more rigorous approach to precision design.

### 4.4.4 Bandwidth and the op-amp current source

Back in $\S 4.2 .5$ we remarked that op-amp current sources rely on the op-amp's voltage gain (thus loop gain) to raise its inherently low output resistance $R_{\mathrm{o}}$ (of order $\sim 100 \Omega$, see Figure 5.20), and that the decrease of open-loop gain with increasing frequency degrades the current-source's output impedance. Put another way, the op-amp current source is a peculiar circuit, because an op-amp virtue (inherently low output impedance, i.e., a voltage source) becomes a vice, which must be punished with the cudgel of plentiful loop gain. This can be made quantitative: because of finite bandwidth $f_{\mathrm{T}}$, the output impedance of an opamp current source at increasing frequencies is of the form $R_{0} \cdot f_{\mathrm{T}} / f$, dropping ultimately to the op-amp's native output resistance $R_{\mathrm{O}}$ at the unity-gain frequency $f_{\mathrm{T}}$.

Likewise, finite slew rate affects the current-source's output impedance, making it look like a shunt capacitance.

Here's how to think about it: an ideal current source with a real capacitive load slews at a rate $S=d V / d t=I / C$; so a current source that is afflicted with a maximum slew rate $S$ looks like an ideal current source burdened with an effective shunt capacitance $C_{\text {eff }}=I_{\text {out }} / S$. For example, a 10 mA current source made with an op-amp of slew rate $1 \mathrm{~V} / \mu \mathrm{s}$ has an effective capacitive load of 10 nF ; this is rather large, compared even with a large MOSFET.

## 4.5 A detailed look at selected op-amp circuits

The performance of the next few circuits is affected significantly by the limitations of op-amps; we will go into a bit more detail in their description.

### 4.5.1 Active peak detector

There are numerous applications in which it is necessary to determine the peak value of some input waveform. The simplest method is a diode and capacitor (Figure 4.57). The highest point of the input waveform charges up $C$, which holds that value while the diode is back-biased.
image_name:Figure 4.57. Passive peak detector.
description:
[
name: D1, type: Diode, ports: {Na: Vin, Nc: Vout}
name: C, type: Capacitor, value: C, ports: {Np: Vout, Nn: GND}
]
extrainfo:This is a passive peak detector circuit using a diode and capacitor. The diode charges the capacitor to the peak value of the input voltage, and the capacitor holds that value until the diode becomes forward-biased again.

Figure 4.57. Passive peak detector.
This method has some serious problems. The input impedance is variable and is very low during peaks of the input waveform. Also, the diode drop makes the circuit insensitive to peaks less than about 0.6 volt, and inaccurate (by one diode drop) for larger peak voltages. Furthermore, since the diode drop depends on temperature and current, the circuit's inaccuracies depend on the ambient temperature and on the rate of change of output; recall that $I=C(d V / d t)$. An input emitter follower would improve the first problem only.

Figure 4.58A shows a better circuit, which exhibits the benefits of feedback. By taking feedback from the voltage at the capacitor, the diode drop doesn't cause any problems. The sort of output waveform you might get is shown in Figure 4.59.

Op-amp limitations affect this circuit in three ways.
(a) A finite op-amp slew rate causes a problem, even with relatively slow input waveforms. To understand this, note that the op-amp's output goes into negative saturation when the input is less positive than the output
image_name:A
description:
[
name: A1, type: OpAmp, value: A1, ports: {InP: Vin, InN: InN(A1), OutP: Out(A1)}
name: A2, type: OpAmp, value: A2, ports: {InP: InN(A1), InN: GND, Out: Vout}
name: D1, type: Diode, ports: {Na: Out(A1), Nc: InN(A1)}
name: C, type: Capacitor, value: C, ports: {Np: InN(A1), Nn: GND}
]
extrainfo:The circuit diagram 'A' is an op-amp based peak detector. It uses feedback from the capacitor voltage to mitigate diode drop issues. The op-amp A1 tracks the input voltage peaks, while A2 buffers the output. The diode D1 ensures that the capacitor C holds the peak voltage.
image_name:B
description:
[
name: U1, type: OpAmp, value: U1, ports: {InP: Vin, InN: InN(U1), OutP: Out(U1), OutN: InN(U1)}
name: D1, type: Diode, ports: {Na: Out(U1), Nc: InN(U1)}
name: D2, type: Diode, ports: {Na: InN(U1), Nc: X1}
name: 20k, type: Resistor, value: 20k, ports: {N1: InN(U1), N2: InN(U2)}
name: 1k, type: Resistor, value: 1k, ports: {N1: X1, N2: InP(U2)}
name: C, type: Capacitor, value: 1nF, ports: {Np: X1, Nn: GND}
name: U2, type: OpAmp, value: U2, ports: {InP: InP(U2), InN: InN(U2), OutP: Vout}
]
extrainfo:The circuit is an improved peak detector that utilizes feedback to track peak values. The feedback from the capacitor helps mitigate the diode drop issues, and the op-amp U2 helps in providing the output voltage. The design is supposed to respond better to short peaks.

Figure 4.58. A. Op-amp peak detector (more accurately, a "peak tracker"). B. Improved peak tracker responds to short peaks, because the input op-amp does not have to slew from negative saturation.
image_name:Figure 4.59. Peak detector output waveform
description:The graph in Figure 4.59 is a time-domain waveform depicting the output voltage (Vout) of a peak detector circuit against time (t). The x-axis represents time, while the y-axis represents voltage (V). The waveform shows two primary curves: the input voltage (Vin) and the output voltage (Vout).

- **Axes Labels and Units:**
- The x-axis is labeled as time (t), with no specific units provided, but it is typically in seconds or milliseconds.
- The y-axis is labeled as voltage (V), again with no specific units, but it is generally in volts.

- **Overall Behavior and Trends:**
- The input voltage (Vin) is depicted as a fluctuating waveform with multiple peaks and valleys, indicating varying voltage levels over time.
- The output voltage (Vout) follows a staircase-like pattern, where it tracks and holds the peak values of the input waveform. This behavior is characteristic of a peak detector circuit.

- **Key Features and Technical Details:**
- The output voltage (Vout) rises to match the peaks of the input voltage (Vin) and remains constant until a higher peak is detected.
- The graph illustrates the improved peak tracking ability of the circuit, as the output quickly adjusts to new peaks without significant delay.
- The staircase pattern of Vout demonstrates the circuit's ability to hold the peak voltage, mitigating the diode drop issue commonly found in basic peak detectors.

- **Annotations and Specific Data Points:**
- The graph is annotated with labels for Vout and Vin, clearly distinguishing between the input and output waveforms.
- No specific numerical values or gridlines are provided, but the general trend and behavior of the circuit's response to input voltage changes are clearly depicted.

Figure 4.59. Peak detector output waveform.
(try sketching the op-amp voltage on the graph; don't forget about diode forward drop). So the op-amp's output has to race back up to the output voltage (plus a diode drop) when the input waveform next exceeds the output. At slew rate $S$, this takes roughly $\left(V_{\text {out }}-V_{-}\right) / S$, where $V_{-}$is the negative supply voltage. Improved circuit 4.58B solves this problem.
(b) Input bias current causes a slow discharge (or charge, depending on the sign of the bias current) of the capacitor. This is sometimes called "droop," and it is best avoided by using op-amps with very low bias current. For the same reason, the diode must be a low-leakage type (e.g., the FJH1100, with less than 1 pA reverse current at 20 V , an "FET diode" such as the PAD5, or a diode-connected JFET such as the 2N4417; see the diode discussion in Chapter $1 x$ ), and the follow-
ing stage must also present high impedance (ideally it should also be an FET or FET-input op-amp).
(c) The maximum op-amp output current limits the rate of change of voltage across the capacitor, i.e., the rate at which the output can follow a rising input. Thus the choice of capacitor value is a compromise between low droop and high output slew rate.

For instance, a $1 \mu \mathrm{~F}$ capacitor used in this circuit with the common LM358 (which would be a poor choice because of its high bias current) would droop at $d V / d t=I_{\mathrm{B}} / C=$ $0.04 \mathrm{~V} / \mathrm{s}$ (using the "typical" value $I_{\mathrm{B}}=40 \mathrm{nA}$; the worstcase value of $I_{\mathrm{B}}=500 \mathrm{nA}$ produces a droop of $0.5 \mathrm{~V} / \mathrm{s}$ ) and would follow input changes only up to $d V / d t=I_{\text {output }} / C=$ $0.02 \mathrm{~V} / \mu \mathrm{s}$. This maximum follow rate is much less than the op-amp's slew rate of $0.5 \mathrm{~V} / \mu \mathrm{s}$, being limited by the maximum output current of 20 mA driving $1 \mu \mathrm{~F}$. By decreasing $C$ you could achieve greater output slewing rate, at the expense of greater droop. A more realistic choice of components would be the popular TLC2272 MOSFET-input opamp as driver and output follower (1 pA typical bias current) and a value of $C=0.01 \mu \mathrm{~F}$. With this combination you would get a droop of only $0.0001 \mathrm{~V} / \mathrm{s}$ and an overall circuit slew rate of $2 \mathrm{~V} / \mu \mathrm{s}$. For even better performance, use a MOSFET op-amp like the LMC660 or LMC6041, with a typical input current of 2 femtoamps. Capacitor leakage (or diode leakage or both) may then limit performance even if unusually good capacitors are used, e.g., polystyrene or polypropylene (see Chapter $1 x$ ). ${ }^{29}$

#### A. Resetting a peak detector

In practice it is usually desirable to reset the output of a peak detector in some way. One possibility is to put a resistor across the peak-hold capacitor so that the circuit's output decays with a time constant $R C$. In this way it holds only the most recent peak values. A better method is to put a transistor switch across $C$; a short pulse to the base then zeros the output. An FET switch is often used instead. For example, in Figure 4.58 you could connect an $n$-channel MOSFET such as a 2N7000 across $C$; bringing the gate

[^39]image_name:A
description:### Type of Graph and Function:
The graph in Figure A is a time-domain waveform depicting the behavior of a sample-and-hold circuit. It shows how the capacitor voltage changes over time in response to a sampling signal.

Axes Labels and Units:
- **X-axis:** Represents time, divided into intervals labeled as 'hold' and 'sample'.
- **Y-axis:** Represents capacitor voltage, though specific voltage units are not provided.

Overall Behavior and Trends:
- **Acquisition Time:** The waveform begins with a rising edge during the acquisition period, indicating that the capacitor is charging to the input voltage.
- **Hold Step (Charge Injection):** After the acquisition time, a noticeable drop or 'hold step' occurs due to charge injection when the circuit transitions from sample to hold mode.
- **Droop:** During the hold period, the voltage slightly decreases, illustrating droop, which is a gradual loss of the held voltage over time.
- **Repetition:** The waveform repeats the cycle of sampling and holding, showing periodic behavior.

Key Features and Technical Details:
- **Charge Injection:** The graph highlights the effect of charge injection as a small downward step at the transition from sampling to holding.
- **Droop:** The graph shows a gradual decline in voltage during the hold period, indicating droop, which is a common issue in sample-and-hold circuits.
- **Sampling Intervals:** The waveform clearly marks transitions between hold and sample states, which are critical for understanding the timing of the circuit.

Annotations and Specific Data Points:
- The graph annotates the acquisition time, charge injection ('hold step'), and droop, providing a clear understanding of these phenomena.
- There are no specific numerical values provided for the voltage or time intervals, but the waveform is exaggerated to emphasize the key behaviors of the sample-and-hold operation.
image_name:B
description:
[
name: A1, type: OpAmp, value: A1, ports: {InP: signal input, InN: GND, OutP: Out(A1), OutN:}
name: A2, type: OpAmp, value: A2, ports: {InP: InP(A2), InN: InN(A2), Out: output}
name: C, type: Capacitor, value: 1nF, ports: {Np: InN(A2), Nn: GND}
name: D1, type: Diode, ports: {Na: InN(A1), Nc: Out(A1)}
name: D2, type: Diode, ports: {Na: Out(A1), Nc: InN(A1)}
name: S1, type: Switch, ports: {N1: Out(A1), N2: InP(A2)}
name: R1, type: Resistor, value: 30k, ports: {N1: InN(A1), N2: InN(A2)}
name: R2, type: Resistor, value: 300Ω, ports: {N1: InP(A2), N2: output}
]
extrainfo:This circuit is a sample-and-hold (S/H) configuration using the LF398 integrated circuit. It processes a signal input and holds the value with the help of an op-amp and a capacitor. The diodes D1 and D2 form a feedback loop around A1 to stabilize the output. The switch S1 is used to control the sampling and holding phases. The resistors R1 and R2 set the gain and time constant of the circuit. The capacitor C is used to store the sampled voltage.

B. LF398 (integrated circuit S/H)

GND
Figure 4.60. Sample-and-hold: A. Standard configuration, with exaggerated waveform; B. LF398 single-chip S/H.
momentarily positive then zeros the capacitor voltage. An integrated CMOS analog switch (such as the MAX318, with a small series resistor to limit the current) can be used instead of a discrete nMOS (n-type metal-oxide semiconductor) transistor.

### 4.5.2 Sample-and-hold

Closely related to the peak detector is the "sample-andhold" (S/H) circuit (sometimes called "follow-and-hold"). These are especially popular in digital systems in which you want to convert one or more analog voltages to num-
bers so that a computer can digest them: the favorite method is to grab and hold the voltage(s), then do the digital conversion at your leisure. The basic ingredients of an S/H circuit are an op-amp and an FET switch; Figure 4.60 A shows the idea. $\mathrm{IC}_{1}$ is a follower to provide a low-impedance replica of the input. CMOS analog switch $S_{1}$ passes the signal through during "sample" and disconnects it during "hold." Whatever signal was present when $S_{1}$ was turned OFF is held on capacitor $C . \mathrm{IC}_{2}$ is a high-input-impedance follower (FET inputs), so that capacitor current during "hold" is minimized. The value of $C$ is a compromise: leakage currents in $S_{1}$ and the follower cause $C$ 's voltage to"droop" during the hold interval according to $d V / d t=I_{\text {leakage }} / C$. Thus $C$ should be large to minimize droop. But $S_{1}$ 's ON-resistance forms a lowpass filter in combination with $C$, so $C$ should be small if high-speed signals are to be followed accurately. $\mathrm{IC}_{1}$ must be able to supply $C$ 's charging current ( $I=C d V / d t$ ) and must have sufficient slew rate to follow the input signal. In practice, the slew rate of the whole circuit will usually be limited by IC ${ }_{1}$ 's output current and $S_{1}$ 's ON-resistance.

Exercise 4.16. Suppose $\mathrm{IC}_{1}$ can supply 10 mA of output current and $C=0.01 \mu \mathrm{~F}$. What is the maximum input slew rate the circuit can accurately follow? If $S_{1}$ has $50 \Omega$ oN resistance, what will be the output error for an input signal slewing at $0.1 \mathrm{~V} / \mu \mathrm{s}$ ? If the combined leakage of $S_{1}$ and $\mathrm{IC}_{2}$ is 1 nA , what is the droop rate during the "hold" state?

For both the S/H circuit and the peak detector, an opamp drives a capacitive load. When designing such circuits, make sure you choose an op-amp that is stable at unity gain when loaded by the capacitor $C$. Some op-amps, (e.g., the LT1457, a member of Linear Technology's "CLOAD" ${ }^{\mathrm{TM}}$ stable" op-amps) are specifically designed to drive large $(0.01 \mu \mathrm{~F})$ capacitive loads directly. Some other tricks you can use are discussed in §4.6.1B and in Chapter $4 x$.

You don't have to design S/H circuits from scratch, because there are nice monolithic ICs that contain all the parts you need. National's LF398 is a popular part, containing the FET switch and two op-amps in an inexpensive (\$1.25) 8-pin package. Figure 4.60B shows how to use it. Note how feedback closes the loop around both op-amps. There are plenty of fancy S/H chips available, if you need better performance than the LF398 offers. For example, the AD783 from Analog Devices includes an internal capacitor and guarantees a maximum acquisition time of $0.4 \mu \mathrm{~s}$ for $0.01 \%$ accuracy following a 5 volt step.
image_name:Figure 4.61
description:
[
name: A1, type: OpAmp, value: A1, ports: {InP: +15, InN: Vin, OutP: Vout, OutN: , Vdd: , -Vdd:}
name: D, type: Diode, ports: {Na: Vout, Nc: Out(A1)}
name: 2k, type: Resistor, value: 2k, ports: {N1: Vin, N2: InN(A1)}
name: 10k, type: Resistor, value: 10k, ports: {N1: +15, N2: InP(A1)}
name: 20k, type: Resistor, value: 20k, ports: {N1: InP(A1), N2: GND}
]
extrainfo:The circuit is an active clamp that uses an op-amp to control the output voltage. The diode prevents the output from going below the op-amp output. The resistors set a reference voltage for the op-amp input.

Figure 4.61. Active clamp.
image_name:Figure 4.62
description:The graph in Figure 4.62 illustrates the behavior of an active clamp circuit, focusing on the output voltage glitches caused by the finite slew-rate of the operational amplifier (op-amp).

1. Type of Graph and Function:
This is a time-domain waveform graph showing the relationship between input voltage \( V_{in} \), output voltage \( V_{out} \), and the op-amp output over time.

2. Axes Labels and Units:
- The horizontal axis represents time \( t \), though specific units are not labeled.
- The vertical axis represents voltage in volts, with key levels marked at +10 volts (\( V_{clamp} \)) and +15 volts.

3. Overall Behavior and Trends:
- The graph shows \( V_{in} \) initially increasing linearly until it reaches the clamping threshold of +10 volts. At this point, \( V_{out} \) follows \( V_{in} \) until the clamp engages.
- When \( V_{in} \) exceeds +10 volts, the output \( V_{out} \) is clamped at +10 volts due to the feedback loop involving the diode.
- The op-amp output initially rises to +15 volts, indicating saturation, and then follows \( V_{in} \) until clamping occurs.

4. Key Features and Technical Details:
- The graph highlights small glitches in \( V_{out} \) when \( V_{in} \) transitions through the clamping threshold. These glitches are due to the finite slew-rate of the op-amp, which causes a delay in the op-amp's response.
- The op-amp output is shown as a dashed line, indicating its behavior as it attempts to keep up with \( V_{in} \) changes.

5. Annotations and Specific Data Points:
- The graph includes annotations for \( V_{clamp} \) at +10 volts and labels the glitches in \( V_{out} \).
- The input voltage \( V_{in} \) is shown exceeding +10 volts, causing the clamp action, and then returning below the threshold, allowing \( V_{out} \) to follow \( V_{in} \) again.

This graph effectively demonstrates how the active clamp circuit manages to maintain the output voltage within a specified range despite rapid changes in input voltage, illustrating the impact of the op-amp's slew-rate limitations on circuit performance.

Figure 4.62. Finite slew-rate causes clamp output "glitches".

### 4.5.3 Active clamp

Figure 4.61 shows a circuit that is an active version of the clamp function we discussed in Chapter 1. For the values shown, $V_{\text {in }}<+10$ volts puts the op-amp output at positive saturation, and $V_{\text {out }}=V_{\text {in }}$. When $V_{\text {in }}$ exceeds +10 volts the diode closes the feedback loop, clamping the output at 10 volts. In this circuit, op-amp slew-rate limitations allow small glitches as the input reaches the clamp voltage from below (Figure 4.62).

Exercise 4.17. The active clamp in Figure 4.61 suffers from a slew-rate speed limitation similar to that of the peak tracker of Figure 4.58A. Figure out an improvement to the clamp circuit, analogous to the trick used in Figure 4.58B.

### 4.5.4 Absolute-value circuit

The circuit shown in Figure 4.63 gives a positive output equal to the magnitude of the input signal; it is a full-wave rectifier. As usual, the use of op-amps and feedback eliminates the diode drops of a passive full-wave rectifier.

You can imagine situations in which you want an output proportional to the logarithm of the absolute value. A simple circuit change might be to substitute a diode (or transistor with base tied to collector) for the feedback resistor of the second op-amp, exploiting the Ebers-Moll relation between diode voltage and summing-junction current. As we will see in Chapter $4 x$, this is the basis of the logarithmic amplifier; the circuit needs a few
image_name:Figure 4.63. Active full-wave rectifier.
description:
[
name: Vin, type: VoltageSource, ports: {Np: Vin, Nn: GND}
name: R1, type: Resistor, value: R, ports: {N1: Vin, N2: InN(A1)}
name: R2, type: Resistor, value: R, ports: {N1: InN(A1), N2: X1}
name: R3, type: Resistor, value: R, ports: {N1: X1, N2: InN(A2)}
name: R4, type: Resistor, value: R/2, ports: {N1: InN(A2), N2: Out(A2)}
name: D1, type: Diode, ports: {Na: InN(A1), Nc: Out(A1)}
name: D2, type: Diode, ports: {Na: X1, Nc: Out(A1)}
name: A1, type: OpAmp, value: A1, ports: {InP: GND, InN: InN(A1), OutP: Out(A1)}
name: A2, type: OpAmp, value: A2, ports: {InP: X1, InN: InN(A2), OutP: Out(A2)}
]
extrainfo:This circuit is an active full-wave rectifier. It uses two operational amplifiers, A1 and A2, along with diodes D1 and D2, to rectify the input signal Vin(t). The output voltage Vout(t) is equal to the absolute value of the input voltage Vin(t). The circuit efficiently converts both the positive and negative half-cycles of the input signal to a positive output.

Figure 4.63. Active full-wave rectifier.
image_name:Figure 4.63
description:
[
name: R1, type: Resistor, value: 10k 1%, ports: {N1: Vin, N2: X}
name: R2, type: Resistor, value: 10k 1%, ports: {N1: InN(A2), N2: Vout}
name: R3, type: Resistor, value: 5k, ports: {N1: Vin, N2: X}
name: A1, type: OpAmp, value: TLC2272, ports: {InP: GND, InN: X, OutP: Out(A1)}
name: A2, type: OpAmp, ports: {InP: X, InN: InN(A2), OutP: Vout}
name: D1, type: Diode, ports: {Na: X, Nc: Out(A1)}
]
extrainfo:This circuit is an active full-wave rectifier using op-amps A1 and A2, and diodes to rectify the input signal Vin(t). The output voltage Vout(t) is the absolute value of Vin(t), converting both positive and negative cycles to a positive output.

Figure 4.64. Another full-wave rectifier; note that ground is the negative supply voltage for $\mathrm{IC}_{2}$.
additional components, however, to compensate for the temperature coefficient of $V_{\mathrm{BE}}$.

Exercise 4.18. Figure out how the circuit in Figure 4.63 works. Hint: apply first a positive input voltage and see what happens; then do negative.

Figure 4.64 shows another absolute-value circuit. It is readily understandable as a simple combination of an optional inverter $\left(\mathrm{IC}_{1}\right)$ and an active clamp $\left(\mathrm{IC}_{2}\right)$. For negative input levels the clamp holds point $X$ at ground, making $\mathrm{IC}_{1}$ a unity-gain inverter; for positive input levels, the clamp is out of the circuit, with its output at negative saturation, making $\mathrm{IC}_{1}$ a follower. Thus the output is equal to the absolute value of the input voltage. By running $\mathrm{IC}_{2}$ from a single positive supply, you avoid problems of slew-rate limitations in the clamp, since its output moves over only one diode drop. Note that no great accuracy is required of $R_{3}$.

### 4.5.5 A closer look at the integrator

We introduced the op-amp integrator in $\S 4.2 .6$, before dealing with input bias current and offset voltage. One problem with that circuit (Figure 4.16) is that the output tends
image_name:Figure 4.65
description:
[
name: Vin, type: VoltageSource, ports: {Np: Vin, Nn: GND}
name: R, type: Resistor, value: 1M, ports: {N1: Vin, N2: N1}
name: Iin, type: CurrentSource, ports: {Np: N1, Nn: GND}
name: C, type: Capacitor, value: 0.1uF, ports: {Np: N2, Nn: Vout}
name: OpAmp, type: OpAmp, ports: {InP: GND, InN: N1, OutP: Vout}
]
extrainfo:The circuit is an integrator using an op-amp with a feedback capacitor and input resistor. The op-amp's bias current and offset voltage can cause errors in the integration process. The table provides current error values for different op-amps, indicating their suitability for precision applications.
image_name:Current Error
description:The image displays a schematic diagram of an op-amp integrator circuit and a table detailing the current error for different op-amps.

### Circuit Diagram:
- **Components**:
- A resistor labeled as \(R\) with a value of 1MΩ connected to the input voltage \(V_{in}\).
- An operational amplifier (op-amp) with input bias currents \(I_B\) and offset voltage \(V_{os}\).
- A capacitor \(C\) with a value of 0.1µF connected in feedback with the op-amp.
- **Inputs**:
- \(V_{in}\) or \(I_{in}\) can be used as inputs.
- **Output**:
- The output voltage \(V_{out}\) is expressed as \(\frac{1}{C} \int I_{in} \, dt = \frac{1}{RC} \int V_{in} \, dt\).

### Table: Current Error
- **Columns**:
- "always" showing \(I_e = I_B\) and \([+ \frac{V_{os}}{R}]\)
- "if voltage input" indicating total current error for \(I_{input}\) and \(V_{input}\)
- **Op-Amps**:
- **OP27E**:
- \(I_B = 40nA\)
- \([+ 25pA] (25µV/1M)\)
- \(I_{input} = 40nA\)
- \(V_{input} = 40nA\)
- **LMC6042A**:
- \(I_B = 4pA\)
- \([+ 3nA] (3mV/1M)\)
- \(I_{input} = 0.004nA\)
- \(V_{input} = 3nA\)
- **OP97E**:
- \(I_B = 100pA\)
- \([+ 25pA] (25µV/1M)\)
- \(I_{input} = 0.1nA\)
- \(V_{input} = 0.13nA\)

Figure 4.65. Integrator errors: bias current and offset voltage.
to wander off, even with the input grounded, because of op-amp offsets and bias current (there's no feedback at dc, which violates the third item in §4.2.7). This problem can be minimized by using a FET op-amp for low input current and offset, trimming the op-amp input offset voltage, and using large $R$ and $C$ values. Furthermore, in applications in which the integrator is zeroed periodically by closing a switch placed across the capacitor (Figures 4.18A-C), only the drift over short time scales matters.

It's worth looking at this in a bit more detail. Look at the integrator in Figure 4.65, shown with a choice of voltage input $V_{\text {in }}$ (which, in the absence of op-amp errors, produces a current into the summing junction of $I=V_{\text {in }} / R$ ), or a current input $I_{\text {in }}$ (in which case you omit the input resistor $R$ ). The ideal integrator produces an output

$$
V_{\text {out }}(t)=-\frac{1}{C} \int I_{\text {in }}(t) d t=-\frac{1}{R C} \int V_{\text {in }}(t) d t
$$

It's easy enough to figure out the effect of the op-amp's input errors $I_{\mathrm{B}}$ and $V_{\mathrm{OS}}$. Let's first take the case of an integrator circuit with current input. ${ }^{30}$ The op-amp's bias current $I_{\mathrm{B}}$ adds (or subtracts) from the true input current $I_{\mathrm{in}}$; in the absence of any external input current the integrator's output would ramp at a rate $d V_{\text {out }} / d t=I_{\mathrm{B}} / C$. The effect of op-amp input offset voltage, on the other hand, is simply

[^40]to offset the output voltage by $V_{\mathrm{OS}}$, without ramping; ${ }^{31}$ so, when you reset the integrator by shorting the feedback capacitor $C$, the output goes to a voltage equal to $V_{\mathrm{OS}}$ rather than zero.

Let's look at some actual values. In Figure 4.65 we've chosen, rather arbitrarily, values of $0.1 \mu \mathrm{~F}$ for $C$ and (for voltage input) $1 \mathrm{M} \Omega$ for $R$. So a positive input current of $1 \mu \mathrm{~A}$ produces an output ramp of $-10 \mathrm{~V} / \mathrm{s}$. If we were to choose the precision bipolar OP27E, its relatively high input current of $\pm 40 \mathrm{nA}$ (max) would cause an output ramp of as much as $d V_{\text {out }} / d t=I_{B} / C= \pm 0.4 \mathrm{~V} / \mathrm{s}$.

This isn't good, particularly if you want to integrate for a few seconds or more. So let's fix things by choosing an op-amp that excels in low bias current, for example the CMOS LMC6041A (the suffixes denote the particular grade; we've chosen the best in all cases). It has a specified maximum bias current of 4 pA over its temperature range (but an astounding 32 "typical" value of 2 fA , or $2 \times 10^{-15} \mathrm{~A}$ ). Now the worst-case output ramp, in the absence of any input signal current, is reduced to $d V_{\text {out }} / d t=I_{\mathrm{B}} / C= \pm 40 \mu \mathrm{~V} / \mathrm{s}$. The "typical" ramping rate is 2000 times smaller, if the specs can be believed; that's a mere $0.02 \mu \mathrm{~V} / \mathrm{s}$.

At this point, the lesson seems to be that the best opamp for any integrator is the one with the smallest bias current $I_{\mathrm{B}}$. But, alas, life is more complicated. In particular, if the integrator is wired for voltage input, with a series input resistor $R$, then the op-amp's offset voltage $V_{\mathrm{OS}}$ now produces a ramp when the input to the circuit is held at ground. Imagine the input is grounded ( $V_{\mathrm{in}}=0$ ), and think about it this way: the op-amp strives to align its inputs with a voltage $V_{\text {OS }}$ between them; that small voltage then produces a current $I=V_{\mathrm{OS}} / R$ through the input resistor. That current has to come through the feedback capacitor, that is, the output must ramp to produce the current needed to satisfy the op-amp's twisted belief that its inputs should differ by $V_{\mathrm{OS}}$. Another way to say it is that the current acts just like an input current of $I=-V_{\mathrm{OS}} / R$.

Now the choice of op-amp is not so clear! Look at Figure 4.65 again. The CMOS op-amp with its very low bias current has a pretty large offset voltage, $V_{\mathrm{OS}}=3 \mathrm{mV}$ (max). So in this circuit it can produce an equivalent input current of $3 \mathrm{nA}(3 \mathrm{mV}$ across $1 \mathrm{M} \Omega)$; that's nearly a thousand times

[^41]larger than the worst-case contribution of its bias current, and it's getting into the same ballpark as the input current of the OP27E bipolar op-amp we considered first.

If minimum drift is needed with these particular circuit values, the solution is to choose an op-amp with the best compromise of low bias current and low offset voltage; to be precise, it should have the minimum value of the total worst-case error current $I_{\mathrm{E}}=I_{\mathrm{B}}+V_{\mathrm{OS}} / R$. A good choice would be the bipolar OP97E, a precision (low-offset) opamp with internal bias-cancellation circuitry. It sports maximum values of $I_{\mathrm{B}}=0.1 \mathrm{nA}$ and $V_{\mathrm{OS}}=25 \mu \mathrm{~V}$; the corresponding worst-case current error is $I_{\mathrm{E}}=0.125 \mathrm{nA}$, which is 25 times better than that of the LMC6041A and 320 times better than that of the OP27.

Note that the relative contribution of $V_{\mathrm{OS}}$ and $I_{\mathrm{B}}$ to integrator error is scaled by the value of $R$. So you can simply choose a larger resistor value if you have an op-amp with excellent $I_{\mathrm{B}}$ but only modest $V_{\mathrm{OS}}$.

If the residual drift of an integrator circuit is still too large for a given application, or if long-term accuracy is unimportant, one solution is to put a large resistor $R_{2}$ across $C$ to provide dc feedback for stable biasing, as shown in Figure 4.18D. The effect is to roll off the integrator action at very low frequencies, $f<1 / R_{2} C$. The feedback resistor may become rather large in this sort of application. Figure 4.66 shows a trick for producing the effect of a large feedback resistor using smaller values in any op-amp circuit. In this case - an inverting amplifier circuit - the feedback network behaves like a single $10 \mathrm{M} \Omega$ resistor, thus producing a voltage gain of -100 . This technique has the advantage of using resistors of convenient values without the problems of stray capacitance, etc., that occur with very large resistor values. Note that this "T-network" trick may increase the effective input offset voltage if used in a transresistance configuration (§4.3.1C). For example, the circuit of Figure 4.66, driven from a high-impedance source (e.g., the current from a photodiode, with the input resistor omitted), has an output offset of 100 times $V_{\text {OS }}$, whereas the same circuit with a $10 \mathrm{M} \Omega$ feedback resistor has an output equal to $V_{\mathrm{OS}}$ (assuming the offset that is due to input current is negligible).

### 4.5.6 A circuit cure for FET leakage

Sometimes a circuit technique is so elegant and fascinating that we feel compelled to tell others about it. That's the case for the circuit in this section, brought over and updated from our 2nd edition. Read it and delight in its cleverness; but then check our remarks in the concluding paragraph.

In the integrator with a FET reset switch (Figure 4.18),
image_name:Figure 4.66
description:
[
name: R1, type: Resistor, value: 100k, ports: {N1: LOAD, N2: InN(A1)}
name: R2, type: Resistor, value: 100k, ports: {N1: InN(A1), N2: X1}
name: R3, type: Resistor, value: 1.02k, ports: {N1: X1, N2: GND}
name: R4, type: Resistor, value: 51k, ports: {N1: InP(A1), N2: GND}
name: A1, type: OpAmp, value: A1, ports: {InP: InP(A1), InN: InN(A1), OutP: Out(A1), OutN: GND}
]
extrainfo:The circuit is a T-network connected to an op-amp, simulating a large-value resistor. It is used to address FET leakage in an integrator circuit.

Figure 4.66. "T-network" simulates large-value resistor (here $10 \mathrm{M} \Omega$ ).
drain-source leakage sources a small current into the summing junction even when the FET is OFF. With an ultra-low-input-current op-amp and low-leakage capacitor, this can be the dominant error in the integrator. For example, the excellent LMC6001A JFET-input "electrometer" op-amp has a maximum input current of 0.025 pA , and a high-quality $0.1 \mu \mathrm{~F}$ metallized Teflon or polystyrene capacitor specifies leakage resistance as $10^{7}$ megohms, minimum. Thus the integrator, exclusive of reset circuit, keeps stray currents at the summing junction below 1 pA (for a worst-case 10 V full-scale output), corresponding to an output $d V / d t$ of less than $0.01 \mathrm{mV} / \mathrm{s}$. Compare this with the leakage contribution of a MOSFET such as the SD210 (enhancement mode), which specifies a maximum leakage current of 10 nA at $V_{\mathrm{DS}}=10 \mathrm{~V}$ and $V_{\mathrm{GS}}=-5 \mathrm{~V}$ ! In other words, the reset FET can contribute up to 10,000 times as much leakage as everything else combined.

Figure 4.67 shows a clever circuit solution. Although both $n$-channel MOSFETs are switched together, $Q_{1}$ is switched with gate voltages of 0 and +15 volts so that gate leakage (as well as drain-source leakage) is entirely eliminated during the OFF state (zero gate voltage). In the ON state the capacitor is discharged as before, but with twice $R_{\mathrm{ON}}$. In the OFF state, $Q_{2}$ 's small leakage passes to ground through $R_{2}$ with negligible drop. There is no leakage current at the summing junction because $Q_{1}$ 's source, drain, and substrate are all at the same voltage. (Sharpeyed readers may have noticed that the virtual ground at the op-amp's inverting input is imperfect to the extent of its offset voltage $V_{\mathrm{OS}} .{ }^{33}$ This can be trimmed to eliminate completely any leakage current from $Q_{1}$.)

The ultimate limit to capacitor "droop" in this circuit, once FET switch leakage has been eliminated, is set by the op-amp's input current and by the capacitor's selfdischarge. The capacitor shown has a specified ${ }^{34}$ leakage

[^42]image_name:Figure 4.67
description:
[
name: R1, type: Resistor, value: 100M, ports: {N1: InN(A1), N2: GND}
name: R2, type: Resistor, value: 100k, ports: {N1: X3, N2: GND}
name: C1, type: Capacitor, value: 100nF, ports: {Np: Out(A1), Nn: InN(A1)}
name: Q1, type: PMOS, ports: {S: X1, D: X3, G: GND}
name: Q2, type: PMOS, ports: {S: X2, D: X3, G: -15}
name: D, type: Diode, ports: {Na: X1, Nc: X2}
name: A1, type: OpAmp, value: LMC6001A, ports: {InP: GND, InN: InN(A1), OutP: Out(A1), OutN: GND}
]
extrainfo:The circuit is designed to minimize leakage currents using PMOS transistors Q1 and Q2. The LMC6001A op-amp is used for its low bias current characteristics, contributing to the low droop rate of the capacitor C1. The diode D provides a path for current between nodes X1 and X2.

Figure 4.67. MOSFET leakage defeated by clever circuit.
resistance of $10^{7} \mathrm{M} \Omega$, i.e., $10^{13} \Omega$. The resulting leakage currents, of order $10^{-16} \mathrm{~A}$ (following reset), are entirely negligible compared with op-amp bias currents. For the opamp shown, the specified bias current is 25 fA maximum (10 fA typ) at $25^{\circ} \mathrm{C}$; that bias current produces a maximum droop of $0.25 \mu \mathrm{~V} / \mathrm{s}$. There are no op-amps with lower specified maximum bias current currently available; but you can find op-amps whose "typical" bias current is lower for example, the LMC6041, an inexpensive op-amp whose datasheet proclaims $I_{\mathrm{B}}=2 \mathrm{fA}$ (typ) at $25^{\circ} \mathrm{C}$ (no maximum is given at room temperature; $I_{\mathrm{B}}=4 \mathrm{pA}$ max over the full temperature range). What is one to make of an op-amp whose typical input current is 2000 times smaller than the guaranteed maximum? Just that the manufacturer knows that it's very good, but it's too painful to test in production. You'd do well to use these inexpensive units in such a circuit if you're willing to screen the op-amps yourself; otherwise pay the bounty for a unit that has a guaranteed limit (but note that the LMC6001A, such a unit, has a typi$\mathrm{cal} I_{\mathrm{B}}$ that is five times higher than that of the less expensive LMC6041).

When designing circuits where low input current is needed, watch out for temperature effects: all FET opamps (both JFET and CMOS types) exhibit dramatic increases in input current with rising temperature, typically doubling each $10^{\circ} \mathrm{C}$; the LMC6001A's guaranteed maximum bias current jumps from 25 fA at $25^{\circ} \mathrm{C}$ to 2000 fA at $85^{\circ} \mathrm{C}$. At high temperatures, the input (leakage) currents

[^43]of FET op-amps may often be higher than the input (bias) currents of low- $I_{\mathrm{B}}$ bipolar types; that is because leakage currents rise exponentially with temperature, whereas transistor bias currents remain roughly constant (or decrease slightly). Look back at Figure 3.48 for a good illustration; see also Figures 5.6 and 5.38.

It may be difficult to find discrete low-capacitance MOSFETs with substrate pins; currently the SD210 family (with SST-prefix SMT versions) is available from Linear Systems (Fremont, CA). The two-switch T-configuration is sound, though it may be challenging to find suitable switch components without substrate-diode conduction, etc. These MOSFETs work well, but if they become "unobtanium" we suggest you modify the circuit to use JFETs, in the manner of Figure 5.5.

### 4.5.7 Differentiators

Differentiators are similar to integrators, but with $R$ and $C$ reversed (Figure 4.68). Because the inverting input is at ground, the rate of change of input voltage produces a current $I=C\left(d V_{\text {in }} / d t\right)$ and hence an output voltage

$$
\begin{equation*}
V_{\mathrm{out}}=-R C \frac{d V_{\mathrm{in}}}{d t} \tag{4.7}
\end{equation*}
$$

Differentiators are bias stable, but they generally have problems with noise and instabilities at high frequencies because of the op-amp's high gain and internal phase shifts. For this reason it is necessary to roll off the differentiator action at some maximum frequency. The usual method is shown in Figure 4.69. The choice of the rolloff components $R_{1}$ and $C_{2}$ depends on the noise level of the signal and the bandwidth of the op-amp, with larger values providing greater stability and less noise, at the expense of differentiator bandwidth. A minimum recommended value for $R_{1}$ is given by $R_{1}=0.5 \sqrt{R_{2} / C_{1} f_{\mathrm{T}}} ; C_{2}$ can be added for further noise reduction, with a starting value of $C_{2} \approx C_{1} R_{1} / R_{2}$. At high frequencies $\left(f \gg 1 / 2 \pi R_{1} C_{1}\right)$ this circuit becomes an integrator because of $R_{1}$ and $C_{2}$. We'll explain what's going on here in more detail in §4.9.3.
image_name:Figure 4.68
description:
[
name: C, type: Capacitor, value: C, ports: {Np: Vin, Nn: N1}
name: R, type: Resistor, value: R, ports: {N1: N1, N2: Vout}
name: OpAmp1, type: OpAmp, ports: {InP: GND, InN: N1, OutP: Vout, OutN: ''}
]
extrainfo:This is an op-amp differentiator circuit. The capacitor C and resistor R form the differentiating network. The op-amp is configured with its non-inverting input grounded and the inverting input connected to the junction of R and C.
image_name:Figure 4.69
description:
[
name: C, type: Capacitor, value: C, ports: {Np: Vin, Nn: N1}
name: R, type: Resistor, value: R, ports: {N1: N1, N2: Vout}
name: OpAmp, type: OpAmp, ports: {InP: GND, InN: N1, OutP: Vout, OutN: GND}
]
extrainfo:The circuit is a stabilized op-amp differentiator with added resistor R and capacitor C.

Figure 4.68. Op-amp differentiator (noisy, probably unstable!).
image_name:Figure 4.69
description:
[
name: R1, type: Resistor, value: 1k, ports: {N1: LOAD, N2: X}
name: C1, type: Capacitor, value: 10nF, ports: {Np: X, Nn: InN(A1)}
name: R2, type: Resistor, value: 100k, ports: {N1: Out(A1), N2: InN(A1)}
name: C2, type: Capacitor, value: 50pF, ports: {Np: InN(A1), Nn: Out(A1)}
name: A1, type: OpAmp, value: A1, ports: {InP: GND, InN: InN(A1), OutP: Out(A1), OutN: GND}
]
extrainfo:The circuit is a stabilized op-amp differentiator with added resistor R1 and capacitor C2. It reduces high-frequency noise.

Figure 4.69. Adding $R_{1}$ and $C_{2}$ stabilizes the basic op-amp differentiator (consisting of $C_{1}, R_{2}$, and the op-amp); they also reduce high-frequency noise.

## 4.6 Op-amp operation with a single power supply

Op-amps don't require $\pm 15$ volt regulated supplies. They can be operated from split supplies of lower voltages ${ }^{35}$ or from unsymmetrical supply voltages (e.g, +12 and -3 ), as long as the total supply voltage $\left(V_{+}-V_{-}\right)$is within specifications (see Table 4.1 on page 245 for generic values, and Tables 4.2a,b on pages 271-272 for specific parts). Unregulated supply voltages are often adequate because of the high "power-supply rejection ratio" you get from negative feedback (for the 411 it's 90 dB typ). But there are many occasions when it would be nice to operate an op-amp from a single supply, say +9 volts. This can be done with ordinary op-amps by generating a "reference" voltage above ground, if you are careful about minimum supply voltages, output-swing limitations, and maximum common-mode input range.

In many cases, however, you can simplify these circuits by taking advantage of a class of op-amps designed for single supply operation. With characteristic directness, engineers call these "single-supply op-amps." Their common feature is that both their input common-mode range and their output swing extends to the negative supply rail (i.e., ground, when run from a single positive supply). A subclass of these can swing their outputs to both supplies ("rail-to-rail outputs"), and some of those even permit input swings to both rails ("rail-to-rail I/O"). Keep in mind, though, that operation with symmetrical split supplies should be considered the normal op-amp technique for most applications.

[^44]
### 4.6.1 Biasing single-supply ac amplifiers

For a general-purpose op-amp like the 411, the inputs and output can typically swing to within about 1.5 volts of either supply. With $V_{-}$connected to ground, you can't have either of the inputs or the output at ground; that is, it won't work properly if you drive the inputs to ground, and it simply cannot swing its output to ground.

Thus one reason why the circuit in Figure 4.70 won't work is that the ac-coupled low-level signal from the microphone is centered on ground, where the op-amp will not work. But even if the op-amp's input common-mode range included the negative rail (ground, here), we'd still be in trouble, because in this circuit the amplified output would also be centered on ground (so that it would have to swing both above and below ground). It is important to understand that this problem with the output cannot be solved in this manner - an op-amp simply cannot swing beyond its supply rails. Even an op-amp with rail-to-rail inputs and outputs would not work.

Exercise 4.19. Draw a sketch of the output waveform from the circuit of Figure 4.70, when driven with a 10 mV input sinewave, assuming that the op-amp is of the special class with rail-to-rail inputs and outputs.
image_name:Figure 4.70
description:
[
name: mic, type: Other, ports: {N1: GND, N2: InP(A1)}
name: 0.1uF, type: Capacitor, value: 0.1uF, ports: {Np: InP(A1), Nn: GND}
name: 1M, type: Resistor, value: 1M, ports: {N1: InP(A1), N2: GND}
name: 1k, type: Resistor, value: 1k, ports: {N1: InN(A1), N2: GND}
name: 100k, type: Resistor, value: 100k, ports: {N1: InN(A1), N2: Out(A1)}
name: A1, type: OpAmp, value: A1, ports: {InP: InP(A1), InN: InN(A1), OutP: Out(A1), OutN: GND}
]
extrainfo:The circuit is a single-supply microphone amplifier using an op-amp. The input signal is AC-coupled through a capacitor, and the op-amp is configured with feedback resistors for amplification. The op-amp has rail-to-rail inputs and outputs.

Figure 4.70. Defective single-supply microphone amplifier.
image_name:Figure 4.70. Defective single-supply microphone amplifier.
description:
[
name: R1, type: Resistor, value: 220k, ports: {N1: X1, N2: V4}
name: R2, type: Resistor, value: 220k, ports: {N1: V+, N2: X1}
name: R3, type: Resistor, value: 1.0k, ports: {N1: X1, N2: GND}
name: R4, type: Resistor, value: 100k, ports: {N1: InN(A1), N2: X1}
name: R5, type: Resistor, value: 1M, ports: {N1: input, N2: GND}
name: R6, type: Resistor, value: 1M, ports: {N1: output, N2: GND}
name: C1, type: Capacitor, value: 0.22μF, ports: {Np: input, Nn: InN(A1)}
name: C2, type: Capacitor, value: 15μF, ports: {Np: X1, Nn: GND}
name: C3, type: Capacitor, ports: {Np: Out(A1), Nn: output}
name: A1, type: OpAmp, value: LF411, ports: {InP: X1, InN: InN(A1), OutP: Out(A1), OutN: GND}
]
extrainfo:The circuit is a single-supply microphone amplifier using an op-amp. It is configured with feedback resistors for amplification, and the input signal is AC-coupled through a capacitor. The op-amp has rail-to-rail inputs and outputs.

Figure 4.71. A reference voltage at $\frac{1}{2} V_{+}$(created by divider $R_{1} R_{2}$ ) allows single-supply operation with an ordinary op-amp.
image_name:A.
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: V+, N2: InP(A1)}
name: R2, type: Resistor, value: R2, ports: {N1: InP(A1), N2: GND}
name: C, type: Capacitor, value: C, ports: {Np: InP(A1), Nn: GND}
name: A1, type: OpAmp, value: A1, ports: {InP: InP(A1), InN: InN(A1), OutP: Vref, OutN: GND}
]
extrainfo:The circuit in diagram A is a single-supply microphone amplifier using an op-amp. It employs feedback resistors for amplification and AC-couples the input signal through a capacitor. The op-amp has rail-to-rail inputs and outputs. A reference voltage at half of V+ is created by a voltage divider (R1, R2) to allow single-supply operation with an ordinary op-amp. The reference voltage is labeled Vref. The circuit is designed for biasing schemes suitable for single-supply operation as depicted in diagrams B, C, and D.
image_name:B.
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: V+, N2: InP(A1)}
name: R2, type: Resistor, value: R2, ports: {N1: InP(A1), N2: GND}
name: C, type: Capacitor, value: C, ports: {Np: InN(A1), Nn: GND}
name: A1, type: OpAmp, value: A1, ports: {InP: InP(A1), InN: InN(A1), OutP: Vref, OutN: GND}
]
extrainfo:The circuit in diagram B is a biasing scheme for single-supply operation. It utilizes an op-amp configured with feedback resistors R1 and R2 to create a virtual ground (Vref). This allows the op-amp to operate with a single supply voltage V+. The circuit is designed to provide a reference voltage Vref at the output of the op-amp, which is used for biasing purposes.
image_name:C.
description:
[
name: C, type: Capacitor, ports: {Np: V+, Nn: GND}
name: C, type: Capacitor, ports: {Np: Vref, Nn: GND}
name: A1, type: OpAmp, ports: {InP: Vref, InN: Vref, OutP: Vout, OutN: GND}
]
extrainfo:The circuit diagram C shows a single-supply op-amp configuration with feedback resistors for amplification. The input signal is AC-coupled through a capacitor. The op-amp is configured for single-supply operation with a reference voltage at Vref. The circuit is designed to amplify signals with a reference voltage, allowing for single-supply operation.
image_name:D.
description:
[
name: 10k, type: Resistor, value: 10k, ports: {N1: V+, N2: Vref}
name: LM385-2.5, type: Diode, ports: {Na: Vref, Nc: GND}
name: 0.1µF, type: Capacitor, value: 0.1µF, ports: {Np: Vref, Nn: GND}
]
extrainfo:The circuit diagram 'D' is a voltage reference circuit. It uses a 10k resistor, an LM385-2.5 diode, and a 0.1µF capacitor to produce a stable reference voltage of +2.50V. The LM385-2.5 is used as a Zener diode to maintain a constant voltage across it, and the capacitor is used for filtering.

Figure 4.72. Biasing schemes for single-supply operation A. Common reference (also known, confusingly, as a "virtual ground") for multiple stages; note bypass capacitor. B. Follower generates low-impedance reference. C. The reference can serve as the return path for feedback, with significant signal currents. D. Zener-type fixed voltage reference.

#### A. Reference voltage

One solution is to generate a reference voltage somewhere between ground and the positive supply (e.g. at half of $V_{+}$) to bias the op-amp for successful operation (Figure 4.71). This circuit is an audio amplifier with 40 dB gain. Choosing $V_{+}=12 \mathrm{~V}$ and $V_{\text {ref }}=0.5 \mathrm{~V}_{+}$gives an output swing of about 9 volts pp before the onset of clipping. Capacitive coupling is used at the input and output to block the dc level, which equals $V_{\text {ref }}$. The optional resistors should be used if this circuit connects to the outside world; they ensure that there is no dc voltage at the input and output, which prevents loud clicks and pops when external stuff is connected.

The reference voltage can be generated at the op-amp input with a simple resistive divider, as shown. If the circuit requires several op-amp stages, it is simpler to generate a common reference, with a single bias resistor to each stage, as in Figure 4.72A. Be sure to bypass the reference, to prevent signal coupling. You can also buffer the reference with a follower (Figure 4.72B), which is particularly useful if any significant dc or signal currents flow through that path, as in Figure 4.72C. Note that the follower can be any ordinary op-amp, because it is operating with a midsupply signal. In this circuit the reference voltage doesn't have to be half of the supply voltage; it may be best to split the supply unsymmetrically, to allow maximum signal swing. In some instances it may be preferable to put it at a fixed voltage from one rail, using an IC zener-like fixed
reference, as in Figure 4.72D; that rail is then a regulated supply with respect to the common reference.

Contemporary circuit design is moving to lower supply voltages, often in the form of a single positive supply. For operation with a single +5 V supply, for example, a conventional op-amp like the 411 simply will not do: Not only can its outputs not swing typically closer than 1.5 V to the supply rails; in fact, it is not even specified for operation from a total supply voltage of less than 10 V . So for such circuits you should use op-amps designed for low-voltage operation. These are often called "single-supply" op-amps and come in several forms, some of which include specified operation of both inputs and outputs down to the negative rail; others feature output swings to both rails, of which a subset permits both inputs and outputs to go to both rails. We'll deal with these shortly, in §4.6.3.

#### B. Supply splitter

The circuit in Figure 4.72C suggests a different approach to operation with a battery. Instead of piping a line called $V_{\text {ref }}$ around as a signal common, with the negative battery terminal called ground, why not ground the "reference" output, effectively splitting the single supply into a positivenegative pair? This is a common technique in battery operated equipment, and is shown in Figure 4.73. The battery voltage is split by the resistive divider, which feeds a follower to generate a low-impedance common voltage. To
image_name:Figure 4.73
description:
[
name: 9V battery, type: VoltageSource, value: 9V, ports: {Np: V+, Nn: V-}
name: 100k, type: Resistor, value: 100k, ports: {N1: V+, N2: V-}
name: 100k, type: Resistor, value: 100k, ports: {N1: V-, N2: InP(A1)}
name: 0.1μF, type: Capacitor, value: 0.1μF, ports: {Np: V-, Nn: Out(A1)}
name: 1μF, type: Capacitor, value: 1μF, ports: {Np: V+, Nn: GND}
name: 1μF, type: Capacitor, value: 1μF, ports: {Np: V+, Nn: V-}
name: A1, type: OpAmp, value: A1, ports: {InP: InP(A1), InN: V-, OutP: Out(A1), OutN: , Vdd: V+, -Vdd: V-}
]
extrainfo:The circuit is a split-supply generator using an op-amp to create a virtual ground at mid-battery voltage. The op-amp LT1097 is configured as a voltage follower to provide a low-impedance output at half the battery voltage, effectively splitting the 9V supply into +/-4.5V. The capacitors are used for bypassing to maintain low-impedance supply rails.

Figure 4.73. Op-amp split-supply generator. A follower generates a low-impedance mid-battery output voltage, which becomes circuit ground.
the outside world that common voltage is "ground," with both ends of the battery floating.

The output should be bypassed, as always, to maintain low-impedance supply rails, relative to ground, at signal frequencies. That is necessary because ground is usually the common return for filters, biasing networks, loads, etc. Look at almost any normal split-supply circuit and you'll find dc and signal currents flowing into and out of ground.

This raises an interesting problem, which we discuss in detail in Chapter $4 x$ and in 89.1 .1 C , namely that the op-amp's output resistance, in combination with the bypass capacitor, creates a lagging phase shift at high frequencies that can cause the feedback loop to go into oscillation. Some op-amps are designed to circumvent this problem, for example the LT1097 shown in the figure (whose datasheet states that it is stable with any capacitive load). Even so, this circuit exhibits a peak in its output impedance versus frequency (Figure 4.74), and a related effect, namely, a ringing transient with that same characteristic frequency (Figure 4.75); you can think of these effects as the not-quite-banished ghost of an oscillation. As the figures show, a small series damping resistor at the opamp's output (Figure 4.76A) effectively stops this resonant behavior, at the expense of an increase in dc output impedance.

If increased output impedance is undesirable (which often it is not), another approach is to take "slow" feedback downstream of the damping resistor (which preserves accurate dc performance, i.e., low dc output impedance), with a parallel "fast" feedback path from the upstream side (Figure 4.76B) to prevent ringing. You can see the result in Figure 4.75 , where we used $R_{1}=2.7 \Omega, R_{2}=10 \mathrm{k}$, and $C=2.7 \mathrm{nF}$ : the initial transient looks just like that with a $2.7 \Omega$ damping resistor, but then returns to the correct dc level because dc feedback is taken from the point of load. A third possibility is to "overcompensate" the op-amp, for which the LT1097 provides hospitality in the form of a convenient "overcomp" pin; adding a capacitor to ground from this
pin increases the phase margin by shifting the dominant pole downward in frequency (§4.9).

There's a nice integrated solution from Texas Instruments, the TLE2425 and TLE2426 "rail-splitter" ICs. These come in a convenient 3-terminal TO-92 (small transistor) package, draw less than 0.2 mA quiescent current, are stable into any capacitive load greater than $0.33 \mu \mathrm{~F}$, and can source or sink an unbalanced current of 20 mA (Figure 4.77). The TLE2426 splits the rails $50 \%$ with an internal resistive divider, whereas the TLE2425 uses an internal voltage reference to put the output common 2.50 V above the negative rail.
image_name:Figure 4.74
description:Figure 4.74 is a Bode plot depicting the output impedance of a circuit as a function of frequency. The x-axis represents frequency in hertz (Hz), ranging from 100 Hz to 1 MHz, with a logarithmic scale. The y-axis represents impedance in ohms, ranging from 0 to 30 ohms.

The graph features two curves representing impedance under different conditions. Without a damping resistor, the impedance shows a pronounced peak at around 10 kHz, reaching a maximum of approximately 30 ohms. This peak indicates a resonance effect caused by the capacitive load.

With a 5-ohm damping resistor, the peak is significantly reduced, demonstrating the effectiveness of the resistor in minimizing the resonance. The impedance at the peak is lower, and the curve is more flattened, indicating a more stable impedance across the frequency range.

Overall, the graph illustrates how a damping resistor can effectively reduce the impedance peak caused by capacitive loading, leading to a more stable output impedance across a wide range of frequencies.

Figure 4.74. One effect of the capacitive load is a bump in the output impedance, which is greatly reduced with a $5 \Omega$ damping resistor; see text.
image_name:Figure 4.75
description:The graph in Figure 4.75 is a time-domain waveform illustrating the measured output voltage transient of a rail-splitter circuit in response to a 4.5 mA load current step. The graph displays several curves, each representing a different value of series damping resistor ($R_S$), and one curve for a 'split feedback' configuration.

Axes and Units:
- **X-axis:** Time, with a scale of $40 \mu s / \text{div}$.
- **Y-axis (left):** Load current, scaled at $5 \text{mA} / \text{div}$.
- **Y-axis (right):** Output voltage, scaled at $10 \text{mV} / \text{div}$, with AC coupling.

Overall Behavior and Trends:
- The load current step is represented by a sharp rise on the left side of the graph.
- The output voltage shows a transient response that varies with different damping resistor values.
- Without a damping resistor ($R_S = 0 \Omega$), the output voltage exhibits significant ringing.
- As the damping resistor value increases ($R_S = 2.7 \Omega$ and $R_S = 6.8 \Omega$), the ringing is progressively reduced, showing more stability with higher resistance.
- The 'split feedback' configuration with $R_S = 2.2 \Omega$ also reduces ringing but to a lesser extent than the higher resistor values.

Key Features and Technical Details:
- **$R_S = 0 \Omega$:** High amplitude oscillations are observed immediately after the current step.
- **$R_S = 2.7 \Omega$:** The oscillations are dampened significantly, with reduced amplitude and frequency.
- **$R_S = 6.8 \Omega$:** The transient response is the most stable, with minimal oscillations.
- **Split feedback ($R_S = 2.2 \Omega$):** Provides a compromise between stability and reduced ringing, showing moderate oscillations.

Annotations and Specific Data Points:
- The graph includes annotations indicating the different $R_S$ values and the split feedback configuration.
- The load current step is consistent across all configurations, providing a clear baseline for comparing the impact of the damping resistor on the output voltage transient.

This graph effectively demonstrates how varying the series damping resistor affects the transient response of the rail-splitter circuit, highlighting the trade-off between damping oscillations and maintaining low DC output impedance.

Figure 4.75. Measured output voltage transient of the rail-splitter circuit of Figure 4.76 A caused by a 4.5 mA load current step, with several values of series damping resistor. The latter eliminates ringing, at the expense of dc output impedance. An alternative is the "split-feedback" scheme of Figure 4.76B. Scales: $5 \mathrm{~mA} / \mathrm{div}$ and $10 \mathrm{mV} / \mathrm{div}$; $40 \mu \mathrm{~s} / \mathrm{div}$.
image_name:Figure 4.76A
description:
[
name: A1, type: OpAmp, value: A1, ports: {InP: InP(A1), InN: InN(A1), OutP: Out(A1), OutN:}
name: 220, type: Resistor, value: 220, ports: {N1: Out(A1), N2: V-}
name: 1μF, type: Capacitor, value: 1μF, ports: {Np: V-, Nn: GND}
]
extrainfo:The circuit in Figure 4.76A is a rail-splitter circuit using an operational amplifier with a decoupling resistor (220 ohms) and a capacitor (1μF) to stabilize the output voltage. The output is connected to ground through the capacitor, providing a low impedance path for AC signals while maintaining DC stability.
image_name:Figure 4.76B
description:
[
name: A1, type: OpAmp, value: A1, ports: {InP: InP, InN: InN, OutP: Out, OutN:}
name: R1, type: Resistor, value: 100, ports: {N1: Out, N2: V-}
name: R2, type: Resistor, value: 10k, ports: {N1: InN, N2: V-}
name: C1, type: Capacitor, value: 10nF, ports: {Np: InN, Nn: Out}
name: C2, type: Capacitor, value: 1uF, ports: {Np: V-, Nn: GND}
]
extrainfo:The circuit is a split-feedback rail-splitter with fast and slow feedback paths for stabilization. The op-amp A1 is used with resistors R1 and R2, and capacitors C1 and C2 to manage damping and output impedance.

Figure 4.76. Stabilizing the split-supply generator: A. Decoupling resistor, B. Decoupling resistor with fast and slow feedback paths.
image_name:Figure 4.77
description:
[
name: 9V battery, type: VoltageSource, value: 9V, ports: {Np: V+, Nn: V-}
name: TLE2426, type: Other, ports: {N1: IN, N2: OUT, N3: COM}
name: Capacitor1, type: Capacitor, value: 1µF, ports: {Np: V+, Nn: OUT}
name: Capacitor2, type: Capacitor, value: 1µF, ports: {Np: OUT, Nn: GND}
name: Switch, type: Switch, ports: {N1: V+, N2: 9V battery}
]
extrainfo:This circuit is an integrated 3-terminal rail splitter using the TLE2426. It converts a single supply voltage into a split supply voltage with V+ and V- outputs. The capacitors are used for stabilization and decoupling.
image_name:TO-92
description:The image depicts a circuit schematic featuring a 3-terminal rail splitter, specifically using the TLE2426 component housed in a TO-92 package. The circuit is powered by a 9V battery. The TLE2426 is a precision voltage regulator that serves as a rail splitter, providing a virtual ground (COM) at half the supply voltage.

**Identification of Components and Structure:**
1. **9V Battery:** The power source for the circuit, providing a supply voltage.
2. **TLE2426 (TO-92 Package):** A 3-terminal integrated circuit used as a rail splitter. It has three pins labeled IN, OUT, and COM.
3. **Capacitors:** Two 1µF capacitors are connected in the circuit. One is connected between the OUT pin and GND, and the other between the COM pin and GND.

**Connections and Interactions:**
- The positive terminal of the 9V battery is connected to the IN pin of the TLE2426, while the negative terminal is connected to V-.
- The OUT pin of the TLE2426 provides the split voltage, which is half of the input voltage, and is connected to V+.
- The COM pin acts as a virtual ground (GND) for the circuit.
- The capacitors are used for decoupling, ensuring stability by filtering out noise and providing a stable output.

**Labels, Annotations, and Key Features:**
- The TLE2426 is clearly labeled, indicating its function as a rail splitter.
- The schematic includes clear annotations for the battery, capacitor values, and the TO-92 package configuration of the TLE2426.
- The diagram also illustrates the pin configuration of the TO-92 package, with the OUT, IN, and COM pins clearly marked.

Figure 4.77. Integrated 3-terminal rail splitter.

### 4.6.2 Capacitive loads

This particular example of a supply-splitter illuminates a more general problem, namely, the effect of capacitive loading at the output of any op-amp circuit. Although we'll deal with this further in the advanced Chapter $4 x$, it's important to appreciate now the causes, and cures, because it can cause mischief in even the simplest of op-amp circuits.

Let's say you build a little box, with some op-amps inside and the output(s) brought out through the ever-popular BNC panel connectors. It's easy to forget that something like a length of shielded cable - say a 2 m BNC cable going from an output connector to some other instrument has plenty of capacitance: the standard RG-58 shielded cable patch cords have 100 pF per meter (see Appendix H). So an innocuous connecting cable alone loads the op-amp's output with 200 pF . That's sometimes enough to make an op-amp follower oscillate (we rig up just such a demonstration in our circuit design class, where an LF411 follower screams loudly when asked to drive 8 ft of cable). And even if it doesn't break into oscillation, it will likely exhibit response peaks at high frequencies, evident as overshoot and ringing.

The causes are the same as with the supply splitter: the capacitive load creates a lagging phase shift, and it's within the feedback loop. ${ }^{36}$

And the possible cures are the same (Figure 4.78); taking the figure's circuits in order (A-E):

- You can add a small series resistor (perhaps $25-100 \Omega$ ) at the op-amp's output, outside the feedback loop. (It's quite common to see a $50 \Omega$ output resistor, which forms a matched source to " $50 \Omega$ cable"; see Appendix H.) This is OK , and easy; but it does mean that feedback does not act on the actual output signal, which may be significant with nasty loads, or at high frequencies, etc.
image_name:A
description:
[
name: OpAmp_A, type: OpAmp, ports: {InP: V+, InN: V-, OutP: N1, OutN:}
name: 50Ω, type: Resistor, value: 50Ω, ports: {N1: N1, N2: N2}
name: C_LOAD, type: Capacitor, value: C_LOAD, ports: {Np: N2, Nn: GND}
name: C_CABLE, type: Capacitor, value: C_CABLE, ports: {Np: N2, Nn: GND}
]
extrainfo:The circuit in Figure A shows an op-amp driving a capacitive load through a 50Ω resistor. The feedback loop is not closed directly at the load, which can improve stability at high frequencies.
image_name:B
description:
[
name: OpAmp_B, type: OpAmp, ports: {InP: Vin, InN: X1, Out: X2}
name: Resistor_100, type: Resistor, value: 100Ω, ports: {N1: X2, N2: X3}
name: Capacitor_CLOAD, type: Capacitor, value: CLOAD, ports: {Np: X3, Nn: GND}
name: Capacitor_CCABLE, type: Capacitor, value: CCABLE, ports: {Np: X3, Nn: GND}
name: Capacitor_C1, type: Capacitor, value: 1nF, ports: {Np: X2, Nn: X1}
name: Resistor_R1, type: Resistor, value: 10kΩ, ports: {N1: X1, N2: GND}
]
extrainfo:Circuit B is an op-amp based configuration designed to drive capacitive loads. It includes a feedback network with a series resistor and capacitors to stabilize the output. The feedback is split between a resistor and a capacitor to manage high-frequency stability.
image_name:C
description:
[
name: OpAmpC, type: OpAmp, ports: {InP: GND, InN: GND, OutP: Node1}
name: R1, type: Resistor, value: 9k, ports: {N1: Node1, N2: Node2}
name: R, type: Resistor, value: 1k, ports: {N1: Node2, N2: GND}
name: C, type: Capacitor, value: ~10pF, ports: {Np: Node1, Nn: Node2}
name: C, type: Capacitor, value: C_LOAD, ports: {Np: Node1, Nn: GND}
]
extrainfo:The circuit in Diagram C is designed to stabilize driving capacitive loads by using a feedback network consisting of resistors and a capacitor. The op-amp's output is connected through a feedback resistor and capacitor to manage stability and frequency response.
image_name:D
description:
[
name: OpAmp D, type: OpAmp, ports: {InP: Vin, InN: GND, Out: Vout}
name: CLOAD, type: Capacitor, value: CLOAD, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is a basic op-amp configuration designed to drive a capacitive load (CLOAD) while maintaining stability. The op-amp output directly connects to the capacitive load, and the feedback loop is designed to ensure stability into CLOAD.
image_name:E
description:
[
name: OpAmp U1, type: OpAmp, ports: {InP: Vin, InN: GND, Out: N1}
name: Buffer U2, type: Buffer, ports: {In: N1, Out: Vout}
]
extrainfo:The circuit uses an op-amp (U1) followed by a buffer (U2) to drive the load. The buffer ensures stability by providing a bandwidth much greater than the unity-gain bandwidth of the op-amp U1.

Figure 4.78. Driving capacitive loads.

[^45]- You can split the feedback loop, as shown, so that feedback comes directly from the op-amp's output at high frequencies, where instability lurks. And at lower frequencies the feedback accurately controls the signal seen by the load. This is not really a compromise, because those high frequencies are exactly where the thing would oscillate anyway if you were to allow feedback from the load.
- You can reduce the loop gain, for example by increasing the closed-loop gain, to regain stability.
- You can seek an op-amp that guarantees stability into the range of load capacitances you expect. Many op-amps provide good data in the form of plots of "Stability versus Capacitive Load." Figure 4.79 shows an example, taken from the datasheet for the LMC6482.
- You can add a unity-gain buffer, with its low native output impedance, either within or outside the feedback loop. If you add it inside the loop, you need to worry about phase shifts introduced by the buffer; it should have significantly higher $f_{\mathrm{T}}$ than the op-amp, and it's often a good idea to include a $50-100 \Omega$ series resistor at the buffer's input (not shown). You may need to rolloff the op-amp's response with a small capacitor, as in Figure 4.87 on page 274.

### 4.6.3 "Single-supply" op-amps

As we just remarked, some op-amps are designed specifically to allow inputs and outputs to go to the negative rail. These are called "single-supply" (or "ground-sensing") opamps, the idea being that their negative rail is actually tied to ground. The input range actually extends slightly below ground, typically to -0.3 V . In some cases the outputs can swing also to the positive rail ("rail-to-rail output"), and a subset of these permits input swings to (and slightly be-
image_name:Figure 4.79
description:The graph in Figure 4.79 is a stability plot illustrating the relationship between load capacitance and output voltage for an LMC6482 op-amp follower. The op-amp is powered by \( \pm 7.5 \text{ V} \) supplies, and the load resistance \( R_{\text{load}} \) is set to 2 kΩ.

**Type of Graph:**
This is a stability versus capacitive load graph.

**Axes Labels and Units:**
- The x-axis represents the output voltage in volts (V), ranging from \(-6\) to \(+6\) volts.
- The y-axis represents the load capacitance in farads (F), specifically ranging from 10 pF to 10 nF, with a logarithmic scale.

**Overall Behavior and Trends:**
- The graph shows a region where the op-amp is stable, bounded by two curves. Outside this region, the op-amp becomes unstable, particularly at higher load capacitances.
- The stable region is approximately centered around an output voltage of 0 V and extends from about -5 V to +5 V, with varying capacitance limits.

**Key Features and Technical Details:**
- There is a marked area indicating 'unstable' behavior at high load capacitances and extreme output voltages.
- A specific point on the graph is annotated with '25% overshoot,' occurring around an output voltage of +2 V and a load capacitance of approximately 100 pF.

**Annotations and Specific Data Points:**
- The 'unstable' region is hatched, indicating areas where the op-amp's performance is not reliable.
- The '25% overshoot' annotation highlights a significant point of interest, suggesting a potential performance issue at that specific load capacitance and output voltage.

Figure 4.79. Stability versus capacitive load for a LMC6482 opamp follower with $R_{\text {load }}=2 \mathrm{k}$ and $\pm 7.5 \mathrm{~V}$ supplies.
yond) both rails ("rail-to-rail input"). Linear Technology has introduced an exotic new twist - op-amps that permit input swings well beyond the positive rail (they call them "Over-The-Top ${ }^{\mathrm{TM}}$ " amplifiers).

These amplifiers can simplify single-supply circuits because you don't need a midsupply reference, rail splitter, etc. But you have to remember that the output cannot go below ground - so you can't build an audio amplifier like Figure 4.70, whose output would need to swing both sides of ground. Before looking at the characteristics of these op-amps in more detail, let's look at a design example.

#### A. Example: single-supply photometer

Figure 4.80 shows a typical example of a circuit for which single-supply operation is convenient. We discussed a similar circuit earlier under the heading of current-to-voltage converters (and we will go further in Chapter $4 x$ ). Because a photocell circuit might well be used in a portable lightmeasuring instrument, and because the output is known to be positive only, this is a good candidate for a batteryoperated single-supply circuit. $R_{1}$ sets the full-scale output at 5 volts for an input photocurrent of $0.5 \mu \mathrm{~A}$. The small feedback capacitor is added to ensure stability, as we'll explain in §4.9.3. No offset voltage trim is needed in this circuit, since the worst-case untrimmed offset of 10 mV corresponds to a negligible $0.2 \%$ of full-scale meter indication. The TLC27L1 is an inexpensive micropower ( $10 \mu \mathrm{~A}$ supply current) CMOS op-amp with input and output swings to the negative rail. Its low input current ( 0.6 pA , typ, at room temperature ${ }^{37}$ ) makes it good for low-current applications like this. If you choose a bipolar op-amp for this kind of low signal-current circuit, better performance at
image_name:Figure 4.81. Photodiode amplifier with simple bias current cancellation.
description:
[
name: C1, type: Capacitor, value: 10pF, ports: {Np: InN(A1), Nn: Out(A1)}
name: R1, type: Resistor, value: 10M, ports: {N1: InN(A1), N2: Out(A1)}
name: A1, type: OpAmp, value: TLC27L1, ports: {InP: GND, InN: InN(A1), OutP: Out(A1), OutN: GND}
name: photodiode, type: Diode, ports: {Na: GND, Nc: InN(A1)}
]
extrainfo:This circuit is a photodiode amplifier with a simple bias current cancellation. It uses a TLC27L1 op-amp to amplify the current from the photodiode. The output current drives a meter, with a full-scale reading of 0.5 mA and a photodiode current range of 0-500 nA.

Figure 4.80. Single-supply photometer.

[^46]image_name:Figure 4.81
description:
[
name: Rf, type: Resistor, value: Rf, ports: {N1: Out(A1), N2: InN(A1)}
name: D, type: Diode, ports: {Na: GND, Nc: InN(A1)}
name: A1, type: OpAmp, value: A1, ports: {InP: GND, InN: InN(A1), OutP: Out(A1), OutN: GND}
]
extrainfo:This circuit is a photodiode amplifier with bias current cancellation using a TLC27L1 op-amp. It amplifies the current from the photodiode, driving a meter with a full-scale reading of 0.5 mA and a photodiode current range of 0-500 nA.

Figure 4.81. Photodiode amplifier with simple bias current cancellation.
low light levels results if the photodiode is connected as in the circuit shown in Figure 4.81.

It's worth noting that the "current budget" of this circuit is dominated by the output current that drives the meter, which can go as high as $500 \mu \mathrm{~A}$. It's easy to overlook a point like that, blithely assuming that the battery need provide only the op-amp's $10 \mu \mathrm{~A}$ quiescent current. At $10 \mu \mathrm{~A}$ a standard 9 V battery lasts 40,000 hours ( 5 years), whereas with continuous operation at $500 \mu \mathrm{~A}$ it would last a month.

#### B. Single-supply op-amp innards

It's helpful to look at the circuitry of a typical single-supply op-amp, both to understand how these types achieve operation to one or both rails, and also to appreciate some of the subtleties and pitfalls of designing them into your circuits. Figure 4.82 is a simplified schematic of the very popular TLC270 series of CMOS single-supply op-amps. The input stage is a $p$-channel MOSFET differential amplifier with current-mirror active load. The use of enhancementmode $p$-channel input transistors lets the inputs go to the negative rail (and a bit beyond, until the omnipresent input protection diodes begin to conduct), but prevents input operation to the positive rail (because there would be no forward gate-source voltage).

Unlike the classic conventional op-amp with its pushpull follower output stage (Figure 4.43), this output stage is unsymmetrical: an $n$-channel follower $Q_{6}$ for the pullup and another $n$-channel common-source amplifier $Q_{7}$ for the pull-down. That's done because a follower at $Q_{7}$ (which would have to be p-channel) could not pull all the way down, given that its lowest gate drive voltage is ground. This unsymmetrical output requires the common-source driver $Q_{5}$ for $Q_{6}$ 's gate, with matching threshold voltages for $Q_{5}$ and $Q_{7}$ to set the output-stage quiescent current. The feedback capacitor $C_{\text {comp }}$ is for frequency compensation (see §4.9.2). This output stage can saturate at ground, with an impedance of $Q_{7}$ 's $R_{\mathrm{ON}}$; but it can't reach $V_{+}$, because $Q_{6}$ is an $n$-channel MOSFET follower.

Exercise 4.20. What sets the source voltage of $Q_{1}$ and $Q_{2}$ when the inputs are approximately at ground? And what determines the high end of the input range? Why is the latter always below $V_{+}$?

Exercise 4.21. What sets the maximum positive voltage to which $Q_{6}$ can pull the output, assuming the op-amp is lightly loaded?

This same output-stage structure - follower pullup with amplifier pull-down - can be built with bipolar transistors; an example is the popular LT1013/LT1014 singlesupply dual-quad op-amps, improved variants of the classic LM358/LM324 op-amps. A note of caution: don't make the mistake of assuming that you can make any op-amp's output work down to the negative rail simply by providing an external current sink. In most cases the circuitry driving the output stage does not permit that. Look for explicit permission in the datasheet!

One way to achieve rail-to-rail outputs - i.e., operation to both supply rails - is to replace the $n$-channel follower pullup $Q_{6}$ in Figure 4.82 with a $p$-channel common-source amplifier; then each transistor can saturate to its respective rail. This requires some driver circuitry changes, of course. An analogous circuit can be built with bipolar transistors common emitter pnp pullup and npn pull-down. Contemporary examples include the CMOS TLC2270, LMC6000, and MAX406 series, and the bipolar LM6132, LT1881, and MAX4120 series. As we'll see in Chapter $4 x$, there are other ways to make single-supply and rail-to-rail outputs. These amplifiers differ in important ways, and you must watch out for misleading statements about output swing to the negative rail (ground).

These output stages are pretty straightforward, and not surprising. But they don't generalize to the input stage. How, indeed, can you possibly achieve rail-to-rail input capability? To complete the picture without going into any
image_name:Figure 4.82. Simplified schematic of the TLC271-series singlesupply op-amp.
description:
[
name: Q1, type: PMOS, ports: {S: V+, D: X2, G: in(-)}
name: Q2, type: PMOS, ports: {S: V+, D: X3, G: in(+)}
name: Q3, type: NMOS, ports: {S: ground, D: X2, G: X2}
name: Q4, type: NMOS, ports: {S: ground, D: X3, G: X3}
name: Q5, type: NMOS, ports: {S: ground, D: X5, G: X3}
name: Q6, type: NMOS, ports: {S: V+, D: X5, G: X4}
name: Q7, type: NMOS, ports: {S: ground, D: out, G: X5}
name: Ccomp, type: Capacitor, value: Ccomp, ports: {Np: X3, Nn: X3}
name: X1, type: CurrentSource, ports: {Np: V+, Nn: X1}
name: X4, type: CurrentSource, ports: {Np: V+, Nn: X4}
]
extrainfo:The circuit is a simplified schematic of the TLC271-series single-supply op-amp. It features a differential input stage with PMOS transistors (Q1, Q2) and a current mirror load with NMOS transistors (Q3, Q4). The output stage includes NMOS transistors (Q5, Q6, Q7) with a compensation capacitor (Ccomp) for stability. The op-amp operates with a single positive supply voltage (V+).

Figure 4.82. Simplified schematic of the TLC271-series singlesupply op-amp.
image_name:Figure 4.82
description:
[
name: R1, type: Resistor, value: 7.50k, ports: {N1: Vin, N2: InN(A1)}
name: R2, type: Resistor, value: 10.0k, ports: {N1: InN(A1), N2: InP(A1)}
name: R3, type: Resistor, value: 10.0k, ports: {N1: InP(A1), N2: GND}
name: R4, type: Resistor, value: 3.74k, ports: {N1: InN(A1), N2: GND}
name: R5, type: Resistor, value: 10.0k, ports: {N1: InP(A2), N2: GND}
name: R6, type: Resistor, value: 10.0k, ports: {N1: Vref, N2: InP(A2)}
name: R7, type: Resistor, value: 10.0k, ports: {N1: Out(A2), N2: GND}
name: C1, type: Capacitor, value: 0.1µF, ports: {Np: V+, Nn: GND}
name: C2, type: Capacitor, value: 4.7µF, ports: {Np: Vref, Nn: GND}
name: Q1, type: NMOS, ports: {S: GND, D: InN(A1), G: Out(A1)}
name: IC1, type: OpAmp, value: L1077C, ports: {InP: InP(A1), InN: InN(A1), Out: Out(A1)}
name: IC2, type: OpAmp, value: TLV3501, ports: {InP: InP(A2), InN: Out(A1), Out: Out(A2)}
name: IC3, type: VoltageSource, value: LT1027D, ports: {Np: Vref, Nn: GND}
]
extrainfo:The circuit is a precision voltage-controlled waveform generator. It generates a triangle wave and a square wave from the input voltage Vin. The frequency of the output waveforms is determined by the formula f = (3/4R1C1) * (Vin/Vref), where Vin is the input voltage and Vref is a reference voltage. The circuit utilizes two op-amps (IC1 and IC2) and a MOSFET (Q1) to achieve the waveform generation. The circuit operates with a power supply voltage (V+) ranging from +8V to +15V and uses a reference voltage (Vref) of +5V.
image_name:Figure 4.83
description:The diagram in Figure 4.83 illustrates a precision voltage-controlled waveform generator circuit. It consists of two operational amplifiers (IC1 and IC2) and several passive components. The circuit is powered by a supply voltage (V+) ranging from +8 to +15 volts and uses a reference voltage (Vref) of +5.0 volts.

Components and Configuration:
1. **Operational Amplifiers:**
- **IC1 (A1):** Labeled as an LT1077C op-amp, it is configured with resistors R1 (7.50kΩ), R2 (10.0kΩ), and R3 (10.0kΩ) to form a voltage divider network.
- **IC2 (A2):** A TLV3501 op-amp, with input resistors R5 (10.0kΩ) and R7 (10.0kΩ).

2. **Transistor:**
- **Q1:** A 2N7000 NMOS transistor is used to control the grounding in the circuit.

3. **Capacitors:**
- **C1:** A 0.1µF capacitor is connected to the output of A1 to stabilize the voltage.
- **C2:** A 4.7µF capacitor is used for additional filtering.

4. **Reference Circuit:**
- **IC3:** An LT1027D is used to generate a stable reference voltage.

5. **Voltage Outputs:**
- The circuit produces two types of outputs: a triangle wave and a square wave.
- The triangle wave output oscillates between 1/3 Vref and 2/3 Vref.
- The square wave output switches between Vref and ground.

Frequency Calculation:
The frequency of the waveform is determined by the formula:
\[ f = \frac{3}{4R_1C_1} \frac{V_{in}}{V_{ref}} \]
Given that \( V_{in} \) ranges from 0 to 2Vref, the output frequency is 200 times \( V_{in} \) in Hertz.

Annotations:
- The diagram includes annotations for the triangle and square wave outputs, indicating their voltage levels relative to Vref and ground.
- The circuit is grounded at multiple points, ensuring stability and reducing noise.

Overall Function:
This circuit is designed to generate precise waveform outputs (triangle and square waves) that are controlled by the input voltage (Vin). It is useful in applications that require stable waveform generation with minimal distortion.

Figure 4.83. Precision voltage-controlled waveform generator.
detail, the trick is to design an amplifier with two independent input stages, one $p$-channel (or $p n p$ ) and the other $n$-channel (or npn). We talk about them, and some other nifty tricks (such as putting on-chip voltage generators to create bias supplies beyond the rails, in combination with a conventional op-amp like Figure 4.43), in Chapter $4 x$. Single-supply op-amps are indispensable in batteryoperated equipment.

### 4.6.4 Example: voltage-controlled oscillator

Figure 4.83 shows a clever circuit, borrowed from the application notes of several manufacturers. $\mathrm{IC}_{1}$ is an integrator, rigged up so that the capacitor current ( $V_{\text {in }} / 15 \mathrm{k}$ ) changes sign, but not magnitude, when $Q_{1}$ conducts. $\mathrm{IC}_{2}$ is connected as a Schmitt trigger, with thresholds at one-third and two-thirds of $V_{\text {ref }}$. The $n$-channel MOSFET $Q_{1}$ is here used as a switch, pulling the bottom side of $R_{4}$ to ground when $\mathrm{IC}_{2}$ 's output is HIGH and leaving it open-circuited when the output is LOW.

A nice feature of this circuit is its operation from a single positive supply. The TLV3501 is a CMOS comparator with rail-to-rail output swing, which means that the output of the Schmitt goes all the way from $V_{\text {ref }}$ to ground; this ensures that the thresholds of the Schmitt don't drift, as they would with an op-amp of conventional output-stage design, with its ill-defined limits of output swing. In this case the result is stable frequency and amplitude of the triangle wave. Note that the frequency depends on only the ratio $V_{\text {in }} / V_{\text {ref }}$; this means that if $V_{\text {in }}$ is generated from $V_{\text {ref }}$ by a resistive divider (made from some sort of resistive transducer, say), the output frequency won't vary with $V_{\text {ref }}$, only with changes in resistance. This is another example
of ratiometric techniques; circuit designers like to use this trick to minimize dependence on power-supply voltages.

Some additional points.

- Both the frequency conversion coefficient and the output swing amplitude are set by the reference voltage that powers $\mathrm{IC}_{2}\left(V_{\text {ref }}\right)$, in this case a precise and stable +5.00 V provided by the 3 -terminal voltage reference $\mathrm{IC}_{3}$. This voltage could be left unregulated if the control voltage is arranged to be proportional to it, as described above. The output amplitude would, however, still be dependent on that supply rail. The solution just shown is preferable.
- The integrator op-amp, $\mathrm{IC}_{1}$, is a "precision" op-amp, with a maximum offset voltage of $60 \mu \mathrm{~V}$. It was chosen to provide accurately proportional frequency down near zero volts input. You can think of this instead in terms of dynamic range of the frequency control: input offset voltage in the integrator op-amp produces an error in frequency equivalent to a value of $V_{\text {in }}$ of twice that offset voltage (because of the divider $R_{2} R_{3}$ ); to say it another way, at an input voltage $V_{\text {in }} \approx 2 V_{\mathrm{OS}}$, the output frequency will be in error by $100 \%$ (it could be as large as twice the programmed frequency and as low as zero). So the ratio of maximum to minimum frequency is roughly equal to $V_{\mathrm{ref}} / V_{\mathrm{OS}}$. The LT1077C shown in the figure provides a dynamic range of nearly 100,000:1 (the ratio $V_{\text {ref }} / V_{\text {OS }}=5 \mathrm{~V} / 60 \mu \mathrm{~V}$ ).
- The integrator op-amp must operate down to zero volts input; i.e., it must be a "single-supply" (or "groundsensing") op-amp, of which the LT1077C is an example.
- Input current $I_{\mathrm{B}}$ of the integrator op-amp also causes an error, most serious when the control voltage $V_{\text {in }}$ is near zero volts. The LT1077C has well-matched inputs with $I_{\mathrm{B}}(\max )=11 \mathrm{nA}$, which causes a worst-case error
equivalent to about $30 \mu \mathrm{~V}$ of unbalance when it flows through the network of unequal input resistors. This is smaller than the error contribution that is due to worstcase $V_{\mathrm{OS}}$; the combination results in a worst-case equivalent error of $90 \mu \mathrm{~V}$, or a dynamic range (untrimmed) of 50,000:1. The fact that offset voltage effects dominate over bias current effects is no accident: that is why the resistor values $R_{1}-R_{4}$ were chosen as small as they are (and the capacitor value $C_{1}$ was then chosen to produce the desired frequency range).
- The LT1077C could be trimmed to extend the dynamic range; ultimately it is drift in $V_{\mathrm{OS}}$ and $I_{\mathrm{B}}$ (over time and temperature) that set the circuit's overall stability near zero frequency.
- The TLV3501 is an unusually fast ( 4.5 ns ) comparator with rail-to-rail output swing. However, its supply voltage is limited to +5.5 V maximum. If you wanted to run that portion of the circuit at a higher voltage, you could substitute a fast rail-to-rail op-amp like the CA3130. The latter part has been around a long time and is nearing extinction; ${ }^{38}$ but it excels in speed for a low-power op-amp because it is uncompensated (see $\S 4.9 .2 \mathrm{~B}$ ). It would not be suitable for the input op-amp, however, because it is not stable as an integrator, for reasons we will see shortly. It also has large input offset voltage.
- Another possibility is to replace the Schmitt trigger circuit with a CMOS 555-type timer IC, for example, an ICL7555. These have stable input thresholds at one-third and two-thirds of the supply rail, and rail-to-rail fast output swing.
- Switch alternatives: IC switches like the SD210 or 74HC4066 (the latter belongs to the 74HC family of digital logic) could replace the discrete MOSFET $Q_{1}$; their lower capacitance would improve operation at high frequencies.
- Another possibility, if power consumption matters more than maximum frequency or dynamic range, is to use low-power CMOS rail-to-rail op-amps for both ICs, for example, a TLC2252 dual op-amp ( $35 \mu \mathrm{~A}$ per channel). In this case scale up the resistor values, particularly in the input stage, because CMOS op-amps have negligible input current for this application.
- If the use of a dual op-amp in a single package seems particularly appealing, then a good overall choice is the bipolar LM6132, with rail-to-rail inputs and outputs and a slew rate of $14 \mathrm{~V} / \mu \mathrm{s}$; in the same family you can get faster op-amps (LM6142, LM6152), at the cost of higher input and supply currents.

[^47]- An elegant single-IC solution is the use of a combination op-amp-comparator-reference IC like the MAX951. We looked around for a way to use such a chip here, but, alas, we couldn't squeeze the excellent performance of Figure 4.83 out of any of the combination chips currently available, nor from special-purpose timers like the LTC699x-series (§7.1.4B). This illustrates the circuit performance advantage you get if you can combine the best available ICs for the given task, rather than having to accept a pre-assembled combination.

Exercise 4.22. Derive the expression for output frequency shown in Figure 4.83. Along the way, verify that the Schmitt thresholds and integrator currents are as advertised.

### 4.6.5 VCO implementation: through-hole versus surface-mount

Traditionally, electronic components were made with wire leads sticking out the ends (e.g., "axial-lead" resistors and capacitors), or rows of pins sticking down (e.g., ICs with DIP - "dual in-line" - packaging). Contemporary practice has shifted strongly toward "surface-mount" components, in which the connections are made directly to contacts on a ceramic or plastic package. See, for example, the photographs of resistors in Chapter 1 (Figure 1.2), of op-amps earlier in this chapter (Figure 4.1), or of small logic (Figure 10.23) in Chapter 10.

The good news is that surface-mount technology (SMT) lets you make smaller gadgets; and it is better electrically as well, because of reduced inductances in the smaller packages.

The bad news is that SMT makes it difficult to wire up a circuit on the spur of the moment on a prototype "breadboard" (of either the solder-in or plug-in style), an exercise that is fast and easy with through-hole components. The problem is compounded by the fact that many new highperformance components (e.g., op-amps) are available only in surface-mount packages.

In a nutshell, your choices boil down to (a) sticking with through-hole components (if you can get the parts you need) and enjoying the easy prototyping and ability to build a one-off gadget quickly; (b) going with the flow, and using mostly SMT components, laying out a printed circuit board for each circuit you want to build; or (c) trying to retain the best of both worlds by prototyping with through-hole components, where available, and using SMT adapters (or "carriers") for the SMT components that you cannot get in through-hole packages. The latter are tiny circuit boards on which you solder an SMT component, whose leads connect
to a row of pins, producing a faux through-hole component. We've struggled with this whole business and have concluded that this last option, though attractive in principle, is fast fading away, because of the decreasing availability of through-hole components.

To give a glimpse of the tradeoffs, we laid out the voltage-controlled oscillator (VCO) circuit of Figure 4.83 on printed-circuit boards, exploring the alternatives of (a) through-hole components, (b) relatively large SMT components, and (c) small SMT components. Figure 4.84 shows them at actual size; we've shown only the component outlines and "pads" (metal foil patterns that make the connections to the components). For the through-hole board we used standard DIP op-amp and comparator and axial-lead $1 / 4$-watt resistors; for the large SMT we used SOIC-8 opamp and comparator and 0805 SMT resistors; and for the small SMT we used SOT-23 op-amp and comparator and the smaller 0603 resistors. ${ }^{39}$ The latter is 4.5 times smaller than the through-hole board. And there is no penalty in performance; in fact, smaller components generally deliver somewhat better performance owing to smaller parasitic inductances.

### 4.6.6 Zero-crossing detector

This example illustrates the use of a single-supply comparator, a close kin to the single-supply op-amp. Like the latter, it will operate with input signals all the way to the lower supply rail, which often is ground. The circuit, shown in Figure 4.85, generates an output square wave for use with 5 V "TTL" logic ( 0 to +5 V range) from an input wave of any amplitude up to 150 volts rms. The LM393 is a comparator IC (like the TLV3501 we used in the last example), specialized for this sort of application; it cannot be used as an amplifier, in the manner of an op-amp, because its internal phase shifts are not tailored ("compensated," see §4.9) to permit feedback without oscillation. It also has an "open-collector" output, which you must pull up externally to a supply rail, as shown. Its internal circuit is shown in Figure 4.86; note the overall similarity to an op-amp (Figure 4.43), with the important omission of the compensation capacitor $C_{\mathrm{C}}$, and the lack of a "pullup" transistor at the output. We treat comparators in more detail in §12.3.

[^48]image_name:DIP (through-hole)
description:The image displays printed circuit board (PCB) layouts for three different packaging types: DIP (through-hole), SOIC (0805), and SOT-23 (0603). Each layout is designed for different component mounting techniques, with the DIP being for through-hole components and the other two for surface-mount devices.

DIP (Through-Hole) Layout:
- **Components:**
- **U1A, U2A, U3A:** These are likely IC sockets for through-hole integrated circuits.
- **R1A, R2A, R3A, R4A, R5A, R6A, R7A:** Resistor placements.
- **Q1A:** Transistor or other similar component.
- **C1A, C2A, C3A:** Capacitor placements.
- **W5, W7, W8, W10, W14:** Wire or connector points.
- **Connections:**
- The layout shows traces connecting various components, indicating signal paths.

SOIC (0805) Layout:
- **Components:**
- **U1, U2, U3:** IC placements for surface-mount integrated circuits.
- **R1, R2, R3, R4, R5, R6, R7:** Resistor placements.
- **Q1:** Transistor or similar component.
- **C1, C2, C3:** Capacitor placements.
- **W10, W13:** Wire or connector points.
- **Connections:**
- Compact layout with traces connecting components, optimized for space efficiency.

SOT-23 (0603) Layout:
- **Components:**
- **U1B, U2B, U3B:** IC placements for small surface-mount integrated circuits.
- **R1B, R2B, R3B, R4B, R5B, R6B, R7B:** Resistor placements.
- **Q1B:** Transistor or similar component.
- **C1B, C2B, C3B:** Capacitor placements.
- **W6, W9, W11, W12, W15:** Wire or connector points.
- **Connections:**
- Extremely compact layout, suitable for very small PCB designs.

General Features:
- **Labels and Annotations:** Each component placement is labeled with a reference designator (e.g., R1, C1) for easy identification.
- **Scale:** The SOT-23 layout includes a scale marker indicating the layout is 1 cm across, emphasizing its compact size.

This image illustrates how different component mounting technologies affect PCB design, with through-hole being larger and more robust, while surface-mount allows for more compact and efficient designs.
image_name:SOIC / 0805
description:The image displays various printed-circuit board (PCB) layouts for different package types: DIP (through-hole), SOIC/0805, and SOT-23/0603. These layouts are used for implementing electronic circuits with different mounting technologies.

1. **DIP (Through-Hole) Layout**:
- **Components**: This layout includes areas for placing through-hole components such as resistors (R1A to R7A), capacitors (C1A, C2A, C3A), and integrated circuits (U1A, U2A, U3A). There is also a position for a transistor (Q1A).
- **Connections**: The layout shows holes for component leads and PCB traces connecting various components. It includes connection points labeled W5, W7, W8, W10, and W14, indicating potential points for external connections or signals.
- **Annotations**: The layout is labeled with component identifiers and indicates the use of a DIP package type.

2. **SOIC / 0805 Layout**:
- **Components**: This layout is designed for surface-mount components, including resistors (R1 to R7), capacitors (C1, C2, C3), integrated circuits (U1, U2, U3), and a transistor (Q1).
- **Connections**: The layout features pads for surface-mount component placement and traces connecting these components. Connection points are labeled W1, W2, W3, and W13.
- **Annotations**: The layout is labeled for SOIC and 0805 package types, indicating a compact design with reduced board area.

3. **SOT-23 / 0603 Layout**:
- **Components**: This layout supports very small surface-mount components, including resistors (R1B to R7B), capacitors (C1B, C2B, C3B), integrated circuits (U1B, U2B, U3B), and transistors (Q1B).
- **Connections**: It shows pads for small components and traces for connectivity. Connection points are labeled W6, W9, W11, W12, and W15.
- **Annotations**: The layout is labeled for SOT-23 and 0603 package types, emphasizing miniaturization and efficient use of space.

Each of these layouts is designed to accommodate different component packages and mounting techniques, optimizing for space, performance, and available components. The use of surface-mount technology (SMT) in the SOIC and SOT-23 layouts allows for a more compact design compared to the through-hole DIP layout.
image_name:SOT-23 / 0603
description:The image illustrates three different printed-circuit board (PCB) layouts for a VCO (Voltage Controlled Oscillator), each utilizing different component mounting technologies: DIP (through-hole), SOIC (Small Outline Integrated Circuit), and SOT-23/0603 (Surface-Mount Technology).

1. **DIP (through-hole) Layout:**
- This layout features components that are mounted through holes in the PCB. It includes several resistors labeled R1A through R7A, capacitors such as C1A, C2A, and C3A, and integrated circuit slots for U1A, U2A, and U3A. There is also a transistor or similar component labeled Q1A. The layout includes various connection points labeled W5, W7, W8, W10, and W14.

2. **SOIC / 0805 Layout:**
- The SOIC layout uses surface-mount components, which are smaller and allow for more compact designs. It includes resistors labeled R1 through R7, capacitors C1, C2, and C3, and integrated circuits U1, U2, and U3. A transistor or similar device is labeled Q1. Connection points are labeled W1, W2, W3, W4, W10, and W13.

3. **SOT-23 / 0603 Layout:**
- This is the most compact layout, using the smallest surface-mount components. It features resistors labeled R1B through R7B, capacitors C1B, C2B, and C3B, and integrated circuits U1B, U2B, and U3B. A transistor or similar device is labeled Q1B. Connection points include W6, W9, W11, W12, and W15.

**Connections and Interactions:**
- Each layout shows interconnections between components, such as traces connecting resistors to capacitors and integrated circuits. The presence of various wiring points (labeled W) indicates potential connection to external circuitry or power sources.

**Labels, Annotations, and Key Features:**
- The layouts are annotated with labels indicating component types and connection points. The SOT-23 / 0603 layout is marked with a scale indicating its compact size (1 cm), highlighting the reduced board area compared to the other layouts. This demonstrates the advantage of using surface-mount technology for minimizing board space while maintaining functionality.

Figure 4.84. Printed-circuit layouts for the VCO of Figure 4.83. The use of small surface-mount components reduces the board area to $22 \%$ of the analogous board using through-hole components. Additional benefits are a greater selection of available parts, and better electrical performance.

Resistor $R_{1}$, combined with $D_{1}$ and $D_{2}$, limits the input swing to -0.6 volt to +5.6 volts, approximately; its power rating is set by the maximum rms input voltage. Resistive divider $R_{2} R_{3}$ is necessary to limit negative swing to less than 0.3 volt, the limit for a 393 comparator. $R_{5}$ and $R_{6}$ provide hysteresis for this Schmitt trigger circuit, with $R_{4}$ setting the trigger points symmetrically about ground. The input impedance is nearly constant because of the large $R_{1}$ value relative to the other resistors in the input attenuator. A 393 is used because its inputs can go all the way to ground, making single-supply operation simple.
image_name:Figure 4.85
description:
[
name: R1, type: Resistor, value: 47k, ports: {N1: Vin, N2: X1}
name: R2, type: Resistor, value: 7.5k, ports: {N1: X1, N2: InN}
name: R3, type: Resistor, value: 6.2k, ports: {N1: InN, N2: GND}
name: R4, type: Resistor, value: 2.7M, ports: {N1: V+, N2: InN}
name: R5, type: Resistor, value: 1M, ports: {N1: InP, N2: Out}
name: R6, type: Resistor, value: 4.12k, ports: {N1: GND, N2: InP}
name: R7, type: Resistor, value: 4.7k, ports: {N1: V+5, N2: Out}
name: C1, type: Capacitor, value: 5pF, ports: {Np: InP, Nn: Out}
name: C2, type: Capacitor, value: 330pF, ports: {Np: InN, Nn: GND}
name: D1, type: Diode, ports: {Na: X1, Nc: GND}
name: D2, type: Diode, ports: {Na: V+, Nc: X1}
name: IC1, type: OpAmp, value: LM393A, ports: {InP: InP, InN: InN, Out: Out}
]
extrainfo:The circuit is a zero-crossing level detector with input protection. It uses an LM393A comparator, with R5 and R6 providing hysteresis and R4 setting the trigger points symmetrically about ground. The resistive divider R2 and R3 limits the negative swing to less than 0.3V. The input impedance is stabilized by the large R1 value. The circuit is designed for single-supply operation and allows inputs to go all the way to ground.
image_name:Figure 4.86
description:
[
name: R1, type: Resistor, value: 47k, ports: {N1: Vin, N2: X1}
name: R2, type: Resistor, value: 7.5k, ports: {N1: X1, N2: InN}
name: R3, type: Resistor, value: 6.2k, ports: {N1: InN, N2: GND}
name: R4, type: Resistor, value: 2.7M, ports: {N1: V+, N2: InN}
name: R5, type: Resistor, value: 1M, ports: {N1: InP, N2: Out}
name: R6, type: Resistor, value: 4.12k, ports: {N1: InP, N2: GND}
name: R7, type: Resistor, value: 4.7k, ports: {N1: V+, N2: Out}
name: C1, type: Capacitor, value: 5pF, ports: {Np: InP, Nn: Out}
name: C2, type: Capacitor, value: 330pF, ports: {Np: InN, Nn: GND}
name: D1, type: Diode, ports: {Na: X1, Nc: GND}
name: D2, type: Diode, ports: {Na: V+, Nc: X1}
name: A1, type: OpAmp, value: LM393A, ports: {InP: InP, InN: InN, OutP: Out, OutN: GND}
]
extrainfo:The circuit is a zero-crossing level detector with input protection, utilizing the LM393A comparator. It features input protection diodes (D1 and D2) and a resistive divider (R2 and R3) to limit negative swing. Hysteresis is provided by resistors R5 and R6, with R4 setting trigger points symmetrically about ground. The input impedance is stabilized by R1.

Figure 4.85. Zero-crossing level detector with input protection.
image_name:Figure 4.86
description:
[
name: Q1, type: PNP, ports: {C: P1, B: in(+), E: GND}
name: Q2, type: PNP, ports: {C: P2, B: P1, E: X1}
name: Q3, type: PNP, ports: {C: P3, B: P2, E: X2}
name: Q4, type: PNP, ports: {C: GND, B: P3, E: GND}
name: Q5, type: NPN, ports: {C: X1, B: X1, E: GND}
name: Q6, type: NPN, ports: {C: X2, B: X1, E: GND}
name: Q7, type: PNP, ports: {C: P4, B: in(-), E: GND}
name: Q8, type: PNP, ports: {C: out, B: P4, E: GND}
name: P1, type: CurrentSource, value: 4µA, ports: {Np: V+, Nn: P1}
name: P2, type: CurrentSource, value: 100µA, ports: {Np: V+, Nn: P2}
name: P3, type: CurrentSource, value: 4µA, ports: {Np: V+, Nn: P3}
name: P4, type: CurrentSource, value: 100µA, ports: {Np: V+, Nn: P4}
]
extrainfo:The circuit is a schematic of the LM393 single-supply comparator. It shows the arrangement of PNP and NPN transistors along with current sources to achieve the comparator functionality. The input is fed into Q1 and Q7, while the output is taken from Q8. The current sources provide biasing for the transistors.

Figure 4.86. Schematic of the LM393 single-supply comparator.

Exercise 4.23. Verify that the trigger points are at $\pm 100 \mathrm{mV}$ at the input signal.

Some additional points.

- The vintage LM393 severely limits the allowable swing below ground, because the output will switch polarity if the input goes below -0.3 V , a pathology tactfully called phase reversal in the datasheet. That is prevented here by diode $D_{1}$ and divider $R_{2} R_{3}$; alternatively the low side of $D_{1}$ could be biased a diode drop above ground, as in Figure 5.81. Resistor $R_{3}$ could be omitted if a modern comparator like the LT1671 were used; the latter also has internal active pullup to +5 V , so you would omit pull-up resistor $R_{7}$ as well.
- We intentionally set the Schmitt thresholds symmetrically around ground, but that may not be the best choice. For example, you might want output transitions accurately synchronized with the exact zero crossings of the input waveform. Omitting $R_{4}$ would set the negativegoing input threshold exactly at 0 V ; alternatively, you could set the positive-going threshold to 0 V with a properly-chosen value for $R_{4}$ (test your understanding with Exercise 4.24).
- By using capacitive feedback only (omitting $R_{5}$ ), you can have both thresholds at 0 V with some of the benefits of hysteresis. In this case, the hysteresis is transient, with a time constant $\tau=C_{1} R_{6}$, by which time you are assuming the input waveform will have left the threshold region. So, for example, if you were using this circuit to sense zero crossings of a 60 Hz sinewave, you might choose $C_{1}=0.1 \mu \mathrm{~F}$ for a 0.5 ms time constant (but see next item). The drawback is that you're making assumptions about the input's minimum slew rate and maximum zero-crossing frequency. You could imagine a more elaborate scheme, with additional comparators, such that the input threshold is restored to 0 V after the input wave-
form passes a second higher threshold. This design challenge would yield a precise zero-crossing circuit (for both waveform slopes) with no restrictions on input speed, etc.
- Be careful if you decide to increase the value of the speed-up capacitor $C_{1}$ - this capacitor causes a negativegoing transient at the inverting input of the comparator, and if the capacitor is much larger than a few picofarads you may cause phase reversal at the comparator's output (a pathology of many comparators, including the LM393). In that case it's best to use a modern comparator whose datasheet specifically brags that it is free of phase reversal; an example is the MAX989.

Exercise 4.24. What value of $R_{4}$ in Figure 4.85 puts the positivegoing input threshold at 0 V ?

Exercise 4.25. Try designing a hysteretic circuit, with several comparators, such that both thresholds are precisely at 0 V , under the assumption that the input waveform always travels a minimum of 50 mV beyond ground before coming back.

### 4.6.7 An op-amp table

We've collected in Table 4.2a on the facing page a representative selection of useful op-amps, including many of our favorites. You can get an idea of the price and performance of parts that are in wide use. Better yet, use this table as a starting point in your next design! More comprehensive op-amp tables are located in the chapter on precision design (Table 5.4, High-speed op-amps; Table 5.5, Precision op-amps; Table 5.6, Auto-zero op-amps), and in the chapter on noise (Table 8.3, Low-noise op-amps).

## 4.7 Other amplifiers and op-amp types

In this first op-amp chapter we've met the "standard" splitsupply op-amp, implemented variously with bipolar transistors, JFETs and MOSFETs. We've also seen examples of single-supply op-amps, some with rail-to-rail outputs (and even rail-to-rail inputs).

There are other choices, some of which we'll look at in Chapters $4 x$ and 5. It's worth listing them here, because one or more of them may be the best solution to a design problem that looks initially like it needs an op-amp.

#### Current-feedback op-amps

These look a lot like ordinary ("voltage-feedback") opamps, but differ by having a low-impedance inverting input terminal that is a current summing junction. They excel in wideband circuits with moderate to high voltage gain; see the discussion in Chapter $4 x$.
Table 4.2a Representative Operational Amplifiers (see also Tables 5.2-5.6 and 8.3)

| Part \# ${ }^{\text {a }}$ | Package |  |  | Total Supply |  | $I_{Q}$ <br> typb <br> (mA) | $\begin{gathered} f_{\mathrm{T}} \\ \text { typ } \\ (\mathrm{MHz}) \end{gathered}$ | image_name:SR typ (V/μs)
description:The image is a vertical label that reads 'SR typ (V/μs)', which stands for 'Slew Rate typical (Volts per microsecond)'. This label is likely used in a table to indicate a column where the typical slew rate values of various operational amplifiers are listed, measured in volts per microsecond (V/μs). Slew rate is a parameter that describes how quickly an op-amp can change its output voltage in response to a rapid change on the input signal. It is an important specification in wideband circuits or applications where fast signal processing is required."
| $V_{\text {os }}$ max $(\mu \mathrm{V})$ | $I_{\text {bias }}$ typ (nA) | image_name:en typ (nV/√Hz)
description:The image contains text that reads 'en typ (nV/√Hz)', which likely refers to a column heading in a table. This indicates the typical input voltage noise density of operational amplifiers, measured in nanovolts per square root of Hertz (nV/√Hz). This parameter is crucial for understanding the noise performance of op-amps, especially in low-noise applications.
| Swing to supplies?$\frac{\mathrm{IN}}{+-} \frac{\mathrm{OUT}}{+-}$ | Comments |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
|  | \#/pkg | 응 | qty 25 <br> (\$US) | min <br> (V) | max <br> (V) |  |  |  |  |  |  |  |  |
| LM358, 324 | 2,4 | $\cdot$ $\cdot$ - | 0.16 | 3 | 32 | 1 | 1 | 0.5 | 7000 | 45 | 40 | - $\cdot$ - $\cdot$ | single-supply jellybean |
| LT1013, 1014 | 2,4 | $\cdot$ $\cdot$ - | 1.30 | 4 | 44 | 0.7 | 0.8 | 0.4 | 40 | 12 | 22 | - $\cdot$ - $\cdot$ | precision single-supply |
| LT1077A | 1 | $\cdot$ $\cdot$ - | 4.11 | 2.2 | 44 | 0.05 | 0.23 | 0.08 | 40 | 7 | 27 | - $\cdot$ - $\cdot$ | low-power bipolar, also OP193 |
| LMC6482A, 84A | 2,4 | $\cdot$ $\cdot$ - | 1.73 | 3 | 16 | 1.3 | 1.5 | 1.3 | 750 | 20fA | 37 | $\cdot$ | CMOS jellybean, LMC7101 SOT-23 |
| TLC2272A, 74 | 2,4 | $\cdot$ $\cdot$ - | 1.57 | 4 | 16 | 2.2 | 2.2 | 3.6 | 950 | 0.001 | 9 | - $\cdot$ $\cdot$ $\cdot$ | CMOS |
| LMC6442A | 2 | $\cdot$ $\cdot$ - | 2.00 | 2.2 | 16 | 0.002 | 0.01 | 0.004 | 3000 | 5fA | 170 | $\cdot$ | micro-power! |
| LMC6041, 42, 44 | 1,2,4 | $\cdot$ $\cdot$ - | 1.48 | 4.5 | 16 | 0.02 | 0.08 | 0.015 | 3000 | 2fA | 83 | - $\cdot$ $\cdot$ $\cdot$ |  |
| LMC6081A, 82, 84 | 1,2,4 | $\cdot$ - - | 2.72 | 4 | 16 | 0.45 | 1.3 | 1.5 | 350 | 10fA | 22 | - $\cdot$ $\cdot$ $\cdot$ | for low power, LMC6061 has $I_{\mathrm{Q}}=20 \mu \mathrm{~A}$ |
| TLV2401, 02 | 1,2 | - $\cdot$ $\cdot$ | 1.42 | 2.5 | 16 | 0.0009 | 0.005 | 0.002 | 1200 | 0.1 | 500 | $\cdot$ $\cdot$ $\cdot$ | pico-power, operates to $V_{\mathrm{Cc}}+5 \mathrm{~V}$ |
| LMC7101A | 1 | - - $\cdot$ | 0.93 | 2.7 | 16 | 0.5 | 1 | 1 | 3000 | 0.001 | 37 | $\cdot$ $\cdot$ $\cdot$ $\cdot$ | similar to LMC6482 |
| LF411, 412C | 1,2 | $\cdot$ $\cdot$ - | 0.72 | 7 | 36 | 4.5 | 3 | 13 | 2000 | 0.05 | 18 | - - - - | JFET, TI, dual cheaper than single |
| LF347B | 4 | $\cdot$ $\cdot$ - | 0.58 | 7 | 36 | 8 | 3 | 13 | 5000 | 0.05 | 18 | $\cdot$ - - - | low cost JFET, 15¢ per op-amp |
| LT1057A, 1058 | 2,4 | $\cdot$ $\cdot$ - | 6.30 | 7 | 40 | 3.4 | 5 | 24 | 450 | 0.05 | 13 | - - - - | improved LF412, also see AD712 |
| OPA727, 2727 | 1,2 | - $\cdot$ - | 2.58 | 4 | 13 | 4.3 | 20 | 30 | 150 | 0.085 | 6 | - $\cdot$ $\cdot$ $\cdot$ | e-trim CMOS |
| OPA376, 2376 | 1,2 | - $\cdot$ $\cdot$ | 2.03 | 2.2 | 7 | 0.76 | 5.5 | 2 | 25 | 0.2pA | 7.5 | - $\cdot$ $\cdot$ $\cdot$ | e-trim CMOS |
| TLC272C, 274C | 2,4 | $\cdot$ $\cdot$ - | 0.69 | 3 | 16 | 1.4 | 2.2 | 5.3 | 10 mV | 0.1pA | 27 | - $\cdot$ - $\cdot$ | consider TLV27x family |
| OPA129B | 1 | $\cdot$ $\cdot$ - | 10.15 | 10 | 36 | 1.2 | 1 | 2.5 | 2000 | 30fA | 17 | - - - - | electrometer, mass spec, pH probe |
| LT1012A | 1 | $\cdot$ $\cdot$ - | 5.11 | 2.4 | 40 | 0.37 | 0.4 | 0.2 | 25 | 0.025 | 14 | - - - - | low $I_{B}$ bipolar |
| LTC1050C | 1 | $\cdot$ - - | 4.30 | 6 | 18 | 1.1 | 2.5 | 4 | 5 | 0.01 | $1.6 \mu \mathrm{~V}^{\mathrm{C}}$ | - $\cdot$ $\cdot$ | chopper |
| LT1637 | 1 | $\cdot$ - - | 2.32 | 2.7 | 44 | 0.19 | 1 | 0.35 | 350 | 20 | 27 | + $\cdot$ $\cdot$ | "over-the-top": $V_{\text {in }}$ to $V_{\text {EE }}+44 \mathrm{~V}$ |
| LT1097 | 1 | $\cdot$ $\cdot$ - | 2.33 | 2.6 | 40 | 0.35 | 0.7 | 0.2 | 50 | 0.04 | 14 | - - - - | CLOAD stable, comp pin |
| OPA177 | 1 | $\cdot$ $\cdot$ - | 2.30 | 6 | 44 | 1.5 | 0.6 | 0.3 | 60 | 0.5 | 7 | - - - - | improved OP-07 |
| OPA277, 2277, 4227 | 1,2,4 | $\cdot$ $\cdot$ - | 3.60 | 4 | 36 | 0.8 | 1 | 0.8 | 20 | 0.5 | 8 | - - - - | improved OP-07, see also OPA227 |
| LM6132A, 34 | 2,4 | $\cdot$ - - | 2.92 | 2.7 | 35 | 0.8 | 11 | 14 | 2000 | 110 | 27 | $\cdot$ | early RRIO |
| AD797A | 1 | $\cdot$ - - | 8.36 | 10 | 36 | 8.2 | 80 | 20 | 80 | 250 | 0.9 | - - - - | low distortion, low noise |
| ADA4000-1, 2, 4 | 1,2,4 | - $\cdot$ $\cdot$ | 1.46 | 8 | 36 | 1.3 | 5 | 20 | 1700 | 0.005 | 16 | $\cdot$ - - - | JFET |
| LT6220, 21, 22 | 1,2,4 | - $\cdot$ | 2.61 | 2.5 | 12.6 | 0.9 | 60 | 20 | 200 | $15^{\text {h }}$ | 10 | $\cdot$ $\cdot$ $\cdot$ $\cdot$ |  |
| OPA627A | 1 | $\cdot$ - - | 24.50 | 9 | 36 | 7 | 16 | 55 | 250 | 0.002 | 5.6 | - - - - | low-noise JFET |
| OPA657 | 1 | - $\cdot$ $\cdot$ | 12.90 | 8 | 13 | 14 | 1600 | 700 | 1800 | 0.002 | 4.8 | - - - - | fast JFET |
| OPA454 | 1 | - $\cdot$ - | 4.88 | 10 | 120 | 3.2 | 2.5 | 13 | 4000 | 0.002 | 35 | - $\cdot$ - - | high voltage, also OPA445 miniDIP |
| THS4011, 12 | 1,2 | $\cdot$ $\cdot$ - | 5.60 | 9 | 33 | 7.8 | 290 | 310 | 6000 | 2000 | 7.5 | - - - - | fast VFB ${ }^{\text {; }}$; THS4021/22 decomp, G>10 |
| LM7171A | 1 | - $\cdot$ - | 3.60 | 8 | 36 | 6.5 | 200 | 4100 | 4000 | 2700 | 14 | - - | CFB $^{\text {e }}, 100 \mathrm{~mA}$ output current |
| EL5165 | 1 | - $\cdot$ $\cdot$ | 2.32 | 5 | 12.6 | 5 | 1400 | 6000 | 5000 | 8500 | 1.7 | - | CFB ${ }^{\text {e }}$ |
| AD8011 | 1 | $\cdot$ $\cdot$ - | 3.98 | 3 | 12.6 | 1 | $570^{\text {d }}$ | 3500 | 5000 | 5000 | 2 | - - - | low-power two-stage CFB |
| Notes: (a) Italicized part numbers have corresponding number of op-amps per package. (b) quiescent current per package, for the boldface part number (that with the least number of op-amps; e.g.,1mA for the LM358). (c) peak-to-peak noise voltage. (d) GBW for $\mathrm{GV}=10$. (e) $\mathrm{VFB}=\mathrm{voltage}$ feedback, $\mathrm{CFB}=\mathrm{current}$ feedback. (h) rises to 250nA at the negative rail. |  |  |  |  |  |  |  |  |  |  |  |  |  |

Table 4.2b Monolithic Power and High-Voltage Op-Amps ${ }^{a}$

| Type | Mfg | Total supply |  |  |  |  | $\begin{gathered} f_{\mathrm{T}} \\ \text { typ } \\ (\mathrm{MHz}) \end{gathered}$ | Slew rate typ (V/ / s ) | Iout(max) typ (A) | $P_{\text {diss }}$ <br> ( $50^{\circ} \mathrm{C}$ ) <br> max <br> (W) | image_name:Therm lim
description:The image contains text oriented vertically, with the words "Therm lim" and "Prog curr lim" visible. "Therm lim" likely refers to thermal limit, and "Prog curr lim" suggests programmable current limit. These terms are possibly column headings or labels related to the operational or safety limits of the op-amps mentioned in the context, such as thermal and current constraints.
|  | Package | Cost qty 25 (\$US) | image_name:Comments
description:The image consists of the word "Comments" oriented vertically. This text likely serves as a label or heading for a section dedicated to additional notes or remarks, possibly related to the data or specifications mentioned in the surrounding context, such as thermal limits or programmable current limits of operational amplifiers.
|
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
|  |  |  |  | Diff'l input $^{b}$ | है잉 | image_name:Comments
description:The image contains text oriented vertically, which reads "current down." This text likely serves as a label or note related to the data or specifications in the surrounding context, such as thermal limits or programmable current limits of operational amplifiers.
|  |  |  |  |  |  |  |  |
|  |  | $\begin{gathered} \hline \min ^{\prime} \\ \text { (V) } \end{gathered}$ | max <br> (V) |  | typ <br> (mA) |  |  |  |  |  |  | 岀 華 |  |  |  | image_name:Comments
description:The image contains vertically oriented text that reads "Programmable shutdown." This text is likely a label or note related to the specifications or features of operational amplifiers or similar components, possibly indicating a functionality that allows programmable shutdown of the device.
|
| Iow power |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| LME49726 | TI | 2.5 | 6 | 0.7 | full | $\cdot$ - | 6.8 | 3.7 | 0.35 | $1^{\text {u }}$ | - | - - | MSOP | 1.29 | A |
| OPA567 | TI | 2.7 | 7.5 | 3.4 | full | - - | 1.2 | 1.2 | 2.2 | $12.5^{\text {n }}$ | $\cdot$ | $\cdot$ $\cdot$ | QFN | 5.53 | B |
| OPA569 | TI | 2.7 | 7.5 | 3.4 | full | $\cdot$ - | 1.2 | 1.2 | 2.2 | $25^{n}$ | $\cdot$ |  | SO-20 | 7.41 | B,C |
| AD8010 | Analog | 10 | 12.6 | 16 | 1.2 | - - | 230 | 800 | 0.2 | $1.3^{\text {u }}$ | - - | - - | SO-16 | 6.69 | D |
| LM6171 | TI | 5 | 36 | 2.5 | 10 | - - | 100 | 3000 | 0.12 | 0.7 | - - | - - | DIP, SO | 4.27 | E |
| LTC2057HV | LTC | 4.8 | 65 | 0.8 | full | - - | 1.5 | 0.45 | 0.02 | low | - | - - | SO-8 | 3.32 | F |
| ADA4700 | Analog | 10 | 100 | 1.7 | full | - - | 3.5 | 20 | 0.03 | 2.5 | $\cdot$ - | - - | SO-8 | 6.00 |  |
| OPA445 | TI | 20 | 100 | 4.2 | 80 | - - |  | 10 | 0.015 | 0.6 | - | - - | DIP, SO-8 | 10.07 | G |
| OPA454 | TI | 10 | 100 | 3.2 | fullg |  | 2.5 | 13 | 0.12 | $7.5^{n}$ | $\cdot$ - | - $\cdot$ | SO-8 | 6.09 |  |
| LTC6090 | LTC | 9.5 | 140 | 2.8 | full | - - | 12 | 21 | 0.05 | $15^{n}$ | $\cdot$ - | - $\cdot$ | SO,TTSOP | 4.87 | H |
| medium power |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| L2720W | ST | 4 | 28 | 10 | full | - - | 1.2 | 2 | 1 | 5 | $\cdot$ - | - - | SO-16 | 1.02 | I |
| ISL1532A | Intersil | 10 | 30 | $3.5^{\circ}$ | full | - - | 50 | 400 | 1 | 1 | - | - $\cdot$ | SSOP-20 | $1.43^{r}$ | J |
| THS3120 | TI | 9 | 33 | 7 | 4 | - - | 130 | 900 | 0.47 | $15^{n}$ | - - | - $\cdot$ | MSOP-8 | 5.57 | K |
| LT1794 | LTC | 10 | 36 | 26 | full | - - | 200 | 600 | 0.72 | $25^{n}$ | $\cdot$ - | - $\cdot$ | SO-20 | 8.09 | J |
| LT1206 | LTC | 10 | 36 | $12^{\circ}$ | full | - $\cdot$ | 60 | 900 | 0.5 | $15^{\text {p }}$ | - | - $\cdot$ | DIP,TO-220 | 5.88 | K,L |
| LT1210 | LTC | 8 | 36 | 35 | full | $\cdot$ | 35 | 900 | 2 | $15^{p}$ | - | - $\cdot$ | TO-220-7 | 8.75 | K,M |
| L272 | FSC | 4 | 40 | 8 | full | - - | 0.35 | 1 | 1 | 5 | $\cdot$ - | - - | DIP, SO-16 | 2.08 | N |
| PA75 | Apex | 5 | 40 | 8 | full | - - | 1.4 | 1.4 | 2.5 | 19 | - | - - | TO-220-7 | 28.88 | O |
| TDA7256 | ST | 10 | 50 | 80 | full | - - | 9 | 10 | 3 | 35 | $\cdot$ | - $\cdot$ | TO-220-11 | 3.42 | P |
| LM1875 | TI | 16 | 60 | 70 | full | - - | 5.5 | 8 | 4 | 25 | - | - - | TO-220-5 | 2.75 | P |
| OPA552 | TI | 8 | 60 | 7 | full | $\cdot$ | 12 | $24{ }^{\text {d }}$ | 0.2 | $25^{p}$ | $\cdot$ | - - | DIP, DDPak | 5.70 | Q |
| LM675 | TI | 20 | 60 | 18 | full | - - | 5.5 | 8 | 3 | 40 | - | - - | TO-220-5 | 4.82 | R |
| OPA547 | TI | 8 | 60 | 10 | full | - - | 1 | 6 | 0.5 | 25 | $\cdot$ | - $\cdot$ | TO-220-7 | 9.57 | S |
| OPA548 | TI | 8 | 60 | 17 | full | - - | 1 | 10 | 3 | 30 | - | - $\cdot$ | TO-220-11 | 13.22 | S |
| OPA549 | TI | 8 | 60 | 26 | full | - - | 0.9 | 9 | 8 | 53 | $\cdot$ | - $\cdot$ | TO-220-11 | 20.65 | S |
| OPA453 | TI | 20 | 80 | 4.5 | full |  | 7.5 | $23^{\text {d }}$ | 0.05 | 25 | $\cdot$ | - - | TO-220-7 | 5.50 | T |
| OPA541 | TI | 20 | 80 | 20 | full | - - | 2 | 10 | 10 | 90 | - | - - | TO-3, SIP-11 | 19.28 |  |
| LM3886 | TI | 18 | $84^{\text {s }}$ | 50 | 60 | - - | 8 | 19 | 11.5 | 75 | - | - $\cdot$ | TO-220-11 | 5.94 | P |
| TDA7293 | ST | 24 | 120 | 30 | 30 | - - | - | 15 | 6.5 | 75 | $\cdot$ - | - $\cdot$ | TO-220-15 | 5.49 | P |
| higher voltage |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| PA340 | Apex | 20 | 350 | 2.2 | 16 | $\cdot$ | 10 | $32^{k}$ | 0.06 | 16 | $\cdot$ | - - | DDPak-7 | 21.45 | U |
| PA90 | Apex | 30 | 400 | 10 | 20 | - $\cdot$ | 100 | $300^{\text {e }}$ | 0.2 | 18 | - | - - | SIP-12 +tab | $188.00^{v}$ | U |
| PA15 | Apex | 100 | 450 | 2.0 | 25 | $\cdot$ $\cdot$ | 5.8 | 20 | 0.2 | $18^{n}$ | - | - - | SIP-10 | $185.00^{v}$ | U |
| PA98 | Apex | 30 | 450 | 21 | 25 |  | 100 | $1000^{\text {e }}$ | 0.2 | 18 | - | - - | SIP-12 +tab | $272.00^{V}$ | U |
| PA97 | Apex | 100 | 900 | 0.6 | 20 |  | 1 | $8^{\text {e }}$ | 0.01 | $3^{n}$ | - | - - | SIP-12 | $176.00^{V}$ | V |

Notes: (a) within categories, sorted by maximum voltage, then output current; the Apex parts are hybrid, and neither PCB nor instrument-box types are listed. (b) not to exceed total supply voltage. (c) $P_{\text {diss }}$ with case at $T_{\mathrm{C}}=50 \mathrm{C}$, based on $R_{\theta \mathrm{JC}}$. (d) when comp for $G>10$. (e) when comp for $G>100$. ( g ) internal JFETs limit current to 4 mA . ( h ) see notes. ( k ) for $C_{C}=4.7 \mathrm{pF}, G \geq 10$. ( n ) provided you can get the heat out of the package! (o) adjustable. (p) power package. (r) qty 1k. (s) 94 V w/o signal. (u) to ambient. (v) unit qty; see distributor prices (and your banker) for larger qty.

Comments: (A) dual, RRO. (B) RRIO. (C) with current monitor. (D) video. (E) VFB with CFB. (F) auto-zero, $4 \mu \mathrm{~V}$. (G) has $V_{\text {os }}$ trim; also in TO-99. (H) dual='6091. (I) update of L272. (J) dual, ADSL driver. (K) current-feedback, CFB. (L) can drive 10nF capacitive loads. (M) 1.1A min.
(N) Fairchild's version. ( O ) amp+buffer. (P) audio amplifier. (Q) slower OPA551 for $G=1$. (R) classic workhorse. (S) current-limit adjustment with resistor or external current. (T) slower OPA452 for $G=1$. (U) MOSFET output. (V) "inexpensive."

#### "Zero-drift" op-amps

These unusual op-amps, which include auto-zero and chopper-stabilized amplifiers, are tailored for precision (low-VOS) applications. They use internal MOS switches to measure and correct for input offset error. These are the only amplifiers with values of
untrimmed $V_{\text {OS }}$ down to $5 \mu \mathrm{~V}$ or less. See Table 5.6 on page 335.

High-voltage, high-power op-amps
You can get op-amps with maximum output currents of 25 amps or more, or with power supply voltages to 1 kV or

#### "Here Yesterday, Gone Today"

In its untiring quest for better and fancier chips, the semiconductor industry can sometimes cause you great pain. It might go something like this: you've designed and prototyped a wonderful new gadget; debugging is complete, and you're ready to go into production. When you try to order the parts, you discover that a crucial IC has been discontinued by the manufacturer! An even worse nightmare goes like this: customers have been complaining about late delivery on some instrument that you've been manufacturing for many years. When you go to the assembly area to find out what's wrong, you discover that a whole production run of boards is built, except for one IC that "hasn't come in yet." You then ask purchasing why they haven't expedited the order; turns out they have, just haven't received it. Then you learn from the distributor that the part was discontinued six months ago and that none is available!

Why does this happen, and what do you do about it? We've generally found four reasons that ICs are discontinued.

1. Obsolescence: Much better parts come along, and it doesn't make much sense to keep making the old ones. This has been particularly true with digital memory chips (e.g., small static RAMs and EPROMs, which are superseded by denser and faster versions each year), though linear ICs have not entirely escaped the purge. In these cases there is often a pin-compatible improved version that you can plug into the old socket.
2. Not selling enough: Perfectly good ICs sometimes disappear. If you are persistent enough, you may get an explanation from the manufacturer - "there wasn't enough demand," or some such story. You might characterize this as a case of "discontinued for the convenience of the manufacturer." We've been particularly inconvenienced by Harris's discontinuation of their splendid

HA4925 - a fine chip, the fastest quad comparator, now gone, with no replacement anything like it. In our first edition we reported that Harris also discontinued the HA2705 - another great chip, the world's fastest lowpower op-amp, gone without a trace! Since that time, Maxim came out with the MAX402, similarly a fast low-power op-amp. Lots of us used it; then - whammo - can't get it! Sometimes a good chip is discontinued when the wafer fabrication line changes over to a larger wafer size (e.g., from the original $3^{\prime \prime}$ diameter wafer to a $5^{\prime \prime}$ or $6^{\prime \prime}$ wafer).
3. Lost schematics: You might not believe it, but sometimes the semiconductor house loses track of the schematic diagram of some chip and can't make any more! This apparently happened with the Solid State Systems SSS-4404 CMOS 8-stage divider chip.
4. "Upgraded" production line: Sometimes a manufacturer will replace older test equipment (which may have been working just fine) with the latest and greatest new stuff. Problem is, the programs to run the new testers aren't finished yet. So, the wafer line could be making lots of chips ... but there's no way to test them. This scenario appears to have played out in the case of the magnificent OPA627, one of our all-time favorites (there was nearly a year in which you couldn't get these puppies, but, thankfully, it's back in production).
5. Manufacturer out of business: This also happened to the SSS-4404! If you're stuck with a board and no available IC, you've got several choices. You can redesign the board (and perhaps the circuit) to use something that is available. This is probably best if you're going into production with a new design or if you are running a large production of an existing board. A cheap and dirty solution is to make a little "daughterboard" that plugs into the empty IC socket and includes whatever it takes to emulate the nonexistent chip. Although this latter solution isn't terribly elegant, it gets the job done.
more! These are specialized (and expensive) devices, extremely useful for applications such as piezo drivers, servo drivers, and so on. See Table 4.2 b on the facing page for some favorites.

#### Micropower op-amps

At the other end of the spectrum, you can get op-amps with quiescent currents as low as a microamp or less. These things aren't blazingly fast - the LMC6442, with
$I_{\mathrm{Q}}=10 \mu \mathrm{~A}$ per amplifier, has an $f_{\mathrm{T}}$ of 10 kilohertz, and a slew rate ${ }^{40}$ of $0.004 \mathrm{~V} / \mu \mathrm{s}$ - but they do let you run a portable instrument just about forever on a single battery.

#### Instrumentation amplifiers

These are integrated differential amplifiers with settable voltage gain. They contain several op-amps internally and

[^49]image_name:Figure 4.87
description:
[
name: R1, type: Resistor, value: 10M, ports: {N1: input, N2: input_common}
name: R2, type: Resistor, value: 47k 1/2W, ports: {N1: input, N2: IC1_Out}
name: R3, type: Resistor, value: 50k, ports: {N1: IC1_InN, N2: IC1_Out}
name: R4, type: Resistor, value: 20k, ports: {N1: IC1_InP, N2: input_zero}
name: R5, type: Resistor, value: 50k, ports: {N1: IC1_Out, N2: var_gain}
name: R6, type: Resistor, value: 2.80k 1%, ports: {N1: var_gain, N2: IC1_InN}
name: R7, type: Resistor, value: 25k 1%, ports: {N1: var_gain, N2: IC1_InP}
name: R8, type: Resistor, value: 13k 1%, ports: {N1: gain, N2: ground}
name: R9, type: Resistor, value: 3.09k 1%, ports: {N1: gain, N2: ground}
name: R10, type: Resistor, value: 909 1%, ports: {N1: gain, N2: ground}
name: R11, type: Resistor, value: 280 1%, ports: {N1: gain, N2: ground}
name: R12, type: Resistor, value: 100, ports: {N1: input_common, N2: ground}
name: R13, type: Resistor, value: 10.0k 1%, ports: {N1: IC1_Out, N2: IC2_InP}
name: R14, type: Resistor, value: 10.0k 1%, ports: {N1: IC2_Out, N2: IC3_InP}
name: R15, type: Resistor, value: 10.0k 1%, ports: {N1: IC2_Out, N2: offset_polarity}
name: R16, type: Resistor, value: 10k 1% 10 turns, ports: {N1: output_offset, N2: IC3_InP}
name: R17, type: Resistor, value: 100k, ports: {N1: IC3_InP, N2: ground}
name: R18, type: Resistor, value: 10.0k 1%, ports: {N1: IC3_Out, N2: ground}
name: R19, type: Resistor, value: 10.0k 1%, ports: {N1: IC3_Out, N2: IC4_InP}
name: R20, type: Resistor, value: 10.0k 1%, ports: {N1: IC4_Out, N2: ground}
name: R21, type: Resistor, value: 10.0k 1%, ports: {N1: IC4_InP, N2: ground}
name: R22, type: Resistor, value: 6.8k, ports: {N1: IC2_InN, N2: ground}
name: R23, type: Resistor, value: 50, ports: {N1: output, N2: Zout}
name: R24, type: Resistor, value: 30k, ports: {N1: IC5_Out, N2: ground}
name: C1, type: Capacitor, value: 0.5uF, ports: {Np: input_common, Nn: ground}
name: C2, type: Capacitor, value: 4.7pF, ports: {Np: IC2_InN, Nn: ground}
name: C3, type: Capacitor, value: 150pF, ports: {Np: rolloff, Nn: ground}
name: C4, type: Capacitor, value: 1.5nF, ports: {Np: rolloff, Nn: ground}
name: C5, type: Capacitor, value: 15nF, ports: {Np: rolloff, Nn: ground}
name: C6, type: Capacitor, value: 0.1uF, ports: {Np: IC3_InN, Nn: ground}
name: C7, type: Capacitor, value: 0.1uF, ports: {Np: IC3_InN, Nn: ground}
name: C8, type: Capacitor, value: 0.1uF, ports: {Np: IC4_InN, Nn: ground}
name: C9, type: Capacitor, value: 0.1uF, ports: {Np: IC6_Out, Nn: ground}
name: D1, type: Diode, ports: {Na: IC1_InP, Nc: IC1_InN}
name: D2, type: Diode, ports: {Na: IC1_InN, Nc: IC1_InP}
name: IC1, type: OpAmp, value: OPA627, ports: {InP: IC1_InP, InN: IC1_InN, OutP: IC1_Out}
name: IC2, type: OpAmp, value: OPA627, ports: {InP: IC2_InP, InN: IC2_InN, OutP: IC2_Out}
name: IC3, type: OpAmp, value: OP-177, ports: {InP: IC3_InP, InN: IC3_InN, OutP: IC3_Out}
name: IC4, type: OpAmp, value: OP-177, ports: {InP: IC4_InP, InN: IC4_InN, OutP: IC4_Out}
name: IC5, type: Buffer, value: LT1010CT, ports: {In: IC5_In, Out: IC5_Out}
name: IC6, type: VoltageSource, value: LT1027D, ports: {Np: IC6_Out, Nn: ground}
name: S1, type: Switch, ports: {N1: rolloff, N2: ground}
name: S2, type: Switch, ports: {N1: offset_polarity, N2: ground}
name: S3, type: Switch, ports: {N1: gain, N2: ground}
]
extrainfo:The circuit is a laboratory DC amplifier with output offset. It includes multiple op-amps (OPA627 and OP-177) for amplification and buffering, diodes for protection, and a voltage source for reference. The circuit allows for variable gain and offset adjustments, and features a roll-off frequency selection. The output is buffered by an LT1010CT to drive low impedance loads.

Figure 4.87. Laboratory dc amplifier with output offset. Op-amp power supply connections and bypass capacitors are not shown explicitly, a common practice in circuit schematics.
excel in stability and common-mode rejection. Instrumentation amplifiers are discussed in §5.15.

Video and radiofrequency amplifiers
Specialized amplifiers for use with video signals, or with communications signals at frequencies from 10 MHz to 10 GHz , are widely available as fixed-gain amplifier modules. At these frequencies you generally don't use op-amps.

#### Dedicated amplifier variants

Microphone preamps, speaker amplifiers, stepping motor drivers, and the like are available as customized ICs with superior characteristics and ease of use.

## 4.8 Some typical op-amp circuits

### 4.8.1 General-purpose lab amplifier

Figure 4.87 shows a dc-coupled "decade amplifier" with settable gain, bandwidth, and wide-range dc output offset.
$\mathrm{IC}_{1}$ is a low-noise JFET-input op-amp with noninverting gain from unity $(0 \mathrm{~dB})$ to $\times 100(40 \mathrm{~dB})$ in accurately calibrated 10 dB steps; a vernier is provided for variable gain. $\mathrm{IC}_{2}$ is an inverting amplifier; it allows offsetting the output over a range of $\pm 10$ volts, accurately calibrated by the 10 turn pot $R_{16}$ by injecting current into the summing junction. $C_{3}-C_{5}$ set the high-frequency rolloff, because it is often a nuisance to have excessive bandwidth (and noise). $\mathrm{IC}_{5}$ is a power booster for driving low-impedance loads or cables; it can provide $\pm 150 \mathrm{~mA}$ output current.

Some interesting details: a $10 \mathrm{M} \Omega$ input resistor is small enough, since the bias current of the OPA627 is 10 pA (maximum, at room temperature), thus producing a 0.1 mV error with open input. $R_{2}$, in combination with clamp diodes $D_{1}$ and $D_{2}$, limits the input voltage at the op-amp to the range $V_{-}-0.6 \mathrm{~V}$ to $V_{+}+0.6 \mathrm{~V}$. With the protection components shown, the input can go to $\pm 150$ volts without damage. The JFET-input OPA627 was chosen for its combination of low input current ( $I_{\mathrm{B}}=1 \mathrm{pA}$, typ $)$, modest pre-
cision $\left(V_{\mathrm{OS}}=100 \mu \mathrm{~V}\right.$, max), low noise ( $e_{\mathrm{n}}=5 \mathrm{nV} / \sqrt{\mathrm{Hz}}$, typ), and wide bandwidth ( $f_{\mathrm{T}}=16 \mathrm{MHz}$, typ); the latter is needed to preserve some loop gain at the high-frequency end of the instrument $(100 \mathrm{kHz})$ when running at full gain $(40 \mathrm{~dB})$.

The output stage is an inverter with a unity-gain power buffer inside the feedback loop. The vintage LT1010 has plenty of slew rate, bandwidth, and muscle, with less than $10 \Omega$ open-loop output impedance (which of course is lowered by feedback; see $\S 2.5 .3 \mathrm{C}$ ). Both it and the OPA627 have enough slew rate ( $75 \mathrm{~V} / \mu$ s and $55 \mathrm{~V} / \mu \mathrm{s}$, respectively) to generate a full $\pm 15 \mathrm{~V}$ output swing at the full 100 kHz bandwidth of the instrument. A power buffer like this is good for isolating capacitive loads from the op-amp (more on this in Chapter $4 x$; see also $\S \S 4.6 .1 \mathrm{~B}$ and 4.6.2); furthermore, it takes the heat when driving a hefty load, which keeps $\mathrm{IC}_{2}$ cool, an important consideration with precision (low- $V_{\mathrm{OS}}$ ) op-amps. It takes lots of drive compared with an op-amp - up to 0.5 milliamp - but that's no problem when you're driving it with an op-amp.

The offset circuit consists of a precision LT1027 3terminal voltage reference IC. We'll learn more about these in Chapter 9; they generate a highly stable voltage output when powered from a noncritical dc rail that is at least 2 volts higher than their specified output voltage. This particular part comes in several grades, the best of which (LT1027A) has a maximum error of 1 mV , and is guaranteed to drift less than $2 \mathrm{ppm} /{ }^{\circ} \mathrm{C}$; for this application we'd save some money by choosing the inexpensive " $D$ " grade $\left(5.0 \mathrm{~V} \pm 2.5 \mathrm{mV} ; 5 \mathrm{ppm} /{ }^{\circ} \mathrm{C}\right)$. The OP177 is a highly stable precision op-amp ( $V_{\mathrm{OS}}<10 \mu \mathrm{~V}$, $\mathrm{TC} V_{\mathrm{OS}}<0.1 \mu \mathrm{~V} /{ }^{\circ} \mathrm{C}$ in its best grade) that provides a stable offsetting voltage. Capacitor $C_{6}$ bypasses noise on the reference voltage, and $C_{7}$ and $C_{8}$ reduce amplifier noise by limiting the bandwidth of the amplifiers. For a dc application like this you don't need, and don't want, lots of bandwidth. We'll talk in detail about this sort of precision design in Chapter 5.

Some additional points.

- In a circuit like this the input protection network can limit the ultimate bandwidth, because $R_{2}$ forms a lowpass filter in combination with the combined input capacitance of $\mathrm{IC}_{1}$, diode capacitance, and associated wiring capacitance. In this case the total capacitance is approximately 12 pF , which puts the 3 dB point at 300 kHz , well above the 100 kHz high-frequency limit of the instrument. To use a similar protection circuit in a wideband amplifier, you could reduce the value of $R_{2}$, put a small capacitor ( 47 pF , say) across it, or both. You could also use clamp diodes with lower capacitance, for example a 1N3595 or a PAD5 (see Chapter $1 x$ ).
- A really useful general-purpose laboratory amplifier should have true differential inputs. This is best done with an instrumentation amplifier, rather than an op-amp; see §5.15. Here we've compromised with a "pseudodifferential" configuration, in which the input common terminal (which is the return path for feedback), floating from circuit ground with a $100 \Omega$ resistor, is allowed to accommodate a small amount of signal from the input source. A better arrangement, though still not symmetrically differential, is shown in Figure 4.88, where a difference amplifier $\left(\mathrm{IC}_{7}\right)$ uses the floating input common as a reference. Note the use of a chassis-isolated BNC panel connector.
image_name:Figure 4.88
description:
[
name: IC1, type: Inverter, ports: {In: Node1, Out: Node2}
name: IC7, type: OpAmp, value: INA105, ports: {InP: Node2, InN: Node3, OutP: Node4}
name: R13, type: Resistor, value: R13, ports: {N1: Node4, N2: Node5}
name: R15, type: Resistor, value: R15, ports: {N1: Node5, N2: Node6}
name: S3, type: Switch, ports: {N1: Node3, N2: GND}
]
extrainfo:The circuit uses a difference amplifier (IC7) to cancel error from signal on input common. IC1 is an inverter that processes the input signal. R13 and R15 form a resistor network at the output. S3 is a switch connected to ground. The circuit is designed to handle input signals with a floating common.

Figure 4.88. Difference amp cancels error from signal on input common.

- In many situations it is preferable to introduce the dc offset at the input rather than at the output. Then you can change gain, without adjusting the offset, to zoom in on a portion of the input signal. This requires a much larger range of offset voltage, and other circuit changes as well. We'll see an example in Chapter 5.
- Watch out for op-amps that exhibit phase reversal when their inputs go more than 0.3 V below $V_{-}$; in such cases a restrictive input clamp must be used to prevent negative swings below that limit. This is a common defect of many op-amps, which the excellent OPA627 does not share.
- Contemporary instrumentation usually provides for remote operation, with digital control from a computer. This circuit, however, uses mechanical controls for gain, bandwidth, and offset. You could replace the mechanical switches with analog switches, and use a DAC to generate the offset, to adapt this instrument to digital control.
- The rolloff capacitors $C_{3}-C_{5}$ close the loop around the output amplifier pair $\left(\mathrm{IC}_{2}+\mathrm{IC}_{5}\right)$ at high frequencies, which is beneficial in terms of reducing noise. But it also promotes instability, owing to the combined phase shifts of the two amplifiers. This arrangement is still OK, though, as long as the bandwidth of buffer $\mathrm{IC}_{5}$ is much greater than that of amplifier $\mathrm{IC}_{2}$.

But that is not the case here: the OPA627 op-amp has a unity gain bandwidth of $f_{\mathrm{T}}=16 \mathrm{MHz}$, at which it specifies a $75^{\circ}$ phase margin. But the LT1010 buffer adds about $50^{\circ}$ of additional lagging phase shift, pushing the amplifier close to instability (see $\S 4.9$ for an explanation of phase margin and stability). The solution here is to use a small feedback capacitor around the op-amp ( $\left.4.7 \mathrm{pF}, C_{2}\right)$, which closes the high-frequency feedback path directly. This rolls off its gain to unity at about 1 MHz , at which frequency the buffer contributes less than $5^{\circ}$ additional lagging phase shift.

Exercise 4.26. Check that the gain is as advertised. How does the variable-offset circuitry work? At what frequency would the slew-rate-limited output swing drop below $\pm 15 \mathrm{~V}$ ?

### 4.8.2 Stuck-node tracer

Here's a nice example of an op-amp circuit with nonlinear feedback. A tricky troubleshooting problem is a so-called stuck node, in which there is a short somewhere on a circuit board. It may be an actual short-circuit in the wiring itself, or it may be that the output of some device (for example a digital logic gate, see Chapter 10) is held in a fixed state. It's hard to find, because anywhere you look on that line, you measure zero volts to ground.

A technique that does work, however, is to use a sensitive voltmeter to measure voltage drops along the stuck trace. A typical signal trace on a printed-circuit board might be $0.010^{\prime \prime}$ wide and $0.0013^{\prime \prime}$ thick ( 1 ounce per square foot), which has a resistance along the trace of $53 \mathrm{~m} \Omega / \mathrm{in}$. So if there's a device holding the line to ground somewhere and you inject a diagnostic current of 10 mA dc somewhere else, there will be a voltage drop of $530 \mu \mathrm{~V}$ per inch in the direction of the stuck node.

Let's design a stuck-node tracer. It should be battery powered so that it can float anywhere on the powered circuit under test. It should be sensitive enough to indicate a drop of as little as $\pm 100 \mu \mathrm{~V}$ on its zero-center meter, with larger meter deflections for larger drops. Ideally it should have a nonlinear scale, so that even for voltage drops of tens of millivolts the meter will not go off scale. And with some care it should be possible to design a circuit that draws so little battery current that we can omit the on/off switch: 9 V batteries or AA-size cells give nearly their full shelf life of several years at continuous drain currents of less than $20 \mu \mathrm{~A}$ (they have capacities of about 500 mAh and 2500 mAh , respectively).

With a floating supply provided by batteries, the simplest circuit is a high gain inverting amplifier driving a
zero-center meter (Figure 4.89). Because the input and output are both intrinsically bipolarity, it's probably best to use a pair of AA cells, running the op-amp from $\pm 1.5$ volt unregulated supplies. The back-to-back Schottky diodes reduce the gain gracefully at large output swings and prevent pegging; Figure 4.90 plots the resulting meter deflection versus $V_{\text {in }}$.
image_name:Figure 4.89
description:
[
name: 1k, type: Resistor, value: 1k, ports: {N1: Vin, N2: InN}
name: 100k, type: Resistor, value: 100k, ports: {N1: Out, N2: +1.5}
name: 8k, type: Resistor, value: 8k, ports: {N1: Out, N2: Vout}
name: 1N5711, type: Diode, ports: {Na: Out, Nc: +1.5}
name: 1N5711, type: Diode, ports: {Na: +1.5, Nc: Out}
name: OP193E, type: OpAmp, value: OP193E, ports: {InP: GND, InN: InN, OutP: Out, OutN: Out, Vdd: +1.5, -Vdd: -1.5}
]
extrainfo:The circuit is a high-gain inverting amplifier with nonlinear feedback using Schottky diodes to prevent pegging. It uses a zero-center meter for output indication, powered by ±1.5V from AA batteries.

Figure 4.89. Stuck-node tracer: high-gain floating dc amplifier with nonlinear feedback.
image_name:Figure 4.90
description:The graph in Figure 4.90 is a plot showing the relationship between input voltage and meter deflection in a high-gain amplifier circuit. The x-axis represents the input voltage in volts, ranging from ±100 microvolts (μV) to ±1 volt (V) on a logarithmic scale. The y-axis represents the meter deflection as a percentage, ranging from 0% to 100%.

There are two curves depicted in the graph:
1. **No Diodes Curve**: This curve shows the performance of the amplifier without the use of diodes, labeled with a voltage gain \( G_V = 100 \). It demonstrates a steep increase in meter deflection with increasing input voltage, indicating a highly sensitive response to changes in input.

2. **With Diodes Curve**: This curve represents the amplifier's performance with diodes incorporated into the circuit. It shows a more gradual increase in meter deflection compared to the no diodes curve. The presence of diodes introduces nonlinear feedback, which helps to prevent the meter from pegging at high input voltages, allowing for a larger dynamic range.

Overall, the graph illustrates how the inclusion of diodes in the amplifier circuit moderates the response, providing a more controlled and extended range of operation. The nonlinear feedback introduced by the diodes is crucial for achieving a balanced performance, especially in applications requiring large dynamic ranges.

Figure 4.90. Stuck-node tracer achieves large dynamic range through nonlinear feedback.

The major difficulty in this design is in achieving an input offset of less than $100 \mu \mathrm{~V}$ while maintaining micropower current drain, all with supply voltages of just $\pm 1.5$ volts. The OP193 is specified to operate down to 2 V total supply voltage, and its output stage swings to the negative rail and to within a volt of the positive rail. In its best grade (" $E$ " suffix) its offset voltage is $75 \mu \mathrm{~V}$, maximum. Its quiescent current of just $15 \mu \mathrm{~A}$ ensures that the batteries will last their full shelf life, since that current would provide continuous operation for over 150,000 hours from a 2500 mAh battery.

Some additional points.

- One subtle problem with this circuit is that an alkaline battery at the end of its life is down to about 1.0 V
terminal voltage; so you would have insufficient headroom to provide full-scale positive output voltage $(+0.5 \mathrm{~V})$, given the all-npn output stage. A solution is to use a higher battery voltage (e.g., 3 V lithium cells, or multiple alkaline 1.5 V AA cells). But operation from a single pair of AA cells is an elegance worth preserving. In this case you would do better to use an op-amp with true rail-to-rail output, for example, the CMOS OPA336. The latter has a quiescent current of $20 \mu \mathrm{~A}$, operates down to 2.3 V total supply voltage, and has an untrimmed offset voltage of $125 \mu \mathrm{~V}$. Its input voltage range goes to the negative rail and to within 1 volt of the positive rail; the latter is fine here, because we have chosen an inverting amplifier configuration with both inputs at 0 V .
- We rather artificially constrained the circuit design by choosing a zero-center analog meter and then insisting on using just a pair of AA alkaline cells. In real life you'd probably be happier with an audio output, with the pitch increasing with input voltage drop; then you could keep your eye on the circuit as you probe around. For this job you'd probably use a simple current-controlled oscillator, built with an op-amp relaxation oscillator or a 555-type timer IC (Chapter 7); for a noncritical application you don't need the linearity and stability of the VCO we designed in Figure 4.83.
- Don't forget the "rail-splitter" techniques we discussed in $\S 4.6 .1 \mathrm{~B}$; you can always use those tricks to create a split plus and minus rail, for example, from a single 9 V battery. With $\pm 4.5 \mathrm{~V}$ rails, you have a much wider range of op-amps to choose from. We were forced to choose from a rather small selection that run on 2 V total supply, draw only tens of microamps supply current, and have "precision" low input offset voltage. Once you have 5 V total supply available (a 9 V battery is down to 6 V at the end of its life), there are literally hundreds of available op-amps, dozens of which run on micropower current drain and have precision low offsets. See, for example, Table 5.5 on page 320.

### 4.8.3 Load-current-sensing circuit

Figure 4.91 shows a hefty ( 10 kW !) power supply driving a 100 amp load; the illustrated circuit provides a voltage output proportional to load current, for use with a current regulator, metering circuit, or whatever. The output current is sensed with a current shunt, a calibrated manganinmetal 4-terminal power resistor $R_{\mathrm{S}}$, of resistance $0.0005 \Omega$, whose "Kelvin connection" of four leads ensures that the sensed voltage does not depend on a low-resistance bond to the sensing terminals (as would be the case if you tried
to do the same thing with a conventional 2-terminal resistor). The voltage drop goes from 0 to 50 mV , with probable common-mode offset caused by the effects of resistance in the ground lead (note that the power supply is connected to chassis ground at the output). For that reason the op-amp is wired as a differential amplifier, with a gain of 200 . Voltage offset is trimmed externally with $R_{8}$, as the venerable LM358A doesn't have internal trimming circuitry. A zener reference with a few percent stability is adequate for trimming, because the trimming is itself a small correction (you hope!). The supply voltage, $V_{+}$, could be unregulated, since the power-supply rejection of the op-amp is more than adequate, 85 dB (typ) in this case.

Some additional points.

- Chassis ground and circuit ground would be connected together, somewhere. But there could easily be a volt or so separating circuit ground from the sensing point along the high-current negative return, because of the very large currents flowing. For that reason we connected the negative supply lead of the op-amp to the more negative end of the current-shunt output. This ensures that the commonmode voltage appearing at the op-amp input never goes below its negative rail; it is a "single-supply" op-amp, with operating common-mode range to its negative rail.
- Low offset voltage is important in this application; for example, to achieve $1 \%$ accuracy in a current measurement made at $10 \%$ of full-scale load current (i.e., a 10 A load, producing a sense voltage of 5 mV ) requires an offset voltage no greater than $50 \mu \mathrm{~V}$ ! We chose the vintage LM358A for our initial design, because it costs only 20 cents. But its poor untrimmed offset ( 3 mV , max) necessitates external manual trimming; and its lack of external trim terminals forced us to use lots of components. The need for manual trimming might not seem important if you're just building one of these for your lab; but in production it's an extra step, requiring a test setup and procedure, as well as additional parts inventory, etc.
- So, you might choose instead the LT1006, a single opamp that lets you trim externally with a single 10k pot. However, its improved performance ( $V_{\mathrm{OS}}=80 \mu \mathrm{~V}$, max, untrimmed) in the least expensive grade -40 times better than the LM358A - means that you hardly need to trim at all. Carrying this idea further, you could choose instead the LT1077A, a single-supply op-amp with $40 \mu \mathrm{~V}$ maximum untrimmed offset; it too can be trimmed externally.
- For the utmost in accuracy you should use a chopper-stabilized ("zero-drift") op-amp, for example the LTC1050C. It has $5 \mu \mathrm{~V}$ maximum offset voltage in the cheapest grade (combined with sub-nanoamp input
image_name:Figure 4.91. High-power current-sensing amplifier.
description:
[
name: R1, type: Resistor, value: 100Ω 1%, ports: {N1: Node1, N2: Node2}
name: R2, type: Resistor, value: 20.0k, 1%, ports: {N1: Node2, N2: Vout}
name: R3, type: Resistor, value: 100Ω 1%, ports: {N1: Node3, N2: GND}
name: R4, type: Resistor, value: 20.0k, 1%, ports: {N1: Node4, N2: GND}
name: R6, type: Resistor, value: 200k, ports: {N1: Node5, N2: Node1}
name: R7, type: Resistor, value: 3.3k, ports: {N1: V+, N2: Node6}
name: R8, type: Resistor, value: 10k, ports: {N1: Node5, N2: Node7}
name: RS, type: Resistor, value: 0.0005Ω, 4-term, ports: {N1: OUT+, N2: OUT-}
name: IC1, type: OpAmp, value: LM358A, ports: {InP: Node3, InN: Node2, OutP: Vout}
name: 1N5234, type: Diode, ports: {Na: Node6, Nc: GND}
]
extrainfo:The circuit is a high-power current-sensing amplifier designed to measure current using a shunt resistor (RS) with a very low resistance value of 0.0005Ω. The output voltage (Vout) is proportional to the load current (Iload), with a gain factor of 0.1V/A. The op-amp IC1 (LM358A) is configured to amplify the voltage across the shunt resistor. The diode (1N5234) provides a 6.2V reference voltage. The circuit is powered by an unregulated supply voltage (V+) ranging from +12V to +30V.

Figure 4.91. High-power current-sensing amplifier.
bias current, which doesn't matter here). This op-amp includes on-chip capacitors for its chopper, and operates from a single-supply (with input common-mode range to the negative rail), just like the LM358. Its $5 \mu \mathrm{~V}$ offset voltage corresponds to $1 \%$ accuracy at $1 \%$ of full scale; that's a dynamic range of $10,000: 1$, not bad for a simple circuit. See Table 5.6 on page 335 for auto-zero op-amp choices.

- Finally, an interesting design alternative is to do high-side current sensing. That is, the shunt is connected instead to the out+ power terminal. This has the advantage of keeping all the circuit grounds (power supply, and load) connected together. We'll see how to do this in the advanced Chapter $9 x$.

### 4.8.4 Integrating suntan monitor

We nerds don't ordinarily go to the beach. But when we do, we like to rely on some electronics to tell us when to turn over. What we want to monitor, of course, is the integrated dose of tan-producing (UV-rich) sunlight.

There are many ways to accomplish this; in fact, we'll revisit this task when we turn to mixed-signal (analog + digital) electronics (in Chapter 13), and again when we're looking for nifty things to do with microcontrollers (in Chapter 15). Here we want to show how an op-amp integrator can be used to build a suntan monitor circuit.

The idea is to integrate (accumulate) the photocurrent from a sensor whose output is proportional to the intensity
of tanning sunlight. We'll imagine that we have a photodiode, optically filtered to pass only the UV rays of interest, with an output short-circuit current of $\sim 1 \mathrm{nA}$ (nominal) in full sunlight; we'll assume that the photocurrent might range down to a tenth of this value, or so, in hazy sun.

#### A. First try: direct integration

The circuit in Figure 4.92 is a reasonable first try. It uses a single-supply CMOS micropower op-amp ( $10 \mu \mathrm{~A}$ per amplifier), powered from a 9 V battery, to integrate the (negative) photocurrent. A nanoamp produces a positive-going ramp of $0.5 \mathrm{mV} / \mathrm{s}$ at the op-amp's output, which we connect to a Schmitt trigger comparator with settable positive threshold. The LM385-2.5Z micropower two-terminal (zener-type) voltage reference then gives us a range of 0 to 1.5 hours ( $\sim 5000 \mathrm{~s}$ ) full sunlight equivalent (let's call it "FSE"), at which point the comparator output goes to ground, driving the piezo alarm. The latter draws 15 mA , a substantial battery load, but it is very loud, so even a dozing nerd will quickly enough shut the thing off (via the "reset" button). This circuit draws about $50 \mu \mathrm{~A}$ when integrating, good for about 8000 hours of operation (a 9 V battery has a capacity of 500 mAh at low drain). 8000 hours is about a year, so that's a lot of tanning; the battery will die of old age first.

Exercise 4.27. The LM385 requires a minimum of $10 \mu \mathrm{~A}$ of current for proper operation. What does the circuit provide, at the end of battery life ( 6 V )?
image_name:Figure 4.92
description:
[
name: C1, type: Capacitor, value: 2µF, ports: {Np: Vbatt, Nn: reset}
name: IC1, type: OpAmp, value: IC1, ports: {InP: GND, InN: Vbatt, OutP: film, OutN: GND}
name: IC2, type: OpAmp, value: IC2, ports: {InP: R3, InN: film, OutP: Panasonic, OutN: GND}
name: R1, type: Resistor, value: 10M, ports: {N1: film, N2: R3}
name: R2, type: Resistor, value: 100k, ports: {N1: R3, N2: GND}
name: R3, type: Resistor, value: 500k, ports: {N1: R3, N2: GND}
name: R4, type: Resistor, value: 200k, ports: {N1: Vbatt, N2: LM385-2.5}
name: Diode, type: Diode, ports: {Na: GND, Nc: Vbatt}
name: LM385-2.5, type: VoltageSource, ports: {Np: LM385-2.5, Nn: GND}
]
extrainfo:The circuit is an integrating suntan monitor. It uses a photodiode to measure UV light, generating a current that is integrated by the op-amp IC1. The output voltage increases over time, indicating the cumulative exposure to UV light. A Schmitt trigger (IC2) provides hysteresis, stabilizing the output signal to drive a buzzer (Panasonic EFB-CC28C15) when a threshold is reached. The LM385-2.5 provides a reference voltage of 2.5V.

Figure 4.92. Integrating suntan monitor, first try.

Exercise 4.28. How much hysteresis does Schmitt trigger $\mathrm{IC}_{2}$ provide? How will that affect the operation?

#### B. Second try: two-step conversion

One problem with the last circuit is that the unfiltered photodiode current is at least a few microamps, in direct sunlight. Trying to cut down the light by a factor of a thousand is risky, because you get light leaks, etc., that cause large errors.

The circuit in Figure 4.93 fixes that, by first converting the photocurrent (however large its magnitude) to a voltage, then integrating that in a second stage where we can choose an input resistor to generate a current in the nanoamp range. Now, however, we've got to use split supplies. That's because whichever polarity we choose for the transresistance (current to voltage) amplifier's output (by connecting the photodiode appropriately), the subsequent integrator's output will be the opposite polarity; integrators invert. In our circuit we used a 2.5 V reference to split the 9 V battery; most of the current in the circuit is between the positive and negative rails, so the reference needs less than $20 \mu \mathrm{~A}$ of bias. ${ }^{41}$ In this circuit we've shown a two-pole power switch, wired so the integrating capacitor is held reset until power is turned on.

The integrator output triggers a Schmitt comparator, as before, driving the mighty-lunged piezo screamer. Note that its large drive current is rail-to-rail; it does not pass through our ground reference. The circuit's operating cur-

[^50]rent is about $60 \mu \mathrm{~A}$, good for nearly a year of continuous operation.

A final note: the LMC6044 is a quad, rail-to-rail output, micropower op-amp ( $10 \mu \mathrm{~A} /$ amplifier). So if a stiff ground reference were needed, the unused op-amp section could be configured as in Figure 4.73, with the stabilizing trick of Figure 4.76A.

#### C. The "Mark-III" suntan integrator

It's always fun to see how elegantly you can shrink down circuit complexity. In this case there's a nice trick you can use to eliminate the two-stage integration, namely, a "current divider." Figure 4.94 shows how it's done: the photocurrent drives a pair of resistors, bridging the same voltage (because the inverting input is a virtual ground); the current divides proportional to the relative conductance, in this case in the ratio of $1000: 1$ if pot $R_{2}$ is turned to minimum resistance. That means that a photocurrent of $1 \mu \mathrm{~A}$ would inject a current of 1 nA into the integrator. If you prefer, you can think of the circuit as a resistive load ( $R_{1}$ in series with $R_{2}$, which easily dominates $R_{3}$ ), which develops a voltage $V_{\text {in }}=I_{\text {diode }}\left(R_{1}+R_{2}\right)$; that voltage is the input to the integrator, via $R_{3}$. Because the voltage developed by the photocurrent can range up to nearly a volt, it's necessary to back-bias the detector diode, in this case with a forward-biased diode $D_{2}$, which generates a -0.4 V rail.

The integrator's positive-going output ramp drives Schmitt comparator $\mathrm{A}_{2}$, with fixed comparison voltage provided by reference $D_{1}$. Its output drives the by-now usual piezo alarm.

Now for the elegance: it turns out you can get, packaged in a single small IC, a combination op-amp, comparator, and voltage reference. The MAX951 shown is just one of several such offerings, and it fills the bill here. It is because of the internal connection of $D_{1}$ and $\mathrm{IC}_{2}$ 's inverting input that we were forced to put the suntan control at the input, rather than at the comparator.

A few additional comments.

- The accuracy of the current divider depends on the accuracy of the virtual ground. The op-amp shown has a maximum offset voltage of 3 mV , so at $10 \%$ full sunlight and with the control set to minimum resistance (maximum bake cycle), the error is about $30 \%$ ( 10 mV signal, 3 mV offset). In other words, the circuit elegance involves a compromise in performance, relative to the more straightforward (some might say heavy-handed) approach in Figure 4.93, where the error is about $3 \%$ at minimum sunlight.
- Diode $D_{2}$ will be forward biased by the IC's quiescent
image_name:A
description:
[
name: G5842 Hamamatsu, type: Diode, ports: {Na: 1, Nc: GND}
name: IC1, type: OpAmp, ports: {InP: GND, InN: 1, OutP: 2}
name: IC2, type: OpAmp, ports: {InP: GND, InN: 2, OutP: 3}
name: IC3, type: OpAmp, ports: {InP: 3, InN: 4, OutP: 5}
name: 9V battery, type: VoltageSource, value: 9V, ports: {Np: +, Nn: GND}
name: LM385-2.5Z, type: Diode, ports: {Na: GND, Nc: -2.5}
name: 100pF, type: Capacitor, value: 100pF, ports: {Np: 2, Nn: GND}
name: 2µF, type: Capacitor, value: 2µF, ports: {Np: 3, Nn: GND}
name: 1M, type: Resistor, value: 1M, ports: {N1: 2, N2: 1}
name: 1000M, type: Resistor, value: 1000M, ports: {N1: 2, N2: 3}
name: 50k, type: Resistor, value: 50k, ports: {N1: 3, N2: 4}
name: 10M, type: Resistor, value: 10M, ports: {N1: 4, N2: 5}
name: 1M, type: Resistor, value: 1M, ports: {N1: -1.8, N2: -2.5}
name: 390k, type: Resistor, value: 390k, ports: {N1: -2.5, N2: GND}
name: 300k, type: Resistor, value: 300k, ports: {N1: +, N2: 6}
name: 1k, type: Resistor, value: 1k, ports: {N1: 3, N2: N.C.}
name: N.O., type: Switch, ports: {N1: 6, N2: GND}
name: Murata PKB30SPC-2001, type: Other, ports: {N1: 5, N2: +6}
]
extrainfo:The circuit is an integrating suntan monitor using photodiode G5842 Hamamatsu and LMC6044 op-amps. It measures sunlight intensity and controls a bake cycle. The spectral response of the photodiode is shown, with maximum sensitivity around 350 nm.
image_name:B
description:The graph labeled 'B' is a spectral response graph depicting the sensitivity of the Hamamatsu G5842 photodiode as a function of wavelength.

1. **Type of Graph and Function:**
- This is a spectral response graph, showing how the photodiode's sensitivity varies with different wavelengths of light.

2. **Axes Labels and Units:**
- The x-axis is labeled 'Wavelength (nm)' and spans from 250 nm to 400 nm.
- The y-axis is labeled 'Sensitivity (mA/W)', indicating the photodiode's sensitivity in milliamperes per watt. The scale ranges from 0 to 60 mA/W.

3. **Overall Behavior and Trends:**
- The graph shows an initial increase in sensitivity starting from 250 nm, with a gradual rise as the wavelength increases.
- There is a noticeable peak in sensitivity between 350 nm and 400 nm, indicating the wavelength range where the photodiode is most responsive.

4. **Key Features and Technical Details:**
- The peak sensitivity occurs around the 350-400 nm range, reaching up to approximately 60 mA/W.
- The sensitivity increases sharply from 250 nm, peaks, and then slightly decreases towards 400 nm.

5. **Annotations and Specific Data Points:**
- No specific annotations or markers are present, but the peak sensitivity is a critical feature of this graph.

Figure 4.93. Integrating suntan monitor, second try; FSE is "full sunlight equivalent." A. Schematic. B. Spectral response of the Hamamatsu G5842 photodiode, whose short-circuit photocurrent in sunlight is about $1 \mu \mathrm{~A}$.
current of $7 \mu \mathrm{~A}$ as long as the photocurrent is less than this value. Thus the biasing resistor $R_{6}$ can be omitted unless a maximum photocurrent of more than about $5 \mu \mathrm{~A}$ is anticipated.
image_name:Figure 4.93 A
description:
[
name: R1, type: Resistor, value: 100k, ports: {N1: GND, N2: N1}
name: R2, type: Resistor, value: 500k, ports: {N1: N1, N2: GND}
name: R3, type: Resistor, value: 100M, ports: {N1: N2, N2: N1}
name: R4, type: Resistor, value: 50k, ports: {N1: OutA1, N2: InN_A2}
name: R5, type: Resistor, value: 10M, ports: {N1: OutA2, N2: InP_A2}
name: R6, type: Resistor, value: 200k, ports: {N1: VDD, N2: LED}
name: C1, type: Capacitor, value: 10μF, ports: {Np: OutA1, Nn: GND}
name: A1, type: OpAmp, value: A1, ports: {InP: N2, InN: GND, OutP: OutA1, OutN: GND}
name: A2, type: OpAmp, value: A2, ports: {InP: InP_A2, InN: InN_A2, Out: OutA2}
name: D1, type: Diode, value: 1.25V, ports: {Na: InN_A2, Nc: GND}
name: D2, type: Diode, value: IN4148, ports: {Na: OutA2, Nc: GND}
name: VoltageSource, type: VoltageSource, value: 3V to 6V, ports: {Np: VDD, Nn: GND}
]
extrainfo:The circuit is an integrating suntan monitor with a photodiode generating a photocurrent (ID) of 1μA. The current divider formed by R3 and R1 scales the photocurrent. A1 is an op-amp integrator, while A2 is a comparator. D1 provides a reference voltage of 1.25V. The circuit operates within 3V to 6V range, and R6 is omitted unless higher photocurrents are anticipated.

Figure 4.94. Integrating suntan monitor, third try. $\mathrm{A}_{1}, \mathrm{~A}_{2}$, and $D_{1}$ all live inside a MAX951 multifunction chip. $A_{2}$ is a comparator.

- The MAX951 has a specified operating voltage range of 2.7 V to 7 V . The low-voltage operation is a pleasant bonus; but for this particular IC it also means that we cannot run directly from a 9 V battery, unless we use a voltage regulator (see Chapter 9) to reduce the supply voltage to 7 V or less. This illustrates an important lesson, namely, that you have to watch out for low maximum supply-voltage ratings when using ICs intended for low-voltage operation. It also illustrates the trend of IC
manufacturers toward lower supply voltages for their new product designs.

## 4.9 Feedback amplifier frequency compensation

We first met feedback in Chapter 2 (§2.5), where we saw its beneficial effects on stability and predictability of amplifier gain, and the reduction of an amplifier's inherent nonlinearities. We saw, also, how it affects input and output impedances of amplifiers: for example, by sensing output voltage, and using series feedback at the input, the input impedance is raised and the output impedance is lowered, both by a factor of the loop gain. All is not rosy, though: the combination of gain with feedback creates the possibility of oscillation. Here, in the context of op-amps, we continue the treatment of negative feedback, looking at the important subject of frequency compensation - the business of preventing oscillation in amplifiers with negative feedback. The material in $\S 2.5$ is a necessary background for the sections that follow.

Let's begin by looking at a graph of open-loop voltage gain versus frequency for several op-amps: you'll typically see something like the curves in Figure 4.95. From a superficial look at such a Bode plot (a log-log plot of openloop gain and phase versus frequency) you might conclude that the OP27 is an inferior op-amp, since its open-loop gain drops off so rapidly with increasing frequency. In fact, that rolloff is built into the op-amp intentionally and is
image_name:Figure 4.95
description:The graph in Figure 4.95 is a Bode plot showing the open-loop voltage gain versus frequency for three different operational amplifiers (op-amps): OP-27, OP-37, and HA-5147.

1. **Type of Graph and Function:**
- This is a Bode plot, which is a type of graph used to represent the frequency response of a system, specifically showing the magnitude of gain in decibels (dB) against frequency in hertz (Hz).

2. **Axes Labels and Units:**
- The x-axis represents frequency, labeled in hertz (Hz), with a logarithmic scale ranging from 10 Hz to 100 MHz.
- The y-axis represents voltage gain, labeled in decibels (dB), with a linear scale ranging from -20 dB to 120 dB.

3. **Overall Behavior and Trends:**
- Each curve shows a decrease in gain as frequency increases, characteristic of an RC low-pass filter. The gain starts high at low frequencies and rolls off at higher frequencies.
- The rolloff begins around 10 Hz and continues steadily, indicating a consistent decrease in gain with increasing frequency.

4. **Key Features and Technical Details:**
- The OP-27 curve starts at around 120 dB and shows a steep decline in gain as frequency increases, following a slope of approximately -6 dB per octave.
- The OP-37 and HA-5147 curves are similar in shape but differ slightly in their initial gain and rolloff characteristics. The OP-37 has a slightly higher initial gain compared to the OP-27.
- The HA-5147 curve is positioned between the OP-27 and OP-37 curves, indicating its gain characteristics are intermediate between the two.
- All curves converge towards lower gain levels as they approach higher frequencies, nearing 0 dB around 10 MHz.

5. **Annotations and Specific Data Points:**
- The graph includes annotations labeling the curves for each op-amp: OP-27, OP-37, and HA-5147.
- There are no specific numerical markers for cutoff frequencies or other critical points, but the general trend indicates a standard decline in gain across the frequency spectrum.

Figure 4.95. Open-loop gain versus frequency for three similar opamps.
recognizable as the same $-6 \mathrm{~dB} /$ octave curve characteristic of an $R C$ lowpass filter. The OP37, by comparison, is identical to the OP27 except that it is decompensated (and similarly for the discontinued ${ }^{42}$ HA-5147). Op-amps are most often internally compensated, with decompensated and uncompensated varieties sometimes available. Let's take a look at this business of frequency compensation.

### 4.9.1 Gain and phase shift versus frequency

An op-amp (or, in general, any multistage amplifier) will begin to roll off at some frequency because of the lowpass filters formed by signals of finite source impedance driving capacitive loads within the amplifier stages. For instance, it is common to have an input stage consisting of a differential amplifier, perhaps with current-mirror load (see the LF411 schematic in Figure 4.43), driving a commonemitter second stage. For now, imagine that the capacitor labeled $C_{\mathrm{C}}$ in that circuit is removed. The high output impedance of the input stage $Q_{2}$, in combination with the combined capacitance seen at its output, forms a lowpass filter whose 3 dB point might fall somewhere in the range of 100 Hz to 10 kHz .

The decreasing reactance of this capacitance with increasing frequency gives rise to the characteristic $6 \mathrm{~dB} /$ octave rolloff: at sufficiently high frequencies (which may be below 1 kHz ), the capacitive loading dominates the collector load impedance, resulting in a voltage gain $G_{\mathrm{V}}=g_{m} X_{\mathrm{C}}$, i.e., the gain drops off as $1 / f$. It also produces a $90^{\circ}$ lagging phase shift at the output relative to the input signal. (You can think of this as the tail of an $R C$ low-

[^51]pass filter characteristic, where $R$ represents the equivalent source impedance driving the capacitive load. However, it is not necessary to have any actual resistors in the circuit.)

In a multistage amplifier there will be additional rolloffs at higher frequencies, caused by lowpass filter characteristics in the other amplifier stages, and the overall open-loop gain will look something like that shown in Figure 4.96. The open-loop gain begins dropping at $6 \mathrm{~dB} /$ octave at some low frequency $f_{1}$, because of capacitive loading of the firststage output. It continues dropping off with that slope until an internal $R C$ of another stage rears its ugly head at frequency $f_{2}$, beyond which the rolloff goes at $12 \mathrm{~dB} /$ octave, and so on.
image_name:Figure 4.96
description:The graph in Figure 4.96 is a Bode plot depicting the open-loop gain of a multistage amplifier versus frequency. Both axes are on a logarithmic scale. The vertical axis represents the open-loop gain in decibels (dB), and the horizontal axis represents frequency.

Overall Behavior and Trends:
- **Initial Flat Region:** At low frequencies, the gain remains constant, indicating no attenuation.
- **First Slope:** Beginning at frequency \( f_1 \), the gain starts to decrease at a rate of \( 6 \text{ dB/octave} \). This is due to the capacitive loading of the first stage output.
- **Second Slope:** At frequency \( f_2 \), the slope steepens to \( 12 \text{ dB/octave} \), indicating the influence of an internal RC lowpass filter in another stage.
- **Third Slope:** Beyond frequency \( f_3 \), the roll-off increases further to \( 18 \text{ dB/octave} \), suggesting additional filtering effects.

Key Features and Technical Details:
- **Cutoff Frequencies:** The graph highlights key frequencies \( f_1 \), \( f_2 \), and \( f_3 \), where changes in slope occur.
- **Slope Changes:** The transitions at these frequencies are marked by dashed lines, showing the potential extension of each section if the slope remained constant.

Annotations and Specific Data Points:
- The plot is annotated with the slope values (6 dB/octave, 12 dB/octave, 18 dB/octave) to clearly indicate the rate of gain decrease at different frequency ranges.

Figure 4.96. Multistage amplifier: gain versus frequency.
What is the significance of all this? Remember that an $R C$ lowpass filter has a phase shift that looks as shown in Figure 4.97. Each lowpass filter within the amplifier has a similar phase-shift characteristic, so the overall phase
image_name:Figure 4.96
description:The graph in Figure 4.96 is a Bode plot, which is used to represent the gain and phase shift of a multistage amplifier as a function of frequency. It consists of two separate plots: the upper plot shows the gain (V_out/V_in) in decibels (dB) versus frequency, and the lower plot shows the phase shift in degrees versus frequency.

Gain Plot:
- **Type of Graph:** Bode plot (gain versus frequency).
- **Axes Labels and Units:**
- **Y-axis:** Gain (V_out/V_in) in decibels (dB), ranging from 0 dB to -20 dB.
- **X-axis:** Frequency on a logarithmic scale, marked at specific points like 0.1f_3dB, f_3dB, and 10f_3dB.
- **Overall Behavior and Trends:**
- The gain remains constant at 0 dB over a low-frequency range, indicating no attenuation.
- As frequency increases, the gain decreases linearly, indicating a low-pass filter characteristic.
- The slope of the gain decrease is annotated with values like 6 dB/octave, 12 dB/octave, and 18 dB/octave, showing different stages of roll-off.

Phase Shift Plot:
- **Type of Graph:** Bode plot (phase shift versus frequency).
- **Axes Labels and Units:**
- **Y-axis:** Phase Shift in degrees, ranging from 0° to -90°.
- **X-axis:** Frequency on a logarithmic scale, marked similarly to the gain plot.
- **Overall Behavior and Trends:**
- The phase shift starts at 0° at low frequencies and decreases towards -90° as frequency increases.
- Key markers are annotated, such as a 6° shift at 0.1f_3dB and an 84° shift at 10f_3dB.

Key Features and Technical Details:
- **Cutoff Frequency (f_3dB):** The frequency at which the gain starts to roll off, marked on the x-axis.
- **Phase Shift Characteristics:** Important for understanding the stability of the amplifier when used in feedback configurations, as excessive phase shift can lead to oscillations.
- **Annotations:** Slope values on the gain plot indicate the rate of gain decrease, and specific phase shift values are noted on the phase plot.

### Significance:
The Bode plot illustrates the frequency response of the amplifier, highlighting the gain reduction at higher frequencies and the associated phase shift. These characteristics are critical for designing stable amplifiers, particularly in feedback applications where phase shift can lead to oscillations if not managed properly.
image_name:Figure 4.97
description:The graph in Figure 4.97 is a Bode plot consisting of two parts: a gain plot and a phase plot, both plotted against frequency on a logarithmic scale.

Gain Plot:
- **Type of Graph:** The upper part is a gain versus frequency plot.
- **Axes Labels and Units:**
- The vertical axis represents gain \( V_{out}/V_{in} \) in decibels (dB).
- The horizontal axis represents frequency in a logarithmic scale.
- **Overall Behavior and Trends:**
- The gain is constant at 0 dB at low frequencies, indicating no attenuation.
- As frequency increases, the gain begins to decrease, showing a slope of approximately -20 dB/decade.
- **Key Features and Technical Details:**
- The plot shows a typical low-pass filter behavior, with a flat response at low frequencies and a roll-off at higher frequencies.
- The cutoff frequency \( f_{3dB} \) is marked on the graph, where the gain starts to decrease.

Phase Plot:
- **Type of Graph:** The lower part is a phase shift versus frequency plot.
- **Axes Labels and Units:**
- The vertical axis represents phase shift in degrees.
- The horizontal axis represents frequency in a logarithmic scale.
- **Overall Behavior and Trends:**
- The phase shift starts at 0° at low frequencies and becomes more negative as frequency increases.
- It approaches -90° at high frequencies.
- **Key Features and Technical Details:**
- Specific phase shifts are annotated at certain frequencies, such as 6° at 0.1\( f_{3dB} \) and 84° at 10\( f_{3dB} \).
- The phase plot illustrates the characteristic phase lag introduced by a low-pass filter.

Annotations and Specific Data Points:
- The gain plot is annotated with the slope of -20 dB/decade, indicating the rate of gain decrease.
- The phase plot includes annotations at specific frequencies, providing precise phase shift values.

Figure 4.97. Bode plot: gain and phase versus frequency.
shift of the hypothetical amplifier will be as shown in Figure 4.98.

Now here's the problem: if you were to connect this amplifier as an op-amp follower, for instance, it would oscillate. That's because the open-loop phase shift reaches $180^{\circ}$ at some frequency at which the gain is still greater than 1 (negative feedback becomes positive feedback at that frequency). That's all you need to generate an oscillation, as any signal whatsoever at that frequency builds up each time around the feedback loop, just like a public address system with the gain turned up too far.

#### A. Stability criterion

The criterion for stability against oscillation for a feedback amplifier is that its open-loop phase shift must be less than $180^{\circ}$ at the frequency at which the loop gain is unity. This criterion is hardest to satisfy when the amplifier is connected as a follower, since the loop gain then equals the open-loop gain, the highest it can be. Internally compensated op-amps are designed to satisfy the stability criterion even when connected as followers; thus they are stable when connected for any closed-loop gain with a simple resistive feedback network. As we hinted earlier, this is accomplished by deliberately modifying an existing internal rolloff in order to put the 3 dB point at some low frequency, typically 1 Hz to 20 Hz . Let's see how that works.

### 4.9.2 Amplifier compensation methods

#### A. Dominant-pole compensation

The goal is to keep the open-loop phase shift much less than $180^{\circ}$ at all frequencies for which the loop gain is greater than 1. Assuming that the op-amp may be used as a follower, the words "loop gain" in the last sentence can be replaced with "open-loop gain." The easiest way to do this is to add enough additional capacitance at the
image_name:Figure 4.98
description:The graph in Figure 4.98 is a Bode plot, which displays both the gain and phase shift of a multistage amplifier as functions of frequency. The horizontal axis represents frequency on a logarithmic scale, denoted as 'Frequency (log)'. The vertical axis on the left side shows the gain also on a logarithmic scale, labeled 'Gain (log)', while the right vertical axis indicates phase shift in degrees, ranging from 0° to -270°.

**Overall Behavior and Trends:**
- **Gain Curve:** The gain starts high at low frequencies, maintaining a constant level of approximately 10^5. As frequency increases, the gain begins to decrease, showing a typical roll-off behavior. This roll-off starts around the frequency labeled \( f_1 \), and the gain continues to drop as the frequency increases, passing through \( f_2 \) and \( f_3 \).
- **Phase Shift Curve:** The phase shift starts at 0° at low frequencies and gradually increases. It passes through -90° and approaches -180° as the frequency further increases. The phase shift continues to rise towards -270° at very high frequencies.

**Key Features and Technical Details:**
- **Cutoff Frequencies:** The graph indicates three significant frequencies labeled \( f_1 \), \( f_2 \), and \( f_3 \), which are key points where the gain and phase shift exhibit noticeable changes.
- **Gain Roll-off:** The gain decreases at a consistent rate, following a -20 dB/decade slope after \( f_1 \).
- **Phase Behavior:** The phase shift exhibits a gradual increase, indicating a lag in response as frequency increases, which is typical in multistage amplifiers.

**Annotations and Specific Data Points:**
- The graph is annotated with markers at \( f_1 \), \( f_2 \), and \( f_3 \) on the frequency axis, indicating important transition points for both gain and phase shift.
- The gain curve is dashed, while the phase shift curve is solid, clearly distinguishing the two plots.

This plot is critical for understanding the frequency response of the amplifier, particularly how the gain and phase shift are managed across different frequencies to ensure stability and performance in the amplifier's operation.

Figure 4.98. Gain and phase in a multistage amplifier.
point in the circuit that produces the initial $6 \mathrm{~dB} /$ octave rolloff, so that the open-loop gain drops to unity at about the 3 dB frequency of the next "natural" $R C$ filter. In this way the open-loop phase shift is held at a constant $90^{\circ}$ over most of the passband, increasing toward $180^{\circ}$ only as the gain approaches unity. Figure 4.99 shows the idea. Without compensation, the open-loop gain drops toward 1, first at $6 \mathrm{~dB} /$ octave, then at $12 \mathrm{~dB} /$ octave, etc., resulting in phase shifts of $180^{\circ}$ or more before the gain has reached 1. By moving the first rolloff down in frequency (forming a "dominant pole"), the rolloff is controlled so that the phase shift begins to rise above $90^{\circ}$ only as the open-loop gain approaches unity. Thus, by sacrificing open-loop gain, you buy stability. Because the natural rolloff of lowest frequency is usually caused by the Miller effect in the stage driven by the input differential amplifier, the usual method of dominant-pole compensation consists simply of adding additional feedback capacitance around the second-stage transistor, so the combined voltage gain of the two stages is $g_{m} X_{\mathrm{C}}$ or $g_{m} / 2 \pi f C_{\text {comp }}$ over the compensated region of the amplifier's frequency response (Figure 4.100). In practice, Darlington-connected transistors would probably be used for both stages.

By putting the dominant-pole unity-gain crossing at the 3 dB point of the next rolloff, you get a phase margin of about $45^{\circ}$ in the worst case (follower), since a single $R C$ filter has a $45^{\circ}$ lagging phase shift at its 3 dB frequency, i.e., the phase margin equals $180^{\circ}-\left(90^{\circ}+45^{\circ}\right)$, with the $90^{\circ}$ coming from the dominant pole.

An additional advantage of using a Miller-effect pole for
image_name:Figure 4.99
description:The graph labeled as "Figure 4.99" consists of two plots: an open-loop gain plot and a phase shift plot, both plotted against frequency on a logarithmic scale.

Open-loop Gain Plot:
- **Type of Graph:** Bode plot showing open-loop gain.
- **Axes:**
- **Y-Axis:** Open-loop Gain in decibels (dB), ranging from 0 dB to 100 dB.
- **X-Axis:** Frequency on a logarithmic scale, unspecified units.
- **Overall Behavior:**
- The graph shows two curves: one labeled "compensated" and the other "uncompensated."
- The uncompensated curve starts at a high gain of 100 dB and decreases sharply as frequency increases, indicating a rapid roll-off.
- The compensated curve maintains a higher gain over a wider frequency range before rolling off more gradually, illustrating the effect of compensation.
- **Key Features:**
- The compensated curve shows a slower decline in gain compared to the uncompensated curve.
- An arrow labeled "increase C" suggests that increasing capacitance shifts the compensated curve to lower frequencies, enhancing stability.

Phase Shift Plot:
- **Type of Graph:** Bode plot showing phase shift.
- **Axes:**
- **Y-Axis:** Phase Shift in degrees, ranging from 0° to -270°.
- **X-Axis:** Frequency on a logarithmic scale, unspecified units.
- **Overall Behavior:**
- The phase shift plot also shows two curves: compensated and uncompensated.
- Both curves start near 0° phase shift at low frequencies.
- The uncompensated curve exhibits a more rapid increase in phase shift, reaching more negative values quickly.
- The compensated curve rises more gradually, indicating improved phase stability.
- **Key Features:**
- The compensated curve helps maintain a phase margin by reducing the rate of phase shift increase.

Annotations and Specific Data Points:
- The graph highlights the effect of compensation on both gain and phase shift, showing how compensation can stabilize an op-amp by altering frequency response characteristics.
image_name:Figure 4.100
description:The graph in Figure 4.100 is a Bode plot consisting of two parts: the top graph shows the open-loop gain versus frequency, and the bottom graph illustrates the phase shift versus frequency.

Top Graph: Open-loop Gain
- **Type of Graph:** Bode plot for open-loop gain.
- **Axes Labels and Units:**
- **Y-axis:** Open-loop Gain in decibels (dB), ranging from 0 dB to 100 dB.
- **X-axis:** Frequency on a logarithmic scale.
- **Overall Behavior and Trends:**
- The uncompensated gain curve starts at 100 dB and remains flat until it begins to roll off at higher frequencies. The roll-off is steep after a certain frequency.
- The compensated gain curve also starts at 100 dB but begins to roll off at a lower frequency compared to the uncompensated curve. The roll-off is more gradual, showing the effect of compensation.
- **Key Features and Technical Details:**
- The compensated curve shifts the roll-off frequency to a lower point, effectively reducing the bandwidth while stabilizing the system.
- An annotation indicates that increasing the capacitance (C) moves the compensated curve to the left, further lowering the roll-off frequency.

Bottom Graph: Phase Shift
- **Type of Graph:** Bode plot for phase shift.
- **Axes Labels and Units:**
- **Y-axis:** Phase Shift in degrees, ranging from 0° to -270°.
- **X-axis:** Frequency on a logarithmic scale.
- **Overall Behavior and Trends:**
- The uncompensated phase shift curve begins at 0° and gradually decreases, reaching more negative values as frequency increases.
- The compensated phase shift curve also starts at 0° but decreases more gradually than the uncompensated curve, showing less phase shift at higher frequencies.
- **Key Features and Technical Details:**
- The compensation reduces the phase shift at higher frequencies, which can improve stability and phase margin.

Annotations and Specific Data Points:
- The plot includes annotations indicating the difference between compensated and uncompensated responses, with specific reference to the effect of increasing capacitance on the compensated curve.

Figure 4.99. "Dominant-pole" compensation.
image_name:Figure 4.100. Classic op-amp input stage with compensation.
description:
[
name: Q1, type: PMOS, ports: {S: VCC, D: X1, G: in-}
name: Q2, type: PMOS, ports: {S: VCC, D: X2, G: in+}
name: Q3, type: NPN, ports: {C: X1, B: X1, E: VEE}
name: Q4, type: NPN, ports: {C: X2, B: X1, E: VEE}
name: Q5, type: NPN, ports: {C: X2, B: X2, E: VEE}
name: P1, type: CurrentSource, ports: {Np: VCC, Nn: X1}
name: P2, type: CurrentSource, ports: {Np: X2, Nn: Out}
name: Ccomp, type: Capacitor, value: Ccomp, ports: {Np: X2, Nn: Out}
]
extrainfo:This circuit is a classic op-amp input stage with compensation. It includes PMOS transistors Q1 and Q2 for differential input, NPN transistors Q3, Q4, and Q5 for current mirroring and amplification, and a compensation capacitor Ccomp to improve stability. The circuit is powered by VCC and VEE, and it outputs to a push-pull follower stage.

Figure 4.100. Classic op-amp input stage with compensation.
compensation is that the compensation is inherently insensitive to changes in voltage gain with temperature or manufacturing spread of gain: higher gain causes the feedback capacitance to look larger, moving the pole downward in frequency in exactly the right way to keep the unity-gain crossing frequency unchanged. In fact, the actual 3 dB frequency of the compensation pole is quite irrelevant; what matters is the point at which it intersects the unity-gain axis (Figure 4.101).

#### B. Decompensated and uncompensated op-amps

If an op-amp is used in a circuit with closed-loop gain greater than unity (i.e., not a follower), it is not necessary to put the pole (the term for the "corner frequency" of a lowpass filter, see Chapter $1 x$ ) at such a low frequency as the stability criterion is relaxed because of the lower loop gain. Figure 4.102 shows the situation graphically.

For a closed-loop gain of 30 dB , the loop gain (which is the ratio of the open-loop gain to the closed-loop gain) is less than for a follower, so the dominant pole can be placed at a higher frequency. It is chosen so that the openloop gain reaches 30 dB (rather than 0 dB ) at the fre-
image_name:Figure 4.101
description:The graph in Figure 4.101 is a Bode plot, which is used to depict the gain of an amplifier circuit as a function of frequency. The plot is presented on a logarithmic scale for both the gain (in decibels, dB) and frequency.

Axes Labels and Units:
- **X-axis:** Frequency (logarithmic scale)
- **Y-axis:** Gain (logarithmic scale, in dB)

Overall Behavior and Trends:
The graph shows a typical lowpass filter response. Initially, at low frequencies, the gain is constant and high, indicating that the amplifier maintains its gain across this range. As the frequency increases, the gain begins to roll off, depicted by the downward slope on the plot. This indicates the onset of the filter's cutoff region.

Key Features and Technical Details:
- **Flat Region:** At lower frequencies, the gain remains flat, indicating that the compensation capacitor is not significantly affecting the gain in this range.
- **Roll-off:** The slope of the line beyond the flat region represents the frequency at which the gain starts to decrease. This is the point where the compensation capacitor (C_comp) is chosen to set the open-loop unity-gain frequency.
- **Annotations:** There are annotations on the graph indicating a region marked as "don't know (or care)," which suggests that the specific gain values in this region are not critical for the design considerations. Another annotation states "pick C_comp for gain out here," emphasizing the importance of selecting the compensation capacitor to achieve the desired gain at higher frequencies.

Annotations and Specific Data Points:
- **Unity-Gain Frequency:** The graph does not explicitly mark the unity-gain frequency, but it is implied by the point where the gain line intersects the 0 dB level on the Y-axis.
- **Design Focus:** The emphasis on choosing the compensation capacitor indicates the designer's focus on achieving stable gain characteristics at higher frequencies, beyond the initial flat gain region.

Figure 4.101. The compensation capacitor is chosen to set the open-loop unity-gain frequency; the low-frequency gain is unimportant.
image_name:Figure 4.102
description:The graph in Figure 4.102 is a Bode plot illustrating the relationship between voltage gain (in decibels) and frequency (on a logarithmic scale). The X-axis represents frequency, and the Y-axis represents voltage gain.

**Type of Graph and Function:**
This is a Bode plot, which is typically used to analyze the frequency response of systems, such as operational amplifiers. It shows various gain characteristics against frequency.

**Axes Labels and Units:**
- **X-axis:** Frequency (log scale)
- **Y-axis:** Voltage Gain (dB)

**Overall Behavior and Trends:**
The graph displays multiple lines representing different compensation states of an operational amplifier:
1. **Open-loop gain (uncompensated):** This line starts at a high gain of around 100 dB and decreases steadily as frequency increases.
2. **Open-loop gain (compensated for 30 dB):** This line also begins at a high gain but is lower than the uncompensated line, indicating a reduction in gain due to compensation.
3. **Open-loop gain (unity-gain compensation):** This line starts with a lower initial gain compared to the uncompensated and 30 dB compensated lines, showing further reduction in gain due to compensation.
4. **Closed-loop gain (unity-gain compensation):** This line is flat at around 20 dB across the frequency range, indicating stable gain.
5. **Closed-loop gain (30 dB compensation):** This line is also flat but at a higher level than the unity-gain compensation, suggesting more gain stability.

**Key Features and Technical Details:**
- The open-loop gain lines show how compensation affects the gain across frequencies, with higher initial gains decreasing more sharply with frequency.
- The closed-loop gain lines are flat, indicating stable gain across the frequency spectrum, with the unity-gain compensation having a lower gain level compared to the 30 dB compensation.

**Annotations and Specific Data Points:**
- The graph is annotated with labels indicating the type of compensation applied to each line (e.g., uncompensated, compensated for 30 dB, unity-gain compensation).
- The flat lines in the closed-loop gain indicate stability, which is crucial for maintaining performance in operational amplifiers at varying frequencies.

Figure 4.102. Stability is easier to achieve with larger closed-loop gain.
quency of the next natural pole of the op-amp. As the graph shows, this means that the open-loop gain is higher over most of the frequency range, and the resultant amplifier will work at higher frequencies. Some op-amps are available in "decompensated" (a better word might be "undercompensated") versions, which are internally compensated for closed-loop gains greater than some minimum $\left(A_{\mathrm{v}}>5\right.$ in the case of the OP37); these specify a minimum closed-loop gain, and require no external capacitor. Another example is the THS4021/2, a decompensated version $\left(G_{V} \geq 10\right)$ of the unity-gain stable THS4011/2. These are really speedy op-amps, with an $f_{\mathrm{T}}$ of 300 MHz (for the "slow" THS4011/2), and greater than 1 GHz for the THS4021/2. For the decompensated versions the manufacturer (TI) supplies recommended external capacitance values (sometimes in combination with a resistor; see below) for a selection of minimum closed-loop gains. ${ }^{43}$ Decompensated or uncompensated op-amps are worth using if you need the added bandwidth and your circuit operates at high gain; see Chapter $4 x$ for further discussion.

Some intuition: it may at first seem paradoxical that an op-amp circuit configured for a low-gain circuit is more prone to oscillation than one configured for high-gain. But it makes sense: the better stability of an op-amp connected for a closed-loop gain of $G_{\mathrm{CL}}=100(40 \mathrm{~dB})$, say, comes about because the feedback network (resistive divider) attenuates signals by a factor of 100 . So it's harder to sustain an oscillation going around the loop, compared with a follower (in which the feedback has unity gain).

[^52]
#### C. Pole-zero compensation

It is possible to do a bit better than with dominant-pole compensation by using a compensation network that begins dropping ( $6 \mathrm{~dB} /$ octave, a "pole") at some low frequency, then flattens out again (it has a "zero") at the frequency of the second natural pole of the op-amp. In this way the amplifier's second pole is "cancelled," giving a smooth $6 \mathrm{~dB} /$ octave rolloff up to the amplifier's third pole. Figure 4.103 shows a frequency-response plot. In practice, the zero is chosen to cancel the amplifier's second pole; then the position of the first pole is adjusted so that the overall response reaches unity gain at the frequency of the amplifier's third pole. A good set of datasheets for an opamp with external compensation will often give suggested component values (an $R$ and a $C$ ) for pole-zero compensation, as well as the usual capacitor values for dominantpole compensation. Moving the dominant pole downward in frequency actually causes the second pole of the amplifier to move upward somewhat in frequency, an effect known as "pole splitting." The frequency of the cancelling zero is then chosen accordingly.

### 4.9.3 Frequency response of the feedback network

In all of the discussion thus far we have assumed that the feedback network has a flat frequency response; this is usually the case, with the standard resistive voltage divider as a feedback network. However, there are occasions when some sort of equalization amplifier is desired (integrators and differentiators are in this category) or when the frequency response of the feedback network is modified to improve amplifier stability. In such cases it is important to remember that the Bode plot of loop gain versus frequency is what matters, rather than the curve of open-loop gain. To make a long story short, the curve of ideal closed-loop
image_name:Figure 4.103
description:The graph depicted is a Bode plot, which illustrates the frequency response of an amplifier system with pole-zero compensation. The x-axis represents frequency on a logarithmic scale, while the y-axis represents gain in decibels (dB), also on a logarithmic scale.

Overall Behavior and Trends:
- **Open-loop Gain Curve:** This curve starts at a high gain level at low frequencies and gradually decreases as frequency increases. It follows a typical roll-off pattern associated with amplifier open-loop gain.
- **Response of Pole-Zero Network:** This curve shows how the pole-zero compensation affects the system. It begins at a lower gain compared to the open-loop gain and intersects it at a certain frequency.
- **Overall Response:** The overall response curve is a combination of the open-loop gain and the effect of the pole-zero network. It shows a more stable roll-off, indicating improved stability and bandwidth.

Key Features and Technical Details:
- The intersection point of the open-loop gain and the pole-zero network response is crucial as it indicates the frequency where compensation is most effective.
- The slope difference at the intersection is approximately 6 dB/octave, which is a typical design criterion for stability.
- The plot includes a schematic representation of the circuit used for pole-zero compensation, which consists of resistors and capacitors.

Annotations and Specific Data Points:
- The graph is annotated with labels pointing to the open-loop gain and the response of the pole-zero network, clarifying their respective curves.
- The dashed lines represent theoretical extensions of the slopes, emphasizing the intended slope difference for stability.

This Bode plot effectively demonstrates the concept of pole-zero compensation in stabilizing an amplifier by modifying its frequency response, ensuring that the overall gain intersects the open-loop gain with the desired slope difference for improved stability.
image_name:Figure 4.104
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: Vin, N2: X1}
name: C1, type: Capacitor, value: C1, ports: {Np: X1, Nn: GND}
name: R2, type: Resistor, value: R2, ports: {N1: X1, N2: GND}
]
extrainfo:The circuit is a standard pole-zero compensation network used to modify the frequency response and improve amplifier stability. The Bode plot shows the open-loop gain, the response of the pole-zero network, and the overall response.

Figure 4.103. Cancelling the amplifier's second pole in "pole-zero" compensation.
gain versus frequency should intersect the curve of openloop gain, with a difference in slopes of $6 \mathrm{~dB} /$ octave. As an example, it is common practice to put a small capacitor (a few picofarads) across the feedback resistor in the usual inverting or noninverting amplifier. Figure 4.104 shows the circuit and Bode plot.

The amplifier would have been close to instability with a flat feedback network since the loop gain would have been dropping at nearly $12 \mathrm{~dB} /$ octave where the curves meet. The capacitor causes the loop gain to drop at $6 \mathrm{~dB} /$ octave near the crossing, guaranteeing stability. This sort of consideration is very important when designing differentiators because an ideal differentiator has a closed-loop gain that rises at 6 dB /octave; it is necessary to roll off the differentiator action at some moderate frequency, preferably going over to a $6 \mathrm{~dB} /$ octave rolloff at high frequencies. Integrators, by comparison, are very friendly in this respect, owing to their $6 \mathrm{~dB} /$ octave closed-loop rolloff. It takes real talent to make a low-frequency integrator oscillate!

Exercise 4.29. Show on a Bode plot that the value of stabilizing resistor $R_{1}$ in Figure 4.69 stops the differentiator action (i.e., flattens the curve of closed-loop gain) before the crossing point of open-loop and closed-loop gains. Explain our value of minimum recommended resistance $R_{1}$.

#### A. What to do

In summary, you are generally faced with the choice of internally compensated or uncompensated op-amps. It is simplest to use the compensated variety, and that's the usual choice. You might begin by considering the
image_name:Figure 4.104
description:
[
name: A1, type: OpAmp, value: A1, ports: {InP: InP(A1), InN: InN(A1), OutP: Out(A1)}
name: R1, type: Resistor, value: 10k, ports: {N1: InN(A1), N2: GND}
name: R2, type: Resistor, value: 91k, ports: {N1: InN(A1), N2: Out(A1)}
name: C1, type: Capacitor, value: 3pF, ports: {Np: InN(A1), Nn: Out(A1)}
]
extrainfo:The circuit is a feedback network with an operational amplifier A1. A stabilizing resistor R1 and a feedback capacitor C1 are used to enhance stability and flatten the closed-loop gain curve before it crosses the open-loop gain curve. This configuration helps prevent excessive differentiation in the amplifier's response.
image_name:Figure 4.69
description:The graph in Figure 4.69 is a Bode plot illustrating the frequency response of an operational amplifier circuit with and without a feedback capacitor, \( C_1 \). The plot has the following characteristics:

1. **Axes Labels and Units:**
- The horizontal axis represents frequency, typically in logarithmic scale (though not explicitly labeled here).
- The vertical axis represents voltage gain in decibels (dB).

2. **Overall Behavior and Trends:**
- The graph shows two curves: one for the open-loop gain and another for the closed-loop gain of the amplifier.
- The open-loop gain curve starts at a high gain value (around 100 dB) and decreases steadily as frequency increases.
- The closed-loop gain without \( C_1 \) initially follows the open-loop gain curve but begins to diverge and flatten out at lower frequencies compared to the open-loop gain.
- With the inclusion of \( C_1 \), the closed-loop gain curve flattens further before the crossing point of the open-loop and closed-loop gains, indicating enhanced stability.

3. **Key Features and Technical Details:**
- The open-loop gain decreases sharply, indicating a typical roll-off in high-frequency response.
- The closed-loop gain with \( C_1 \) shows a more stable response at higher frequencies, preventing the differentiator action that would otherwise lead to increased instability.
- The feedback network's closed-loop gain (if \( A_V = \infty \)) is marked around 20 dB.
- The curves illustrate the effect of the feedback capacitor \( C_1 \) in stabilizing the circuit by modifying the frequency response.

4. **Annotations and Specific Data Points:**
- The graph includes annotations indicating the behavior of the gain with and without \( C_1 \).
- The intersection point of the open-loop and closed-loop gains is crucial for determining stability margins, and the use of \( C_1 \) shifts this intersection to a safer frequency range.

Overall, this Bode plot demonstrates the importance of selecting an appropriate stabilizing resistor \( R_1 \) and feedback capacitor \( C_1 \) to ensure that the closed-loop gain flattens out before the open-loop and closed-loop gains intersect, thereby enhancing the operational stability of the amplifier circuit.

Figure 4.104. A small feedback capacitor enhances stability.
image_name:Figure 4.105
description:
[
name: VoltageSource, type: VoltageSource, value: 60Hz 1Vrms, ports: {Np: Vin, Nn: GND}
name: R1, type: Resistor, value: 220, ports: {N1: Vin, N2: N1}
name: R2, type: Resistor, value: 1k, ports: {N1: N1, N2: N2}
name: R3, type: Resistor, value: 50k, ports: {N1: N2, N2: N3}
name: R4, type: Resistor, value: 5.6k, ports: {N1: N3, N2: N4}
name: R5, type: Resistor, value: 10k, ports: {N1: N4, N2: GND}
name: C1, type: Capacitor, value: 1000pF, ports: {Np: N2, Nn: N3}
name: C2, type: Capacitor, value: 10μF, ports: {Np: N3, Nn: GND}
name: Cc, type: Capacitor, value: overcomp, ports: {Np: N1, Nn: GND}
name: Q1, type: NPN, value: 2N6044, ports: {C: +16V, B: N1, E: N2}
name: Q2, type: PNP, value: 2N6041, ports: {C: -16V, B: N1, E: N2}
name: T1, type: Transformer, ports: {In1: N2, In2: GND, Out1: N3, Oou2: N4}
name: T2, type: Transformer, ports: {In1: N3, In2: GND, Out1: N4, Oou2: GND}
name: IC1, type: OpAmp, value: LT1097, ports: {InP: Vin, InN: GND, OutP: N1, OutN: GND}
]
extrainfo:The circuit is an output amplifier designed for a 60 Hz power source. It features push-pull output transistors Q1 and Q2, which are power Darlingtons in a plastic power package. The circuit also includes transformers T1 and T2 for voltage transformation and isolation. The operational amplifier IC1 (LT1097) is used for signal amplification with feedback components R1, R2, and Cc to stabilize the circuit. The circuit is powered by dual supplies of +16V and -16V.

Figure 4.105. Output amplifier for 60 Hz power source. The push-pull output transistors $Q_{1}$ and $Q_{2}$ are power Darlingtons in a plastic power package.
conventional LF411 (JFET, $\pm 5 \mathrm{~V}$ to $\pm 15 \mathrm{~V}$ supply) or an improved version (the LT1057), or the rail-to-rail input and output LMC6482 (CMOS, +3 V to +15 V supply), or perhaps the accurate and quiet LT1012, all internally compensated for unity gain. If you need greater bandwidth or slew rate, look for a faster compensated op-amp (see Table 4.2a on 271 for some choices). If it turns out that nothing is suitable and the closed-loop gain is greater than unity (as it usually is), you can use a decompensated (or uncompensated) op-amp, perhaps with an external capacitor as specified by the manufacturer for the gain you are using. Using our previous example, the popular OP27 low-noise precision op-amp (unity-gain-compensated) has $f_{\mathrm{T}}=8 \mathrm{MHz}$ and a slew rate of $2.8 \mathrm{~V} / \mu \mathrm{s}$; it is available as the decompensated OP37 (minimum gain of 5), with $f_{\mathrm{T}}=63 \mathrm{MHz}$ and a slew rate of $17 \mathrm{~V} / \mu \mathrm{s} .{ }^{44}$

#### B. Example: precision 60 Hz power source

Uncompensated op-amps, or op-amps with a compensation pin, also give you the flexibility of overcompensating, a

[^53]simple solution to the problem of additional phase shifts introduced by other stuff in the feedback loop. Figure 4.105 shows an example. This is a low-frequency amplifier designed to generate a precise and stable 115 volt ac power output from a variable frequency 60 Hz low-level sinewave input. ${ }^{45}$ The op-amp is wired as an ac-coupled noninverting amplifier, with its output driving a Darlington push-pull emitter-follower output stage $Q_{1} Q_{2}$, which in turn drives the low-voltage winding of a small power transformer, $T_{1}$, whose windings are in the ratio of $6.3 \mathrm{~V}: 115 \mathrm{~V}$. In this way we generate 115 V ac output without high-voltage op-amps or transistors. Of course, we pay the price in proportionally higher drive current; here the transistors need to supply about $3 \mathrm{~A}(\mathrm{rms})$ to produce a 15 W output.

To generate low distortion and a stable output voltage under load variations, we want to take feedback from the actual 115 V output sinewave. It is highly desirable, however, to keep the output fully isolated from circuit ground. So we use a second transformer $T_{2}$ to produce a lowvoltage replica of the 115 V output waveform, which is
${ }^{45}$ The original design was used to drive an astronomical telescope at sidereal (star-tracking) rate. Interesting trivia: contrary to popular belief, the Earth turns on its axis once every 23 hours, 56 minutes, and 4.1 seconds; figure out why it isn't 24:00:00!
then fed back via $R_{3}$ to give the needed voltage gain of 6 . Because of the unacceptably large phase shifts of the transformers at high frequencies, the circuit is rigged up so that at higher frequencies - above $\sim 3 \mathrm{kHz}$ - the feedback comes from the low-voltage input to the transformer (via $C_{1}$ ). Even though high-frequency feedback is taken directly from the push-pull output, there are still phase shifts associated with the reactive load (the transformer primary, a motor attached to the output, etc.) seen by the transistors. To ensure good stability, even with reactive loads at the 115 volt output, the op-amp can be overcompensated with a small capacitor, as shown. (The unusual LT1097 obligingly provides a pin for overcompensation.) The loss of bandwidth that results is unimportant in a low-frequency application like this.

The function of $R_{4}$ and $C_{2}$ may be puzzling: this bit of circuitry provides a dc feedback path for the op-amp, by averaging (lowpass filtering) the dc level applied to $T_{1}$, which then feeds back via the floating winding of $T_{2}$. We chose $C_{2}$ large enough so its impedance at 60 Hz is small compared with the 50 k feedback resistor; then we chose $R_{4}$ for adequate smoothing consistent with stability.

The performance of this amplifier is quite satisfying. Figure 4.106 shows the output regulation, i.e., the change of rms output amplitude versus load. For comparison we show the comparable curve when feedback is taken exclusively from the driving winding of $T_{1}$, from which you can see that the desired feedback path improves output amplitude regulation, under load variations from zero to full power, from a mediocre $10 \%$ to just $0.2 \%$. The output sinewave is very clean, with measured distortion well below $1 \%$ under all load conditions, including driving a synchronous motor (which represents a reactive load).

An application such as this represents a compromise,
image_name:Figure 4.106
description:The graph in Figure 4.106 is a line graph depicting the relationship between output voltage (Vout) in volts (rms) on the vertical axis and output power (Pout) in watts on the horizontal axis. The graph uses a linear scale for both axes, with the output voltage ranging from 105 to 115 volts and the output power ranging from 0 to 15 watts.

There are two lines on the graph, each representing a different feedback mechanism:
1. **Feedback from Driver:** This line starts at 115 volts when the output power is zero and decreases linearly to approximately 104.8 volts as the output power reaches 15 watts. This indicates a change in output voltage (ΔV) of 10.2 volts, showing a significant drop in voltage as power increases.

2. **Feedback via Return Transformer (xfmr):** This line also starts at 115 volts at zero output power but remains almost constant, slightly decreasing to about 114.8 volts at 15 watts. The change in output voltage (ΔV) here is only 0.2 volts, demonstrating excellent voltage regulation across the range of output power.

The graph highlights the effectiveness of using feedback via a return transformer to maintain a stable output voltage despite variations in output power, as opposed to feedback from the driver, which results in a much larger voltage drop. This illustrates the improvement in output amplitude regulation from a mediocre 10% to just 0.2% when using the return transformer feedback mechanism.

Figure 4.106. Measured output voltage versus load for 60 Hz power source.
because ideally you would like to have plenty of loop gain to stabilize the output voltage against variations in load current. But a large loop gain increases the tendency of the amplifier to oscillate, especially if a reactive load is attached. This is because the reactive load, in combination with the transformer's finite output impedance, causes additional phase shifts within the low-frequency feedback loop. Because this circuit was built to power a telescope's synchronous driving motors (highly inductive loads), the loop gain was intentionally kept low.

Some additional points.

- With power electronics you should design conservatively so that a fault condition (e.g., too heavy a load, or even a short-circuit) doesn't destroy the device. Here we've used the simplest current-limiting method - a pair of small resistors in the collectors of the drive stage - because we didn't want to clutter the diagram (and it worked well enough, anyway!). There are better ways, though, for example, by adding a pair of transistors to rob base current when the output current (as sensed by a series resistor) exceeds a preset limit; such a scheme is commonly used within the integrated circuitry of op-amps themselves see Figure 4.43. As we'll explain in $\S 9.13 .3$, there are still better protective circuits. The problem with simple current-limiting protection is that a short-circuit load would cause the transistors to experience the limit current with the full supply voltage across them; the resulting power dissipation is far greater than the maximum under ordinary operation, which requires conservative heatsinking and component selection. Foldback current limiting would be better, though a bit more complicated.
- A push-pull follower with the bases tied together has a crossover region in which the feedback loop is effectively broken (see §2.4.1A). With Darlington transistors the crossover region is four $V_{\mathrm{BE}}$ 's, about 2.5 V . The resistor $R_{2}$ in Figure 4.105 ensures that there is always some linear coupling from the op-amp to $T_{1}$, to prevent the feedback loop from rattling around under light load. Better still would be diode biasing, in the manner of Figures 2.71 or 2.72 ; see also the discussion of push-pull follower output stages in Chapter $2 x$.
- There is an elegant way to use a normal $\pm 15 \mathrm{~V}$ op-amp to generate larger voltage swings, by replacing the emitter followers in Figure 4.105 with a "pseudo-Darlington" configuration with modest noninverting gain (also known as a "series feedback pair," see §2.5.5C), say a factor of 5. Then you can run the power output stage from a $\pm 75 \mathrm{~V}$ supply while powering the op-amp from conventional $\pm 15 \mathrm{~V}$.

#### C. Motorboating

In ac-coupled feedback amplifiers, stability problems can also crop up at very low frequencies, because of the accumulated leading phase shifts caused by several capacitively coupled stages. Each blocking capacitor, in combination with the input resistance (from bias strings and the like), causes a leading phase shift that equals $45^{\circ}$ at the low-frequency 3 dB point and approaches $90^{\circ}$ at lower frequencies. If there is enough loop gain, the system can go into a low-frequency oscillation picturesquely known as "motorboating." With the widespread use of dc-coupled amplifiers, motorboating is almost extinct. However, oldtimers can tell you some good stories about it.

## Review of Chapter 4

An A-to-O summary of what we have learned in Chapter 4. This summary reviews basic principles and facts in Chapter 4 , but it does not cover application circuit diagrams and practical engineering advice presented there.

### IA. The Ideal Op-amp.

In Chapter 4 we explored the world of Operational Amplifiers ("Op-amps"), universal building blocks of analog circuits. A good op-amp approaches the ideal of an infinitegain wideband noiseless dc-coupled difference amplifier with zero input current and zero offset voltage. Op-amps are intended for use in circuits with negative feedback, where the feedback network determines the circuit's behavior. Op-amps figure importantly in the topics of Chapter 5 (Precision Circuits), Chapter 6 (Filters), Chapter 7 (Oscillators and Timers), Chapter 8 (Low-Noise Techniques), Chapter 9 (Voltage Regulation and Power Conversion), and Chapter 13 (Digital Meets Analog).

### |B. The "Golden Rules."

At a basic level (and ignoring imperfections, see $\pi I K-M$ below), an op-amp circuit with feedback can be simply understood by recognizing that feedback from the output operates to (I) make the voltage difference between the inputs zero; and, at the same level of ignoration, (II) the inputs draw no current. These rules are quite helpful, and for dc (or low-frequency circuits) they are in error only by typical offset voltages of a millivolt or less (rule I), and by typical input currents of order a picoamp for FET types or tens of nanoamps for BJT types (rule II).

### IC. Basic Op-amp Configurations.

In $\S 4.2$ and $\S 4.3$ we met the basic linear circuits (detailed in TIID-F below): inverting amplifier, non-inverting amplifier (and follower), difference amplifier, current source (transconductance, i.e., voltage-to-current), transresistance amplifier (i.e., current-to-voltage), and integrator. We saw also two important non-linear circuits: the Schmitt trigger, and the active rectifier. And in $\S 4.5$ we saw additional circuit building blocks: peak detector, sample-and-hold, active clamp, active full-wave rectifier (absolute-value circuit), and differentiator.

### 1D. Voltage Amplifiers.

The inverting amplifier (Figure 4.5) combines input current $V_{\text {in }} / R_{1}$ and feedback current $V_{\text {out }} / R_{2}$ into a summing junction; it has voltage gain $G_{\mathrm{V}}=-R_{2} / R_{1}$ and input impedance $R_{1}$. In the noninverting amplifier (Figure 4.6) a fraction of
the output is fed back to the inverting input; it has voltage gain $G_{\mathrm{V}}=1+R_{2} / R_{1}$ and near-infinite input impedance. For the follower (Figure 4.8) the feedback gain is unity, i.e., the resistive divider is replaced by a connection from output to inverting input. The difference amplifier (Figure 4.9) uses a pair of matched resistive dividers to generate an output $V_{\text {out }}=\left(R_{2} / R_{1}\right) \Delta V_{\text {in }}$; its input impedance is $R_{1}+R_{2}$, and its common-mode rejection depends directly on the accuracy of the resistor matching (e.g., $\sim 60 \mathrm{~dB}$ with $\pm 0.1 \%$ resistor tolerance). Difference amplifiers are treated in greater detail in $\S 5.14$. A pair of input followers can be used to achieve high input impedance, but a better 3-op-amp configuration is the instrumentation amplifier, see $\S 5.15$.

### ПE. Integrator and Differentiator.

The integrator (Figure 4.16) looks like an inverting amplifier in which the feedback resistor is replaced by a capacitor; thus the input current $V_{\text {in }} / R_{1}$ and feedback current $C d V_{\text {out }} / d t$ are combined at the summing junction. Ignoring the imperfections in $\mathbb{K}$ below, the integrator is "perfect," thus any non-zero average dc input voltage will cause the output to grow and eventually saturate. The integrator can be reset with a transistor switch across the feedback capacitor (Figure 4.18); alternatively you can use a large shunt resistor to limit the dc gain, but this defeats the integrator operation at low frequencies $\left(f \lesssim 1 / R_{\mathrm{f}} C\right)$. The integrator's input impedance is $R_{1}$.

The op-amp differentiator (Figure 4.68) is a similar configuration, but with $R$ and $C$ interchanged. Without additional components (Figure 4.69) this configuration is unstable (see $\mathbb{T I O}$, below).

IF. Transresistance and Transconductance Amplifiers.
By omitting the input resistor, an inverting voltage amplifier becomes a transresistance amplifier ${ }^{46}$, i.e., a current-to-voltage converter (Figure 4.22). Its gain is $V_{\text {out }} / I_{\mathrm{in}}=-R_{\mathrm{f}}$, and (ignoring imperfections) the impedance at its input (which drives the summing junction) is zero. Capacitance at the input creates issues of stability, bandwidth, and noise; see $\S 8.11$ and the discussion in Chapter $4 x$. Transresistance amplifiers are widely used in photodiode applications.

A transconductance amplifier (Figures 4.10-4.15) converts a voltage input to a current output; it is a voltagecontrolled current source. The simplest form uses an opamp and one resistor (Figure 4.10), but works only with a floating load. The Howland circuit and its variations (Figures 4.14 and 4.15) drive a load returned to ground, but

[^54]their accuracy depends on resistor matching. Circuits with an external transistor (Figures 4.12 and 4.13) drive loads returned to ground, do not require resistor matching, and, in contrast to the other circuits, benefit from the intrinsically high output impedance of the transistor. In Chapter $4 x$ we describe a nice variation on the transistor-assisted current source that achieves both high speed and bipolarity output (i.e., sinking and sourcing)

### |G. Nonlinear Circuits: Peak Detector, S/H, Clamp, Rectifier.

Because of their high gain, op-amps provide accuracy to nonlinear functions that can be performed with passive components alone; in these circuits one or more diodes select the regions in which feedback acts. The peak detector (Figure 4.58) captures and holds the highest (or lowest) voltage since the last reset; the sample-and-hold $(\mathrm{S} / \mathrm{H})$ circuit (Figure 4.60) responds to an input pulse by capturing and holding the value of an input signal voltage; the $a c$ tive clamp (Figure 4.61) bounds a signal to a maximum (or minimum) voltage; the active rectifier creates accurate half-wave (Figures 4.36 and 4.38) or full-wave (Figures 4.63 and 4.64 ) outputs. In practice the performance of these circuits is limited by the finite slew rate and output current of real op-amps (see $\llbracket$ IM, below).

### IH. Positive Feedback: Comparator, Schmitt Trigger, and Oscillator.

If the feedback path is removed, an op-amp acts as a comparator, with the output responding (by saturating near the corresponding supply rail) to a reversal of differential input voltage of a millivolt or less (Figure 4.32A). Adding some positive feedback (Figure 4.32B) creates a Schmitt trigger, which both speeds up the response and also suppresses noise-induced multiple transitions. Op-amps are optimized for use with negative feedback in linear applications (notably by a deliberate internal $-6 \mathrm{~dB} /$ octave rolloff "compensation," see $\llbracket$ ( O below), so special comparator ICs (lacking compensation) are preferred, see $\S 12.3$ and Tables 12.1 and 12.6. A combination of positive feedback (Schmitt trigger) and negative feedback (with an integrator) creates an oscillator (Figure 4.39), a subject treated in detail in Chapter 7.

### qII. Single-Supply and Rail-to-rail Op-amps.

For some op-amps both the input common-mode range and the output swing extend all the way down to the negative rail, making them particularly suited for operation with a single positive supply. Rail-to-rail op-amps allow input swings to both supply rails, or output swings to both rails,
or both; see Table 4.2a. The latter are especially useful in circuits with low supply voltages.

### IIJ. Some Cautions.

In linear op-amp circuits, the Golden Rules (see $\llbracket$ B, above) will be obeyed only if (a) feedback is negative and (b) the op-amp stays in the active region (i.e., not saturated). There must be feedback at dc, or the op-amp will saturate. Power supplies should be bypassed. Stability is degraded with capacitive loads, and by lagging phase shifts in the feedback path (e.g., by capacitance at the inverting terminal). And, most important, real op-amps have a host of limitations (IIIIK-N, below) that bound attainable circuit performance.

### IK. Departures from Ideal Behavior.

In the real world op-amps are not perfect. There is no "best" op-amp, thus one must trade off a range of parameters: input imperfections (offset voltage, drift, and noise; input current and noise; differential and common-mode range), output limitations (slew rate, output current, output impedance, output swing), amplifier characteristics (gain, phase shift, bandwidth, CMRR and PSRR), operating characteristics (supply voltage and current), and other considerations (package, cost, availability). See §4.4, Tables 4.1, 4.2 a , and 4.2 b , the more extensive tables in Chapters 5, and 8 , and IIIL-N below.

### IL. Input Limitations.

The input offset voltage ( $V_{\mathrm{os}}$ ), ranging from about $25 \mu \mathrm{~V}$ ("precision" op-amp) to 5 mV , is the voltage unbalance at the input terminals. It's an important parameter for precision circuits, and circuits with high closed-loop dc gain; the error seen at the output is $G_{\mathrm{CL}} V_{\mathrm{os}}$ ). Some op-amps provide pins for external trimming of offset voltage (e.g., see Figure 4.43).

The offset voltage drift, or tempco ( $\mathrm{TCV}_{\mathrm{os}}$, or $\left.\Delta V_{\mathrm{os}} / \Delta T\right)$, is the temperature coefficient of offset voltage; it ranges from about $0.1 \mu \mathrm{~V} /{ }^{\circ} \mathrm{C}$ ("precision" op-amp) to $10 \mu \mathrm{~V} /{ }^{\circ} \mathrm{C}$. Even if you're lucky and have an op-amp with low $V_{\text {os }}$ (or you've trimmed it to zero), $\mathrm{TC} V_{\text {os }}$ represents the growth of offset with changing temperature.

The input noise voltage density $\left(e_{\mathrm{n}}\right)$ represents a noisy voltage source in series with the input terminals. It ranges from about $1 \mathrm{nV} / \sqrt{\mathrm{Hz}}$ (low-noise bipolar op-amp) to $100 \mathrm{nV} / \sqrt{\mathrm{Hz}}$ or more (micropower op-amps). Noise voltage is important in audio and precision applications.

The input bias current $\left(I_{\mathrm{B}}\right)$ is the (non-zero) dc current at the input terminals. It ranges from a low of about 5 fA (CMOS low-bias op-amps, and "electrometer" op-amps) to

50 nA (typical ${ }^{47}$ BJT op-amps) to a high of $10 \mu \mathrm{~A}$ (wideband BJT-input op-amps). Bias current flowing through the circuit's dc source resistance causes a dc voltage offset; it also creates a current error in integrators and transresistance amplifiers.

The input noise current $\left(i_{n}\right)$ is the equivalent noise current added at the input. For most op-amps ${ }^{48}$ it is simply the shot noise of the bias current $\left(i_{n}=\sqrt{2 q I_{B}}\right)$; it ranges from about $0.1 \mathrm{fA} / \sqrt{\mathrm{Hz}}$ (CMOS low-bias op-amps, "electrometer" op-amps) to $1 \mathrm{pA} / \sqrt{\mathrm{Hz}}$ (wideband BJT op-amps). Input noise current flowing through the circuit's ac source impedance creates a noise voltage, which can dominate over $e_{\mathrm{n}}$. The ratio $r_{\mathrm{n}}=e_{\mathrm{n}} / i_{\mathrm{n}}$ is the op-amp's noise resistance; for signal source impedances greater than $r_{\mathrm{n}}$ the current noise dominates.

Op-amps function properly when both inputs are within the input common-mode voltage range $\left(V_{\mathrm{CM}}\right)$, which may extend to the negative rail ("single-supply" op-amps), or to both rails ("rail-to-rail" op-amps). Beware: many op-amps have a more restricted input differential voltage range, sometimes as little as just a few volts.

### ПM. Output Limitations.

The slew rate (SR) is the op-amp's $d V_{\text {out }} / d t$ with an applied differential voltage at the input. It is set by internal drive currents charging the compensation capacitor, and ranges from about $0.1 \mathrm{~V} / \mu \mathrm{s}$ (micropower op-amps) to $10 \mathrm{~V} / \mu \mathrm{s}$ (general purpose op-amps) to $5000 \mathrm{~V} / \mu \mathrm{s}$ (highspeed op-amps). Slew rate is important in high-speed applications generally, and in large-swing applications such as $\mathrm{A} / \mathrm{D}$ and D/A converters, S/H and peak detectors, and active rectifiers. It limits the large-signal output frequency: a sinewave of amplitude $A$ and frequency $f$ requires a slew rate of $\mathrm{SR}=2 \pi A f$; see Figure 4.54.

Op-amps are small devices, with output current deliberately limited to prevent overheating; see for example Figure 4.43, where $R_{5} Q_{9}$ and $R_{6} Q_{10}$ limit the output sourcing and sinking currents to $I_{\mathrm{lim}}=V_{\mathrm{BE}} / R \approx 25 \mathrm{~mA}$, illustrated in Figure 4.45. If you need more output current, there are a few high-current op-amps available; you can also add an external unity-gain power buffer like the LT1010 ( $I_{\text {out }}$ to $\pm 150 \mathrm{~mA}$ ), or a discrete push-pull follower.

The open-loop output impedance of an op-amp is generally in the neighborhood of $100 \Omega$, which is reduced by the loop gain to fractions of an ohm at low frequencies. Because an op-amp's open-loop gain $G_{\text {OL }}$ falls as $1 / f$ over

[^55]most of its bandwidth (see $\mathbb{T O}$ below), however, the circuit's closed-loop output impedance rises approximately proportional to frequency; it looks inductive (Figure 4.53).

In general the output swing for an op-amp like Figure 4.43 extends only to within a volt or so from either rail. Many CMOS and other low-voltage op-amps, however, specify unloaded rail-to-rail output swings, see Figure 4.46.

Op-amps can be grouped into several supply voltage ranges: "low-voltage" op-amps have a maximum total supply voltage (i.e., $V_{+}-V_{-}$) around 6 V , and generally operate down to 2 V ; "high-voltage" op-amps allow total supply voltages to 36 V , and generally operate down to $5-10 \mathrm{~V}$. In between there is a sparse class of what might be called "mid-voltage" op-amps, with total supply voltages in the neighborhood of $10-15 \mathrm{~V}$. See Table 5.5. There are also op-amps that are truly high-voltage (to hundreds of volts), see Table 4.2b.

### IN. Gain, Phase Shift, and Bandwidth.

Op-amps have large dc open-loop gain $G_{\mathrm{OL}(\mathrm{dc})}$, typically in the range of $10^{5}-10^{7}$ (the latter being typical of "precision" op-amps, see Chapter 5). To ensure stability (see $\mathbb{T I O}$, below) the op-amp's open-loop gain falls as $1 / f$, reaching unity at a frequency $f_{\mathrm{T}}$ (see Figure 4.47). This limits the closed-loop bandwidth to $\mathrm{BW}{ }_{\mathrm{CL}} \approx f_{\mathrm{T}} / G_{\mathrm{CL}}$. Over most of the operating frequency range the op-amp's open-loop phase shift is $-90^{\circ}$, eliminated in the closed-loop response by feedback.

### ПO. Feedback Stability, "Frequency Compensation," and Bode Plots

Finally, negative feedback can become positive feedback, promoting instability and oscillations, if the accumulated phase shift reaches $180^{\circ}$ at a frequency at which the loop gain is $\geq 1$. This topic is foreshadowed in $\S 4.6 .2$ in connection with capacitive loads, and it is discussed in detail in $\S 4.9$. The basic technique is dominant-pole compensation, in which a deliberate $-6 \mathrm{~dB} /$ octave (i.e., $\propto 1 / f$ ) rolloff is introduced within the op-amp in order to bring the gain down to unity at a frequency lower than that at which additional unintended phase shifts rear their ugly heads (Figure 4.99). Most op-amps include such compensation internally, such that they are stable at all closed-loop gains (the unity-gain follower configuration is most prone to instability, because there is no attenuation in the feedback path). "Decompensated" op-amps are less aggressively compensated, and are stable for closed-loop gains greater than some minimum (often specified as $G>2,5$, or 10 ;

Figure 4.95). Compensated op-amps exhibit an open-loop lagging phase shift of $90^{\circ}$ over most of their frequency range (beginning as low as 10 Hz or less). Thus an external feedback network that adds another $90^{\circ}$ of lagging phase shift at a frequency where the loop gain is unity will cause oscillation.

A favorite tool is the Bode Plot, a graph of gain (log) and phase (linear) versus frequency (log); see Figure 4.97. The stability criterion is that the difference of slopes between the open-loop gain curve and the ideal closed-loop gain curve, at their intersection, should ideally be $6 \mathrm{~dB} /$ octave, but in no case as much as $12 \mathrm{~dB} /$ octave.
