# Chapter5 Analog Integrated Circuits

Chapter Outline

5.1 The $\mu \mathrm{A} 741$ Operational Amplifier 473
5.2 The Two-Stage CMOS Operational Amplifier 487
5.3 The Folded-Cascode CMOS Operational Amplifier 495
5.4 Voltage Comparators 501
5.5 Current and Voltage References 510
5.6 Current-Mode Integrated Circuits 521
5.7 Fully Differential Operational Amplifiers 532
5.8 Switched-Capacitor Circuits 541

Appendix 5A: SPICE Macro-Models 553
References 554
Problems 554

The implementation of the integrated-circuit concept by Jack Kilby at Texas Instruments in 1958, and, independently by Robert Noyce at Fairchild Semiconductor in 1959, triggered a feverish activity that led to the development of the first analog integrated circuits (ICs), namely, the $\mu \mathrm{A} 702$ and $\mu \mathrm{A} 709$ operational amplifiers, the $\mu \mathrm{A} 710$ voltage comparator, and the $\mu \mathrm{A} 723$ voltage regulator. These devices were designed in the early 1960s by Robert J. Widlar (1937-1991) while at Fairchild. (He subsequently moved to National Semiconductor, where he continued to develop groundbreaking analog products.) Widlar devised a number of building blocks, such as the Widlar current source and the bandgap voltage reference, that became industry standards and are in widespread use to this very day.

In May 1968 Fairchild introduced the $\mu \mathrm{A} 741$, the first internally compensated op amp. Previous op amps required external components for frequency compensation. By incorporating this function on chip, the 741 relieved the user from having to contend with the arcane issue of frequency compensation, opening up a broad market for experts and neophytes alike. Though a great many other op amp families have been developed since then, the 741 is still the most widely documented op amp and it contains fundamental building blocks that are common to a variety of contemporary analog ICs. It pays, therefore, to start the chapter by studying this device, both from a historical perspective and a pedagogical standpoint.

CHAPTER HIGHLIGHTS

Following a detailed analysis of the classic 741 op amp , with an eye on the most common op amp nonidealities and limitations, the chapter turns to the two CMOS op amp topologies in widest use today, namely, the two-stage and the folded-cascode op amp types. (We return to these three classes of op amps in Chapter 6, where we investigate their frequency and time responses, and again in Chapter 7, where we investigate their stability in negative-feedback operation.)

We then turn to voltage comparators, another popular class of analog ICs. Both bipolar and CMOS types are addressed, including comparators with hysteresis. (Their transient responses are investigated in Chapter 6.)

Virtually every IC requires suitable circuitry to bias its transistors internally. Also, applications such as instrumentation and measurement require stable and predictable current and voltage references. This class of circuits is addressed next, including bandgap-reference types, both for bipolar and CMOS ICs.

It is interesting that the engineering community has traditionally favored the manipulation of voltages while in fact the manipulation of currents is an inherently faster physical process. Though their development has been delayed also because of technological factors, current-mode ICs are now in much use along with their voltage-mode counterparts. The circuits addressed in this chapter include transconductors, current conveyors (CCs), operational transconductance amplifiers (OTAs), current feedback amplifiers (CFAs), and Gilbert Cells.

In today's mixed-mode ICs, where sensitive analog circuitry is forced to coexist with digital circuitry in highly noisy environments and with low-valued power supplies, much signal processing and transmission is done in fully differential form. The chapter investigates some of the most common fully differential op amps in use today.

The desire to implement analog and digital functions on the same chip mandates the rephrasing of some traditional analog functions in terms of CMOS switches and capacitors, the devices most easily available in today's prevalent digital technology. The chapter concludes with switched-capacitor techniques in two representative applications, autozeroing and filtering. A brief discussion of the discrete-time nature of switchedcapacitor integrators illustrates their departure from their continuous-time counterparts.

The chapter makes abundant use of PSpice both as a software oscilloscope to display transfer curves and waveforms, and as a verification tool for dc and ac hand calculations.

## 5.1 THE $\mu$ A741 OPERATIONAL AMPLIFIER

The 741 op amp incorporates a number of clever design ideas that are in widespread use to this very day. Being also the most widely documented analog IC, it offers the student a variety of sources that can be consulted and used as a vehicle to learn otherwise general analog-design techniques.

Shown in Fig. 5.1 is the circuit schematic of the $\mu \mathrm{A} 741$ op amp as provided by Fairchild, its original manufacturer (the 741 has been second-sourced by virtually every analog IC manufacturer, so you are likely to find slight variants in the literature). With two dozen BJTs, a dozen resistors, and a capacitor, the beginner has
image_name:Figure 5.1
description:The diagram represents the internal schematic of the μA741 operational amplifier. It includes differential input stage, gain stage, and output stage. The circuit employs multiple NPN and PNP transistors, resistors, and a compensation capacitor to achieve its functionality. The power supply nodes are VCC and VEE, and the output is labeled as Vout.

FIGURE 5.1 Circuit schematic of the 741 op amp. (Courtesy of Fairchild Semiconductor Corporation.)
legitimate reasons to feel intimidated. However, the proper approach is not to try to understand the whole circuit at once, but to identify already familiar subcircuits and analyze them individually. Only after understanding its parts can we expect to tackle the circuit as a whole. To facilitate this process, it is convenient to redraw the circuit in a simplified form highlighting only the essentials while leaving the finer details for later. This leads us to the schematic of Fig. 5.2, which the reader is encouraged to compare to the original of Fig. 5.1 before moving along.

### A General Overview of the $\mathbf{7 4 1}$ Op Amp

With reference to Fig. 5.2 we make the following observations:

- Starting out at the lower left, we identify the current mirror $Q_{5} Q_{6}$ as forming an active load for the CB pnp pair $Q_{3}-Q_{4}$. Normally we would expect this pair to be of the EC type, but this is not the case here due to the notoriously low betas of lateral pnp BJTs. Op amps are intended to draw negligibly small currents at the input terminals, so in order to minimize these currents the pnp pair $Q_{3}-Q_{4}$ is operated in the CB mode, and the $v_{P}$ and $v_{N}$ inputs are buffered via the CC pair
image_name:FIGURE 5.2 Simplified circuit schematic of the 741 op amp.
description:This is a simplified schematic of the 741 operational amplifier. It includes a differential input stage with active load, a current mirror, and a Darlington-type output stage. The circuit is designed to optimize the performance of NPN transistors due to their higher beta compared to PNP transistors.

FIGURE 5.2 Simplified circuit schematic of the 741 op amp.
$Q_{1}-Q_{2}$. Since the bipolar process in use optimizes npn BJTs, $Q_{1}$ and $Q_{2}$ enjoy much higher betas than their pnp counterparts and therefore draw much lower base currents. We have thus identified our first subcircuit: a differential-input, single-ended-output amplifier stage made up of two CC-CB halves as well as a current-mirror load.

- Moving toward the right we identify a Darlington-type stage made up of the CC-CE pair $Q_{16} Q_{17}$. The function of the CE amplifier $Q_{17}$ is to provide ad ditional gain, and that of the CC buffer $Q_{16}$ is to provide high input resistance in order to avoid loading the first stage excessively. (Figure 5.1 shows also a capacitance $C_{c}$ between this stage's input and output terminals. Its function is to stabilize the op amp against possible oscillations, a subject to be investigated at the end of Chapter 7. The present analysis is limited to low frequencies, where $C_{c}$ acts as an open circuit and will thus be ignored.)
- Moving further to the right we find yet another CC buffer, namely, $Q_{22}$, whose function is to reduce loading of $Q_{17}$. The emitter network of $Q_{22}$ includes the pair $Q_{18^{-}} Q_{19}$ to provide the two $p n$-junction voltage drops needed to bias the Class AB push-pull pair $Q_{14}-Q_{20}$ forming the output stage. The overload protection circuitry has been omitted precisely because at this point we want to highlight only the essentials, leaving the details for later.
- It stands to reason to regard the 741 op amp as consisting of a cascade of three stages, as block-diagrammed in Fig. 5.3. (In fact a great many op amps conform to a similar three-stage schematization.) One further consideration is in order: to function, all active transistors must be operated in the forward-active region, so a fourth subcircuit is needed to properly bias the aforementioned stages. In Fig. 5.1 this subcircuit is made up of the current-mirror pairs $Q_{8}{ }^{-} Q_{9}, Q_{10}-Q_{11}$, and $Q_{12}-Q_{13}$.
image_name:Figure 5.3 Block diagram of the 741 op amp
description:The block diagram of the 741 operational amplifier consists of three main stages and a DC bias circuitry.

1. **Main Components:**
- **Stage I:** This is the input differential amplifier stage. It takes two inputs, labeled as \( v_P \) (non-inverting) and \( v_N \) (inverting), and provides an amplified differential output. This stage is crucial for the initial amplification and common-mode rejection.
- **Stage II:** This is the intermediate gain stage. It further amplifies the signal received from Stage I. This stage is responsible for providing the majority of the voltage gain.
- **Stage III:** This is the output stage. It takes the signal from Stage II and provides the necessary current to drive the load connected to the output \( v_O \). This stage is designed to provide low output impedance and high current drive capability.
- **DC Bias Circuitry:** This block is responsible for providing the necessary bias currents and voltages to ensure that all transistors in the amplifier operate in their active regions. It is connected to all three stages, ensuring proper operation and stability.

2. **Flow of Information or Control:**
- The signal flow begins at the input of Stage I, where the differential input \( v_P - v_N \) is amplified.
- The amplified signal is then passed to Stage II, where further amplification occurs.
- Finally, the signal reaches Stage III, where it is conditioned to drive the output \( v_O \) effectively.
- The DC bias circuitry provides feedback to each stage, ensuring that the transistors remain properly biased.

3. **Labels, Annotations, and Key Indicators:**
- The inputs are labeled \( v_P \) and \( v_N \), while the output is labeled \( v_O \).
- Each stage is numbered I, II, and III, indicating the sequence of signal processing.
- The DC bias circuitry is clearly labeled and shown to be connected to all stages.

4. **Overall System Function:**
- The primary function of this block diagram is to represent the internal structure and signal flow of the 741 operational amplifier. The arrangement of the three stages, along with the DC bias circuitry, facilitates the amplification of the input differential signal to produce a high-gain output, suitable for driving loads. The bias circuitry ensures that the amplifier operates efficiently and remains stable across different operating conditions.

FIGURE 5.3 Block diagram of the 741 op amp.

The overall objective of this section is to calculate the gain $a$ of the 741 op amp , along with its small-signal input and output resistances. These calculations involve parameters such as $g_{m}, r_{\pi}$, and $r_{o}$, all of which are dc-bias dependent. Consequently, we need to find the dc operating point of each of the relevant transistors before we attempt any ac analysis. We shall do this for each stage, one at a time. By the end of the process, our initial intimidation should have eased significantly.

### The Dc Biasing Network

With reference to the dc biasing subcircuit, repeated in Fig. 5.4 for convenience, we observe that $Q_{11}$ and $Q_{12}$ are diode connected, so

$$
\begin{equation*}
I_{R E F}=\frac{\left(V_{C C}-V_{E B 12(\mathrm{on})}\right)-\left(V_{E E}+V_{B E 11(\mathrm{on})}\right)}{R_{5}} \tag{5.1}
\end{equation*}
$$

image_name:Figure 5.4
description:
[
name: Q10, type: NPN, ports: {C: LOAD1, B: X1, E: E1}
name: Q11, type: NPN, ports: {C: X1, B: X1, E: VEE}
name: Q12, type: PNP, ports: {C: X2, B: X2, E: VCC}
name: Q13, type: PNP, ports: {C: B, B: X2, E: VCC}
name: R4, type: Resistor, value: 5 kΩ, ports: {N1: E1, N2: VEE}
name: R5, type: Resistor, value: 39 kΩ, ports: {N1: X1, N2: X2}
]
extrainfo:The circuit represents a portion of the 741 op amp's DC biasing network, including a Widlar current sink formed by Q10 and Q11, and a current mirror using Q12 and Q13. The circuit operates with nominal power supplies of ±15 V, and typical pn junction voltage drops of 0.7 V. The reference current I_REF is calculated to be 733 μA.

FIGURE 5.4 The dc biasing circuitry of the 741 op amp.

The 741 was designed to operate with nominal power supplies of $\pm 15 \mathrm{~V}$, though it can function with lower values just as well, such as $\pm 5 \mathrm{~V}$. In the following analysis we shall assume nominal supplies along with typical pn junction voltage drops of 0.7 V . With these values, Eq. (5.1) gives $I_{R E F}=733 \mu \mathrm{~A}$.

The pair $Q_{10}-Q_{11}$ forms a Widlar current sink. Using the iterative technique presented in Chapter 4 in connection with this type of source, we get

$$
\begin{equation*}
I_{1}=19 \mu \mathrm{~A} \tag{5.2}
\end{equation*}
$$

The $Q_{12}-Q_{13}$ pair forms an ordinary current mirror, except that $Q_{13}$ is equipped with two collectors instead of one. Two collectors are fabricated by making two separate $p$-type diffusions into the $n$-type base region. In the present case the areas are fabricated in a 3-to-1 ratio, so the larger of the two will collect $3 / 4$ and the smaller $1 / 4$ of the total collector current $I_{C 13}$. (Alternatively, you can think of $Q_{13}$ as consisting of two separate transistors $Q_{13 A}$ and $Q_{13 B}$ with their emitters and bases tied pairwise together and with their $I_{s}$ in a 3-to-1 ratio. Except that fabricating two separate BJTs would take up more chip area than a single BJT equipped with two collectors.) By currentmirror action, $I_{C 13}=I_{R E F}\left(1-2 / \beta_{F 13}\right)=733(1-2 / 50)=704 \mu \mathrm{~A}$, where $\beta_{F 13}=50$ is assumed. Letting $I_{2}=3 I_{3}=3 / 4 I_{C 13}$ gives

$$
\begin{equation*}
I_{2}=528 \mu \mathrm{~A} \quad I_{3}=176 \mu \mathrm{~A} \tag{5.3}
\end{equation*}
$$

### The 1st or Input Stage

The operation of this stage is best understood by examining it right after we apply power. With all BJTs still off, the first item to go on is the current $I_{R E F}$ of Fig 5.4, followed by $I_{1}$ through $I_{3}$. Initially all of $I_{1}$ in Fig. 5.5 will be pulled out of the bases of $Q_{3}$ and $Q_{4}$, causing their rapid turn on. But, as $Q_{3}$ and $Q_{4}$ conduct, so do $Q_{1}$ and $Q_{2}$, as the latter are in series with the former. $Q_{1}$ and $Q_{2}$ draw their collector currents from the diode-connected transistor $Q_{8}$, whose current is mirrored by $Q_{9}$ back to the very node where $I_{1}$ triggered the whole sequence of events. We have a negative-feedback situation whereby the circuit will automatically stabilize at the operating point where the current $I_{C 9}$ returned by $Q_{9}$, augmented by the current $2 I_{B}$ coming from the bases of $Q_{3}$ and $Q_{4}$, will equal $I_{1}$.

We know from Chapter 4 that the current returned by $Q_{9}$, compared to that of $Q_{8}$, is afflicted by a fractional error of $-2 / \beta_{F p}$. This may not be negligible, as lateral pnp BJTs have mediocre betas. However, in the present arrangement this error is cancelled out by the current $2 I_{B}$ returned by the bases of $Q_{3}$ and $Q_{4}$ themselves. (This error cancellation is similar to that occurring in Wilson current mirrors.) We thus conclude that the BJTs of each half of the input stage carry a current of $I_{1} / 2$, or

$$
\begin{equation*}
I_{C 1}=I_{C 2}=I_{C 3}=I_{C 4}=I_{C 5}=I_{C 6}=\frac{I_{1}}{2}=9.5 \mu \mathrm{~A} \tag{5.4}
\end{equation*}
$$

The base currents drawn by $Q_{1}$ and $Q_{2}$ are

$$
\begin{equation*}
I_{P}=I_{N}=\frac{I_{1} / 2}{\beta_{F n}}=47.5 \mathrm{nA} \tag{5.5}
\end{equation*}
$$

image_name:Figure 5.5
description:The circuit is a part of the input stage of a 741 op-amp. It includes a differential amplifier with current mirrors and active loads. The transistors Q1 to Q4 form the differential pair and current mirror. Q5 and Q6 are used for active loading, while Q7 acts as a beta helper. The circuit is powered by VCC and VEE.

FIGURE 5.5 Circuit for the dc analysis of the input stage of the 741 op amp.
where $\beta_{F n}=200$ is assumed for the $Q_{1}-Q_{2}$ pair. Once powered, the op amp will automatically draw these currents from the surrounding circuitry. Looking back at Fig. 5.1 we note that both collectors of $Q_{5}$ and $Q_{6}$ are two $p n$-junction voltage drops above $V_{E E}$. Consequently, besides acting as a beta helper, $Q_{7}$ ensures equal collector voltages for $Q_{5}$ and $Q_{6}$ as well as for $Q_{3}$ and $Q_{4}$, thus rendering the two halves of the stage perfectly balanced.

We now wish to find the small-signal gain and the input/output resistances of the input stage. This task is simplified considerably if we exploit the half-circuit concept of Fig. 5.6a. By applying $v_{i d} / 2$ to $Q_{1}$ and $-v_{i d} / 2$ to $Q_{2}$ we force the common base node of $Q_{3}$ and $Q_{4}$ to remain at ac ground, so we can work with just one of the two halves, say, $Q_{1}$ and $Q_{3}$. Their small-signal emitter resistances $r_{e 1}$ and $r_{e 3}$ cause a voltage division by two to give, at their shared emitter terminals, the ac signal
image_name:Figure 5.6 (a)
descriptionThe circuit shown is an AC analysis model of the input stage of a differential amplifier. It uses the half-circuit concept to simplify analysis by applying differential voltages to transistors Q1 and Q2. Q3 and Q4 form a current mirror configuration, while Q5, Q6, and Q7 are part of a biasing and amplification stage. Resistors R1, R2, and R3 provide biasing and load resistance. The circuit exploits symmetry and uses small-signal models for analysis.

(a)
image_name:Figure 5.6 (b)
description:
[
name: Rid, type: Resistor, value: 2.19 MΩ, ports: {N1: vid_plus, N2: vid_minus}
name: Gm1, type: VoltageControlledCurrentSource, value: 1/5.47 kΩ, ports: {Np: vop, Nn: von}
name: Ro1, type: Resistor, value: 6.12 MΩ, ports: {N1: vop, N2: von}
]
extrainfo:The circuit represents a small-signal model of a differential amplifier input stage. It uses a voltage-controlled current source to model the transconductance gain. The resistors provide biasing and load resistance. The circuit shows the relationship between the differential input voltage and the output voltage.

(b)

FIGURE 5.6 (a) Circuit for the ac analysis of the input stage, and (b) input-stage small-signal equivalent.
$(1 / 2)\left(v_{i d} / 2\right)=v_{i d} / 4$. So, the ac current out of $Q_{3}$ 's collector is $i_{3}=g_{m 3} v_{i d} / 4$, whereas the ac current into $Q_{4}$ 's collector is, by symmetry, $i_{4}=g_{m 4} v_{i d} / 4$. The current mirror made up of $Q_{5}$ and $Q_{6}$ reflects $i_{3}$ so that the net short-circuit ac current sunk from the output node is $i_{o 1(\mathrm{sc})}=i_{3}+i_{4}=g_{m 3} v_{i d} / 4+g_{m 4} v_{i d} / 4=g_{m} v_{i d} / 2$, where we have dropped the subscripts as the two $g_{m}$ sare identical. This allows us to write

$$
\begin{equation*}
G_{m 1}=\frac{i_{o l(\mathrm{~s})}}{v_{i d}}=\frac{g_{m}}{2}=\frac{9.5 \mu \mathrm{~A}}{2 \times 26 \mathrm{mV}}=\frac{1}{5.47 \mathrm{k} \Omega} \tag{5.6}
\end{equation*}
$$

where $G_{m 1}$ is the first-stage transconductance. Looking into $Q_{1}$ 's base terminal we find, by inspection, $R_{i d} / 2=r_{\pi 1}+\left(\beta_{01}+1\right) r_{e 3} \cong r_{\pi 1}+\left(\beta_{01}+1\right) r_{e 1}=2 r_{\pi 1}=2 r_{\pi n}$, having used the fact that $r_{e 3} \cong r_{e 1}$. Consequently,

$$
\begin{equation*}
R_{i d} \cong 4 r_{\pi n}=2.19 \mathrm{M} \Omega \tag{5.7}
\end{equation*}
$$

where we again assume $\beta_{0 n}=200$ for the $Q_{1}-Q_{2}$ pair. Finally, turning to the firststage's output terminal, we use inspection to write $R_{o 1}=R_{c 4} / / R_{c 6} \cong\left[r_{o 4}\left(1+g_{m 4} r_{e 2}\right)\right] / /$ $\left[r_{o 6}\left(1+g_{m 0} R_{2}\right)\right]$, or

$$
\begin{equation*}
R_{o 1} \cong 2 r_{o 4} / / 1.37 r_{o 6}=6.12 \mathrm{M} \Omega \tag{5.8}
\end{equation*}
$$

where $V_{A n}=100 \mathrm{~V}$ and $V_{A p}=50 \mathrm{~V}$ are assumed. This completes the analysis of the first stage, whose small-signal characteristics are summarized in Fig. 5.6b.

Before leaving this stage we wish to examine a few additional characteristics that the user needs to be aware of and that are listed in the manufacturer's data sheets.

- Input Bias Current $\boldsymbol{I}_{B}$. This is the average of the two input currents, or $I_{B}=$ $1 / 2\left(I_{P}+I_{N}\right)$. According to Eq. (5.5), $I_{B}$ is in the range of 50 nA , and is strongly influenced by the value of $\beta_{F n}$. Any mismatches in the betas of $Q_{1}$ and $Q_{2}$ will result in an Input Offset Current $I_{O S}=I_{P}-I_{N}$. The 741 data sheets, which you can search on the Web, report the typical values $I_{B}=80 \mathrm{nA}$ and $I_{O S}=20 \mathrm{nA}$.
- Input Offset Voltage $V_{O S}$. Because of $V_{B E}$ mismatches in the BJTs of its two halves, this stage will exhibit some input offset voltage $V_{O S}$. The 741 data sheets give typically $V_{O S}=2 \mathrm{mV}$.
- Input Offset Nulling. The 741 comes with provision for nulling the input offset error stemming from $V_{O S}$ and $I_{O S}$. This is achieved by means of an external $10-\mathrm{k} \Omega$ potentiometer in conjunction with the on-chip resistors $R_{1}$ and $R_{2}$, as depicted in Fig. 5.5. With the wiper halfway, the emitters of $Q_{5}$ and $Q_{6}$ are biased equally at about $[(1 / / 5) \mathrm{k} \Omega] \times(9.5 \mu \mathrm{~A})=8 \mathrm{mV}$ above $V_{E E}$. Moving the wiper away from its center position will make one transistor more conductive by bringing its emitter closer to $V_{E E}$ while leaving the other still about 8 mV above $V_{E E}$. This external imbalance is adjusted empirically by the user until it cancels out any internal imbalance to give the appearance of offset-less behavior.
- Input Voltage Range (IVR). In negative-feedback operation the op amp forces $v_{N}$ to track $v_{P}$, so the common-mode input voltage is $v_{I C}=1 / 2\left(v_{P}+v_{N}\right) \cong v_{P}$. We wish to find the common-mode input voltage range, that is, the range of values of $v_{I C}$ over which the input stage will function properly, with all BJTs operating in the forward-active region or, at most, at the edge of saturation (EOS). Referring to Fig. 5.1 we observe that the upper limit is reached when $Q_{1}$ is driven to the EOS, so we use KVL to write $v_{P(\max )} \cong V_{C C}-V_{E B 8(\text { (n) })}-V_{C E 1(\mathrm{EOS})}+V_{B E 1(\mathrm{on})}$. The lower limit is reached when $Q_{3}$ is driven to the EOS, so $v_{P(\text { min })} \cong V_{E E}+V_{B E S(\text { on })}+$ $V_{B E 7(\text { on })}+V_{E C 3(\mathrm{EOS})}+V_{B E 1(\mathrm{on})}$. Letting $v_{P} \rightarrow v_{I C}$ gives

$$
\begin{equation*}
v_{I C(\max )} \cong V_{C C}-V_{C E(\mathrm{EOS})} \quad v_{I C(\min )} \cong V_{E E}+3 V_{B E(\mathrm{mn})}+V_{E C(\mathrm{EOS})} \tag{5.9}
\end{equation*}
$$

(The above estimates ignore the small voltage drops across $R_{1}, R_{2}$, and $R_{8}$, and also make the simplifying assumption that all junction voltage drops be equal.) To get an idea, if we assume typical junction drops of 0.7 V and EOS drops of 0.2 V , the above estimates give $v_{I C(\max )} \cong V_{C C}-0.2 \mathrm{~V}$ and $v_{I C(\min )} \cong V_{E E}+2.3 \mathrm{~V}$. With $\pm 15-\mathrm{V}$ supplies, the IVR is thus $-12.7 \mathrm{~V} \leq v_{I C} \leq+14.8 \mathrm{~V}$. Pushing $v_{I C}$ outside the IVR will cause malfunction.

### The 2nd or Intermediate Stage

With reference to Fig. 5.7 we have, by inspection, $I_{C 17}=I_{2}$, or

$$
\begin{equation*}
I_{C 17}=528 \mu \mathrm{~A} \tag{5.10}
\end{equation*}
$$

Moreover we have $I_{C 6}=\alpha_{F 6}\left(I_{R_{9}}+I_{B 17}\right)$, which can be approximated as

$$
\begin{equation*}
I_{C 16} \cong \frac{V_{B E 17}+R_{8} I_{2} / \alpha_{F 17}}{R_{9}}+\frac{I_{2}}{\beta_{F 17}} \cong \frac{V_{T} \ln \left(I_{2} / I_{s 17}\right)+R_{8} I_{2}}{R_{9}}+\frac{I_{2}}{\beta_{F 17}} \tag{5.11a}
\end{equation*}
$$

Assuming $I_{s 17}=10 \mathrm{fA}$ and $\beta_{F 17}=250$ we get

$$
\begin{equation*}
I_{C 16}=16 \mu \mathrm{~A} \tag{5.11b}
\end{equation*}
$$

This completes the dc analysis.
For the small-signal analysis refer to Fig. 5.8a, where $C_{c}$ has been omitted because here we are interested only in low-frequency behavior. Starting out at the left and working our way toward the right we write, by inspection

$$
\begin{equation*}
R_{i 2}=r_{\pi 16}+\left(\beta_{016}+1\right)\left\{R_{9} / /\left[r_{\pi 17}+\left(\beta_{017}+1\right) R_{8}\right]\right\} \tag{5.12a}
\end{equation*}
$$

Assuming $\beta_{016}=200$ and $\beta_{017}=250$ we get

$$
\begin{equation*}
R_{i 2}=4.63 \mathrm{M} \Omega \tag{5.12b}
\end{equation*}
$$

Using again inspection, we write

$$
\begin{equation*}
R_{o 2}=r_{o 13 A} / / R_{c 17} \cong r_{o 13 A} / /\left[r_{o 17}\left(1+g_{m 17} R_{8}\right)\right] \tag{5.13a}
\end{equation*}
$$

Letting $r_{o 13 A}=(50 \mathrm{~V}) /(528 \mu \mathrm{~A})=94.7 \mathrm{k} \Omega$ and $r_{o 17}=(100 \mathrm{~V}) /(528 \mu \mathrm{~A})=189.4 \mathrm{k} \Omega$ we get

$$
\begin{equation*}
R_{o 2}=81.3 \mathrm{k} \Omega \tag{5.13b}
\end{equation*}
$$

image_name:FIGURE 5.7 Circuit for the dc analysis of the intermediate stage of the 741 op amp
description:
[
name: Q16, type: NPN, ports: {C: VCC, B: Vo1, E: V1}
name: Q17, type: NPN, ports: {C: V2, B: V1, E: V3}
name: R9, type: Resistor, value: 50kΩ, ports: {N1: V1, N2: VEE}
name: R8, type: Resistor, value: 100Ω, ports: {N1: V3, N2: VEE}
name: I2, type: CurrentSource, value: 528μA, ports: {Np: Vcc, Nn: V2}
]
extrainfo:The circuit represents the intermediate stage of a 741 operational amplifier for DC analysis. It includes two NPN transistors (Q16 and Q17), two resistors (R8 and R9), and a current source (I2). The transistors are configured with Q16 in a common collector mode and Q17 in a common emitter mode.

FIGURE 5.7 Circuit for the dc analysis of the intermediate stage of the 741 op amp .
image_name:(a)
description:
[
name: Q16, type: NPN, ports: {C: GND, B: vi2, E: vb17}
name: Q17, type: NPN, ports: {C: GND, B: vb17, E: ve17}
name: R9, type: Resistor, value: 50kΩ, ports: {N1: vb17, N2: GND}
name: R8, type: Resistor, value: 100Ω, ports: {N1: ve17, N2: GND}
name: ro13A, type: Resistor, value: 94.7kΩ, ports: {N1: GND, N2: GND}
]
extrainfo:The circuit represents the intermediate stage of a 741 operational amplifier for DC analysis. It includes two NPN transistors (Q16 and Q17), two resistors (R8 and R9), and a current source (I2). The transistors are configured with Q16 in a common collector mode and Q17 in a common emitter mode.
image_name:(b)
description:
[
name: Ri2, type: Resistor, value: 4.63MΩ, ports: {N1: Vi2, N2: GND}
name: Gm2, type: VoltageControlledCurrentSource, value: 1/161Ω, ports: {Np: Vo2, Nn: GND}
name: Ro2, type: Resistor, value: 81.3kΩ, ports: {N1: Vo2, N2: GND}
]
extrainfo:The circuit is an AC analysis of the second stage of the 741 op amp. It consists of a voltage-controlled current source Gm2, a resistor Ri2, and a resistor Ro2. The input voltage is Vi2 and the output voltage is Vo2.

FIGURE 5.8 (a) Circuit for the ac analysis of the second stage, and (b) second-stage small-signal equivalent.

Finally, considering that $Q_{16}$ is operating in the CC mode and $Q_{17}$ in the CE-ED mode, we write

$$
\begin{align*}
G_{m 2} & =\frac{i_{o 2(s c)}}{v_{i 2}}=\frac{v_{b 17}}{v_{i 2}} \times \frac{i_{c 17}}{v_{b 17}}=\frac{1}{1+\frac{r_{e 16}}{R_{9} / /\left[r_{\pi 17}+\left(\beta_{017}+1\right) R_{8}\right]}} \times \frac{g_{m 17}}{1+g_{m 17} R_{8}}  \tag{5.14}\\
& =\frac{1}{161 \Omega}
\end{align*}
$$

where $G_{m 2}$ is the second-stage transconductance. The small-signal characteristics of this stage are summarized in Fig. 5.8b, and this completes the second-stage analysis.

### The 3rd or Output Stage

The output stage of the 741 op amp presents some interesting design solutions that are best appreciated by examining the circuit in its standby state. This state is shown in Fig. 5.9 for the case of the input at 0 V and in the absence of any output load. The biasing transistors $Q_{18}$ and $Q_{19}$ are minimum-size devices whereas the push-pull transistors $Q_{14}$ and $Q_{20}$ are fabricated with larger emitter areas (typically four times as large) to maintain good current gains also at high load currents. If $Q_{14}$ and $Q_{19}$ were diode-connected in the manner of Section 4.10, then $Q_{14}$ and $Q_{20}$ would draw a standby current roughly four times as large as that of the diodes. To reduce this current to a more acceptable level $Q_{18}$ is suitably underbiased, as the following example will clarify. It is also worth mentioning that since they share the same collector, $Q_{18}$ and $Q_{19}$ are fabricated inside the same isolation region, thus saving precious die area.
image_name:FIGURE 5.9
description:
[
name: Q14, type: NPN, ports: {C: VCC, B: V1, E: V5}
name: Q18, type: NPN, ports: {C: V1, B: V1, E: V2}
name: Q19, type: NPN, ports: {C: V1, B: V2, E: V3}
name: Q20, type: PNP, ports: {C: VEE, B: V3, E: V6}
name: Q22, type: PNP, ports: {C: VEE, B: GND, E: V3}
name: R6, type: Resistor, value: 27 Ω, ports: {N1: V5, N2: V4}
name: R7, type: Resistor, value: 22 Ω, ports: {N1: V4, N2: V6}
name: R10, type: Resistor, value: 50 kΩ, ports: {N1: V2, N2: GND}
name: I3, type: CurrentSource, value: 176 μA, ports: {Np: VCC, Nn: V1}
]
extrainfo:This circuit is a DC analysis of the 741 output stage in standby mode. It includes NPN and PNP transistors, resistors, and a current source. The analysis involves estimating collector currents and voltages at various nodes to understand the circuit behavior under standby conditions.

FIGURE 5.9 Dc analysis of the 741 output stage in standby.

In the circuit of Fig. 5.9 let $I_{s 18}=I_{s 19}=2 \mathrm{fA}$ and $I_{s 14}=I_{s 20}=8 \mathrm{fA}$ (four times as large). Moreover, whenever appropriate, assume negligible base currents for all BJTs.
(a) Use iterations to estimate the collector currents $I_{C 18}$ and $I_{C 19}$. Hence, find $V_{B B}$, in mV .
(b) Estimate $I_{C 14}$ and $I_{C 20}$ under the simplifying assumption $R_{6}=R_{7}=0$.
(c) Repeat part (b), but with $R_{6}$ and $R_{7}$ in place as shown. Comment on your findings.

#### Solution

(a) Start out with $V_{B E 19}=0.7 \mathrm{~V}$, so $I_{C 18} \cong V_{B E 19} / R_{10} \cong 0.7 / 50=14 \mu \mathrm{~A}$. By $\mathrm{KCL}, I_{C 19}=I_{3}-I_{C 18} \cong 176-14=162 \mu \mathrm{~A}$. By the BJT equation, $V_{B E 19}=$ $V_{T} \ln \left(I_{C 19} / I_{s 19}\right)=0.026 \ln \left[\left(162 \times 10^{-6}\right) /\left(2 \times 10^{-15}\right)\right]=0.653 \mathrm{~V}$. Use this value for the improved estimate $I_{C 18} \cong 0.653 / 50 \cong 13 \mu \mathrm{~A}$. Allowing for, say, $1 \mu \mathrm{~A}$ of base current for $Q_{19}$, we finally get

$$
\begin{equation*}
I_{C 18} \cong 14 \mu \mathrm{~A} \quad I_{C 19} \cong 162 \mu \mathrm{~A} \tag{5.15}
\end{equation*}
$$

and no further iterations are needed. Applying again the BJT equation with $I_{s 18}=I_{s 19}=2 \mathrm{fA}$ we get

$$
V_{B B}=V_{B E 18}+V_{B E 19}=589.4+653.1 \cong 1242 \mathrm{mV}
$$

(b) In standby we have $I_{C 14}=I_{C 20}$. Moreover, with $I_{s 14}=I_{s 20}$ we also have $V_{B E 14}=$ $V_{E B 20}=V_{B B} / 2$ so

$$
I_{C 14}=I_{C 20}=8 \times 10^{-15} \exp (1242 / 52) \cong 190 \mu \mathrm{~A}
$$

Even though $Q_{14}$ and $Q_{20}$ are large-area devices, they conduct a standby current that is comparable to $I_{3}$.
(c) With $R_{6}$ and $R_{7}$ in place, the voltage drop across the combined junctions of $Q_{14}$ and $Q_{20}$ will be reduced by $\Delta V=\left(R_{6}+R_{7}\right) I_{Q}$, where $I_{Q}$ is the new value of the quiescent current of $Q_{14}$ and $Q_{20}$. Using $190 \mu \mathrm{~A}$ as our initial estimate for $I_{Q}$ we find $\Delta V=(27+22) 190 \times 10^{-6} \cong 9.3 \mathrm{mV}$, so we get

$$
\begin{equation*}
I_{Q}=8 \times 10^{-15} \exp [(1242-9.3) / 52] \cong 160 \mu \mathrm{~A} \tag{5.16}
\end{equation*}
$$

This is lower than the previous estimate because of the voltage dropped by $R_{6}$ and $R_{7}$.

In actual application the output stage is unlikely to be in standby, so for a more realistic ac analysis we consider the typical situation of a $2-\mathrm{k} \Omega$ load being driven by a voltage centered at $V_{O}=5 \mathrm{~V}$. Under these conditions, the lower half of the pushpull stage will be off, leaving $Q_{14}$ to source the current $I_{L}=5 / 2=2.5 \mathrm{~mA}$ to the load. The ac equivalent of the output stage simplifies as in Fig. 5.10a, where $Q_{13 B}$ is modeled with the resistance $r_{o 13 B}=(50 \mathrm{~V}) /(176 \mu \mathrm{~A})=284 \mathrm{k} \Omega$, and the biasing network made up of $Q_{18}, Q_{19}$, and $R_{10}$ with a single small-signal resistance $r_{b b} \cong 174 \Omega$ (see Exercise 5.1).
image_name:(a)
description:
[
name: Q22, type: PNP, ports: {C: GND, B: vi3, E: ve22}
name: Q14, type: NPN, ports: {C: GND, B: v1, E: v2}
name: Ro13B, type: Resistor, value: 284kΩ, ports: {N1: GND, N2: v1}
name: Rbb, type: Resistor, value: 174Ω, ports: {N1: v1, N2: ve22}
name: R02, type: Resistor, value: 81.3kΩ, ports: {N1: vi3, N2: GND}
name: R6, type: Resistor, value: 27kΩ, ports: {N1: v2, N2: vo}
name: RL, type: Resistor, value: 2kΩ, ports: {N1: vo, N2: GND}
]
extrainfo:The circuit is an AC analysis model of an output stage. It includes a push-pull amplifier configuration with transistors Q22 and Q14, resistors for biasing and load, and models for small-signal analysis. The circuit is designed to analyze the behavior of the output stage under AC conditions.
image_name:(b)
description:
[
name: Ri3, type: Resistor, value: 9.33MΩ, ports: {N1: Vi3, N2: GND}
name: Ro, type: Resistor, value: 47Ω, ports: {N1: Vi3, N2: Vo}
name: vi3, type: VoltageControlledCurrentSource, value: vi3, ports: {Np: Vi3, Nn: GND}
]
extrainfo:The circuit is an AC equivalent output stage with a push-pull configuration. Q14 sources current to the load, while Q22 is part of the biasing network. The circuit includes a feedback loop with resistors and a small-signal equivalent for AC analysis.

FIGURE 5.10 (a) Circuit for the ac analysis of the output stage, and (b) output-stage small-signal equivalent.

#### EXercise 5.1

Draw the small-signal equivalent of the biasing network of Fig. 5.9, consisting of $Q_{18}, Q_{19}$, and $R_{10}$, and show that the entire network acts as a single resistance

$$
\begin{equation*}
r_{b b}=\frac{r_{d 18}+\left(R_{10} / / r_{\pi 19}\right)}{1+g_{m 19}\left(R_{10} / / r_{\pi 19}\right)} \cong 174 \Omega \tag{5.17}
\end{equation*}
$$

where $r_{d 18}=V_{T} / I_{C 18}$ is the ac resistance of diode-connected $Q_{18}$, and $g_{m 19}=I_{C 19} / V_{T}$ and $r_{\pi 19}=\beta_{019} / g_{m 19}$ are the small-signal parameters of $Q_{19}$. Assume the currents of Example 5.1 as well as $\beta_{019}=200$.

To find the small-signal characteristics of the output stage refer again to Fig. 5.10a. Considering that we have two voltage-followers coupled via the small resistance $r_{b b}$, we can approximate

$$
\begin{equation*}
v_{o} \cong 1 \times v_{i 3} \tag{5.18}
\end{equation*}
$$

By inspection we also have

$$
\begin{equation*}
R_{i 3}=r_{\pi 22}+\left(\beta_{022}+1\right)\left[r_{b b}+\left(r_{o 13 B} / / R_{b 14}\right)\right] \tag{5.19a}
\end{equation*}
$$

where $R_{b 14}$ is the ac resistance seen looking into the base of $Q_{14}$,

$$
R_{b 14}=r_{\pi 14}+\left(\beta_{014}+1\right)\left(R_{6}+R_{L}\right)
$$

Assuming $I_{C 14}=2.5 \mathrm{~mA}$ and $\beta_{014}=250$ we get $R_{b 14} \cong 511 \mathrm{k} \Omega$. Substituting into Eq. (5.19a) and assuming $\beta_{022}=50$, we finally obtain

$$
\begin{equation*}
R_{i 3}=9.33 \mathrm{M} \Omega \tag{5.19b}
\end{equation*}
$$

Using again inspection, we write

$$
\begin{equation*}
R_{o}=R_{6}+\frac{R_{B 14}+r_{\pi 14}}{\beta_{014}+1} \tag{5.20a}
\end{equation*}
$$

where $R_{B 14}$ is the ac resistance presented to $Q_{14}$ 's base by the circuitry upstream,

$$
R_{B 14}=r_{o 13 B} / /\left(r_{b b}+R_{e 22}\right)
$$

and $R_{e 22}$ is the ac resistance seen looking into $Q_{22}$ 's emitter

$$
R_{e 22}=\frac{R_{o 2}+r_{\pi 22}}{\beta_{022}+1}=\frac{81.3+50(26 / 0.176)}{50+1}=1.74 \mathrm{k} \Omega
$$

Substituting gives $R_{B 14}=1.9 \mathrm{k} \Omega$. Substituting in turn into Eq. (5.20a) we finally get

$$
\begin{equation*}
R_{o}=47 \Omega \tag{5.20b}
\end{equation*}
$$

The small-signal characteristics of the output stage are summarized in Fig. 5.10b. Before leaving this stage we wish to investigate one additional characteristic that the user needs to know and that is reported in the data sheets.

- Output Voltage Swing (OVS). This is the range of values of $v_{O}$ over which the output stage will function properly, with all active BJTs operating in the forward-active region or at most at the edge of saturation (EOS). Simple inspection of Fig. 5.1 reveals that the upper limit for $v_{O}$ is reached when $Q_{13 B}$ is driven to the EOS, and the lower limit when $Q_{17}$ is driven to the EOS. Using KVL we thus write $v_{O(\max )} \cong V_{C C}-V_{E C 13(\mathrm{EOS})}-V_{B E 14(\mathrm{on})}$ and $v_{O(\min )} \cong V_{E E}+V_{C E 17(\mathrm{EOS})}+$ $V_{\text {EB22(on) }}+V_{\text {EB20(on) }}$. These simplify as

$$
\begin{equation*}
v_{O(\max )} \cong V_{C C}-V_{E C(\mathrm{EOS})}-V_{B E(\mathrm{on})} \quad v_{O(\min )} \cong V_{E E}+V_{C E(\mathrm{EOS})}+2 V_{E B(\mathrm{on})} \tag{5.21}
\end{equation*}
$$

(The above estimates assume identical junction voltage drops for the BJTs, along with light output loading so that the voltage drops across $R_{6}$ and $R_{7}$ can be ignored.) To get an idea, if we assume junction drops of 0.7 V and EOS drops of 0.2 V , the above estimates give $v_{O(\max )} \cong V_{C C}-0.9 \mathrm{~V}$ and $v_{O(\min )} \cong V_{E E}+1.6 \mathrm{~V}$. With $\pm 15-\mathrm{V}$ supplies, the OVS is thus $-13.4 \mathrm{~V} \leq v_{O} \leq+14.1 \mathrm{~V}$.

### The Small-Signal Characteristics of the $\mathbf{7 4 1}$ Op Amp

We now use the three-stage cascade of Fig. 5.11 to find the overall small-signal gain a. By inspection

$$
\begin{align*}
a & =\frac{v_{o}}{v_{i d}} \cong\left(-G_{m 1}\right)\left(R_{o 1} I / R_{i 2}\right)\left(-G_{m 2}\right)\left(R_{o 2} / / R_{i 3}\right)=(-482) \times(-501)  \tag{5.22}\\
& =241 \times 10^{3} \mathrm{~V} / \mathrm{V}
\end{align*}
$$

indicating that the first two stages contribute gains on the order of $500 \mathrm{~V} / \mathrm{V}$ each. The 741 data sheets give typically $R_{i d}=2 \mathrm{M} \Omega, a=200 \times 10^{3} \mathrm{~V} / \mathrm{V}$, and $R_{o}=75 \Omega$. Our calculations are influenced by the assumed values for the betas and the Early voltages, both of which depend on critical fabrication parameters such as the base width. Also, assuming infinite Early voltages to simplify the dc calculations may have underestimated dc currents by as much as 20-30\%, especially in the case of pnp BJTs. Finally, $R_{o}$ depends on the operating current of $Q_{14}$, which was arbitrarily assumed to be 2.5 mA ,
image_name:FIGURE 5.11 Small-signal model of the 741 op amp.
description:
[
name: Rid, type: Resistor, value: 2.19 MΩ, ports: {N1: Vid, N2: GND}
name: Gm1, type: VoltageControlledCurrentSource, value: GmVid, ports: {Np: Vi2, Nn: GDD}
name: Ro1, type: Resistor, value: 6.12 MΩ, ports: {N1: V12, N2: GND}
name: Ri2, type: Resistor, value: 4.63 MΩ, ports: {N1: V12, N2: GND}
name: Gm2, type: VoltageControlledCurrentSource, value: 1/161 Ω, ports: {Np: V23, Nn: GND}
name: Ro2, type: Resistor, value: 81.3 kΩ, ports: {N1: V23, N2: GND}
name: Ri3, type: Resistor, value: 9.33 MΩ, ports: {N1: V23, N2: GND}
name: Ro, type: Resistor, value: 47 Ω, ports: {N1: V23, N2: Vo}
name: Iv23, type: VoltageControlledVoltageSource, ports: {Np: V23, Nn: Vo}
]
extrainfo:This is a small-signal model of the 741 operational amplifier, showing the internal resistance and transconductance stages. The model illustrates the interaction between voltage-controlled current sources and various resistors to simulate the behavior of the op-amp.

FIGURE 5.11 Small-signal model of the 741 op amp.
image_name:Small-signal model of the 741 op amp
description:
[
name: VI, type: VoltageSource, value: VI, ports: {Np: VI, Nn: GND}
name: μA741, type: OpAmp, value: μA741, ports: {InP: VI, InN: GND, OutP: Vo, OutN: GND, Vdd: VCC(+15V), -Vdd: VCC(-15V)}
name: RL, type: Resistor, value: 2kΩ, ports: {N1: Vo, N2: GND}
]
extrainfo:This circuit is a small-signal model of the 741 operational amplifier. It includes a voltage source VI, an op-amp μA741, and a load resistor RL. The op-amp is powered by a dual supply of +15V and -15V. The output voltage Vo is taken across the load resistor RL connected to the ground.

(a)
image_name:(b)
description:The graph shown is a Voltage Transfer Characteristic (VTC) for a 741 operational amplifier. It plots the output voltage \( v_o \) in volts (V) against the differential input voltage \( v_P - v_N \) in microvolts (\( \mu V \)).

1. **Type of Graph and Function:**
- The graph is a Voltage Transfer Characteristic (VTC) plot.

2. **Axes Labels and Units:**
- The x-axis represents the differential input voltage \( v_P - v_N \) in microvolts (\( \mu V \)), ranging from -150 \( \mu V \) to 150 \( \mu V \).
- The y-axis represents the output voltage \( v_o \) in volts (V), ranging from -15 V to 15 V.

3. **Overall Behavior and Trends:**
- The graph shows a linear region where the output voltage \( v_o \) increases with the input voltage \( v_P - v_N \). This linear region is centered around 0 \( \mu V \) and extends approximately from -100 \( \mu V \) to 100 \( \mu V \).
- Beyond this linear region, the output voltage saturates at approximately -15 V for input voltages less than -100 \( \mu V \) and at approximately 15 V for input voltages greater than 100 \( \mu V \).

4. **Key Features and Technical Details:**
- The slope of the linear region represents the gain of the operational amplifier.
- The saturation levels indicate the supply voltage limits of the op-amp, approximately \( \pm 15 \) V.

5. **Annotations and Specific Data Points:**
- The graph clearly shows the transition from the linear region to saturation, marking the limits of linear operation for the op-amp.
- The center of the linear region is at 0 \( \mu V \), which is typical for op-amp VTCs, indicating balanced input conditions.

(b)

FIGURE $\mathbf{5 . 1 2}$ (a) PSpice circuit to display (b) the VTC of the 741 op amp.
so, the discrepancies between calculated and data-sheets values are not surprising. Yet, the mental process exercised in the estimation of these parameters is undoubtedly quite instructive-and presumably it has helped demystify our initial intimidation.

### PSpice Simulation of the $\mathbf{7 4 1} \mathbf{0 p}$ Amp

To facilitate the simulation of op amps in an application setting, manufacturers usually provide SPICE macro-models of their device (see Appendix 5A). The PSpice circuit of Fig. 5.12a utilizes the uA741 macro-model available in PSpice's library to display the VTC as well as to calculate the ac gain $a$ and the input and output resistances $r_{i}$ and $r_{o}$. The results are as follows.

```
V(OUT)/VI = 1.992E+05
INPUT RESISTANCE AT VI = 9.963E+05
OUTPUT RESISTANCE AT V(OUT) = 1.517E+02
```

Figure $5.12 b$ confirms that the output saturates in the vicinity of the supply voltages. It also shows a (systematic) input offset voltage of about $20 \mu \mathrm{~V}$. This macro-model will be used in subsequent chapters to investigate other behavioral aspects, such as the frequency and transient responses as well as the stability of 741 circuits.

## 5.2 THE TWO-STAGE CMOS OPERATIONAL AMPLIFIER

This classic CMOS op amp topology (and variants thereof) is used especially in mixed-mode ICs. Shown in its basic form in Fig. 5.13, it comprises two gain stages and a dc biasing circuit as follows:

- The 1st or input stage consists of the $p$-channel differential pair $M_{1}-M_{2}$ and the $n$-channel mirror load $M_{3}-M_{4}$. As we know, its voltage gain is

$$
\begin{equation*}
a_{1}=-g_{m 1}\left(r_{o 2} / / r_{o 4}\right) \tag{5.23}
\end{equation*}
$$

image_name:Figure 5.13 Two-stage CMOS op amp
description:
[
name: M1, type: PMOS, ports: {S: x3, D: x2, G: vN}
name: M2, type: PMOS, ports: {S: x3, D: x1, G: vP}
name: M3, type: NMOS, ports: {S: Vss, D: x2, G: x2}
name: M4, type: NMOS, ports: {S: GND, D: x1, G: x2}
name: M5, type: NMOS, ports: {S: Vss, D: vO, G: x1}
name: M6, type: PMOS, ports: {S: VDD, D: vO, G: x4}
name: M7, type: PMOS, ports: {S: VDD, D: x3, G: x4}
name: M8, type: PMOS, ports: {S: VDD, D: x4, G: x4}
name: I_REF, type: CurrentSource, ports: {Np: x4, Nn: VSS}
name: R_C, type: Resistor, value: R_C, ports: {N1: x1, N2: RC}
name: C_C, type: Capacitor, value: C_C, ports: {Np: RC, Nn: vO}
]
extrainfo:The circuit is a two-stage CMOS operational amplifier with a differential input stage and a common-source output stage. It includes a compensation network with R_C and C_C for stability.

FIGURE 5.13 Two-stage CMOS op amp.

- The 2nd or output stage consists of the CS amplifier $M_{5}$ and the active load $M_{6}$. (Also shown is an $R_{c}-C_{c}$ network whose function is to stabilize the amplifier against possible oscillations in negative-feedback operation, a subject to be addressed in Chapter 7. The present analysis is restricted to low frequencies, where $C_{c}$ acts as an open circuit, so the $R_{c}-C_{c}$ network will be ignored.) This stage's low-frequency voltage gain is

$$
\begin{equation*}
a_{2}=-g_{m 5}\left(r_{o 5} / / r_{o 6}\right) \tag{5.24}
\end{equation*}
$$

- The dc biasing circuit consists of the dual-output current mirror $M_{6}-M_{7}-M_{8}$, along with the $I_{R E F}$ current reference. The details of this reference have been omitted for simplicity, but this is typically a circuit shared among different op amps on the same chip. It generates a regulated current $I_{R E F}$ once, which is then replicated by a multiple-output current mirror to each of the other on-chip op amps. In Fig. 5.13, $I_{R E F}$ is replicated by $M_{7}$ to bias the $M_{1}-M_{2}$ pair, and by $M_{6}$ to actively load the CS stage $M_{5}$.
Thanks to the infinite resistance presented by $M_{5}$ 's gate, there is no inter-stage loading, so the overall gain is simply the product of the individual gains

$$
\begin{equation*}
a=\frac{v_{o}}{v_{p}-v_{n}}=a_{1} \times a_{2}=g_{m 1}\left(r_{o 2} / / r_{o 4}\right) g_{m 5}\left(r_{o 5} / / r_{o 6}\right) \tag{5.25a}
\end{equation*}
$$

Adapting Eq. (4.152) to the present case, we express gain in the insightful alternative form

$$
\begin{equation*}
a=\frac{2}{V_{O V 1}\left(\lambda_{2}+\lambda_{4}\right)} \times \frac{2}{V_{O V 5}\left(\lambda_{5}+\lambda_{6}\right)} \tag{5.25b}
\end{equation*}
$$

If the op amp is realized with FETs having the same channel length $L$ and overdrive voltage $V_{O V}$, then gain takes on the concise form

$$
\begin{equation*}
a=\left[\frac{2 L}{V_{O V}\left(\lambda_{n}^{\prime}+\lambda_{p}^{\prime}\right)}\right]^{2} \tag{5.25c}
\end{equation*}
$$

where, by Eq. (4.31), $\lambda_{n}^{\prime}$ and $\lambda_{p}^{\prime}$ are the process parameters characterizing channellength modulation in the $n$ FETs and $p$ FETs, respectively. Clearly, the longer $L$ and the lower $V_{O V}$, the higher the gain. The ac resistances between the two inputs and between the output and ground are, respectively,

$$
\begin{equation*}
R_{i}=\infty \quad R_{o}=r_{o 5} / / r_{o 6} \tag{5.26}
\end{equation*}
$$

We note a close resemblance of the CMOS stages of Fig. 5.13 to the 1st and 2nd stages of the 741 op amp of Fig. 5.2. Actually, thanks to the infinite resistance presented by the gates, the CMOS stages are much simpler. We also note the absence of an output stage, even though $R_{o}$ can be fairly high. Typically, an op amp of the type of Fig. 5.13 is likely to drive other on-chip CMOS circuits also presenting infinite input resistance (though not necessarily zero capacitance), so there is no need for a dedicated output stage. Only when meant to drive resistive loads, most likely off chip, will a two-stage op amp be equipped with a dedicated 3rd stage. This might be an output stage of the type discussed in Section 4.11.

### Input Offset Voltage Considerations

It is important to realize that the $W / L$ ratios of $M_{5}$ and $M_{6}$ cannot be specified arbitrarily, but must satisfy a specific constraint in order to avoid introducing gross input offset voltage errors. To find this constraint, note that since $V_{S G 6}=V_{S G 7}, I_{D 6}$ and $I_{D 7}$ must scale in proportion to their $W / L$ ratios as

$$
\begin{equation*}
\frac{I_{D 6}}{I_{D 7}}=\frac{W_{6} / L_{6}}{W_{7} / L_{7}} \tag{5.27a}
\end{equation*}
$$

Note also that at dc balance we have $V_{D S 4}=V_{D S 3}$. Consequently, $V_{G S 5}=V_{D S 4}=V_{D S 3}=$ $V_{G S 3}$, indicating that $I_{D 5}$ and $I_{D 3}$ must scale in proportion to their $W / L$ ratios as

$$
\begin{equation*}
\frac{I_{D 5}}{I_{D 3}}=\frac{W_{5} / L_{5}}{W_{3} / L_{3}} \tag{5.27b}
\end{equation*}
$$

But, $I_{D 5}=I_{D 6}$ and $I_{D 3}=I_{D 7} / 2$. Substituting into Eq. (5.27) and simplifying gives the important constraint

$$
\begin{equation*}
\frac{W_{5} / L_{5}}{W_{3} / L_{3}}=2 \frac{W_{6} / L_{6}}{W_{7} / L_{7}} \tag{5.28}
\end{equation*}
$$

Once this constraint is met, any $k$ and $V_{t}$ mismatches in the $M_{1}-M_{2}$ and $M_{3}-M_{4}$ pairs will cause the 1st stage to exhibit an input offset voltage of the type of Eq. (4.161). Adapting to the present case, we have

$$
\begin{equation*}
V_{O S(1 \text { ststage })} \cong \frac{V_{O V_{p}}}{2} \sqrt{\left(\frac{\Delta k_{p}}{k_{p}}\right)^{2}+\left(\frac{\Delta k_{n}}{k_{n}}\right)^{2}+\left(\frac{\Delta V_{t p}}{0.5 V_{O V_{p}}}\right)^{2}+\left(\frac{\Delta V_{t n}}{0.5 V_{O V_{p}}}\right)^{2}} \tag{5.29}
\end{equation*}
$$

where subscripts $p$ and $n$ refer, respectively, to the $M_{1}-M_{2}$ and $M_{3}-M_{4}$ pairs. Even if the $M_{1}-M_{2}$ and $M_{3}-M_{4}$ pairs are perfectly matched, letting $v_{P}=v_{N}=0$ is likely to result in $v_{O} \neq 0$ because of a possible imbalance between $M_{5}$ and $M_{6}$. Reflected to the input, the effect of this imbalance will result in an additional component for $V_{O S}$ (this issue is explored further in the end-of-chapter problems).

### Input Voltage Range (IVR)

In negative-feedback operation the op amp forces $v_{N}$ to track $v_{P}$, so the common-mode input voltage is $v_{I C}=1 / 2\left(v_{P}+v_{N}\right) \cong v_{P}$. We wish to find the common-mode input voltage range, that is, the range of values of $v_{I C}$ over which the input stage will function properly, with all FETs operating in saturation or at most at the edge of saturation (EOS). The upper limit is reached when $M_{7}$ is driven to the EOS, where $V_{S D 7}=$ $V_{O V 7}$. Using inspection and KVL we thus write $v_{I C(\max )}=V_{D D}-V_{O V 7}-V_{S G 1}$, that is,

$$
\begin{equation*}
v_{I C(\max )}=V_{D D}-V_{O V 7}-V_{O V 1}-\left|V_{t t}\right| \tag{5.30a}
\end{equation*}
$$

Similarly, the lower limit for $v_{I C}$ is reached when $M_{1}$ is driven to the EOS, where $V_{S D 1}=$ $V_{O V 1}$. Using inspection and KVL we thus write $v_{I C(\min )}=V_{S S}+V_{G S 3}+V_{S D 1}-V_{S G 1}$. But, $V_{S D 1}-V_{S G 1}=V_{O V 1}-\left(V_{O V 1}+\left|V_{t 1}\right|\right)=-\left|V_{t 1}\right|$, so

$$
\begin{equation*}
v_{I C(\min )}=V_{S S}+V_{O V 3}+V_{t 3}-\left|V_{t}\right| \tag{5.30b}
\end{equation*}
$$

It is apparent that for this circuit $v_{I C(\max )}$ is more restrictive than $v_{I C(\min )}$.

### Output Voltage Swing (OVS)

This is the range of values of $v_{0}$ over which $M_{5}$ and $M_{6}$ operate in saturation or at most at the EOS. By inspection, we readily find

$$
\begin{equation*}
v_{O(\max )}=V_{D D}-V_{O V 6} \quad v_{O(\text { min })}=V_{S S}+V_{O V 5} \tag{5.31}
\end{equation*}
$$

In words, $v_{O}$ can swing within a $V_{O V}$ voltage drop of each supply rail.

EXAMPLE 5.2 (a) Suppose the two-stage CMOS op amp of Fig. 5.13 is fabricated in a process characterized by $k_{n}^{\prime}=2.5 k_{p}^{\prime}=100 \mu \mathrm{~A} / \mathrm{V}^{2}, V_{t n}=-V_{t p}=0.75 \mathrm{~V}, \lambda_{n}^{\prime}=$ $0.1 \mu \mathrm{~m} / \mathrm{V}$ and $\lambda_{p}^{\prime}=0.05 \mu \mathrm{~m} / \mathrm{V}$. Moreover, all FETs are fabricated with $L=1 \mu \mathrm{~m}$ and are designed to operate with $V_{O V}=0.25 \mathrm{~V}$. If the circuit is powered from $\pm 2.5-\mathrm{V}$ supplies and uses $I_{R E F}=100 \mu \mathrm{~A}$, specify suitable values for $W_{1}$ through $W_{8}$ to bias both stages at $100 \mu \mathrm{~A}$ (for simplicity assume $\lambda_{n}=\lambda_{p}=0$ in the course of your dc calculations).
(b) Find the individual-stage gains, the overall gain, the output resistance, the IVR, and the OVS.
(c) Check with PSpice and account for any differences between calculated and simulated values.

#### Solution

(a) $M_{6}, M_{7}$, and $M_{8}$ must each satisfy the saturation-region condition

$$
100 \mu \mathrm{~A}=\frac{40 \mu \mathrm{~A}}{2} \frac{W}{1 \mu \mathrm{~m}} 0.25^{2}
$$

which gives $W=80 \mu \mathrm{~m}$. So, $W_{6}=W_{7}=W_{8}=80 \mu \mathrm{~m} . M_{1}$ and $M_{2}$ draw half as much current as $M_{7}$ but with the same overdrive voltage, so $W_{1}=W_{2}=$ $W_{7} / 2=40 \mu \mathrm{~m} . M_{3}$ and $M_{4}$ must each satisfy the condition

$$
50 \mu \mathrm{~A}=\frac{100 \mu \mathrm{~A}}{2} \frac{W}{1 \mu \mathrm{~m}} 0.25^{2}
$$

which gives $W_{3}=W_{4}=16 \mu \mathrm{~m}$. By Eq. $(5.28),\left(W_{5} / 1\right) /(16 / 1)=2(80 / 1) /$ (80/1), or $W_{5}=32 \mu \mathrm{~m}$. In summary,

$$
\begin{array}{ll}
W_{1}=W_{2}=40 \mu \mathrm{~m} & W_{3}=W_{4}=16 \mu \mathrm{~m} \\
W_{5}=32 \mu \mathrm{~m} & W_{6}=W_{7}=W_{8}=80 \mu \mathrm{~m}
\end{array}
$$

(b) By Eq. (5.25c) we have

$$
\begin{aligned}
& \quad a=\left[\frac{2 \times 1}{0.25(0.1+0.05)}\right]^{2}=53.3^{2}=2,844 \mathrm{~V} / \mathrm{V} \\
& \text { so } a_{1}=a_{2}=-53.3 \mathrm{~V} / \mathrm{V} \text {. Also, } \lambda_{n}=\lambda_{n}^{\prime} / 1=0.1 \mathrm{~V}^{-1} \text { and } \lambda_{p}=\lambda_{p}^{\prime} / 1=0.05 \mathrm{~V}^{-1}, \text { so } \\
& r_{o 5}=1 /\left(0.1 \times 100 \times 10^{-6}\right)=100 \mathrm{k} \Omega, r_{o 6}=1 /\left(0.05 \times 100 \times 10^{-6}\right)=200 \mathrm{k} \Omega, \text { and } \\
& \quad R_{o}=100 / / 200=66.7 \mathrm{k} \Omega
\end{aligned}
$$

Finally, Eqs. (5.30) and (5.31) give

$$
\begin{aligned}
& v_{I C(\max )}=2.5-2 \times 0.25-0.75=1.25 \mathrm{~V} \\
& v_{I C(\min )}=v_{O(\min )}=-2.5+0.25=-2.25 \mathrm{~V} \\
& v_{O(\max )}=2.25 \mathrm{~V}
\end{aligned}
$$

(c) A PSpice simulation using the circuit of Fig. 5.14a gives the VTC of Fig. 5.14b, which reveals a (systematic) input offset of $166 \mu \mathrm{~V}$ and confirms output saturation levels within a $V_{O V}$ of the $\pm 2.5-\mathrm{V}$ supplies. (The offset can be compensated for by specifying a dc component of $-166 \mu \mathrm{~V}$ for the ac input source $v_{p}$.) After directing PSpice to perform the small-signal analysis (.TF) we get $a=v_{o} / v_{p}=4,271 \mathrm{~V} / \mathrm{V}$ and $R_{o}=75 \mathrm{k} \Omega$. The discrepancy between calculated and simulated values stems primarily from the assumption $\lambda=0$, especially while calculating $g_{m 1}$ and $g_{m 5}$. For more accurate results we must multiply the calculated value of $g_{m 1}$ by $\left(1+\lambda V_{S D 1}\right) \cong(1+0.05 \times 2.5)=1.125$
and that of $g_{m 5}$ by $\left(1+\lambda V_{D S 5}\right) \cong(1+0.1 \times 2.5)=1.25$. With these corrections we get $a_{1} \cong-53.3 \times 1.125=-60 \mathrm{~V} / \mathrm{V}, a_{2} \cong-53.3 \times 1.25=-66.7 \mathrm{~V} / \mathrm{V}$, and $a \cong-4,000 \mathrm{~V} / \mathrm{V}$, in better agreement with PSpice.
image_name:(a)
description:
[
name: M8, type: PMOS, ports: {S: VDD, D: x1, G: x1}
name: M7, type: PMOS, ports: {S: VDD, D: x2, G: x1}
name: M6, type: PMOS, ports: {S: VDD, D: vo, G: x1}
name: M1, type: PMOS, ports: {S: x2, D: x3, G: GND}
name: M2, type: PMOS, ports: {S: x2, D: x4, G: VP}
name: M5, type: NMOS, ports: {S: GND, D: vo, G: x4}
name: M4, type: NMOS, ports: {S: Vss, D: x4, G: x3}
name: M3, type: NMOS, ports: {S: Vss, D: x3, G: x3}
name: IREF, type: CurrentSource, value: 100uA, ports: {Np: x1, Nn: Vss}
name: VP, type: VoltageSource, value: VP, ports: {Np: VP, Nn: GND}
]
extrainfo:The circuit is a differential amplifier with PMOS and NMOS transistors. It uses a current source IREF to provide biasing, and the differential input is applied at VP. The output is taken at vo. The circuit operates between VDD and VSS supply voltages.
image_name:(b)
description:The graph in question is a Voltage Transfer Characteristic (VTC) graph. It is typically used to represent the output voltage as a function of the input voltage in a MOSFET circuit.

1. **Type of Graph and Function:**
- This is a Voltage Transfer Characteristic (VTC) graph.

2. **Axes Labels and Units:**
- The x-axis represents the input voltage, usually in volts (V).
- The y-axis represents the output voltage, also in volts (V).
- Both axes are likely on a linear scale.

3. **Overall Behavior and Trends:**
- The graph generally shows a transition from a low output voltage to a high output voltage as the input voltage increases, typical of a MOSFET inverter.
- There is a region where the output voltage remains relatively constant at a low level, followed by a sharp transition region, and then a region where the output voltage stabilizes at a high level.

4. **Key Features and Technical Details:**
- The transition region is characterized by a steep slope, indicating the point where the MOSFET switches from off to on.
- The graph may show the threshold voltage (Vt) where the MOSFET begins to conduct significantly.
- The saturation region is visible at both ends of the graph where the output voltage levels off.

5. **Annotations and Specific Data Points:**
- Critical points such as the threshold voltage and maximum output voltage are essential for understanding the device's operation.
- The graph might include markers or annotations indicating specific operating regions or voltages, such as the -3 dB point or other reference voltages.

(a)
image_name:(b)
description:The graph in figure (b) is a Voltage Transfer Characteristic (VTC) curve. It depicts the relationship between the input voltage difference \( v_P - v_N \) (in millivolts) on the x-axis and the output voltage \( v_O \) (in volts) on the y-axis.

1. **Type of Graph and Function:**
- This is a Voltage Transfer Characteristic curve, often used to illustrate the behavior of circuits like amplifiers or comparators.

2. **Axes Labels and Units:**
- The x-axis is labeled "Input \( v_P - v_N \)" with units in millivolts (mV), ranging from -1.0 mV to 1.0 mV.
- The y-axis is labeled "Output \( v_O \)" with units in volts (V), ranging from -2.5 V to 2.5 V.
- The scale for both axes is linear.

3. **Overall Behavior and Trends:**
- The graph shows a central linear region where the output voltage increases with the input voltage.
- At the extreme ends of the input voltage range, the graph levels off, indicating saturation regions where changes in input voltage have little effect on the output voltage.
- The curve transitions smoothly from one saturation region through the linear region to the other saturation region.

4. **Key Features and Technical Details:**
- The linear region is approximately centered around the origin, where the input voltage difference is zero.
- This central linear region suggests that the device has a gain, where small changes in input voltage result in proportional changes in output voltage.
- The saturation regions at both ends represent the limits of the device's output capability.

5. **Annotations and Specific Data Points:**
- No specific markers or annotations are visible on the graph, but critical points include the threshold where the curve begins to deviate from the linear region and the maximum output voltage in the saturation regions.
- The graph is symmetric around the origin, indicating balanced behavior for positive and negative input voltages.

(b)

FIGURE 5.14 (a) PSpice circuit for Example 5.2, and (b) its VTC. The MOSFET parameters are as follows: $k_{n}^{\prime}=2.5 k_{p}^{\prime}=100 \mu \mathrm{~A} / \mathrm{V}^{2}, V_{t n}=-V_{t p}=0.75 \mathrm{~V}$, and $\lambda_{n}=2 \lambda_{\rho}=0.1 \mathrm{~V}^{-1}$.

### Common-Mode Rejection Ratio (CMRR)

We estimate this parameter by adapting Eq. (4.158) to the present circuit,

$$
\begin{equation*}
\operatorname{CMRR}=\frac{1+g_{m 3} r_{o 3}}{1+r_{o 3} / r_{o 1}}\left[1+2\left(g_{m 1}+g_{m b 1}\right) r_{o 7}\right] \tag{5.32}
\end{equation*}
$$

If necessary, the CMRR can be improved by raising $M_{7}$ 's output resistance, for instance via the cascoding technique. The price is a reduction in the value of $v_{I C(\max )}$.

### Power-Supply Rejection Ratio (PSRR)

The output of an amplifier should be unaffected by any variations in its power-supply voltages, such as ripple and supply noise induced by adjacent circuitry. However, a real-life amplifier will be somewhat sensitive also to these variations (besides the already familiar common-mode input voltage), so the small-signal output of an op amp with split supplies takes on the more general form

$$
\begin{equation*}
v_{o}=a_{d m} v_{i d}+a_{c m} v_{i c}+a_{d d} v_{d d}+a_{s s} v_{s s} \tag{5.33}
\end{equation*}
$$

where $v_{d d}$ and $v_{s s}$ are, respectively, the variations in the supply voltages $V_{D D}$ and $V_{S S}$, and $a_{d d}$ and $a_{s s}$ are the gains with which the amplifier magnifies these variations, that is, $a_{d d}=v_{o} / v_{d d}$ and $a_{s s}=v_{o} / v_{s s}$. Ideally, both $a_{d d}$ and $a_{s s}$ should be zero (just like $a_{c m}$ should be). To tell how insensitive a real-life amplifier is to power-supply variations we use a figure of merit called the power-supply rejection ratio (PSRR), which, in the case of split supplies, takes on the separate forms

$$
\begin{equation*}
\mathrm{CMRR}_{d d}=\left|\frac{a_{d m}}{a_{d d}}\right| \quad \mathrm{CMRR}_{s s}=\left|\frac{a_{d m}}{a_{s s}}\right| \tag{5.34}
\end{equation*}
$$

where $a_{d m}$ is the familiar differential-mode gain. To estimate the PSRRs of the twostage CMOS op amp, refer to its ac equivalents of Fig. 5.15, with respect to which we make the following observations:

- Applying $v_{d d}$ to the emitters of the $M_{1}-M_{2}$ pair via $r_{o 7}$ has the same effect as lifting their bases off ground and driving them with a common voltage of $-v_{d d}$ while holding the upper terminal of $r_{o 7}$ at ac ground. We can thus adapt the commonmode gain of Eq. (4.157c) to the present circuit. Ignoring the body effect for simplicity, we have

$$
v_{d s 4}=a_{c m(\mathrm{MOS})}\left(-v_{d d}\right) \cong \frac{v_{d d}}{2 g_{m 4} r_{o 7}}
$$

Applying KCL at node $v_{o}$ gives

$$
\frac{v_{d d}-v_{o}}{r_{o 6}}=g_{m 5} \frac{v_{d d}}{2 g_{m 4} r_{o 7}}+\frac{v_{o}}{r_{o 5}}
$$

image_name:(a)
description:
[
name: M1, type: PMOS, ports: {S: s1s2, D: x1, G: GND}
name: M2, type: PMOS, ports: {S: s1s2, D: d2d4g5, G: GND}
name: M3, type: NMOS, ports: {S: GND, D: x1, G: x1}
name: M4, type: NMOS, ports: {S: GND, D: d2d4g5, G: x1}
name: M5, type: NMOS, ports: {S: GND, D: vo, G: d2d4g5}
name: ro7, type: Resistor, value: ro7, ports: {N1: Vdd, N2: s1s2}
name: ro6, type: Resistor, value: ro6, ports: {N1: vo, N2: VDD}
name: vdd, type: VoltageSource, value: vdd, ports: {Np: Vdd, Nn: GND}
]
extrainfo:The circuit is an AC equivalent model for estimating supply rejection ratios. It includes PMOS and NMOS transistors, resistors, and a voltage source. The PMOS transistors M1 and M2 are connected to the supply voltage Vdd, and M3, M4, and M5 are NMOS transistors forming a differential pair and current mirror. The resistors ro7 and ro6 are used for biasing and load, respectively.
image_name:(b)
description:
[
name: M1, type: PMOS, ports: {S: s1s2, D: x1, G: GND}
name: M2, type: PMOS, ports: {S: s1s2, D: vo, G: GND}
name: M3, type: NMOS, ports: {S: vss, D: x1, G: x1}
name: M4, type: NMOS, ports: {S: x1, D: d2d4g3, G: d2d4g3}
name: M5, type: NMOS, ports: {S: vss, D: vo, G: d2d4g3}
name: r_o7, type: Resistor, value: r_o7, ports: {N1: s1s2, N2: 0}
name: r_o6, type: Resistor, value: r_o6, ports: {N1: vo, N2: GND}
name: v_ss, type: VoltageSource, value: v_ss, ports: {Np: vss, Nn: GND}
]
extrainfo:This circuit is an AC equivalent model for estimating the supply rejection ratios to VDD and VSS. It includes PMOS and NMOS transistors arranged to analyze the effect of supply variations on the output voltage.

FIGURE 5.15 Ac equivalents for the estimation of the supply rejection ratios to (a) $V_{D D}$ and (b) $V_{S S}$.

Since $V_{O V 5}=V_{O V 4}$ and $V_{O V 6}=V_{O V 7}$, it follows that $r_{o 6} / r_{o 7}=2 g_{m 4} / g_{m 5}$, so the above expression gives $v_{o}\left(1 / r_{o 6}+1 / r_{o 5}\right)=v_{d d}\left(1 / r_{o 6}-1 / r_{o 6}\right)=0$. This is possible only if $v_{o}=0$, so

$$
\begin{equation*}
a_{d d}=\frac{v_{o}}{v_{d d}}=\frac{0}{v_{d d}}=0 \mathrm{~V} / \mathrm{V} \tag{5.35a}
\end{equation*}
$$

and

$$
\begin{equation*}
\operatorname{PSRR}_{d d}=\infty \tag{5.35b}
\end{equation*}
$$

Interestingly, the contributions by $v_{d d}$ to $v_{o}$ via $r_{o 6}$ and $r_{o 7}$ cancel each other out. However, because of various approximations made, $\operatorname{PSRR}_{d d}$ will in practice not be infinite, though we expect it to be reasonably high.

- Turning next to Fig. 5.15b, we observe that the balance condition of the input stage is unperturbed by $v_{s s}$, so we have $v_{d s 4}=v_{d s 3}=0 . M_{5}$ 's internal dependent source is now dormant, so we use the voltage divider rule to write

$$
\begin{equation*}
a_{s s}=\frac{v_{o}}{v_{s s}}=\frac{r_{o 6}}{r_{o 5}+r_{o 6}} \tag{5.36a}
\end{equation*}
$$

Substituting into Eq. (5.34), along with $a_{d m}$ as given in Eq. (5.25a), we finally get

$$
\begin{equation*}
\operatorname{PSRR}_{s s}=g_{m 1}\left(r_{o 2} / / r_{o 4}\right) g_{m 5} r_{o 5} \tag{5.36b}
\end{equation*}
$$

EXAMPLE 5.3 Estimate the CMRR and PSRRs of the CMOS op amp of Example 5.2 (ignore the body effect for $M_{1}$ and $M_{2}$ ). Compare with PSpice, and comment.

#### Solution

Using $g_{m 1}=g_{m 3}=\left(2 \times 50 \times 10^{-6} / 0.25\right) \times 1.125=0.45 \mathrm{~mA} / \mathrm{V}$ and $g_{m 5}=(2 \times$ $\left.100 \times 10^{-6} / 0.25\right) \times 1.25=1 \mathrm{~mA} / \mathrm{V}$, we have, by Eqs. (5.32), (5.35b), and (5.36),

$$
\operatorname{CMRR}=\frac{1+0.45 \times 200}{1+200 / 400}[1+2(0.45+0) 200]=10,981=80.8 \mathrm{~dB}
$$

$$
\operatorname{PSRR}_{d d}=\infty \quad \operatorname{PSRR}_{s s}=0.45(400 / / 200) \times 1 \times 100=6,000=75.6 \mathrm{~dB}
$$

To find the CMRR via PSpice, use again the circuit of Fig. 5.14, but with the inputs tied together and driven by a common ac source $v_{i c}$. The small-signal analysis (.TF) gives $a_{c m}=v_{o} / v_{i c}=0.4214 \mathrm{~V} / \mathrm{V}$, so CMRR $=a_{d m} / a_{c m}=4271 / 0.4214=$ $10,135=80.1 \mathrm{~dB}$, in good agreement with the calculated value.

To find $\operatorname{PSRR}_{d d}$, ground the inputs and insert an ac source $v_{d d}$ in series with the $V_{D D}$ source (alternatively, implement $V_{D D}$ with an ac source having a dc component of 2.5 V ). The small-signal analysis (.TF) gives $a_{d d}=v_{o} / v_{d d}=-0.04158 \mathrm{~V}$. Though not zero as predicted by the calculations, $a_{d d}$ is fairly small, giving $\operatorname{PSRR}_{d d}=\left|a_{d m} / a_{d d}\right|=4271 / 0.04158=102,718=100 \mathrm{~dB}$, which, though not infinite, is still fairly high. Likewise, using an ac source $v_{s s}$ in series with $V_{S S}$ gives $a_{s s}=$ $v_{o} / v_{s s}=0.6202 \mathrm{~V} / \mathrm{V}$, so $\operatorname{PSRR}_{s s}=\left|a_{d m} / a_{s s}\right|=4271 / 0.6202=6,886=76.8 \mathrm{~dB}$, in reasonable agreement with the calculated value.

Rewriting Eq. (5.33) in the form

$$
\begin{align*}
v_{o} & =a_{d m}\left(v_{i d}+\frac{a_{c m}}{a_{d m}} v_{i c}+\frac{a_{d d}}{a_{d m}} v_{d d}+\frac{a_{s s}}{a_{d m}} v_{s s}\right) \\
& =a_{d m}\left(v_{i d}+\frac{v_{i c}}{\operatorname{CMRR}}+\frac{v_{d d}}{\operatorname{PSRR}_{d d}}+\frac{v_{s s}}{\operatorname{PSRR}_{s s}}\right) \tag{5.37}
\end{align*}
$$

offers an instructive interpretation for the rejection ratios: (a) the voltages $v_{i c}, v_{d d}$, and $v_{s s}$, reflected to the input, get divided by the corresponding rejection ratios; (b) since the reflected voltages are in series with $v_{i d}$, they act as separate input offset-voltage components. Clearly, the higher a rejection ratio, the smaller the corresponding input offset term.

## 5.3 THE FOLDED-CASCODE CMOS OPERATIONAL AMPLIFIER

The two-stage op amp just studied realizes voltage gain in the form $a=\left(G_{m 1} R_{o 1}\right) \times$ $\left(G_{m 2} R_{o 2}\right)$, that is, as the product of its individual stage gains. Regrouping as $a=$ $G_{m 1}\left(R_{o 1} G_{m 2} R_{o 2}\right)$ suggests an alternative implementation, namely, a single stage ( $\left.G_{m 1}\right)$ but having a much higher output resistance ( $R_{o}=R_{o 1} G_{m 2} R_{o 2}$ ). We start out with an active-loaded differential pair to implement $G_{m 1}$, and then we cascode both the pair and the load to raise the output resistance. To avoid the notorious voltage-swing limitations of straight cascodes we use the folded-cascode scheme introduced at the end of Section 4.9. This results in the popular CMOS op amp alternative of Fig. 5.16, in
image_name:(a)
description:The circuit is a folded-cascode CMOS op amp with a p-channel differential pair M1-M2 cascoded by n-channel M3-M4. It employs a folded-cascode architecture to increase output resistance and avoid voltage-swing limitations. The current source ISS biases the differential pair, while IBIAS provides additional biasing. The capacitor CC is used for compensation.

(a)
image_name:(b)
description:
[
name: Gm(vp-vn), type: VoltageControlledCurrentSource, ports: {Np: VO, Nn: GND}
name: Ro, type: Resistor, value: Ro, ports: {N1: VO, N2: GND}
]
extrainfo:The circuit diagram (b) represents the Norton equivalent of a folded-cascode CMOS op amp. It includes a voltage-controlled current source Gm(vp-vn) and a resistor Ro connected in parallel between the output node VO and ground (GND). The input nodes are labeled vp and vn, and the output node is labeled vo.

(b)

FIGURE 5.16 (a) Simplified diagram of the folded-cascode CMOS op amp and (b) its Norton equivalent.
connection with which we note the following:

- The heart of the circuit is the $p$-channel differential pair $M_{1}-M_{2}$, in turn cascoded by the $n$-channel CG pair $M_{3}-M_{4}$. As we know, in the folded arrangement the CG pair requires separate biasing, a function here provided by the two $I_{B A S}$ current sinks.
- The active load is the cascode current mirror made up of the $M_{5}-M_{6}$ and $M_{7}-M_{8}$ pairs. (The function of capacitor $C_{c}$ is to stabilize the amplifier against possible oscillations in negative-feedback operation, a subject to be addressed in detail in Chapter 7.)
- The dc biasing circuitry comprises the sources $I_{S S}, I_{B A S}$, and $V_{B A A S}$. Should the $M_{1}-M_{2}$ pair be over-driven, one of its FETs would go off. To prevent the corresponding half of the load from also turning off and then require a delay to go back on when the overdrive condition is removed, it is customary to specify $I_{B A S}>I_{S S}$, such as $I_{B A S} \cong 1.25 I_{S S}$. Shown in Fig. 5.17 is a possible realization of the dc biasing circuitry: $M_{9}$ and $M_{10}$ sink the $I_{B A S}$ currents, $M_{11}$ sources the $I_{S S}$ current, and $M_{12}$ through $M_{16}$ provide the proper voltages to bias $M_{11}$ as well as the $M_{3}-M_{4}$ and $M_{9}-M_{10}$ pairs.

We now wish to find the element values $G_{m}$ and $R_{o}$ of the Norton equivalent depicted in Fig. 5.16b. To find $G_{m}$ we need to find $i_{o(\mathrm{sc})}$, a task that we shall carry out using the half-circuit concept of Fig. 5.18. The differential pair responds to an input imbalance $v_{i d}=v_{p}-v_{n}$ with the drain currents

$$
i_{1}=g_{m 1} \frac{v_{i d}}{2} \quad i_{2}=g_{m 2} \frac{v_{i d}}{2}
$$

image_name:FIGURE 5.17 Detailed circuit schematic of the folded-cascode CMOS op amp
description:The circuit is a folded-cascode CMOS operational amplifier. It includes differential pairs, current mirrors, and cascode configurations for improved performance. The design features NMOS and PMOS transistors, with current source biasing and differential input stages. The circuit is powered by VDD and VSS, with output taken from vO.

FIGURE 5.17 Detailed circuit schematic of the folded-cascode CMOS op amp.
image_name:FIGURE 5.18
description:
[
name: M1, type: PMOS, ports: {S: s1s2, D: X1, G: Vid/2}
name: M2, type: PMOS, ports: {S: s1s2, D: X2, G: -Vid/2}
name: M3, type: NMOS, ports: {S: x1, D: X4, G: GND}
name: M4, type: NMOS, ports: {S: X2, D: GND, G: GND}
name: M5, type: PMOS, ports: {S: X3, D: X4, G: X4}
name: M6, type: PMOS, ports: {S: GND, D: X4, G: X3}
name: M7, type: PMOS, ports: {S: GND, D: X3, G: X3}
name: M8, type: PMOS, ports: {S: GND, D: X3, G: X3}
name: r09, type: Resistor, value: r09, ports: {N1: X1, N2: GND}
name: r010, type: Resistor, value: r010, ports: {N1: X2, N2: GND}
name: Vid, type: VoltageSource, value: Vid/2, ports: {Np: Vid/2, Nn: GND}
name: Vid, type: VoltageSource, value: -Vid/2, ports: {Np: -Vid/2, Nn: GND}
]
extrainfo:The circuit is an AC model of a folded-cascode CMOS operational amplifier. It includes differential pairs, current mirrors, and cascode configurations for improved performance. The design features NMOS and PMOS transistors, with current source biasing and differential input stages. The circuit is powered by VDD and GND, with output taken from the short-circuit current i_o(sc).

FIGURE 5.18 Ac model to find the short-circuit output current $i_{o(\mathrm{~s})}$.

Since $g_{m 2}=g_{m 1}$, it follows that $i_{2}=i_{1}$. Once $i_{2}$ reaches $M_{4}$ 's source, it divides between the resistance seen looking into $M_{4}$ 's source and that seen looking into $M_{10}$ 's drain. The former is $R_{s 4}=\left[1 /\left(g_{m 4}+g_{m b 4}\right)\right] / / r_{o 4}$ and the latter is $R_{d 10}=r_{o 10}$. Since $R_{s 4} \ll R_{d 10}$, virtually all of $i_{2}$ will flow into $M_{4}$ and thence to the output ac short, as shown. Similar considerations hold for the current division experienced by $i_{1}$ at $M_{3}$ 's source. Virtually all of $i_{1}$ will come out of $M_{3}$ and will thus be mirrored into the output ac short, as shown. By KCL, $i_{o(\mathrm{sc})}=i_{1}+i_{2}=2\left(g_{m 1} v_{i d} / 2\right)=g_{m 1} v_{i d}$. Consequently,

$$
\begin{equation*}
G_{m}=\frac{i_{o(\mathrm{sc})}}{v_{p}-v_{n}}=g_{m 1} \tag{5.38}
\end{equation*}
$$

To find the small-signal output resistance $R_{o}$, set the input sources to zero, apply a test voltage $v$, find the current $i$ out of the test source, and let $R_{o}=v / i$. The test method is depicted in Fig. 5.19, where we observe that $i$ consists of three components:

- The component $i_{6}=v / R_{d 6}$, where $R_{d 6}$ is the resistance seen looking into $M_{6}$ 's drain. Adapting Eq. (4.41) to the present circuit we have

$$
i_{6}=\frac{v}{r_{o 6}+r_{o 8}+\left(g_{m 6}+g_{m b 6}\right) r_{o 6} r_{o 8}} \cong \frac{v}{\left(g_{m 6}+g_{m b 6}\right) r_{o 6} r_{o 8}}
$$

image_name:FIGURE 5.19
description:
[
name: M1, type: PMOS, ports: {S: S1S2, D: X3, G: GND}
name: M2, type: PMOS, ports: {S: S1S2, D: X4, G: GND}
name: M3, type: NMOS, ports: {S: X3, D: X2, G: GND}
name: M4, type: NMOS, ports: {S: X4, D: V, G: GND}
name: M5, type: PMOS, ports: {S: X1, D: X2, G: X2}
name: M6, type: PMOS, ports: {S: d8s6, D: V, G: X2}
name: M7, type: PMOS, ports: {S: GND, D: X1, G: X1}
name: M8, type: PMOS, ports: {S: GND, D: d8s6, G: X1}
name: ro9, type: Resistor, value: ro9, ports: {N1: X3, N2: GND}
name: ro10, type: Resistor, value: ro10, ports: {N1: X4, N2: GND}
]
extrainfo:The circuit diagram is used to find the output resistance R0 using a test voltage v. The current i is composed of three components: i6, i4, and i2. The circuit utilizes PMOS and NMOS transistors to achieve this measurement. The resistances ro9 and ro10 are used to model the output resistances of the devices.

FIGURE 5.19 Ac model to find the output resistance $R_{0}$.

- The component $i_{4}=v / R_{d 4}$, where $R_{d 4}$ is the resistance seen looking into $M_{4}$ 's drain. Again adapting we get

$$
i_{4}=\frac{v}{r_{o 4}+\left(2 r_{o 2} / / r_{o 10}\right)+\left(g_{m 4}+g_{m b 4}\right) r_{o 4}\left(2 r_{o 2} / / r_{o 10}\right)} \cong \frac{v}{\left(g_{m 4}+g_{m b 4}\right) r_{o 4}\left(2 r_{o 2} / / r_{o 10}\right)}
$$

where $2 r_{o 2}$ is the resistance seen looking into $M_{2}$ 's drain.

- Upon exiting $M_{4}, i_{4}$ divides between $2 r_{o 2}$ and $r_{o 10}$ to give, by the current divider rule,

$$
i_{2}=\frac{r_{o 10}}{2 r_{o 2}+r_{o 10}} i_{4}=\frac{2 r_{o 2} / / r_{o 10}}{2 r_{o 2}} i_{4} \cong \frac{v}{\left(g_{m 4}+g_{m b 4}\right) 2 r_{o 2} r_{o 4}}
$$

This current continues through $M_{1}$ to $M_{3}$ 's source, where it experiences negligible current division to proceed through $M_{3}$ to the mirror, which then replicates it at the test source, as shown.

We now apply KCL to write

$$
i \cong \frac{v}{\left(g_{m 6}+g_{m b 6}\right) r_{o 6} r_{o 8}}+\frac{v}{\left(g_{m 4}+g_{m b 4}\right) r_{o 4}\left(2 r_{o 2} / / r_{o 10}\right)}+\frac{\nu}{\left(g_{m 4}+g_{m b 4}\right) 2 r_{o 2} r_{o 4}}
$$

Combining the last two terms and simplifying, we write

$$
i \cong \frac{v}{\left(g_{m 6}+g_{m b 6}\right) r_{o 6} r_{o 8}}+\frac{v}{\left(g_{m 4}+g_{m b 4}\right) r_{o 4}\left(r_{o 2} / / r_{o 10}\right)}=\frac{v}{R_{o}}
$$

where

$$
\begin{equation*}
R_{o} \cong\left[\left(g_{m 6}+g_{m b 6}\right) r_{o 6} r_{o 8}\right] / /\left[\left(g_{m 4}+g_{m b 4}\right) r_{o 4}\left(r_{o 2} / / r_{o 10}\right)\right] \tag{5.39}
\end{equation*}
$$

Finally, the unloaded voltage gain is

$$
\begin{equation*}
a=\frac{v_{o}}{v_{p}-v_{n}}=g_{m 1} R_{o} \tag{5.40}
\end{equation*}
$$

### Input Voltage Range and Output Voltage Swing

In order for the circuit to function properly, all FETs must operate in saturation or at most at its edge (EOS). The permissible range of values for the common-mode input voltage $v_{I C}$ defines the input voltage range (IVR). Using inspection and KVL in the circuit of Fig. 5.17 we readily find

$$
\begin{equation*}
v_{I C(\max )}=V_{D D}-V_{O V 11}-V_{O V 1}-\left|V_{t 1}\right| \quad v_{I C(\min )}=V_{S S}+V_{O V 9}-\left|V_{t 1}\right| \tag{5.41}
\end{equation*}
$$

Likewise, the limits of the output voltage swing (OVS) are

$$
\begin{equation*}
v_{O(\max )}=V_{D D}-\left|V_{t 8}\right|-V_{O V 8}-V_{O V 6} \quad v_{O(\min )}=V_{S S}+V_{O V 10}+V_{O V 4} \tag{5.42}
\end{equation*}
$$

We can eliminate the $\left|V_{t 8}\right|$ term from $v_{O(\max )}$ by using a wide-swing cascode mirror such as the $p$-channel version of the Sooch mirror discussed in Section 4.8.
(a) Suppose the folded-cascode op amp of Fig. 5.17 is fabricated in a process with $k_{n}^{\prime}=2.5 k_{p}^{\prime}=100 \mu \mathrm{~A} / \mathrm{V}^{2}, V_{t n}=-V_{t p}=0.75 \mathrm{~V}, \lambda_{n}^{\prime}=0.1 \mu \mathrm{~m} / \mathrm{V}$ and $\lambda_{p}^{\prime}=$ $0.05 \mu \mathrm{~m} / \mathrm{V}$. Moreover, all FETs are fabricated with $L=1 \mu \mathrm{~m}$ and are designed to operate with $V_{O V}=0.25 \mathrm{~V}$. If the circuit is powered from $\pm 2.5-\mathrm{V}$ supplies and uses $I_{R E F}=100 \mu \mathrm{~A}$, specify suitable values for $W_{1}$ through $W_{16}$ for $I_{S S}=100 \mu \mathrm{~A}$ and $I_{B A S}=125 \mu \mathrm{~A}$. (For simplicity assume $\lambda=0$ and ignore the body effect in the course of your dc calculations.)
(b) Assuming $\chi=0.1$ throughout, find $R_{o}, a$, the IVR, and the OVS.

#### Solution

(a) Each FET (except for $M_{13}$ ) must satisfy the saturation-region condition

$$
I_{D}=\frac{k^{\prime}}{2} \frac{W}{1 \mu \mathrm{~m}} 0.25^{2}
$$

which allows us to perform the following calculations:

- Letting $I_{D}=100 \mu \mathrm{~A}$ and $k^{\prime}=40 \mu \mathrm{~A} / \mathrm{V}^{2}$ in the above expression gives $W_{11}=W_{12}=80 \mu \mathrm{~m}$.
- Since $M_{1}$ and $M_{2}$ draw half as much dc current as $M_{11}$ we have $W_{1}=W_{2}=$ $W_{11} / 2=80 / 2=40 \mu \mathrm{~m}$.
- Letting $I_{D}=100 \mu \mathrm{~A}$ and $k^{\prime}=100 \mu \mathrm{~A} / \mathrm{V}^{2}$ gives $W_{14}=W_{15}=W_{16}=$ $32 \mu \mathrm{~m}$. Also, $W_{13}=32 / 4=8 \mu \mathrm{~m}$.
- Since $M_{9}$ and $M_{10}$ draw $125 \mu \mathrm{~A}(=1.25 \times 100 \mu \mathrm{~A})$, they must be 1.25 times as wide as $M_{15}$, so $W_{9}=W_{10}=1.25 W_{15}=1.25 \times 32=40 \mu \mathrm{~m}$.
- At dc balance $M_{3}$ and $M_{4}$ draw $125-50=75 \mu \mathrm{~A}$ each, or $3 / 4 I_{D 15}$. Consequently, $W_{3}=W_{4}=3 / 4 W_{15}=3 / 432=24 \mu \mathrm{~m}$.
- $M_{5}$ through $M_{8}$ draw $75 \mu \mathrm{~A}$, or $3 / 4 I_{D 11}$, so $W_{5}=W_{6}=W_{7}=W_{8}=3 / 4 W_{11}=$ $3 / 480=60 \mu \mathrm{~m}$. The widths of the signal-processing FETs are

$$
\begin{array}{ll}
W_{1}=W_{2}=W_{9}=W_{10}=40 \mu \mathrm{~m} & W_{3}=W_{4}=24 \mu \mathrm{~m} \\
W_{5}=W_{6}=W_{7}=W_{8}=60 \mu \mathrm{~m} & W_{11}=80 \mu \mathrm{~m}
\end{array}
$$

(b) Proceeding as usual, we find

$$
\begin{aligned}
& g_{m 1}=2 \frac{I_{D 1}}{V_{O V 1}}=2 \frac{50 \times 10^{-6}}{0.25}=0.4 \mathrm{~mA} / \mathrm{V} \\
& g_{m 4}=g_{m 6}=2 \frac{75 \times 10^{-6}}{0.25}=0.6 \mathrm{~mA} / \mathrm{V} \\
& r_{o 2}=\frac{1}{\lambda_{2} I_{D 2}}=\frac{1}{0.05 \times 50 \times 10^{-6}}=400 \mathrm{k} \Omega \\
& r_{o 4}=\frac{1}{0.1 \times 75 \times 10^{-6}}=133 \mathrm{k} \Omega \\
& r_{o 6}=r_{o 8}=\frac{1}{0.05 \times 75 \times 10^{-6}}=267 \mathrm{k} \Omega \\
& r_{o 10}=\frac{1}{0.1 \times 125 \times 10^{-6}}=80 \mathrm{k} \Omega
\end{aligned}
$$

Substituting into Eqs. (5.32) and (5.33) we get

$$
\begin{aligned}
R_{o} & \cong[0.6(1+0.1) 267 \times 267] /[0.6(1+0.1) 133(400 / / 80)] \\
& \cong(49,050 / / 5867) \mathrm{k} \Omega=5.22 \mathrm{M} \Omega \\
a & \cong 0.4 \times 10^{-3} \times 5.22 \times 10^{6}=2,088 \mathrm{~V} / \mathrm{V}
\end{aligned}
$$

Finally, use Eq. (5.41) and (5.42) to find

$$
\begin{array}{ll}
v_{I C(\max )}=1.25 \mathrm{~V} & v_{I C(\min )}=-3.0 \mathrm{~V} \\
v_{O(\max )}=1.25 \mathrm{~V} & v_{O(\min )}=-2 \mathrm{~V}
\end{array}
$$

The two-stage and folded-cascode topologies, along with variants thereof, are in widespread use today. As mentioned, both topologies achieve an overall gain on the order of $\left(g_{m} r_{o}\right)^{2}$, though by different means. Yet the folded cascode requires more transistors and its OVS is more limited, so one may wonder what its advantages are compared to the two-stage version. To answer this question we need to study stability and frequency compensation, in Chapter 7. There we shall see that in negativefeedback operation, which is the preferred mode of operation of op amps, the folded cascode is much easier to stabilize against unwanted oscillations. This advantage alone warrants the additional transistor count!
