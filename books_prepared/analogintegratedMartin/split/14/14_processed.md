# 14  Switched-Capacitor Circuits

Perhaps the most popular approach for realizing analog signal processing in MOS (or BiCMOS) integrated circuits is through the use of switched-capacitor circuits [Poschenrieder, 1966; Fried, 1972; Caves, 1977; Hosticka, 1977; Young, 1977]. A switched-capacitor circuit operates as a discrete-time signal processor (although without the use of A/D or D/A converters). As a result, these circuits are most easily analyzed with the use of z-transform techniques and typically require anti-aliasing and smoothing filters when combined with continuoustime circuits.

As a filtering technique, switched-capacitor circuits are popular due to their accurate frequency response as well as good linearity and dynamic range. Accurate discrete-time frequency responses are obtained since filter coefficients are determined by capacitance ratios which can be set quite precisely in an integrated circuit (on the order of 0.1 percent). Such an accuracy is orders of magnitude better than that which occurs for integrated RC time constants (which can vary by as much as 20 percent). Once the coefficients of a switched-capacitor discretetime filter are accurately determined, its overall frequency response remains a function of the clock (or sampling) frequency. Fortunately, clock frequencies can also be set very precisely through the use of a crystal oscillator.

In addition to creating filtering functions, switched-capacitor circuit techniques can be used to realize a variety of other signal-processing blocks such as gain-stages, voltage-controlled oscillators, and modulators. This chapter will introduce the basic principles of switched-capacitor filters as well as some other nonfiltering functions realized using switched-capacitor circuits.

## 14.1 BASIC BUILDING BLOCKS

A switched-capacitor circuit is realized with the use of some basic building blocks such as opamps, capacitors, switches, and nonoverlapping clocks. Brief descriptions of each of these blocks and their important nonidealities with respect to switched-capacitor circuits are given in this section.

### 14.1.1 Opamps

The basic principles of switched-capacitor circuits can be well understood assuming ideal opamps. However, some important opamp nonidealities in practical switchedcapacitor circuits are dc gain, unity-gain frequency and phase-margin, slew-rate, and dc offset. Opamp input impedance is generally capacitive assuming MOSFET input stages are used. ${ }^{1}$

The dc gain of opamps in a MOS technology intended for switched-capacitor circuits is typically on the order of 40 to 80 dB . Low dc gains affect the coefficient

Key Point: Opamp nonidealities such as dc gain, unity-gain frequency and phase-margin, slew-rate, and dc offset impact switched-capacitor circuit performance.
accuracy of the discrete-time transfer function of a switched-capacitor filter.

[^1]The unity-gain frequency and phase margin of an opamp gives an indication of its small signal settling behavior. A general rule of thumb is that the clock frequency of a switched-capacitor circuit should be at least five times lower than the unity-gain frequency of the opamp, assuming little slew-rate behavior occurs and the phase margin is greater than 70 degrees. Modern SC circuits are often realized using high-frequency single-stage opamps having very large output impedances (up to $100 \mathrm{k} \Omega$ or much larger). Since the loads of these opamps are purely capacitive (never resistive), their dc gains remain high despite the lack of an output buffer stage. It should be noted here that their unity-gain frequency and phase margin are determined by the load capacitance, which also serves as the compensation capacitor. Thus, in these single-stage opamps, doubling the load capacitance would halve the unity-gain frequency and improve the phase margin.

The finite slew rate of an opamp can limit the upper clock rate in a switched-capacitor circuit as these circuits rely on charge being quickly transferred from one capacitor to another. Thus, at the instance of charge transfer, it is not uncommon for opamps to slew-rate limit.

A nonzero dc offset can result in a high output dc offset for the circuit depending on the topology chosen. Fortunately, a technique known as correlated double sampling can significantly reduce this output offset and at the same time reduce low-frequency opamp input noise (i.e., $1 / \mathrm{f}$ noise).

### 14.1.2 Capacitors

A highly linear capacitance in an integrated circuit is typically constructed from two closely-spaced conducting layers, as shown in Fig. 14.1(a). ${ }^{2}$ The desired capacitance, C, is formed as the intersection of area between the two conductive layers, layer 1 and layer 2. However, since the substrate below layer 1 is an ac ground (the substrate is connected to one of the power supplies or analog ground), there also exists a substantial parasitic capacitance, $\mathrm{C}_{\mathrm{pl}}$, which may be as large as 20 percent of $\mathrm{C}_{1}$. This large parasitic capacitance, $\mathrm{C}_{\mathrm{p} 1}$, is known as the bottom plate capacitance. A top plate capacitance, $\mathrm{C}_{\mathrm{p} 2}$, also exists due primarily to the interconnect capacitance, but it is typically much smaller (generally less than 5 percent of C ). In summary, the equivalent model for a single integrated capacitor is three capacitors, as shown in Fig. 14.1(b), where the bottom plate is often explicitly shown to indicate that a larger parasitic capacitance occurs on that node.

### 14.1.3 Switches

The requirements for switches used in switched-capacitor circuits are that they have a very high off resistance (so little charge leakage occurs), a relatively low on resistance (so that the circuit can settle in less than half the clock
image_name:(a)
description:The image consists of two parts labeled as (a) and (b), representing the physical construction and circuit model of an integrated circuit capacitor used in switched-capacitor circuits.

1. **Identification of Components and Structure:**
- **Part (a): Physical Construction**
- The diagram shows a cross-sectional view of an integrated capacitor. It consists of two primary layers labeled as 'layer 1' and 'layer 2,' which are separated by a dielectric material. These layers form the plates of the capacitor.
- The capacitor is built on a silicon (Si) substrate, which provides the foundation for the structure.
- The main capacitance is labeled as 'C,' indicating the primary capacitance between the two layers.
- Two parasitic capacitances are shown: 'C_p1' and 'C_p2.' These are connected from the layers to the ground, with 'C_p1' being significantly larger than 'C_p2,' as indicated by the notation 'C_p1 >> C_p2.'

2. **Connections and Interactions:**
- The main capacitor 'C' is formed between layer 1 and layer 2. The parasitic capacitors 'C_p1' and 'C_p2' are connected to the ground, representing additional unwanted capacitance due to the physical construction and proximity to the substrate.
- The diagram suggests that the parasitic capacitance 'C_p1' is more significant, likely due to its closer proximity to the substrate or a larger surface area.

3. **Labels, Annotations, and Key Features:**
- The labels 'C,' 'C_p1,' and 'C_p2' clearly identify the different capacitances in the structure.
- The silicon substrate is explicitly labeled as 'Si substrate,' indicating the material used for the base of the integrated circuit.

4. **Part (b): Circuit Model**
- This part shows the equivalent circuit model of the physical construction in (a).
- The main capacitor 'C' is shown in series with two parasitic capacitors 'C_p1' and 'C_p2,' each connected to the ground.
- The circuit model provides a simplified representation of the physical structure, showing how the main and parasitic capacitances interact within the circuit.
image_name:(b)
description:
[
name: Cp1, type: Capacitor, value: Cp1, ports: {Np: Node1, Nn: GND}
name: C, type: Capacitor, value: C, ports: {Np: Node1, Nn: Node2}
name: Cp2, type: Capacitor, value: Cp2, ports: {Np: Node2, Nn: GND}
]
extrainfo:The circuit diagram represents an equivalent model of an integrated capacitor, consisting of three capacitors: Cp1, C, and Cp2, where Cp1 and Cp2 are parasitic capacitances to ground.

Fig. 14.1 An integrated circuit capacitor for switched-capacitor circuits: (a) physical construction; (b) circuit model.
image_name:(a)
description:The diagram (a) shows a switch symbol used in electronic circuits, representing a basic connection between two nodes V1 and V2 controlled by a signal φ. This is typically used in switched-capacitor circuits to control the flow of charge between nodes.
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: V1, D: V2, G: phi}
]
extrainfo:The circuit diagram (b) represents a transmission gate using an NMOS and a PMOS transistor. The NMOS transistor M1 is connected with its source at V1, drain at V2, and gate at phi. The PMOS transistor M1 is connected with its source at phi, drain at V2, and gate at V1.
image_name:(c)
description:
[
name: M1, type: NMOS, ports: {S: V1, D: V2, G: phi_bar}
name: Inv1, type: Inverter, ports: {In: phi, Out: phi_bar}
]
extrainfo:The circuit diagram (c) represents an NMOS transistor M1 controlled by an inverted clock signal. The inverter generates the phi_bar signal from the input phi, controlling the gate of M1. The source of M1 is connected to V1, and the drain is connected to V2.
image_name:(d)
description:
[
name: M1, type: PMOS, ports: {S: V1, D: V2, G: phi}
name: M2, type: NMOS, ports: {S: V1, D: V2, G: phi_bar'}
]
extrainfo:The circuit diagram (d) represents a transmission gate using a PMOS (M1) and an NMOS (M2) transistor. The PMOS is controlled by the signal ϕ, and the NMOS is controlled by the inverted signal ϕ̅. The transmission gate allows signals to pass from V1 to V2 when ϕ is high.

Fig. 14.2 Switch symbol and some transistor circuits: (a) symbol, (b) n-channel switch, (c) p channe switch, (d) transmission gate.
period), and introduce no offset voltage when turned on (as does a bipolar switch whose on voltage equals $\mathrm{V}_{\mathrm{CE}(\mathrm{sat})}$ ). The use of MOSFET transistors as switches satisfies these requirements, as MOSFET switches can have off resistances up to the $\mathrm{G} \Omega$ range, have no offset on voltages, and have on resistances of $5 \mathrm{k} \Omega$ or much less depending on transistor sizing.

The symbol for a switch and some MOSFET circuits that realize a switch are shown in Fig. 14.2. Here, the signal $\phi$ is one of two logic levels typically corresponding to the maximum and minimum power supply levels. As a convention, when the clock signal $\phi$ is high, the switch is assumed to be on (i.e., shorted). Although a switch can be implemented using a single transistor, as shown in Fig. 14.2(b) and Fig. 14.2(c), the signal range of the switch is reduced. For example, consider the ideal n-channel transistor switch shown in Fig. 14.2(b) being used in a circuit having power supplies of 0 to 1.8 V and a threshold voltage of $\mathrm{V}_{\mathrm{tn}}=0.45 \mathrm{~V}$. The switch can always be turned off irrespective of the input voltage by putting 0 V on its gate. However, when the switch is on, its gate voltage will be $\mathrm{V}_{\mathrm{DD}}=1.8 \mathrm{~V}$; in this case, the switch can only equalize the two voltages if $\mathrm{V}_{1}$ and/or $\mathrm{V}_{2}$ are lower than $\mathrm{V}_{\mathrm{DD}}-\mathrm{V}_{\mathrm{tn}}$ or around 1.3 V taking the body effect into account. Thus, the signal range for this switch is limited from 0 to 1.3 V . A similar argument can be made for the p-channel switch shown in Fig. 14.2(c) except that its signal range would be limited from 0.5 to 1.8 V . While this signal range is acceptable in some situations, the full signal range of 0 to 1.8 V can be achieved using two transistors in parallel, as shown in Fig. 14.2(d). This combination is commonly called either a CMOS switch (as opposed to the NMOS switch of Fig. 14.2(a)) or a CMOS transmission gate.

Some of the important nonideal switch effects in switched-capacitor circuits are the nonlinear junction capacitance on each side of the switch, channel charge injection, and capacitive coupling from the logic signal, $\phi$, to each side of the switch. Nonlinear capacitance effects are alleviated through the use of parasitic insensitive structures, as discussed in Section 14.2, while channel charge injection is reduced by careful switch timing, as seen in Section 14.6.

### 14.1.4 Nonoverlapping Clocks

At least one pair of nonoverlapping clocks is essential in switched-capacitor circuits. These clocks determine when charge transfers occur and they must be nonoverlapping in order to guarantee charge is not inadvertently lost. As seen in Fig. 14.3(a), the term nonoverlapping clocks refers to two logic signals running at the same frequency and arranged in such a way that at no time are both signals high. Note that the time axis in Fig. 14.3(a) has been normalized with respect to the clock period, T. Such a normalization illustrates the location of the sample numbers of the discrete-time signals that occur in switched-capacitor filters. As a convention, we denote
image_name:(a)
description:The graph labeled (a) in Fig. 14.3 illustrates the concept of nonoverlapping clock signals, specifically depicting two periodic waveforms, \( \phi_1 \) and \( \phi_2 \), which are used in digital circuits to control the timing of operations. The graph is a time-domain waveform plot.

1. **Type of Graph and Function:**
- The graph is a time-domain waveform plot displaying two digital clock signals, \( \phi_1 \) and \( \phi_2 \), over time.

2. **Axes Labels and Units:**
- The horizontal axis is labeled \( t/T \), representing normalized time with respect to the clock period \( T \). This axis is dimensionless but indicates time intervals relative to the clock period.
- The vertical axis is labeled with voltage levels \( V_{on} \) and \( V_{off} \), indicating the high and low states of the digital signals.

3. **Overall Behavior and Trends:**
- Both \( \phi_1 \) and \( \phi_2 \) are square waves oscillating between \( V_{on} \) and \( V_{off} \).
- \( \phi_1 \) and \( \phi_2 \) are arranged such that they are never high at the same time, ensuring nonoverlapping behavior.
- The signals are periodic, repeating every clock period \( T \).

4. **Key Features and Technical Details:**
- \( \phi_1 \) has transitions at integer multiples of the period, specifically at \( n-2, n-1, n, n+1 \), where \( n \) is an integer.
- \( \phi_2 \) is offset by half a sample period, with transitions occurring at \( n-3/2, n-1/2, n+1/2 \), etc.
- This offset ensures that there is a gap between the high phases of \( \phi_1 \) and \( \phi_2 \), preventing both signals from being high simultaneously.

5. **Annotations and Specific Data Points:**
- The frequency of the clock signals is denoted as \( f_s = 1/T \), indicating the sampling frequency.
- The diagram visually demonstrates the nonoverlapping nature of the clock signals, which is critical in applications like switched-capacitor filters to prevent charge sharing between phases.

The graph effectively illustrates the timing and sequence of the nonoverlapping clock signals, emphasizing their synchronized yet non-simultaneous high states.
image_name:(b)
description:The circuit implements nonoverlapping clock signals ϕ1 and ϕ2 from a single clock input ϕ. The delays ensure that ϕ1 and ϕ2 do not overlap.

Fig. 14.3 Nonoverlapping clocks. (a) Clock signals, $\phi_{1}$ and $\phi_{2}$. (b) A possible circuit implementation of nonoverlapping clocks from a single clock.
the sampling numbers to be integer values (i.e., $(n-1),(n),(n+1)$, etc.) just before the end of clock phase $\phi_{1}$, while the end of clock phase $\phi_{2}$ is deemed to be $1 / 2$ sample off the integer values as shown (i.e., $(n-3 / 2),(n-1 / 2)$, etc.). However, it should be noted that it is not important that the falling clock edge of $\phi_{2}$ occur precisely one-half a clock period earlier than the falling edge of $\phi_{1}$. In general, the locations of the clock edges of $\phi_{1}$ and $\phi_{2}$ need only be moderately controlled to allow for complete charge settling (assuming separate low-jitter sample and holds are used at the input and output of the overall circuit).

One simple method for generating nonoverlapping clocks is shown in Fig. 14.3(b) [Martin, 1981]. Here, delay blocks are used to ensure that the clocks remain nonoverlapping. These delays could be implemented as a cascade of an even number of inverters or perhaps an RC network.

## 14.2 BASIC OPERATION AND ANALYSIS

### 14.2.1 Resistor Equivalence of a Switched Capacitor

Consider the switched-capacitor circuit shown in Fig. 14.4(a), where $\mathrm{V}_{1}$ and $\mathrm{V}_{2}$ are two dc voltage sources. To analyze this circuit's behavior, we analyze the circuit from a charge perspective. Recall that the charge on a capacitor, $\mathrm{Q}_{\mathrm{x}}$, is equal to the capacitance value, $\mathrm{C}_{\mathrm{x}}$, times the voltage across it, $\mathrm{V}_{\mathrm{x}}$. In mathematical terms, we have

$$
\begin{equation*}
Q_{x}=C_{x} V_{x} \tag{14.1}
\end{equation*}
$$

image_name:(a)
description:The switched-capacitor circuit alternates the connection of C1 between V1 and V2 using non-overlapping clock signals ϕ1 and ϕ2. This results in a change in charge ΔQ = C1(V1 - V2) every clock period.

image_name:(b)
description:
[
name: Req, type: Resistor, value: Req, ports: {N1: V1, N2: V2}
]
extrainfo:The resistor equivalent of the switched-capacitor circuit is shown. The equivalent resistance is given by Req = T/C1, where T is the clock period and C1 is the capacitance.

Fig. 14.4 Resistor equivalence of a switched capacitor. (a) Switched-capacitor circuit, and (b) resistor equivalent.

Now, since $\phi_{1}$ and $\phi_{2}$ are assumed to be a pair of nonoverlapping clocks, $\mathrm{C}_{1}$ is charged to $\mathrm{V}_{1}$ and then $\mathrm{V}_{2}$ during each clock period. Therefore, the change in charge (in coulombs) over one clock period, $\Delta \mathbf{Q}_{1}$, that is transferred from node $V_{1}$ into node $V_{2}$ is given by

$$
\begin{equation*}
\Delta Q_{1}=C_{1}\left(V_{1}-V_{2}\right) \tag{14.2}
\end{equation*}
$$

Since this charge transfer is repeated every clock period, we can find the equivalent average current due to this charge transfer by dividing by the clock period. In other words, the average current, $\mathrm{I}_{\mathrm{avg}}$ (in amps), is equal to the average number of coulombs/second and is given by

$$
\begin{equation*}
\mathrm{I}_{\mathrm{avg}}=\frac{\mathrm{C}_{1}\left(\mathrm{~V}_{1}-\mathrm{V}_{2}\right)}{\mathrm{T}} \tag{14.3}
\end{equation*}
$$

where $T$ is the clock period (i.e., the sampling frequency $f_{s}=1 / T$ ). Relating (14.3) to an equivalent resistor circuit shown in Fig. 14.4(b) where

$$
\begin{equation*}
I_{e q}=\frac{V_{1}-V_{2}}{R_{e q}} \tag{14.4}
\end{equation*}
$$

we see that the average current through the switched-capacitor circuit of Fig. 14.4(a) will equal that for the resistor circuit of Fig. 14.4(b) if

$$
\begin{equation*}
R_{e q}=\frac{T}{C_{1}}=\frac{1}{C_{1} f_{s}} \tag{14.5}
\end{equation*}
$$

This relation is intuitively satisfying because as the clock frequency is increased, the same charge is transferred each period but at a faster rate, so the average current is higher. If $C_{1}$ is increased, a larger amount of charge is transferred each period, which would also increase the average current. In addition, increasing the average current is equivalent to decreasing the equivalent resistance seen between the two voltage nodes, and therefore the equivalent resistance is inversely related to the capacitance and clock frequency.

Finally, it should be noted that this resistor approximation assumes that the charge transferred per clock cycle is constant over many cycles allowing one to arrive at an average current flow. Hence, it is mainly useful for looking at the lowfrequency behavior of a switched-capacitor circuit, when voltages are changing very slowing compared to the clock frequency. For moderate input frequencies (in relation to the sampling frequency), an accurate discrete-time analysis is required, as discussed in the next subsection. Discrete-time analysis can be used in switched-capacitor circuits because the charge transfers are dependent on values of node voltages at particular instances in time and are ideally independent of transients during nonsampled times.

Key Point: When signal voltages change very slowly compared with the clock frequency, a switchedcapacitor gives rise to an average current inversely proportional to the voltage across it, behaviorally equivalent to a resistor.

Key Point: When signal voltages change appreciably from one clock cycle to the next, a discrete-time analysis is needed to accurately predict the input-output behavior of switched-capacitor circuits.

#### EXAMPLE 14.1

What is the equivalent resistance of a 5 pF capacitance sampled at a clock frequency of 100 kHz ?

#### Solution

Using (14.5), we have

$$
\mathrm{R}_{\mathrm{eq}}=\frac{1}{\left(5 \times 10^{-12}\right)\left(100 \times 10^{3}\right)}=2 \mathrm{M} \Omega
$$

What is interesting here is that a very large impedance of $2 \mathrm{M} \Omega$ can be realized on an integrated circuit through the use of two transistors, a clock, and a relatively small capacitance. Such a large impedance typically requires a large amount of CMOS silicon area if it is realized as a resistor without any special processing fabrication steps.

### 14.2.2 Parasitic-Sensitive Integrator

An example of one of the first switched-capacitor discrete-time integrators [Hosticka, 1977] is shown in Fig. 14.5. Here, an extra switch is shown near the output voltage, $\mathrm{v}_{\mathrm{co}}(\mathrm{t})$, to indicate that the output signal is valid at the end of $\phi_{1}$ in keeping with the sampling-time convention shown in Fig. 14.3(a). In other words, any circuit that uses the output of this discrete-time integrator should sample $\mathrm{v}_{\mathrm{co}}(\mathrm{t})$ on $\phi_{1}$. Note however that no assumptions are made about when $\mathrm{v}_{\mathrm{ci}}(\mathrm{t})$ changes its value (it could be either $\phi_{1}$ or $\phi_{2}$ ); it is not important because $\mathrm{v}_{\mathrm{ci}}(\mathrm{t})$ is sampled at the end of $\phi_{1}$ in the circuit shown.

Key Point: Each clock cycle, a switched-capacitor integrator samples a quantity of charge proportional to an inputvoltage and the sampling capacitance, then delivers it to a second integrating capacitor.

To analyze this circuit, we again look at the charge behavior and note that a virtual ground appears at the opamp's negative input. Assuming an initial integrator output voltage of $\mathrm{v}_{\mathrm{co}}(\mathrm{nT}-\mathrm{T})$ implies that the charge on $\mathrm{C}_{2}$ is equal to $\mathrm{C}_{2} \mathrm{v}_{\mathrm{co}}(n T-T)$ at time $(n T-T)$. Now also at time $(n T-T), \phi_{1}$ is just turning off (and $\phi_{2}$ is off) so the input signal $\mathrm{v}_{\mathrm{ci}}(\mathrm{t}$ ) is sampled, resulting in the charge on $\mathrm{C}_{1}$ being equal to $\mathrm{C}_{1} \mathrm{v}_{\mathrm{ci}}(\mathrm{nT}-\mathrm{T})$, as shown in Fig. 14.6(a). When $\phi_{2}$ goes high, its switch forces $C_{1}$ to discharge since it places a virtual ground on the top plate of $\mathrm{C}_{1}$, as shown in Fig. 14.6(b). However, this discharging current must pass through $\mathrm{C}_{2}$ and hence the charge on $\mathrm{C}_{1}$ is added to the charge already present on $\mathrm{C}_{2}$. Note that a positive
image_name:Fig. 14.5
description:
[
name: M1, type: Switch, ports: {N1: Vci(t), N2: Vcx(t)}
name: M2, type: Switch, ports: {N1: Vcx(t), N2: InN(A1)}
name: C1, type: Capacitor, value: C1, ports: {Np: Vcx(t), Nn: GND}
name: C2, type: Capacitor, value: C2, ports: {Np: Vco(t), Nn: InN(A1)}
name: A1, type: OpAmp, value: A1, ports: {InP: GND, InN: InN(A1), OutP: Vco(t)}
]
extrainfo:The circuit is a discrete-time integrator that is sensitive to parasitic capacitances. It operates over two clock phases, phi1 and phi2, where M1 and M2 act as switches controlled by these clock phases. The input voltage Vci is integrated over time to produce the output voltage Vco. The integrator is inverting, meaning a positive input results in a negative output voltage.
Fig. 14.5 A discrete-time integrator. This structure is sensitive to parasitic capacitances (not shown).
image_name:(a)
description:
[
name: C1, type: Capacitor, value: C1, ports: {Np: Vci(nT-T), Nn: GND}
name: C2, type: Capacitor, value: C2, ports: {Np: InN(A1), Nn: Vco(nT-T)}
name: A1, type: OpAmp, value: A1, ports: {InP: GND, InN: InN(A1), OutP: Vco(nT-T)}
]
extrainfo:The circuit is a parasitic-sensitive discrete-time integrator that operates in two phases (phi1 and phi2). During phi1, M1 is on, charging C1. During phi2, M2 is on, transferring the charge from C1 to C2, which integrates the input voltage Vci to produce the output voltage Vco. It is an inverting integrator, resulting in a negative output voltage.
image_name:(b)
description:
[
name: C1, type: Capacitor, value: C1, ports: {Np: InN(A1), Nn: GND}
name: C2, type: Capacitor, value: C2, ports: {Np: Vco(nT-T/2), Nn: InN(A1)}
name: A1, type: OpAmp, value: A1, ports: {InP: GND, InN: InN(A1), OutP: Vco(nT-T/2)}
]
extrainfo:The circuit is a parasitic-sensitive discrete-time integrator operating in two phases (phi1 and phi2). During phi1, M1 is on, charging C1. During phi2, M2 is on, transferring the charge from C1 to C2, integrating the input voltage Vci to produce the output voltage Vco. The integrator is inverting, resulting in a negative output voltage.

Fig. 14.6 The parasitic-sensitive integrator circuit for the two clock phases: (a) $\phi_{1}$ (b) $\phi_{2}$
input voltage will result in a negative voltage across $\mathrm{C}_{2}$ and therefore a negative output voltage; thus, the integrator is an inverting integrator. At the end of $\phi_{2}$ (once things have settled out), we can write the charge equation,

$$
\begin{equation*}
\mathrm{C}_{2} \mathrm{v}_{\mathrm{co}}(\mathrm{nT}-\mathrm{T} / 2)=\mathrm{C}_{2} \mathrm{v}_{\mathrm{co}}(\mathrm{nT}-\mathrm{T})-\mathrm{C}_{1} \mathrm{v}_{\mathrm{ci}}(\mathrm{nT}-\mathrm{T}) \tag{14.6}
\end{equation*}
$$

The negative sign in (14.6) reflects the fact that the integrator is an inverting integrator.
Although (14.6) is correct, we would like to find the charge on $\mathrm{C}_{2}$ at the end of $\phi_{1}$ (or equivalently, nT ) as indicated by the switch shown near $v_{\mathrm{co}}(\mathrm{t})$ in Fig. 14.5. To find this charge, we note that once $\phi_{2}$ turns off, the charge on $\mathrm{C}_{2}$ will remain the same during the next $\phi_{1}$, until $\phi_{2}$ turns on again in its next cycle. Therefore, the charge on $C_{2}$ at time $(n T)$ at the end of the next $\phi_{1}$ is equal to that at time ( $n T-T / 2$ ), or mathematically,

$$
\begin{equation*}
\mathrm{C}_{2} \mathrm{v}_{\mathrm{co}}(\mathrm{nT})=\mathrm{C}_{2} \mathrm{v}_{\mathrm{co}}(\mathrm{nT}-\mathrm{T} / 2) \tag{14.7}
\end{equation*}
$$

and we can combine (14.6) and (14.7) to write

$$
\begin{equation*}
\mathrm{C}_{2} \mathrm{v}_{\mathrm{co}}(\mathrm{nT})=\mathrm{C}_{2} \mathrm{v}_{\mathrm{co}}(\mathrm{nT}-\mathrm{T})-\mathrm{C}_{1} \mathrm{v}_{\mathrm{ci}}(\mathrm{nT}-\mathrm{T}) \tag{14.8}
\end{equation*}
$$

Dividing by $C_{2}$ and using the discrete-time variables $v_{i}(n)=v_{\mathrm{ci}}(n T)$ and $v_{0}(n)=v_{c o}(n T)$, we have the following discrete-time relationship for the circuit of Fig. 14.5:

$$
\begin{equation*}
v_{0}(n)=v_{0}(n-1)-\frac{C_{1}}{C_{2}} v_{i}(n-1) \tag{14.9}
\end{equation*}
$$

Taking the $\mathbf{z}$-transform of (14.9), we also have

$$
\begin{equation*}
V_{0}(z)=z^{-1} V_{0}(z)-\frac{C_{1}}{C_{2}} z^{-1} V_{i}(z) \tag{14.10}
\end{equation*}
$$

from which we can finally find the transfer function, $H(z)$, to be given by

$$
\begin{equation*}
H(z) \equiv \frac{V_{0}(z)}{V_{i}(z)}=-\left(\frac{C_{1}}{C_{2}}\right) \frac{z^{-1}}{1-z^{-1}} \tag{14.11}
\end{equation*}
$$

Note that this transfer function realizes its gain coefficient as a ratio of two capacitances, and thus the transfer function can be accurately defined in an integrated circuit. Often, the transfer function would be rewritten to eliminate terms of $z$ having negative powers to give

$$
\begin{equation*}
H(z) \equiv \frac{V_{0}(z)}{V_{i}(z)}=-\left(\frac{C_{1}}{C_{2}}\right) \frac{1}{z-1} \tag{14.12}
\end{equation*}
$$

Some typical voltage waveforms for this discrete-time integrator are shown in Fig. 14.7. Note here that the discrete-time equation derived only represents the relationship of the voltage signals $\mathrm{v}_{\mathrm{ci}}(\mathrm{t})$ and $\mathrm{v}_{\mathrm{co}}(\mathrm{t})$ at the time $(\mathrm{nT})$, which occurs just before the end of $\phi_{1}$. It does not say anything about what the voltages are at other times. In actual fact, the voltages are constant at other times (ignoring second-order effects), which is equivalent to taking the sampled voltages and then using them as inputs to a sample and hold for this particular SC integrator.

Key Point: The discrete-time transfer function of a switched-capacitor integrator has a pole at $d c, z=1$.

#### EXAMPLE 14.2

Show that for frequencies much less than the sampling frequency, equation (14.11) approximates the transfer function of an ideal continuous-time integrator.
image_name:Fig. 14.7
description:The graph in Fig. 14.7 is a set of time-domain waveforms depicting the behavior of a discrete-time integrator. It consists of several waveforms plotted against time (t) on the horizontal axis.

1. **Type of Graph and Function:**
- This is a time-domain waveform graph illustrating the operation of a switched-capacitor integrator.

2. **Axes Labels and Units:**
- The horizontal axis represents time (t).
- The vertical axes show various voltage levels, labeled as \( \phi_1 \), \( \phi_2 \), \( v_{ci}(t) \), \( v_{cx}(t) \), and \( v_{co}(t) \).

3. **Overall Behavior and Trends:**
- **\( \phi_1 \) and \( \phi_2 \) Waveforms:** These are digital clock signals with non-overlapping square wave patterns. \( \phi_1 \) and \( \phi_2 \) alternate in a complementary fashion, indicating the switching phases of the integrator.
- **\( v_{ci}(t) \):** This waveform shows a continuous and slightly decreasing trend, representing the input voltage to the integrator.
- **\( v_{cx}(t) \):** This waveform exhibits a step-like behavior with a slight downward trend, reflecting the intermediate voltage across the capacitor during switching.
- **\( v_{co}(t) \):** This is a step waveform, showing discrete levels that change only at the edges of the clock cycles, representing the output voltage of the integrator.

4. **Key Features and Technical Details:**
- The clock signals \( \phi_1 \) and \( \phi_2 \) are crucial for controlling the timing of the switched-capacitor network.
- The input voltage \( v_{ci}(t) \) shows a smooth decay, typical of a signal being integrated over time.
- The step changes in \( v_{cx}(t) \) and \( v_{co}(t) \) correspond to the clock edges, with \( v_{co}(t) \) showing the sampled and held output of the integrator.

5. **Annotations and Specific Data Points:**
- The graph features dashed vertical lines indicating the sampling instances where the clock signals transition, marking key points for the waveform changes.
- There are no specific numerical values provided for the voltages or time intervals, but the consistent pattern of the waveforms suggests regular clock intervals and voltage levels consistent with typical switched-capacitor integrator operation.

Fig. 14.7 Typical voltage waveforms for the discrete-time integrator shown in Fig. 14.5.

#### Solution

Equation (14.11) can be rewritten as

$$
\begin{equation*}
H(z)=-\left(\frac{C_{1}}{C_{2}}\right) \frac{z^{-1 / 2}}{z^{1 / 2}-z^{-1 / 2}} \tag{14.13}
\end{equation*}
$$

To find the frequency response, we make use of the fact that

$$
\begin{equation*}
z=e^{j \omega T}=\cos (\omega T)+j \sin (\omega T) \tag{14.14}
\end{equation*}
$$

where T , the period, is one over the sampling frequency. Therefore,

$$
\begin{equation*}
z^{1 / 2}=\cos \left(\frac{\omega T}{2}\right)+j \sin \left(\frac{\omega T}{2}\right) \tag{14.15}
\end{equation*}
$$

and

$$
\begin{equation*}
z^{-1 / 2}=\cos \left(\frac{\omega T}{2}\right)-j \sin \left(\frac{\omega T}{2}\right) \tag{14.16}
\end{equation*}
$$

Substituting (14.15) and (14.16) into (14.13) gives

$$
\begin{equation*}
H(z)=-\left(\frac{C_{1}}{C_{2}}\right) \frac{z^{-1 / 2}}{j 2 \sin \left(\frac{\omega T}{2}\right)} \cong-\left(\frac{C_{1}}{C_{2}}\right) \frac{z^{-1 / 2}}{j \omega T} \tag{14.17}
\end{equation*}
$$

image_name:Fig. 14.8
description:The circuit is a discrete-time integrator with parasitic capacitances. It uses two NMOS transistors (M1 and M2) for switching, controlled by clock signals (Phi1 and Phi2). The op-amp A1 is used to achieve the integration with capacitors C1 and C2. Parasitic capacitors Cp1, Cp2, Cp3, and Cp4 are connected to ground. The input voltage is Vi(n) and the output is Vo(n).

Fig. 14.8 A discrete-time integrator with parasitic capacitances shown.
for $\omega \mathrm{T}<<1$. The $\mathrm{z}^{-1 / 2}$ in the numerator represents a simple delay and can be ignored. Thus, we see that the transfer function is approximately that of a continuous-time integrator having a gain constant of

$$
\begin{equation*}
\mathrm{K}_{\mathrm{I}} \cong-\left(\frac{\mathrm{C}_{1}}{\mathrm{C}_{2} \mathrm{~T}}\right) \tag{14.18}
\end{equation*}
$$

which is a function of the integrator capacitor ratio and clock frequency only.

Thus far we have ignored the effect of the parasitic capacitances due to the creation of $\mathrm{C}_{1}$ and $\mathrm{C}_{2}$ as well as the nonlinear capacitances associated with the switches. The addition of such parasitic capacitances results in the circuit shown in Fig. 14.8. Here, $\mathrm{C}_{\mathrm{p} 1}$ represents the parasitic capacitance of the top plate of $\mathrm{C}_{1}$ as well as the nonlinear capacitances associated with the two switches; $\mathrm{C}_{\mathrm{p} 2}$ represents the parasitic capacitance of the bottom plate of $\mathrm{C}_{1}$; while $\mathrm{C}_{\mathrm{p} 3}$ represents the parasitic capacitance associated with the top plate of $\mathrm{C}_{2}$, the input capacitance of the opamp, and that of the $\phi_{2}$ switch. Finally, $\mathrm{C}_{\mathrm{p} 4}$ accounts for the bottom-plate parasitic capacitance of $\mathrm{C}_{2}$ as well as any extra capacitance that the opamp output must drive.

In accounting for these parasitic capacitances, we can immediately discard the effect of $\mathrm{C}_{\mathrm{p} 2}$ since it always remains connected to ground. Similarly, the effect of $\mathrm{C}_{\mathrm{p} 3}$ on the transfer function is small since it is always connected to the virtual ground of the opamp. Also, $\mathrm{C}_{\mathrm{p} 4}$ is connected to the opamp output; therefore, although it may affect the speed of the opamp, it would not affect the final settling point of the opamp output. Finally, we note that $C_{p 1}$ is in parallel with $C_{1}$ and therefore the transfer function of this discrete-time integrator including the effects of parasitic capacitance is given by

$$
\begin{equation*}
H(z)=-\left(\frac{C_{1}+C_{p 1}}{C_{2}}\right) \frac{1}{z-1} \tag{14.19}
\end{equation*}
$$

From (14.19), we see that the gain coefficient is related to the parasitic coefficient $\mathrm{C}_{\mathrm{pl}}$, which is not well controlled and would be partially nonlinear due to the input capacitances of the switches and top-plate parasitic capacitance. To overcome this deficiency, ingenious circuits known as parasitic-insensitive structures were developed [Martin, 1978; Allstot, 1978; Jacobs, 1978].

### 14.2.3 Parasitic-Insensitive Integrators

The parasitic-insensitive integrator was a critical development that allowed the realization of high-accuracy integrated circuits. In the first integrated integrator-based filters, the noninverting integrators (Fig. 14.9) were parasitic insensitive, whereas the inverting integrators (Fig. 14.8) were parasitic sensitive [Allstot, 1978]. The
image_name:Fig. 14.9
description:
[
name: C1, type: Capacitor, value: C1, ports: {Np: X1, Nn: X2}
name: C2, type: Capacitor, value: C2, ports: {Np: Vco(t), Nn: InN(A1)}
name: A1, type: OpAmp, value: A1, ports: {InP: GND, InN: InN(A1), OutP: Vout,}
name: ϕ1, type: Switch, ports: {N1: Vci(t), N2: X1}
name: ϕ1, type: Switch, ports: {N1: X2, N2: GND}
name: ϕ2, type: Switch, ports: {N1: Vci(t), X1: GND}
name: ϕ2, type: Switch, ports: {N1: X2, N2: InN(A1)}
]
extrainfo:The circuit is a noninverting delaying discrete-time integrator that is insensitive to parasitic capacitances. It operates on two clock phases, ϕ1 and ϕ2, with input and output voltages represented as vi(n) and vo(n), respectively.
Fig. 14.9 A noninverting delaying discrete-time integrator that is not sensitive to parasitic capacitances.
image_name:(a)
description:
[
name: C1, type: Capacitor, value: C1, ports: {Np: Vci(nT-T), Nn: GND}
name: C2, type: Capacitor, value: C2, ports: {Np: InN(A1), Nn: Vco(nT-T)}
name: A1, type: OpAmp, value: A1, ports: {InP: GND, InN: InN(A1), OutP: Vco(nT-T), OutN: ''}
]
extrainfo:The circuit is a noninverting delaying discrete-time integrator that is insensitive to parasitic capacitances. It operates on two clock phases, ϕ1 and ϕ2, with input and output voltages represented as vi(n) and vo(n), respectively.
image_name:(b)
description:
[
name: C1, type: Capacitor, value: C1, ports: {Np: InN(A1), Nn: GND}
name: C2, type: Capacitor, value: C2, ports: {Np: Vco(nT-T/2), Nn: InN(A1)}
name: A1, type: OpAmp, value: A1, ports: {InP: GND, InN: InN(A1), OutP: Vco(nT-T/2)}
]
extrainfo:The circuit is a noninverting delaying discrete-time integrator that is insensitive to parasitic capacitances. It operates on two clock phases, ϕ1 and ϕ2, with input and output voltages represented as vi(n) and vo(n), respectively.

Fig. 14.10 The noninverting discrete-time integrator on the two clock phases: (a) $\phi_{1}$ (b) $\phi_{2}$
development of the parasitic-insensitive inverting integrator [Martin, 1978; Jacobs, 1978] allowed the complete filter to be insensitive, which greatly decreased second-order errors. To realize a parasitic-insensitive discrete-time integrator, two extra switches are used, as shown in Fig. 14.9. Analyzing this circuit as before, note that when $\phi_{1}$ is on, $\mathrm{C}_{1}$ is charged to $\mathrm{C}_{1} \mathrm{v}_{\mathrm{ci}}(\mathrm{nT}-\mathrm{T})$, as shown in Fig. 14.10(a). When $\phi_{2}$ turns on, $\mathrm{C}_{1}$ is effectively "hooked" up backwards, and the discharge now occurs through what was the ground node rather than the input signal side, as shown in Fig. 14.10(b). Such a reverse connection results in $\mathrm{v}_{\mathrm{co}}(\mathrm{t})$ rising for a positive $\mathrm{v}_{\mathrm{ci}}(\mathrm{nT}-\mathrm{T})$, and therefore the integrator is noninverting. With the rest of the analysis being performed as before, the transfer function, $\mathrm{H}(\mathrm{z})$, for this discrete-time integrator is given as

$$
\begin{equation*}
H(z) \equiv \frac{V_{0}(z)}{V_{i}(z)}=\left(\frac{C_{1}}{C_{2}}\right) \frac{z^{-1}}{1-z^{-1}} \tag{14.20}
\end{equation*}
$$

Note that (14.20) represents a positive discrete-time integrator with a full delay from input to output (due to the $\mathrm{z}^{-1}$ in the numerator, which represents a one-period delay) so we refer to the circuit of Fig. 14.9 as a delaying discrete-time integrator. As was done for the parasitic sensitive inverting integrator of Fig. 14.8, one often rewrites the transfer function to eliminate negative powers of $z$ yielding

$$
\begin{equation*}
H(z) \equiv \frac{V_{0}(z)}{V_{i}(z)}=\left(\frac{C_{1}}{C_{2}}\right) \frac{1}{z-1} \tag{14.21}
\end{equation*}
$$

To investigate the behavior of this noninverting integrator with respect to parasitic capacitances, consider the same circuit drawn with parasitic capacitances, as shown in Fig. 14.11. Here, $\mathrm{C}_{\mathrm{p} 3}$ and $\mathrm{C}_{\mathrm{p} 4}$ do not affect the operation of the circuit as before. In addition, $\mathrm{C}_{\mathrm{p} 2}$ is either connected to ground through the $\phi_{1}$ switch or to virtual ground through the $\phi_{2}$ switch. Therefore, since $\mathrm{C}_{\mathrm{p} 2}$ always remains discharged (after settling), it also does not affect the operation of the circuit. Finally, $C_{p 1}$ is continuously being charged to $v_{i}(n)$ and discharged to ground. However during $\phi_{1}$ on, the fact that $C_{p 1}$ is also charged to $v_{i}(n-1)$ does not affect

Key Point: In order to make a switched-capacitor integrator insensitive to the circuit's parasitic capacitances to ground, it is necessary to add two extra switches, for a total of four, on each switched capacitor.
the charge that is placed on $C_{1}$. When $\phi_{2}$ is turned on, $C_{p 1}$ is discharged through the $\phi_{2}$ switch attached to its node and none of its discharging current passes through $C_{1}$ to affect the charge accumulating on $\mathrm{C}_{2}$. Therefore, it also does not affect the circuit operation. In summary, while the parasitic capacitances may slow down settling time behavior, they do not affect the discrete-time difference equation that occurs in the integrator shown in Fig. 14.9.

To obtain an inverting discrete-time integrator that is also parasitic insensitive, the same circuit as the parasitic-insensitive noninverting integrator can be used, but with the two switch phases on the switches near the opamp input side of $C_{1}$ (that is, the top-plate of $C_{1}$ ) interchanged as shown in Fig. 14.12 [Martin, 1978]. With this arrangement, note that the charge on $\mathrm{C}_{2}$ does not change when $\phi_{2}$ turns on (and $\phi_{1}$ is off) as illustrated in Fig. 14.13(b). Therefore, we can write

$$
\begin{equation*}
\mathrm{C}_{2} \mathrm{v}_{\mathrm{co}}(\mathrm{nT}-\mathrm{T} / 2)=\mathrm{C}_{2} \mathrm{v}_{\mathrm{co}}(\mathrm{nT}-\mathrm{T}) \tag{14.22}
\end{equation*}
$$

Also note that $C_{1}$ is fully discharged at the end of $\phi_{2}$ on. Now when $\phi_{1}$ is turned on in Fig. 14.13(a), $C_{1}$ is charged up to $\mathrm{v}_{\mathrm{ci}}(\mathrm{t})$. However, the current needed to charge $\mathrm{C}_{1}$ passes through $\mathrm{C}_{2}$, in effect changing the charge on $C_{2}$ by that amount. At the end of $\phi_{1}$ on, the charge left on $C_{2}$ is equal to its old charge (before $\phi_{1}$ was on)
image_name:Fig. 14.11 A parasitic-insensitive delayed integrator with parasitic capacitances shown.
description:The circuit is a parasitic-insensitive delayed integrator. It uses NMOS transistors for switching and capacitors to store charge. The OpAmp A1 provides amplification with feedback from the output node Vout.

Fig. 14.11 A parasitic-insensitive delayed integrator with parasitic capacitances shown.
image_name:Fig. 14.12
description:The circuit is a parasitic-insensitive delayed integrator using NMOS transistors for switching and capacitors for charge storage. The OpAmp A1 provides amplification with feedback from the output node Vout. The circuit operates in two clock phases, phi1 and phi2, to control the switching of the NMOS transistors.

Fig. 14.12 A delay-free discrete-time integrator (not sensitive to parasitic capacitances).
image_name:(a)
description:The circuit is a parasitic-insensitive delayed integrator using NMOS transistors for switching and capacitors for charge storage. The OpAmp A1 provides amplification with feedback from the output node Vco(nT-T/2). The circuit operates in two clock phases, phi1 and phi2, to control the switching of the NMOS transistors.
image_name:(b)
description:The circuit is a parasitic-insensitive delayed integrator using NMOS transistors for switching and capacitors for charge storage. The OpAmp A1 provides amplification with feedback from the output node Vco(nT-T/2). The circuit operates in two clock phases, phi1 and phi2, to control the switching of the NMOS transistors.

Fig. 14.13 A parasitic-insensitive delay-free integrator on the two clock phases: (a) $\phi_{2}$ (b) $\phi_{1}$
subtracted from the charge needed to charge up $\mathrm{C}_{1}$ to $\mathrm{v}_{\mathrm{ci}}(\mathrm{nT})$. Thus, we have the following charge relationship:

$$
\begin{equation*}
\mathrm{C}_{2} \mathrm{v}_{\mathrm{co}}(\mathrm{nT})=\mathrm{C}_{2} \mathrm{v}_{\mathrm{co}}(\mathrm{nT}-\mathrm{T} / 2)-\mathrm{C}_{1} \mathrm{v}_{\mathrm{ci}}(\mathrm{nT}) \tag{14.23}
\end{equation*}
$$

Note that $\mathrm{v}_{\mathrm{ci}}(\mathrm{nT})$ occurs in the preceding equation rather than $\mathrm{v}_{\mathrm{ci}}(\mathrm{nT}-\mathrm{T})$, since the charge on $\mathrm{C}_{2}$ at the end of $\phi_{1}$ is related to the value of $\mathrm{v}_{\mathrm{ci}}(\mathrm{nT})$ at the same time, and therefore the integrator is considered to be delay free. Substituting in (14.22), dividing by $\mathrm{C}_{2}$, and switching to discrete-time variables, we have

$$
\begin{equation*}
v_{0}(n)=v_{0}(n-1)-\frac{C_{1}}{C_{2}} v_{i}(n) \tag{14.24}
\end{equation*}
$$

Taking the z -transform of both sides, the transfer function, $\mathrm{H}(\mathrm{z})$, for this delay-free integrator is found to be

$$
\begin{equation*}
H(z) \equiv \frac{V_{0}(z)}{V_{i}(z)}=-\left(\frac{C_{1}}{C_{2}}\right) \frac{1}{1-z^{-1}} \tag{14.25}
\end{equation*}
$$

where the fact that the numerator has a purely real term is indicative of the integrator being delay free. As before, (14.25) is often rewritten as

$$
\begin{equation*}
H(z) \equiv \frac{V_{0}(z)}{V_{i}(z)}=-\left(\frac{C_{1}}{C_{2}}\right) \frac{z}{z-1} \tag{14.26}
\end{equation*}
$$

Key Point: Both delayed and delayfree integrators can be realized with the same switched-capacitor circuit by changing the clock phases applied to two of the switches. In a fully-differential implementation, both can be configured to provide either positive or negative dc gain.

Finally, note that the preceding delay-free integrator has a negative gain, while the delaying integrator has a positive gain. While these sign changes in the gain can be quite useful in single-ended switched-capacitor designs, most modern integrated circuits make use of fully differential signals for improved noise performance, and sign changes can be achieved by simply cross-coupling output wires. Hence, either of the circuits in Figs. 14.9 or 14.12, when implemented fully differentially, may be used to realize either a positive or negative gain. It is therefore more specific to refer to Fig. 14.9 as a delayed integrator and Fig. 14.12 as a delay-free integrator.
image_name:(a)
description:
[
name: C1, type: Capacitor, value: C1, ports: {Np: V1(z), Nn: InN(A1)}
name: C2, type: Capacitor, value: C2, ports: {Np: x1, Nn: x2}
name: C3, type: Capacitor, value: C3, ports: {Np: x3, Nn: x4}
name: CA, type: Capacitor, value: CA, ports: {Np: InN(A1), Nn: Vo(z)}
name: A1, type: OpAmp, value: A1, ports: {InP: GND, InN: InN(A1), OutP: Vo(z)}
]
extrainfo:The circuit is a three-input switched capacitor summing/integrator stage. It combines inputs V1(z), V2(z), and V3(z) through capacitors C1, C2, and C3, and integrates the summed signal using capacitor CA and op-amp A1.
image_name:(b)
description:The system block diagram in Fig. 14.14(b) represents a three-input switched capacitor summing/integrator stage, depicted as a signal-flow graph. This diagram provides a simplified representation of the circuit's signal processing.

1. **Main Components:**
- **Input Nodes:** There are three input signals labeled as \( V_1(z) \), \( V_2(z) \), and \( V_3(z) \).
- **Summation Junction:** The inputs are fed into a summation block, where they are weighted and summed.
- **Transfer Function Block:** The summed signal is then processed by a transfer function block, which applies a specific transfer function to the input sum.
- **Output Node:** The output of the transfer function block is \( V_o(z) \), representing the system's output signal.

2. **Flow of Information or Control:**
- The input signals \( V_1(z) \), \( V_2(z) \), and \( V_3(z) \) are each multiplied by specific coefficients before entering the summation block. These coefficients are \(-C_1(1 - z^{-1})\) for \( V_1(z) \), \( C_2z^{-1} \) for \( V_2(z) \), and \(-C_3\) for \( V_3(z) \).
- The summation block combines these weighted inputs into a single signal.
- The combined signal is then fed into a transfer function block characterized by \( \frac{1}{C_A} \frac{1}{1 - z^{-1}} \), which integrates the input based on the given transfer function.

3. **Labels, Annotations, and Key Indicators:**
- Input signals are clearly labeled with \( V_1(z) \), \( V_2(z) \), and \( V_3(z) \).
- Coefficients \(-C_1(1 - z^{-1})\), \( C_2z^{-1} \), and \(-C_3\) indicate the weighting applied to each input.
- The transfer function \( \frac{1}{C_A} \frac{1}{1 - z^{-1}} \) is annotated within the block, defining the system's integration and scaling behavior.

4. **Overall System Function:**
- The primary function of this system is to sum the three input signals with specific weightings and then integrate the result. The integration is accomplished through the transfer function block, which effectively accumulates the input over time, producing the output \( V_o(z) \). This design allows for flexible signal processing, combining multiple inputs into a single integrated output, useful in applications requiring signal summation and integration.

Fig. 14.14 Three-input switched capacitor summing/integrator stage. (a) Circuit. (b) Equivalent signal-flow-graph.

### 14.2.4 Signal-Flow-Graph Analysis

Clearly, applying the charge transfer equations just described to larger circuits would be tedious. Instead, a few rules can be developed to create and analyze such circuits graphically. Consider the three-input integrator shown in Fig. 14.14. Using the principle of superposition, it is clear that the input-output relationships for $\mathrm{V}_{2}(\mathrm{z})$ and $V_{3}(z)$ are given by

$$
\begin{align*}
& \frac{V_{0}(z)}{V_{2}(z)}=\left(\frac{C_{2}}{C_{A}}\right)\left(\frac{z^{-1}}{1-z^{-1}}\right)  \tag{14.27}\\
& \frac{V_{0}(z)}{V_{3}(z)}=-\left(\frac{C_{3}}{C_{A}}\right)\left(\frac{1}{1-z^{-1}}\right) \tag{14.28}
\end{align*}
$$

For the input $\mathrm{V}_{1}(\mathrm{z})$, we note that its relationship to $\mathrm{V}_{0}(\mathrm{z})$ is simply an inverting gain stage given by

$$
\begin{equation*}
\frac{V_{0}(z)}{V_{1}(z)}=-\left(\frac{C_{1}}{C_{A}}\right) \tag{14.29}
\end{equation*}
$$

with the output once again being sampled at the end of $\phi_{1}$ as shown.
Combining (14.27), (14.28), and (14.29), the input-output relationship for the circuit of Fig. 14.14(a) is equal to

$$
\begin{equation*}
V_{0}(z)=-\left(\frac{C_{1}}{C_{A}}\right) V_{1}(z)+\left(\frac{C_{2}}{C_{A}}\right)\left(\frac{z^{-1}}{1-z^{-1}}\right) V_{2}(z)-\left(\frac{C_{3}}{C_{A}}\right)\left(\frac{1}{1-z^{-1}}\right) V_{3}(z) \tag{14.30}
\end{equation*}
$$

image_name:Fig. 14.15 Noise sampling on a switched capacitor
description:The graph in Fig. 14.15 illustrates noise sampling on a switched capacitor circuit. It consists of a time-domain waveform that represents the voltage across the capacitor, denoted as \( V_C(t) \), over time \( t \). The graph is divided into segments that correspond to the switching phases of the circuit, labeled \( \phi_1 \) as 'on' and 'off'.

**Axes Labels and Units:**
- The horizontal axis represents time \( t \), though specific units are not provided, it's implied to be in seconds or a submultiple like milliseconds.
- The vertical axis represents the capacitor voltage \( V_C(t) \). Again, specific units are not given, but it's typically in volts.

**Overall Behavior and Trends:**
- The waveform shows a series of noisy signals sampled at discrete intervals, corresponding to the switching phases.
- During the 'on' phase of \( \phi_1 \), the voltage \( V_C(t) \) is sampled, resulting in a noisy waveform segment.
- In the 'off' phase, the waveform appears to stabilize at discrete values, denoted as \( V_C(k) \), \( V_C(k+1) \), and \( V_C(k+2) \), indicating the sampled voltage levels.

**Key Features and Technical Details:**
- The waveform is characterized by high-frequency noise during the sampling ('on') phase.
- The notation \( T_{on} \gg R_{on}C \) suggests that the time the switch is 'on' is significantly longer than the RC time constant, indicating a long sampling period relative to the switch's resistance-capacitance product.

**Annotations and Specific Data Points:**
- The graph is annotated with the switching phases (on/off) and the sampled voltage levels \( V_C(k) \), \( V_C(k+1) \), and \( V_C(k+2) \), which represent the discrete sampled values during the 'off' phase.
- The transition points between the 'on' and 'off' phases are marked with dashed lines, indicating the sampling intervals.

Fig. 14.15 Noise sampling on a switched capacitor.

Key Point: Complicated switched-capacitor circuits may be analyzed graphically using a signal-flow-graph representing the opamp stage with an integrating block and replacing each input branch with the corresponding non switched, delayed, or delayfree gain factor.

Such a relationship can also be represented by the signal-flow-graph shown in Fig. 14.14(b), where the input stages have been separated from the opamp stage. Thus, we see that to obtain an equivalent signal-flow-graph, the block $\left(1 / C_{A}\right)\left[1 /\left(1-z^{-1}\right)\right]$ is used to represent the opamp stage, while three different gain factors are used to represent the possible input stages. For a nonswitched capacitor input stage, a gain factor of $-C_{1}\left(1-z^{-1}\right)$ is used. If a delaying switched capacitor is used, it is represented by $\mathrm{C}_{2} z^{-1}$. Finally, for a delay-free switched-capacitor input, a gain factor of $-\mathrm{C}_{3}$ is used. Note, however, that the output, $\mathrm{V}_{0}(\mathrm{z})$, should be sampled on $\phi_{1}$ when the switched-capacitor inputs sample their input signals on $\phi_{1}$.
As before, this transfer function might often be rewritten in powers of $\mathbf{z}$ rather than $\mathbf{z}^{-1}$, resulting in

$$
\begin{equation*}
V_{0}(z)=-\left(\frac{C_{1}}{C_{A}}\right) V_{1}(z)+\left(\frac{C_{2}}{C_{A}}\right)\left(\frac{1}{z-1}\right) V_{2}(z)-\left(\frac{C_{3}}{C_{A}}\right)\left(\frac{z}{z-1}\right) V_{3}(z) \tag{14.31}
\end{equation*}
$$

Finally, it should be noted that in a fully differential implementation, effective negative capacitances for $\mathrm{C}_{1}$, $\mathrm{C}_{2}$, and $\mathrm{C}_{3}$ can be achieved by simply interchanging the input wires.

## 14.3 NOISE IN SWITCHED-CAPACITOR CIRCUITS

The analysis of noise in switched-capacitor circuits is subtly different than that introduced earlier in this text. The noise analysis in Chapter 9 presumes continuous-time circuits under constant bias conditions, so that the random noise statistics may be considered stationary. By contrast, switched-capacitor circuits are constantly changing their configuration due to the opening and closing of switches. We will perform a simplified analysis, useful for design, by considering the circuit in each of its clock phases. Moreover, we assume that the noise voltage across capacitors is sampled instantaneously and perfectly when the switches turn off.

Key Point: Switched capacitors accumulate the thermal noise of the switches. Sampled kT/C noise from both clock phases superimpose resulting in a total mean squared input-referred noise of $2 \mathrm{kT} / \mathrm{C}$.

The sampling of a noise signal on a capacitor is illustrated in Fig. 14.15. After the switch turns on, thermal noise from the switch accumulates on the capacitor. For any practical switched capacitor circuit, the time constant of the switch on resistance, $R_{o n}$, and capacitance $C$ should be significantly less than the switch on time to ensure settling of signal voltages on the capacitor. Hence, by the time the switch opens the rms noise voltage has reached its steady state value of $\sqrt{\mathrm{kT} / \mathrm{C}}$ (see Chapter 9). The voltage sampled and stored on the capacitor, $\mathrm{V}_{\mathrm{C}}(\mathrm{k})$, is therefore a discrete-time noise voltage with an rms value of $\sqrt{\mathrm{kT} / \mathrm{C}}$. When an input signal is present on the left terminal of the switched capacitor in Fig. 14.15, the sampled noise voltage is superimposed on the sampled input voltage.
image_name:Fig. 14.16
description:The circuit diagram represents a switched-capacitor branch in two clock phases with switch resistances Ron. Noise is analyzed with an assumption of zero input voltage. The rms noise voltage for each capacitor is given as sqrt(kT/C).

Fig. 14.16 A switched-capacitor branch shown in each clock phase with the switch resistances. $\mathrm{R}_{\text {on }}$

Next, consider the delayed parasitic-insensitive switched capacitor introduced in Fig. 14.9. In Fig. 14.16, the switched-capacitor branch is illustrated in each of its two clock phases with the switches replaced by their on resistance $R_{\text {on }}$. Since we are presently interested only in the noise, we assume the input voltage to the branch is zero (ground). Noise is contributed by each of the four switches. In clock phase $\phi_{1}$, a rms voltage $\mathrm{V}_{\mathrm{cl}(\mathrm{ms})}^{2}=\sqrt{\mathrm{kT} / \mathrm{C}}$ is sampled upon the capacitor. The charge stored on the capacitor is, therefore, a random quantity with a rms value

$$
\begin{equation*}
\Delta Q_{1(\mathrm{rms})}=C \cdot \sqrt{\mathrm{kT} / \mathrm{C}}=\sqrt{\mathrm{kTC}} \tag{14.32}
\end{equation*}
$$

This random quantity of charge is completely delivered to the opamp feedback network during clock phase $\phi_{2}$.

Superimposed upon this is another random quantity of charge due to the switches on during clock phase $\phi_{2}$. Again, thermal noise in the switches gives rise to a capacitor noise voltage $\mathrm{V}_{\mathrm{c2} .(\mathrm{rms})}^{2}=\sqrt{\mathrm{kT} / \mathrm{C}}$. Assuming the opamp is ideal, and therefore able to maintain a precise virtual ground during $\phi_{2}$, this capacitor noise voltage results in an additional random charge being delivered to (or from) the feedback network.

$$
\begin{equation*}
\Delta Q_{2(\mathrm{rms})}=C \cdot \sqrt{\mathrm{kT} / \mathrm{C}}=\sqrt{\mathrm{kTC}} \tag{14.33}
\end{equation*}
$$

The noise quantities $V_{c 1}$ and $V_{c 2}$ are uncorrelated, as are the charges $\Delta Q_{1}$ and $\Delta Q_{2}$. Therefore, the mean square total charge delivered by the switched capacitor branch is a sum of squares of (14.32) and (14.33).

$$
\begin{equation*}
\Delta \mathrm{Q}_{(\mathrm{rms})}{ }^{2}=\Delta \mathrm{Q}_{1(\mathrm{rms})}{ }^{2}+\Delta \mathrm{Q}_{2(\mathrm{rms})}{ }^{2}=2 \mathrm{kTC} \tag{14.34}
\end{equation*}
$$

This is precisely the same charge that would be delivered if the switches were noiseless and the input mean squared voltage were $2 \mathrm{kT} / \mathrm{C}$. Hence, assuming an ideal opamp, the switched capacitor branch may be considered to have an input-referred noise,

$$
\begin{equation*}
V_{i n(r m s)}=\sqrt{\frac{2 \mathrm{kT}}{\mathrm{C}}} \tag{14.35}
\end{equation*}
$$

It may be shown that including nonideal effects of the opamp makes the input-referred noise slightly higher than the value in (14.35) but the difference is generally small when the opamp's noise is dominated by its input differential pair transistors [Schreier, 2005].

## 14.4 FIRST-ORDER FILTERS

Key Point: Beginning with conventional continuous-time active RC filters, and replacing each resistor with a switchedcapacitor results in a discrete-time filter whose frequency response closely approximates that of the original continuous-time filter at frequencies far below the sampling frequency. Once a filter structure is obtained, its precise frequency response is determined through the use of discrete-time analysis.
image_name:Fig. 14.17 A first-order active-RC filter.
description:This circuit is a first-order active-RC filter using an operational amplifier. The input is connected through R1 and C1 to the inverting input of the op-amp. The feedback network consists of R2 and C2. The output is taken from the op-amp's output terminal.

Fig. 14.17 A first-order active-RC filter.

We saw in Section 14.2.1 that at low frequencies, a switched capacitor is equivalent to a resistor. Such an equivalence is often used to derive good switched-capacitor filter structures from their active-RC counterparts. However, although such structures would behave very similarly for low-frequency input signals (when compared to the clock frequency), for signal frequencies moderately close to the clock frequency, the behavior of the switched-capacitor circuit is precisely determined through the use of the z-domain signal-flow-graph approach just discussed.

A general first-order active-RC filter is shown in Fig. 14.17. To obtain a switched-capacitor filter having the same lowfrequency behavior, the resistors are replaced with delay-free switched capacitors (delay-free inputs are used since they create negative integration, as do resistive inputs), while the nonswitched capacitor feed-in is left unchanged. The resulting first-order switched-capacitor filter and its equivalent signal-flow-graph are shown in Fig. 14.18. An equation that describes this signal-flow-graph is
image_name:(a)
description:This is a first-order switched-capacitor filter circuit. The resistors are replaced with delay-free switched capacitors to achieve a low-frequency behavior equivalent to an active-RC filter. The circuit consists of capacitors C1, C2, C3, CA, and an operational amplifier A1.
image_name:(b)
description:The block diagram labeled "(b)" represents the equivalent signal-flow graph of a first-order switched-capacitor filter. This diagram provides a visual representation of the filter's mathematical model and signal processing function.

1. **Main Components:**
- **Adder Node:** This is the central component where multiple input signals are summed. It is depicted as a circle with arrows pointing into it, indicating the summation of different weighted signals.
- **Gain Blocks:** There are three gain blocks represented by arrows with labels indicating the gain values:
- **-C1(1 - z^-1):** This block represents the weighted input signal with a gain of -C1 and a delay factor of (1 - z^-1).
- **-C2:** This block represents another input signal weighted by -C2.
- **-C3:** This block represents a feedback path weighted by -C3.
- **Integrator Block:** Represented by a block labeled as \( \frac{1}{C_A} \frac{1}{1 - z^{-1}} \), it models the integration operation performed in the z-domain, which is a characteristic of switched-capacitor filters.

2. **Flow of Information or Control:**
- The input signal \( V_i(z) \) enters the system and is split into two paths: one directly multiplied by \(-C2\) and the other multiplied by \(-C1(1 - z^{-1})\) before entering the adder.
- The output of the adder is sent to the integrator block, which produces the output \( V_o(z) \).
- A feedback loop is present where the output \( V_o(z) \) is multiplied by \(-C3\) and fed back into the adder, contributing to the input of the integrator.

3. **Labels, Annotations, and Key Indicators:**
- The labels \(-C1(1 - z^{-1})\), \(-C2\), and \(-C3\) indicate the weights and operations applied to the respective signals in the flow graph.
- The integrator block is annotated with \( \frac{1}{C_A} \frac{1}{1 - z^{-1}} \), denoting its function as a discrete-time integrator in the z-domain.

4. **Overall System Function:**
- This system functions as a first-order switched-capacitor filter. The arrangement of gain blocks, adder, and integrator creates a filter that modifies the input signal \( V_i(z) \) based on the configured capacitive ratios \( C_1, C_2, C_3, \) and \( C_A \). The feedback loop with \(-C3\) allows for dynamic adjustment of the filter's response, providing a mechanism for controlling the frequency characteristics of the output signal \( V_o(z) \). The system effectively translates the analog filter design into a digital domain using switched-capacitor techniques, maintaining the desired low-frequency behavior.

Fig. 14.18 A first-order switched-capacitor filter: (a) circuit (no switch sharing), (b) equivalent signal-flow-graph.
from which the transfer function for this first-order filter is found to be

$$
\begin{align*}
H(z) \equiv \frac{V_{0}(z)}{V_{i}(z)} & =-\frac{\left(\frac{C_{1}}{C_{A}}\right)\left(1-z^{-1}\right)+\left(\frac{C_{2}}{C_{A}}\right)}{1-z^{-1}+\frac{C_{3}}{C_{A}}}  \tag{14.37}\\
& =-\frac{\left(\frac{C_{1}+C_{2}}{C_{A}}\right) z-\frac{C_{1}}{C_{A}}}{\left(1+\frac{C_{3}}{C_{A}}\right) z-1}
\end{align*}
$$

The pole of (14.37) is found by equating the denominator to zero, which results in a pole location, $\mathrm{z}_{\mathrm{p}}$, given by

$$
\begin{equation*}
z_{p}=\frac{C_{A}}{C_{A}+C_{3}} \tag{14.38}
\end{equation*}
$$

Note that for positive capacitance values, this pole is restricted to the real axis between zero and one, and therefore the circuit is always stable. In fact, with $C_{3}=0$ the circuit's pole is at $\mathbf{z}=1$ or, in other words, it becomes a discrete-time integrator, as expected. The zero of (14.37) is found by equating the numerator to zero, which results in a zero location, $\mathbf{z}_{z}$, given by

$$
\begin{equation*}
\mathrm{z}_{\mathrm{z}}=\frac{\mathrm{C}_{1}}{\mathrm{C}_{1}+\mathrm{C}_{2}} \tag{14.39}
\end{equation*}
$$

Therefore, for positive capacitance values, this zero location is also restricted to the real axis between zero and one. Additionally, the dc gain for this circuit is found by setting $z=1$, which results in the dc gain being given by

$$
\begin{equation*}
\mathrm{H}(1)=\frac{-\mathrm{C}_{2}}{\mathrm{C}_{3}} \tag{14.40}
\end{equation*}
$$

Recall that in a fully differential implementation, effective negative capacitances can be realized for $\mathrm{C}_{1}, \mathrm{C}_{2}$, and $C_{3}$ by interchanging the input wires. For example, a zero at $z=-1$ could be realized by setting

$$
\begin{equation*}
\mathrm{C}_{1}=-0.5 \mathrm{C}_{2} \tag{14.41}
\end{equation*}
$$

In other words, the pair of capacitors representing $C_{1}$ would be half the size of those representing $C_{2}$ and the input wires interchanged into the $C_{1}$ pair such that $-V_{i}(z)$ is applied to that input branch.

#### EXAMPLE 14.3

Find the capacitance values needed for a first-order switched-capacitor circuit such that its $3-\mathrm{dB}$ point is at 10 kHz when a clock frequency of 100 kHz is used. It is also desired that the filter have zero gain at 50 kHz and the dc gain be unity. Assume $C_{A}=10 \mathrm{pF}$.

#### Solution

First note that having a zero gain at 50 kHz is equivalent to placing a zero at -1 . Now, making use of the bilinear transform $p=(z-1) /(z+1)$ as described in Section 13.5.4, the zero at -1 is mapped to $\Omega=\infty$. In addition, the frequency warping between the two domains, $\Omega=\tan (\omega / 2)$, maps the $-3-\mathrm{dB}$ frequency of 10 kHz (or $0.2 \pi \mathrm{rad} /$ sample) in the Z -domain to

$$
\Omega=\tan \left(\frac{0.2 \pi}{2}\right)=0.3249
$$

in the continuous-time domain. Therefore, our specification is now simplified to find the pole location for a con-tinuous-time filter having a $-3-\mathrm{dB}$ frequency equal to $0.3249 \mathrm{rad} / \mathrm{s}$ and a zero at $\infty$. Clearly, the continuous-time pole, $p_{p}$, required here is

$$
\mathrm{p}_{\mathrm{p}}=-0.3249
$$

This pole is mapped back to a $\mathbf{Z}$-domain pole, $\mathbf{z}_{\mathrm{p}}$, of value

$$
\mathrm{z}_{\mathrm{p}}=\frac{1+\mathrm{p}_{\mathrm{p}}}{1-\mathrm{p}_{\mathrm{p}}}=0.5095
$$

Therefore, the desired discrete-time transfer function, $H(z)$, is given by

$$
H(z)=\frac{k(z+1)}{z-0.5095}
$$

where k is determined by setting the dc gain to one (i.e., $\mathrm{H}(1)=1$ ) resulting in

$$
H(z)=\frac{0.24525(z+1)}{z-0.5095}
$$

or equivalently,

$$
\mathrm{H}(\mathrm{z})=\frac{0.4814 \mathrm{z}+0.4814}{1.9627 \mathrm{z}-1}
$$

Equating these coefficients with those of (14.37) (and assuming $\mathrm{C}_{\mathrm{A}}=10 \mathrm{pF}$ ) results in

$$
\begin{aligned}
& \mathrm{C}_{1}=4.814 \mathrm{pF} \\
& \mathrm{C}_{2}=-9.628 \mathrm{pF} \\
& \mathrm{C}_{3}=9.628 \mathrm{pF}
\end{aligned}
$$

where a differential input can realize the negative capacitance.

For designs where the zero and pole frequencies are substantially less than the clock frequency (unlike the previous example, which had a zero at one-half the clock frequency), it is not necessary to pre-warp the specifications using the bilinear transform. Rather, some approximations can be used to derive equations for the capacitor ratios given the desired zero and pole, which are both assumed to be real and positive. As in Example 14.2, using (14.37), we have

$$
\begin{equation*}
H(z) \equiv \frac{V_{0}(z)}{V_{i}(z)}=-\frac{\left(\frac{C_{1}}{C_{A}}\right)\left(z^{1 / 2}-z^{-1 / 2}\right)+\left(\frac{C_{2}}{C_{A}}\right) z^{1 / 2}}{z^{1 / 2}-z^{-1 / 2}+\frac{C_{3}}{C_{A}} z^{1 / 2}} \tag{14.42}
\end{equation*}
$$

Substituting (14.15) and (14.16) into (14.42) gives

$$
\begin{equation*}
H\left(e^{j \omega T}\right) \equiv \frac{V_{0}\left(e^{j \omega T}\right)}{V_{i}\left(e^{j \omega T}\right)}=-\frac{j \frac{2 C_{1}+C_{2}}{C_{A}} \sin \left(\frac{\omega T}{2}\right)+\frac{C_{2}}{C_{A}} \cos \left(\frac{\omega T}{2}\right)}{j\left(2+\frac{C_{3}}{C_{A}}\right) \sin \left(\frac{\omega T}{2}\right)+\frac{C_{3}}{C_{A}} \cos \left(\frac{\omega T}{2}\right)} \tag{14.43}
\end{equation*}
$$

This transfer function is exact. Making the approximation $\omega T<<1$ allows (14.43) to be simplified as

$$
\begin{equation*}
H\left(e^{j \omega T}\right) \equiv \frac{V_{0}\left(e^{j \omega T}\right)}{V_{i}\left(e^{j \omega T}\right)}=-\frac{j\left(\frac{C_{1}+C_{2} / 2}{C_{A}}\right) \omega T+\frac{C_{2}}{C_{A}}}{j\left(1+\frac{C_{3}}{2 C_{A}}\right) \omega T+\frac{C_{3}}{C_{A}}} \tag{14.44}
\end{equation*}
$$

The procedure just used is quite useful when finding a continuous-time transfer function that approximates a discrete-time transfer function. Setting the numerator of (14.44) to zero gives the following approximate equation for the zero frequency:

$$
\begin{equation*}
\mathrm{j} \omega_{\mathrm{z}} \mathrm{~T}=\frac{-\mathrm{C}_{2} / \mathrm{C}_{1}}{1+\frac{\mathrm{C}_{2}}{2 \mathrm{C}_{1}}} \tag{14.45}
\end{equation*}
$$

Similarly, setting the denominator to zero gives the following approximate equation for the pole frequency:

$$
\begin{equation*}
\mathrm{j} \omega_{\mathrm{p}} \mathrm{~T}=\frac{-\mathrm{C}_{3} / \mathrm{C}_{\mathrm{A}}}{1+\frac{\mathrm{C}_{3}}{2 \mathrm{C}_{\mathrm{A}}}} \tag{14.46}
\end{equation*}
$$

#### EXAMPLE 14.4

Find the capacitance values $\mathrm{C}_{3}$ needed for a first-order low-pass switched-capacitor filter that has $\mathrm{C}_{1}=0$ and a pole at the 1/64th sampling frequency using the approximate equations. The low-frequency gain should be unity.

#### Solution

Using (14.46) and solving for $C_{3} / C_{A}$, we have

$$
\begin{equation*}
\frac{C_{3}}{C_{A}}=\frac{\omega_{p} T}{1-\omega_{p} T / 2}=\frac{2 \pi / 64}{1-2 \pi / 128}=0.1032 \tag{14.47}
\end{equation*}
$$

If we choose $C_{A}=10 \mathrm{pF}$, then we have $C_{3}=1.032 \mathrm{pF}$. From (14.44) with $\mathrm{C}_{1}=0$, we see that the lowfrequency gain is given by $\mathrm{C}_{2} / \mathrm{C}_{3}$. For unity gain, this means we need $\mathrm{C}_{2}=1.032 \mathrm{pF}$ as well.

### 14.4.1 Switch Sharing

Careful examination of the switched-capacitor filter shown in Fig. 14.18(a) reveals that some of the switches are redundant. Specifically, the top plate of both $\mathrm{C}_{2}$ and $\mathrm{C}_{3}$ are always switched to the opamp's virtual ground and true ground at the same time. Therefore, one pair of these switches can be eliminated and the two top plates of $\mathrm{C}_{2}$ and $C_{3}$ can be connected together, as shown in Fig. 14.19.

### 14.4.2 Fully Differential Filters

While the circuits seen so far have all been shown with single-ended signals, in most analog applications it is desirable to keep the signals fully differential. Fully differential signals imply that the difference between two lines represents the signal component, and thus any noise which appears as a common-mode signal on those two lines does
image_name:Fig. 14.19
description:The circuit is a first-order switched-capacitor filter with switch sharing. It uses fully differential signals to minimize noise impact. The switches are controlled by clock phases φ1 and φ2.

Fig. 14.19 A first-order switched-capacitor filter with switch sharing.
not affect the signal. Fully differential circuits should also be balanced, implying that the differential signals operate symmetrically around a dc common-mode voltage (typically, analog ground or halfway between the power-supply voltages). Having balanced circuits implies that it is more likely noise will occur as a common-mode signal due to the symmetry of the circuit. Fully differential circuits have the additional benefit that if each single-ended signal is distorted symmetrically around the common-mode voltage, the differential signal will have only odd-order distortion terms (which are often much smaller). To see this distortion improvement, consider the block diagram shown in Fig. 14.20, where the two nonlinear elements are identical and, for simplicity, the common-mode voltage is assumed to be zero. If the nonlinearity is memoryless, then the outputs can be found as a Taylor series expansion given by

Key Point: Fully-differential filter implementations offer several advantages over their single-ended counterparts: they allow for the realization of sign inversion (i.e. a gain of -1 ) by simply interchanging wires, reject common-mode noise, and rejecting even-order distortion terms which generally dominate single-ended circuits.

$$
\begin{equation*}
v_{o}=k_{1} v_{i}+k_{2} v_{i}^{2}+k_{3} v_{i}^{3}+k_{4} v_{i}^{4}+\cdots \tag{14.48}
\end{equation*}
$$

where $\mathrm{k}_{\mathrm{i}}$ are constant terms. In this case, the differential output signal, $\mathrm{v}_{\text {diff }}$, consists of only the linear term, $2 \mathrm{k}_{1} \mathrm{v}_{1}$, and odd-order distortion terms (which are typically smaller than the second-order term). With these two important advantages, most modern switched-capacitor circuits are realized using fully differential structures.

A fully differential realization of the first-order filter is shown in Fig. 14.21. Note here that the fully differential version is essentially two copies of the single-ended version, which might lead one to believe that it would consume twice the amount of integrated area. Fortunately, the increased area penalty is not that high. First, we see that only one opamp is needed although it does require extra common-mode feedback circuitry. Second, note that the input and output signal swings have now been doubled in size. For example, if singleended
image_name:Fig. 14.20
description:The block diagram in Fig. 14.20 illustrates a system designed to demonstrate the cancellation of even-order distortion terms in fully differential circuits when the distortion is symmetrical around the common-mode voltage. The system consists of the following key components:

1. **Nonlinear Elements**: There are two nonlinear elements in the system. The first nonlinear element receives an input voltage $v_1$, and the second receives an inverted input voltage $-v_1$.
- The output from the first nonlinear element is labeled as $v_{p1}$, which is expressed as a power series: $v_{p1} = k_1 v_1 + k_2 v_1^2 + k_3 v_1^3 + k_4 v_1^4 + \ldots$.
- The output from the second nonlinear element is labeled as $v_{n1}$, which is also expressed as a power series but with alternating signs: $v_{n1} = -k_1 v_1 + k_2 v_1^2 - k_3 v_1^3 + k_4 v_1^4 + \ldots$.

2. **Summation Node**: The outputs from the two nonlinear elements are fed into a summation node.
- The summation node combines these outputs by subtracting $v_{n1}$ from $v_{p1}$, resulting in a differential output $v_{diff}$.
- The expression for $v_{diff}$ is simplified to $v_{diff} = 2k_1 v_1 + 2k_3 v_1^3 + 2k_5 v_1^5 + \ldots$, indicating that even-order terms cancel out.

3. **Function and Signal Flow**:
- The primary function of this system is to show that even-order distortion terms are canceled in a fully differential configuration. This is achieved by symmetrically processing the input signal and its inverted counterpart through nonlinear elements and then combining the results.
- The signal flow begins with the input voltage $v_1$ and its inversion, which are processed through the nonlinear elements. The outputs are then combined at the summation node to produce the differential output $v_{diff}$.

Overall, the diagram effectively demonstrates how fully differential circuits can eliminate even-order distortion terms, enhancing signal integrity by focusing on odd-order distortions only.

Fig. 14.20 Demonstrating that even-order distortion terms cancel in fully differential circuits if the distortion is symmetrical around the common-mode voltage. Here, the common-mode voltage is assumed to be zero.
image_name:Fig. 14.21 A fully differential first-order switched-capacitor filter
description:The circuit is a fully differential first-order switched-capacitor filter. It uses capacitors C1, C2, C3, and CA, and an operational amplifier A1 to process differential input signals Vi(z)+ and Vi(z)-, producing differential output signals Vo(z)+ and Vo(z)-. The circuit employs switches controlled by clock phases φ1 and φ2 to alternate connections.

Fig. 14.21 A fully differential first-order switched-capacitor filter.
signals are restricted to $\pm 1 \mathrm{~V}$, then the maximum peak-to-peak signal swing of sin-gle-ended signals is 2 V , while for differential signals it is 4 V . Thus, to maintain the same dynamic range due to $(\mathrm{kT}) / \mathrm{C}$ noise, the capacitors in the fully differential version can be half the size of those in the single-ended case. ${ }^{3}$ Since smaller capacitors can be used, the switch size widths may also be reduced to meet the same set-tling-time requirement. However, the fully differential circuit has more switches and wiring so this circuit will be somewhat larger than its single-ended counterpart, although if properly designed it should be significantly less than two times larger. Moreover, recall that the fully differential circuit has the advantages of rejecting much more common-mode noise and better distortion performance.

Key Point: Although fully-differential circuit implementations require some overhead for additional wiring and commonmode feedback circuitry, if properly designed the overhead should represent a small fraction of the overall circuit.

## 14.5 BIQUAD FILTERS

Similar to the first-order case, good switched-capacitor biquad filter structures can be obtained by emulating wellknown continuous-time filter structures. However, also as in the first-order case, once a filter structure is obtained, its precise frequency response is determined through the use of discrete-time analysis using the signal-flow-graph technique discussed in Section 14.2.4. This exact transfer function, or a close approximation to it, is then used when determining capacitor ratios during the design phase.

### 14.5.1 Low-Q Biquad Filter

A direct-form continuous-time biquad structure can be obtained by rewriting the general biquad transfer function, $\mathrm{H}_{\mathrm{a}}(\mathrm{s})$, as follows:

[^2]\$\$

$$
\begin{equation*}
\mathrm{H}_{\mathrm{a}}(\mathrm{~s}) \equiv \frac{\mathrm{V}_{\text {out }}(\mathrm{s})}{\mathrm{V}_{\text {in }}(\mathrm{s})}=-\frac{\mathrm{k}_{2} \mathrm{~s}^{2}+\mathrm{k}_{1} \mathrm{~s}+\mathrm{k}_{0}}{\mathrm{~s}^{2}+\left(\frac{\omega_{0}}{\mathrm{Q}}\right) \mathrm{s}+\omega_{0}^{2}} \tag{14.49}
\end{equation*}
$$

\$\$

Here, $\omega_{0}$ and Q are the pole frequency and pole Q , respectively, whereas $\mathrm{k}_{0}, \mathrm{k}_{1}$, and $\mathrm{k}_{2}$ are arbitrary coefficients that place this biquad's zeros (i.e., the numerator's roots). Multiplying through by the denominators and dividing by $\mathrm{s}^{2}$, (14.49) can be written as

$$
\begin{equation*}
V_{\text {out }}(s)=\left[-k_{2}-\frac{k_{1}}{s}\right] V_{\text {in }}(s)-\frac{\omega_{0}}{Q s} V_{\text {out }}(s)-\frac{k_{0}}{s^{2}} V_{\text {in }}(s)-\frac{\omega_{0}^{2}}{s^{2}} V_{\text {out }}(s) \tag{14.50}
\end{equation*}
$$

Finally, (14.50) can be expressed as two integrator-based equations. Specifically,

$$
\begin{equation*}
\mathrm{V}_{\mathrm{c} 1}(\mathrm{~s}) \equiv-\frac{1}{\mathrm{~s}}\left[\frac{\mathrm{~K}_{0}}{\omega_{0}} \mathrm{~V}_{\text {in }}(\mathrm{s})+\omega_{0} \mathrm{~V}_{\text {out }}(\mathrm{s})\right] \tag{14.51}
\end{equation*}
$$

and

$$
\begin{equation*}
\mathrm{V}_{\text {out }}(\mathrm{s})=-\frac{1}{\mathrm{~s}}\left[\left(\mathrm{k}_{1}+\mathrm{k}_{2} \mathrm{~s}\right) \mathrm{V}_{\text {in }}(\mathrm{s})+\frac{\omega_{0}}{\mathrm{Q}} \mathrm{~V}_{\text {out }}(\mathrm{s})-\omega_{0} \mathrm{~V}_{\mathrm{cl}}(\mathrm{~s})\right] \tag{14.52}
\end{equation*}
$$

A signal-flow-graph describing the preceding two equations is shown in Fig. 14.22.
Now, allowing negative resistors to be used, an active-RC realization of this general biquad signal-flow-graph is shown in Fig. 14.23 [Brackett, 1978]. Note that for convenience the integrating capacitors, $C_{A}$ and $C_{B}$, have been set to unity.

A switched-capacitor biquad based on this active-RC circuit can be realized as shown in Fig. 14.24 [Martin, 1979]. Here, all positive resistors were replaced with delay-free feed-in switched-capacitor stages while the negative resistor was replaced with a delaying feed-in stage. The switched-capacitor circuit has redundant switches, as switch sharing has not yet been applied.

The input capacitor $\mathrm{K}_{1} \mathrm{C}_{1}$ is the major signal path when realizing low-pass filters; the input capacitor $\mathrm{K}_{2} \mathrm{C}_{2}$ is the major signal path when realizing bandpass filters; whereas, the input capacitor $\mathrm{K}_{3} \mathrm{C}_{2}$ is the major signal path when realizing high-pass filters.

Before proceeding, it is worth mentioning that while this switched-capacitor filter is a natural result when using single-ended circuits, the use of fully differential circuits could result in quite a few other circuits, some of which could have poor performance properties. For example, all the positive resistors could be replaced with delay-free feed-in stages as before, but in addition, the negative resistor could also be replaced with a delay-free
image_name:Fig. 14.22
description:The diagram in Fig. 14.22 represents a signal-flow-graph of a general continuous-time biquad filter. This filter is designed to process an input signal \( V_{in}(s) \) and produce an output signal \( V_{out}(s) \). The main components and flow of information in the diagram are as follows:

1. **Main Components:**
- **Summing Junctions:** There are two summing junctions in the diagram. The first summing junction combines the input signal \( V_{in}(s) \) with a feedback signal scaled by \( k_0/\omega_0 \). The second summing junction combines signals including feedback components and the output of the first integrator.
- **Integrators (\(-1/s\)):** Two integrators are present, each represented by a block labeled \(-1/s\). These integrators process the signals by integrating over time, effectively serving as low-pass filters.
- **Feedback Paths:** Several feedback paths are present in the diagram, indicating a complex interaction between the components to achieve the desired filter characteristics.

2. **Flow of Information or Control:**
- The input signal \( V_{in}(s) \) enters the first summing junction, where it is combined with a feedback signal scaled by \( k_0/\omega_0 \).
- The output of the first summing junction is then integrated by the first integrator \(-1/s\), producing an intermediate signal \( V_{c1}(s) \).
- This intermediate signal is fed back to the second summing junction and also contributes to the output signal \( V_{out}(s) \) after further processing.
- The second summing junction receives additional feedback signals scaled by \( \omega_0 \) and \( \omega_0/Q \), which are combined with \( V_{c1}(s) \) and then integrated by the second integrator.
- The output of the second integrator contributes to the final output signal \( V_{out}(s) \).

3. **Labels, Annotations, and Key Indicators:**
- The diagram includes labels such as \( k_0/\omega_0 \), \( \omega_0 \), \( \omega_0/Q \), and \( k_1 + k_2s \), which indicate scaling factors and feedback paths crucial for the filter's operation.
- The signal \( V_{c1}(s) \) is labeled at the output of the first integrator, indicating its role as an intermediate signal in the filter process.

4. **Overall System Function:**
- The primary function of this system is to act as a continuous-time biquad filter, which can be configured to perform various filtering tasks such as low-pass, high-pass, band-pass, or band-stop filtering, depending on the values of the parameters like \( k_0 \), \( \omega_0 \), \( Q \), \( k_1 \), and \( k_2 \). The arrangement of integrators and summing junctions, along with the feedback paths, allows for precise control over the filter's frequency response and quality factor \( Q \).
image_name:Fig. 14.23
description:The diagram is a signal-flow-graph representation of a general continuous-time biquad filter. It illustrates the flow of signals through various summing junctions and integrators, with feedback and feedforward paths characterized by parameters such as \(k_0/\omega_0\), \(\omega_0\), \(\omega_0/Q\), \(k_1 + k_2s\), and \(-\omega_0\). The input is \(V_{in}(s)\) and the output is \(V_{out}(s)\).
image_name:Fig. 14.24
description:
[
name: 1/s, type: Other, ports: {N1: Vc1(s), N2: Vout(s)}
name: -1/s, type: Other, ports: {N1: Vc1(s), N2: Vout(s)}
]
extrainfo:The diagram represents a signal-flow-graph of a low-Q switched-capacitor biquad filter. It includes integrators and summing nodes with feedback paths characterized by constants k0/ω0, ω0, -ω0, ω0/Q, and k1 + k2s. The input is Vin(s) and the output is Vout(s).

Fig. 14.22 A signal-flow-graph representation of a general continuous-time biquad filter.
image_name:Fig. 14.23
description:The circuit is an active-RC realization of a general continuous-time biquad filter. It includes two operational amplifiers, integrating capacitors, and various resistors to set the filter characteristics. The filter processes an input signal Vin(s) to produce an output Vout(s). The resistors define parameters such as cutoff frequency and quality factor.

Fig. 14.23 An active-RC realization of a general continuous-time biquad filter.
image_name:Fig. 14.24
description:The circuit is a low-Q switched-capacitor biquad filter. It is designed without switch sharing and includes two operational amplifiers, capacitors, and switches. The filter processes an input signal Vi(z) to produce an output Vo(z). The switches and capacitors are used to implement the filter's characteristics.

Fig. 14.24 A low-Q switched-capacitor biquad filter (without switch sharing).
feed-in stage where the differential input wires are interchanged. Such a circuit would have a delay-free loop around the two integrators and may have an excessive settling time behavior. As another example, all resistors might be replaced with delaying feed-in stages where positive resistors are realized by interchanging the input wires of those stages. In this case, settling time behavior would not suffer as there would be two delays around the two-integrator loop, but coefficient sensitivity would be worse for filters having high-Q poles. In summary, what is important is that the two-integrator loop have a single delay around the loop. Such an arrangement is referred to as using lossless discrete integrators (LDI) [Bruton, 1975].

Using the approach presented in Section 14.2.4, the signal-flow-graph for the biquad circuit shown in Fig. 14.24 can be found and is shown in Fig. 14.25. The transfer function, $H(z)$, for this signal-flow-graph is found to be given by

$$
\begin{equation*}
\mathrm{H}(\mathrm{z}) \equiv \frac{\mathrm{V}_{0}(\mathrm{z})}{\mathrm{V}_{\mathrm{i}}(\mathrm{z})}=-\frac{\left(\mathrm{K}_{2}+\mathrm{K}_{3}\right) \mathrm{z}^{2}+\left(\mathrm{K}_{1} \mathrm{~K}_{5}-\mathrm{K}_{2}-2 \mathrm{~K}_{3}\right) \mathrm{z}+\mathrm{K}_{3}}{\left(1+\mathrm{K}_{6}\right) \mathrm{Z}^{2}+\left(\mathrm{K}_{4} \mathrm{~K}_{5}-\mathrm{K}_{6}-2\right) \mathrm{Z}+1} \tag{14.53}
\end{equation*}
$$

image_name:Fig. 14.25
description:The system block diagram, labeled as Fig. 14.25, represents a signal-flow graph of a switched-capacitor circuit. This diagram is designed to implement a discrete-time biquad transfer function. Here's a breakdown of the diagram:

1. **Main Components:**
- **Summing Junctions:** There are two main summing junctions in the diagram. The first summing junction combines the input signal \(V_i(z)\) with feedback and feedforward paths.
- **Delay Elements:** Two blocks labeled \(\frac{1}{1-z^{-1}}\) represent integrators or unit delay elements, which are characteristic of digital filter implementations.
- **Gain Blocks:** Multiple gain blocks with coefficients \(-K_1\), \(-K_2\), \(-K_3(1-z^{-1})\), \(-K_4\), \(-K_5z^{-1}\), and \(-K_6\) are present, controlling the amplification or attenuation of the signals.

2. **Flow of Information or Control:**
- The input signal \(V_i(z)\) enters the system and is affected by the gain \(-K_1\). This signal is then summed with other signals at the first summing junction.
- The output of the first summing junction flows into the first delay element \(\frac{1}{1-z^{-1}}\), creating an intermediate signal \(V_1(z)\).
- \(V_1(z)\) is then multiplied by \(-K_5z^{-1}\) and fed into the second summing junction.
- Feedback paths include signals multiplied by \(-K_4\) and \(-K_6\), which are routed back to the summing junctions.
- A feedforward path from the input includes \(-K_2\) and \(-K_3(1-z^{-1})\), directly affecting the summing junctions.
- The output \(V_o(z)\) is taken after the second delay element and summing junction.

3. **Labels, Annotations, and Key Indicators:**
- The diagram is annotated with gain values and signal labels such as \(V_i(z)\) for the input and \(V_o(z)\) for the output.
- Intermediate signals like \(V_1(z)\) are clearly labeled to indicate their roles within the system.

4. **Overall System Function:**
- The primary function of this system is to implement a discrete-time biquad filter. The arrangement of summing junctions, gain elements, and delay blocks creates a specific transfer function \(H(z)\), which is defined by the provided equation. This function is used to achieve desired filtering characteristics in a digital signal processing application.

Fig. 14.25 A signal-flow-graph describing the switched-capacitor circuit in Fig. 14.24.

While the preceding relation is useful for analyzing the switched-capacitor circuit shown, this relation can also be used during design of a desired transfer function. Assuming the desired discrete-time biquad transfer function has been found using a digital-filter design program, and is given by

$$
\begin{equation*}
H(z)=-\frac{a_{2} z^{2}+a_{1} z+a_{0}}{b_{2} z^{2}+b_{1} z+1} \tag{14.54}
\end{equation*}
$$

we can equate the individual coefficients of $z$ in (14.53) and (14.54), resulting in the following design equations:

$$
\begin{gather*}
\mathrm{K}_{3}=\mathrm{a}_{0}  \tag{14.55}\\
\mathrm{~K}_{2}=\mathrm{a}_{2}-\mathrm{a}_{0}  \tag{14.56}\\
\mathrm{~K}_{1} \mathrm{~K}_{5}=\mathrm{a}_{0}+\mathrm{a}_{1}+\mathrm{a}_{2}  \tag{14.57}\\
\mathrm{~K}_{6}=\mathrm{b}_{2}-1  \tag{14.58}\\
\mathrm{~K}_{4} \mathrm{~K}_{5}=\mathrm{b}_{1}+\mathrm{b}_{2}+1 \tag{14.59}
\end{gather*}
$$

There is some flexibility in choosing the values of $\mathrm{K}_{1}, \mathrm{~K}_{4}$, and $\mathrm{K}_{5}$. A single degree of freedom arises because specifying the overall transfer function, $\mathrm{H}(\mathrm{z})$, places no constraint on the size of the signal at the internal node, $\mathrm{V}_{1}(\mathrm{z})$. Thus, one way to choose appropriate capacitor values is to initially let $\mathrm{K}_{5}=1$ and determine other initial component values, find the signal levels that occur at nodes $\mathrm{V}_{1}(\mathrm{z})$ and $\mathrm{V}_{\mathrm{o}}(\mathrm{z})$, then using that signal level information, perform dynamic range scaling to find the final component values that result in similar signal swings at both nodes. Alternatively, the time constants of the two discrete-time integrators can be set equal by choosing

$$
\begin{equation*}
\mathrm{K}_{4}=\mathrm{K}_{5}=\sqrt{\mathrm{b}_{1}+\mathrm{b}_{2}+1} \tag{14.60}
\end{equation*}
$$

Such a choice usually results in a near optimal dynamically range-scaled circuit.
If it is desired to design the SC biquad so that its transfer function matches that of a continuous-time transfer function as closely as possible, then the approach used in Example 14.2 can be taken. Specifically, (14.53) can be rewritten as

$$
\begin{equation*}
\mathrm{H}(\mathrm{z}) \equiv \frac{\mathrm{V}_{0}(\mathrm{z})}{\mathrm{V}_{\mathrm{i}}(\mathrm{z})}=-\frac{\mathrm{K}_{1} \mathrm{~K}_{5}+\mathrm{K}_{2}\left(\mathrm{z}^{1 / 2}-\mathrm{z}^{-1 / 2}\right) \mathrm{z}^{1 / 2}+\mathrm{K}_{3}\left(\mathrm{z}^{1 / 2}-\mathrm{z}^{-1 / 2}\right)^{2}}{\mathrm{~K}_{4} \mathrm{~K}_{5}+\mathrm{K}_{6}\left(\mathrm{z}^{1 / 2}-\mathrm{z}^{-1 / 2}\right) \mathrm{z}^{1 / 2}+\left(\mathrm{z}^{1 / 2}-\mathrm{z}^{-1 / 2}\right)^{2}} \tag{14.61}
\end{equation*}
$$

Rewriting (14.15) and (14.16) here for convenience, we have

$$
\begin{equation*}
z^{1 / 2}=\cos \left(\frac{\omega T}{2}\right)+j \sin \left(\frac{\omega T}{2}\right) \tag{14.62}
\end{equation*}
$$

and

$$
\begin{equation*}
z^{-1 / 2}=\cos \left(\frac{\omega T}{2}\right)-j \sin \left(\frac{\omega T}{2}\right) \tag{14.63}
\end{equation*}
$$

Substituting these equations into (14.61) and rearranging gives

$$
\begin{equation*}
H\left(e^{j \omega T}\right) \equiv \frac{V_{0}\left(e^{j \omega T}\right)}{V_{i}\left(e^{j \omega T}\right)}=-\frac{K_{1} K_{5}+j K_{2} \sin (\omega T)+\left(4 K_{3}+2 K_{2}\right) \sin ^{2}\left(\frac{\omega T}{2}\right)}{K_{4} K_{5}+j K_{6} \sin (\omega T)+\left(4+2 K_{6}\right) \sin ^{2}\left(\frac{\omega T}{2}\right)} \tag{14.64}
\end{equation*}
$$

For $\omega \mathrm{T}<<1$, we further have

$$
\begin{equation*}
H\left(e^{j \omega T}\right) \equiv \frac{V_{0}\left(e^{j \omega T}\right)}{V_{i}\left(e^{j \omega T}\right)} \approx-\frac{\mathrm{K}_{1} \mathrm{~K}_{5}+j \mathrm{~K}_{2}(\omega T)+\left(\mathrm{K}_{3}+\mathrm{K}_{2} / 2\right)(\omega \mathrm{T})^{2}}{\mathrm{~K}_{4} \mathrm{~K}_{5}+\mathrm{j} \mathrm{~K}_{6}(\omega \mathrm{~T})+\left(1+\mathrm{K}_{6} / 2\right)(\omega \mathrm{T})^{2}} \tag{14.65}
\end{equation*}
$$

The coefficients of (14.65) can be matched to the desired coefficients of the continuous-time transfer function. A closer matching between transfer functions can be obtained if one chooses capacitor ratios to match the real and imaginary parts of both the numerators and denominators of (14.64) and the desired continuous-time transfer function at the resonant frequency, as is outlined in [Martin, 1980].

Finally, an estimate of the largest to smallest capacitance ratio can be made by using the resistor approximation (14.5) for this switched-capacitor circuit. Comparing Fig. 14.23 and Fig. 14.24 and using (14.5), we see the following approximations are valid for the feedback capacitor ratios, $\mathrm{K}_{4}, \mathrm{~K}_{5}$, and $\mathrm{K}_{6}$ (the capacitor ratios that determine the pole locations).

$$
\begin{gather*}
\mathrm{K}_{4} \cong \mathrm{~K}_{5} \cong \omega_{0} T  \tag{14.66}\\
\mathrm{~K}_{6} \cong \frac{\omega_{0} T}{\mathrm{Q}} \tag{14.67}
\end{gather*}
$$

However, the sampling rate, $1 / \mathrm{T}$, is typically much larger that the approximated pole frequency, $\omega_{0}$, resulting in

$$
\begin{equation*}
\omega_{0} \mathrm{~T}<<1 \tag{14.68}
\end{equation*}
$$

Thus, the largest capacitors (that determine the pole locations) in the switched-capacitor biquad circuit of Fig. 14.24 are the integrating capacitors, $\mathrm{C}_{1}$ and $\mathrm{C}_{2}$. Additionally, if $\mathrm{Q}<1$, then the smallest capacitors are $\mathrm{K}_{4} \mathrm{C}_{1}$ and $\mathrm{K}_{5} \mathrm{C}_{2}$, resulting in an approximate capacitance spread of $1 /\left(\omega_{0} T\right)$. However, if $\mathrm{Q}>1$, then from (14.67) the smallest capacitor would be $\mathrm{K}_{6} \mathrm{C}_{2}$, resulting in an approximate capacitance spread of $\mathrm{Q} /\left(\omega_{0} \mathrm{~T}\right)$.

### 14.5.2 High-Q Biquad Filter

The resultant high-capacitance spread in the preceding low-Q circuit, when $\mathrm{Q}>>1$, was a direct result of having a large damping resistance value of $Q / \omega_{0}$ in Fig. 14.23. One way to obtain a high-Q switched-capacitor circuit that does not have such a high capacitance spread is to eliminate this damping resistance in the continuous-time filter counterpart. Such an elimination can be accomplished by rewriting (14.50) as

$$
\begin{equation*}
V_{\text {out }}(\mathrm{s})=-\frac{1}{\mathrm{~s}}\left[\mathrm{k}_{2} \mathrm{~s} \mathrm{~V}_{\text {in }}(\mathrm{s})-\omega_{0} \mathrm{~V}_{\mathrm{cl} 1}(\mathrm{~s})\right] \tag{14.69}
\end{equation*}
$$

and

$$
\begin{equation*}
\mathrm{V}_{\mathrm{c} 1}(\mathrm{~s})=-\frac{1}{\mathrm{~s}}\left[\left(\frac{\mathrm{k}_{0}}{\omega_{0}}+\frac{\mathrm{k}_{1} \mathrm{~s}}{\omega_{0}}\right) \mathrm{V}_{\text {in }}(\mathrm{s})+\omega_{0} \mathrm{~V}_{\text {out }}(\mathrm{s})+\frac{\mathrm{s}}{\mathrm{Q}} \mathrm{~V}_{\text {out }}(\mathrm{s})\right] \tag{14.70}
\end{equation*}
$$

image_name:Fig. 14.26
description:The block diagram depicted in Fig. 14.26 represents an alternate realization for a general continuous-time biquad filter. This system utilizes a combination of integrators, summers, and feedback paths to achieve its filtering function.

Main Components:
1. **Summing Junctions (+):**
- There are two summing junctions in the diagram. The first summing junction combines the input signal \( V_{in}(s) \) with feedback and feedforward components.
- The second summing junction combines the output of the first integrator with another feedback component.

2. **Integrators (\(1/s\)):**
- Two integrators are present. The first integrator processes the output from the first summing junction, and the second integrator processes the output from the second summing junction.

3. **Feedback Paths:**
- The feedback paths include coefficients \( \omega_0 \), \( s/Q \), and \( k_2 s \). These feedback paths are crucial for adjusting the damping and frequency response of the filter.

4. **Feedforward Paths:**
- Coefficients \( k_0/\omega_0 \) and \( (k_1 s)/\omega_0 \) are used in the feedforward paths from the input to the first summing junction.

Flow of Information or Control:
- The input signal \( V_{in}(s) \) enters the system and is processed by the first summing junction, where it is combined with feedforward and feedback components.
- The output of the first summing junction is integrated, and the resulting signal is then sent to the second summing junction.
- The second summing junction combines this signal with additional feedback before it is integrated again.
- The final output \( V_{out}(s) \) is taken after the second integrator.
- Feedback paths from the output and intermediate points adjust the input to the summing junctions, controlling the system's response.

Labels, Annotations, and Key Indicators:
- **\( \omega_0 \):** Represents a frequency coefficient in the feedback path.
- **\( s/Q \):** Represents a damping coefficient, affecting the system's stability and transient response.
- **\( k_0/\omega_0 \), \( (k_1 s)/\omega_0 \), \( k_2 s \):** Coefficients that adjust the gain and frequency characteristics of the filter.

Overall System Function:
The system functions as a biquad filter, which is capable of implementing second-order filtering functions like low-pass, high-pass, band-pass, and band-stop filters. The arrangement of integrators, summing junctions, and feedback/feedforward paths allows for precise control over the filter's frequency response and damping characteristics. This configuration is particularly useful in continuous-time signal processing applications where active-RC implementations are required.

Fig. 14.26 An alternate realization for a general continuous-time biquad filter.
image_name:Fig. 14.26
description:This circuit is a continuous-time active-RC biquad filter, using op-amps A1 and A2 to achieve second-order filtering. It is configured for precise control over frequency response and damping characteristics. The filter includes resistors and capacitors to set the frequency and quality factor (Q) of the filter.

Fig. 14.27 An alternate realization of a general active-RC biquad filter.

The signal-flow-graph representation of these two equations is shown in Fig. 14.26. Note that here the damping path, $\mathrm{s} / \mathrm{Q}$ coefficient, passes through the first integrator stage and can be realized through the use of a capacitor, as shown in Fig. 14.27.

Once again, replacing resistors with appropriate switched-capacitor feed-in stages, the final high-Q switchedcapacitor biquad circuit is shown in Fig. 14.28 [Martin, 1980].

The input capacitor $\mathrm{K}_{1} \mathrm{C}_{1}$ is the major signal path when realizing low-pass filters, the input capacitor $\mathrm{K}_{2} \mathrm{C}_{1}$ is the major signal path when realizing bandpass filters, and the input capacitor $\mathrm{K}_{3} \mathrm{C}_{2}$ is the major signal path when realizing high-pass filters. Other possibilities for realizing different types of functions exist. For example, a nondelayed switched capacitor going from the input to the second integrator could also be used to realize an inverting bandpass function. If the phases on the input switches of such a switched capacitor were interchanged, then a noninverting bandpass function would result, but with an additional period delay.

Using the signal-flow-graph approach described in Section 14.2.4, the transfer function for this circuit is found to be given by

$$
\begin{equation*}
H(z) \equiv \frac{V_{0}(z)}{V_{i}(z)}=-\frac{K_{3} z^{2}+\left(K_{1} K_{5}+K_{2} K_{5}-2 K_{3}\right) \mathrm{z}+\left(\mathrm{K}_{3}-\mathrm{K}_{2} \mathrm{~K}_{5}\right)}{\mathrm{z}^{2}+\left(\mathrm{K}_{4} \mathrm{~K}_{5}+\mathrm{K}_{5} \mathrm{~K}_{6}-2\right) \mathrm{Z}+\left(1-\mathrm{K}_{5} \mathrm{~K}_{6}\right)} \tag{14.71}
\end{equation*}
$$

image_name:Fig. 14.28
description:The circuit is a high-Q switched-capacitor biquad filter without switch sharing. It includes two operational amplifiers, multiple switches, and capacitors arranged to form a filter with a specific transfer function. The switches are controlled by two clock phases, φ1 and φ2, which determine the timing of the switching events.

Fig. 14.28 A high-Q switched-capacitor biquad filter (without switch sharing).

Matching the coefficients of (14.71) to the coefficients of a discrete-time transfer function given by ${ }^{4}$

$$
\begin{equation*}
H(z)=-\frac{a_{2} z^{2}+a_{1} z+a_{0}}{z^{2}+b_{1} z+b_{0}} \tag{14.72}
\end{equation*}
$$

the following equations result:

$$
\begin{align*}
\mathrm{K}_{1} \mathrm{~K}_{5} & =\mathrm{a}_{0}+\mathrm{a}_{1}+\mathrm{a}_{2}  \tag{14.73}\\
\mathrm{~K}_{2} \mathrm{~K}_{5} & =\mathrm{a}_{2}-\mathrm{a}_{0}  \tag{14.74}\\
\mathrm{~K}_{3} & =\mathrm{a}_{2}  \tag{14.75}\\
\mathrm{~K}_{4} \mathrm{~K}_{5} & =1+\mathrm{b}_{0}+\mathrm{b}_{1}  \tag{14.76}\\
\mathrm{~K}_{5} \mathrm{~K}_{6} & =1-\mathrm{b}_{0} \tag{14.77}
\end{align*}
$$

As for the low-Q biquad, we see that there is some freedom in determining the coefficients as there is one less equation than the number of coefficients. A reasonable first choice might be to take

$$
\begin{equation*}
\mathrm{K}_{4}=\mathrm{K}_{5}=\sqrt{1+\mathrm{b}_{0}+\mathrm{b}_{1}} \tag{14.78}
\end{equation*}
$$

after which all other ratios follow. This will give a good dynamic range but not necessarily optimum. After the biquad has been designed, it can be analyzed and the ratios adjusted to equalize the maximum signal strength at the two opamp outputs.

#### EXAMPLE 14.5

The following transfer function describes a bandpass filter having a peak gain of 5 near $f_{s} / 10$ and a $Q$ of about 10 .

$$
\begin{equation*}
H(z)=-\frac{0.288(z-1)}{z^{2}-1.572 z+0.9429} \tag{14.79}
\end{equation*}
$$

Find the largest to smallest capacitor ratio if this transfer function is realized using the high- Q biquad circuit. Compare the results to those which would be obtained if the low- $Q$ circuit were used instead. Let $C_{1}=C_{2}=1$ in both cases.

#### Solution

For the high- Q biquad circuit, making use of (14.73) to (14.76) and assuming $\mathrm{K}_{4}=\mathrm{K}_{5}$ results in the following capacitor values.

$$
\begin{aligned}
\mathrm{K}_{4} & =\mathrm{K}_{5}=0.6090 \\
\mathrm{~K}_{1} & =0 \\
\mathrm{~K}_{2} & =0.4729 \\
\mathrm{~K}_{3} & =0 \\
\mathrm{~K}_{6} & =0.0938
\end{aligned}
$$

Recalling that $C_{1}=C_{2}=1$, in this high- $Q$ circuit the smallest capacitor is $K_{6} C_{1}$, which makes the capacitance spread about 11 to 1 .

For the low-Q biquad circuit design, we first rewrite (14.79) as

$$
\begin{equation*}
H(z)=-\frac{0.3054(z-1) z}{1.0606 z^{2}-1.667 z+1} \tag{14.80}
\end{equation*}
$$

which makes applying equations (14.55) to (14.60) easier. In addition, an extra zero at $\mathbf{z}=0$ was added to avoid negative capacitances. This extra zero does not change the magnitude response.

We obtain the following ratios assuming $\mathrm{K}_{4}=\mathrm{K}_{5}$ :

$$
\begin{align*}
\mathrm{K}_{4} & =\mathrm{K}_{5}=0.6274  \tag{14.81}\\
\mathrm{~K}_{1} & =0  \tag{14.82}\\
\mathrm{~K}_{2} & =0.3054  \tag{14.83}\\
\mathrm{~K}_{3} & =0  \tag{14.84}\\
\mathrm{~K}_{6} & =0.0606 \tag{14.85}
\end{align*}
$$

Thus the capacitance ratio for this circuit is determined by $\mathrm{K}_{6}$, which primarily sets the accuracy of the pole-Q factor, resulting in a spread of near 17. It should be noted here that worse capacitance spreads will occur for this low- $Q$ circuit if the pole $Q$ is higher and/or the sampling frequency is increased relative to the passband edge.

Key Point: Several different discrete-time biquads can be realized by varying the type (i.e., delayed, delay-free) and exact connection of switched-capacitor branches within a two-integrator loop. The choice of which biquad to use depends upon the specific pole and zero locations sought.

There are many other biquadratic stages than the two presented here. For example, a general stage capable of realizing any $\mathbf{z}$-transform is described in [Laker, 1994]. However, the authors have found that for the great majority of filtering applications, the choice of the circuits of either Fig. 14.24 or Fig. 14.28 (with switch sharing) is nearly optimum. The exception to this is for phase equalizers, where often feed-ins approximating negative resistors are needed. To realize higher-order switched-capacitor filters, one can cascade a number of biquad and/or first-order stages. Alternatively, one can use lower-sensitivity techniques such as signal-flow-graph
simulations of the relationships between the state variables of passive doubly terminated LC ladder filters. The interested reader is referred to [Gregorian, 1986] for detailed descriptions on the design of high-order SC filters.

## 14.6 CHARGE INJECTION

As seen in Chapter 10, comparators that make use of switches suffer from charge-injection errors. Fortunately, by turning off certain switches first, the charge-injection errors of the overall circuit are due to only those early switches. This same result applies to switched-capacitor circuits, and thus charge-injection effects can be minimized by having some clock signals slightly advanced with respect to the remaining signals. Which clock signals should be advanced is most easily explained with the following example.

Consider the first-order switched-capacitor filter shown in Fig. 14.29, where switch sharing is used. Here, $\phi_{1 \mathrm{a}}$ and $\phi_{2 a}$ are slightly advanced with respect to the remaining clock signals for the following reasons. First, since $\phi_{2 \mathrm{a}}$ is always connected to ground while $\phi_{1 \mathrm{a}}$ is always connected to virtual ground, when these switches are turned on they need only pass a signal near the ground node (not rail-to-rail signals as might occur at opamp outputs). Thus, these two switches can be realized using single n -channel transistors rather than full CMOS transmission gates. ${ }^{5} \mathrm{~A}$ second, more important reason for using this clock arrangement is that the charge injections due to $Q_{3}, Q_{4}$ are not signal dependent, while those of $Q_{1}, Q_{6}$ are signal dependent. Specifically, we saw in Chapter 10 that the channel charge of an NMOS transistor in triode is given by

$$
\begin{equation*}
Q_{C H}=-W L C_{o x} V_{\text {eff }}=-W L C_{o x}\left(V_{G S}-V_{t}\right) \tag{14.86}
\end{equation*}
$$

Here, we see that the charge is related to the gate-source voltage as well as to the threshold voltage. When $\mathrm{Q}_{3}$ and $\mathrm{Q}_{4}$ are on, $\mathrm{V}_{\mathrm{GS}}=\mathrm{V}_{\mathrm{DD}}$, and since their source remains at zero volts, their threshold voltages also remain constant. As a result, the amount of charge injected by $\mathrm{Q}_{3}, \mathrm{Q}_{4}$ is the same from one clock cycle to the next and can be considered as a dc offset. Unfortunately, the same cannot be said of $\mathbf{Q}_{1}$ and $\mathbf{Q}_{6}$. For example, when $\mathbf{Q}_{1}$ is on, its channel charge is found from (14.86) to be

$$
\begin{equation*}
Q_{C H 1}=-W_{1} L_{1} C_{o x}\left(V_{D D}-V_{i}-V_{t n}\right) \tag{14.87}
\end{equation*}
$$

Thus, one portion of the channel charge is linearly related to $\mathrm{V}_{\mathrm{i}}$. However, its source voltage settles to $\mathrm{V}_{\mathrm{i}}$ and thus the transistor's threshold voltage changes in a nonlinear relationship (due to the bulk effect, assuming its substrate
image_name:Fig. 14.29
description:This is a first-order switched-capacitor circuit with a clock arrangement to reduce charge-injection effects. The switches Q3 and Q4 are turned off slightly earlier to minimize distortion due to charge injection. The circuit uses capacitors C1, C2, C3, and CA, and an operational amplifier A1 to process the input signal Vi(z) and produce the output signal Vo(z).

Fig. 14.29 A first-order switched-capacitor circuit with a clock arrangement to reduce charge-injection effects. $\phi_{1 a}$ and $\phi_{2 a}$ turn off $Q_{3}$ and $Q_{4}$ slightly early.

Key Point: To minimize distortion due to charge injection, switches connected to dcnodes, such as ground, are turned off in advance of other switches. Although there is still some charge injection, it is signal independent.
is set to a fixed voltage). As a result, $\mathrm{Q}_{\mathrm{CH} 1}$ has a linear and nonlinear relationship to $V_{i}$ and thus would cause a gain error and distortion if $Q_{1}$ were turned off early. Finally, while $Q_{2}$ and $Q_{5}$ would also inject constant charge from one cycle to the next, it is best not to add any unnecessary charge into the circuit so these switches are also not advanced.

In summary, to reduce the effects of charge injection in switched-capacitor circuits, realize all switches connected to ground or virtual ground as n -channel switches only, and turn off the switches near the virtual ground node of the opamps first. Such an approach will minimize distortion and gain error as well as keeping dc offset low.

#### EXAMPLE 14.6

Assuming an ideal opamp, estimate the amount of dc offset in the output of the circuit shown in Fig. 14.29 due to channel-charge injection (ignore overlap capacitance charge injection) when $C_{1}=0$ and $C_{2}=C_{A}=10 C_{3}=4 \mathrm{pF}$. Assume that switches $Q_{3}, Q_{4}$ are $n$-channel devices with a threshold voltage of $\mathrm{V}_{\mathrm{tn}}=0.45 \mathrm{~V}$, width of $\mathrm{W}=5 \mu \mathrm{~m}$, length of $\mathrm{L}=0.2 \mu \mathrm{~m}$, and $\mathrm{C}_{\mathrm{ox}}=8.5 \mathrm{fF} / \mu \mathrm{m}^{2}$. A power supply of 1.8 V is used, and the circuit's "ground" node is located at $\mathrm{V}_{\mathrm{DD}} / 2=0.9 \mathrm{~V}$.

#### Solution

The dc feedback around the opamp will keep the negative input of the opamp at $\mathrm{V}_{\mathrm{DD}} / 2=0.9 \mathrm{~V}$. From (14.86), we can calculate the amount of channel charge of $\mathrm{Q}_{3}, \mathrm{Q}_{4}$ (when on) to be

$$
\begin{equation*}
Q_{\mathrm{CH} 3}=Q_{\mathrm{CH} 4}=-(5 \mu \mathrm{~m})(0.2 \mu \mathrm{~m})\left(8.5 \mathrm{fF} / \mu \mathrm{m}^{2}\right)((1.8 \mathrm{~V}-0.9 \mathrm{~V})-0.45 \mathrm{~V})=-3.8 \mathrm{fC} \tag{14.88}
\end{equation*}
$$

All of the dc feedback current is charge transferred through the switched capacitor $C_{3}$. Thus, the charge being transferred through this capacitor must equal the charge injected by both $Q_{3}, Q_{4}$ (assuming the input is at zero volts and therefore does not contribute charge). The charge transfer into $C_{3}$ is given by

$$
\begin{equation*}
Q_{C_{3}}=-C_{3} v_{\text {out }} \tag{14.89}
\end{equation*}
$$

Now, we estimate that half the channel charges of $Q_{3}$ and $Q_{4}$ are injected to the virtual ground node by the following reasoning. When $\phi_{1 a}$ turns off, half the channel charge of $Q_{4}$ goes into the virtual ground while half of its charge is placed at the node between $Q_{3}$ and $Q_{4}$. When $\phi_{2 a}$ goes high, the second charge escapes to ground, but when $\phi_{2 a}$ goes low, half of its channel charge is left between $Q_{3}$ and $Q_{4}$ and is passed into the virtual ground when $\phi_{1 a}$ goes high again. As a result, we can write the following charge equation,

$$
\begin{equation*}
\frac{1}{2}\left(Q_{\mathrm{CH} 3}+Q_{C H 4}\right)=Q_{C_{3}} \tag{14.90}
\end{equation*}
$$

which can be used to find $Q_{\mathrm{C}_{3}}$, and hence the output voltage from (14.89)

$$
\begin{equation*}
\mathrm{v}_{\text {out }}=\frac{3.8 \mathrm{fC}}{0.4 \mathrm{pF}}=9.5 \mathrm{mV} \tag{14.91}
\end{equation*}
$$

Thus, we see that this output dc offset value is affected by the size of capacitors used (in particular, $\mathrm{C}_{3}$ ) as well as the switch sizes and power-supply voltage. It should be mentioned here that if the dc input offset voltage of the opamp was included in the analysis, it would be multiplied by the dc gain of the circuit similar to that which occurs in an active-RC circuit.

Charge-injection is especially troublesome at higher frequencies. At higher frequencies, the time constant of the switch-on resistance and the capacitor being charged or discharged must be smaller; this necessitates larger switches for a given size capacitor and therefore greater charge-injection. It is possible to derive a very simple formula that gives an approximate upper bound on the frequency of operation of an SC circuit for a specified maximum voltage change due to charge injection. This upper bound takes into account switch channel charge only and ignores charge injection due to overlap capacitance.

Key Point: Charge injection is most problematic at high switching speeds where low switch on resistances demand wide transistors and small capacitors.

Most SC circuits will have two series switches for each capacitor. If one assumes that, for good settling, the sampling clock half-period must be greater than five time constants, then we have

$$
\begin{equation*}
\frac{\mathrm{T}}{2}>5 \mathrm{R}_{\mathrm{on}} \mathrm{C} \tag{14.92}
\end{equation*}
$$

where T is the sampling period, $\mathrm{R}_{\mathrm{on}}$ is the on resistance of the n -channel switch, and C is the capacitor. Equation (14.92) may be rewritten

$$
\begin{equation*}
\mathrm{f}_{\mathrm{clk}}<\frac{1}{10 \mathrm{R}_{\mathrm{on}} \mathrm{C}} \tag{14.93}
\end{equation*}
$$

where $\mathrm{f}_{\mathrm{clk}}=1 / \mathrm{T}$ is the clock frequency. Recalling (1.108) from Chapter 1, we have

$$
\begin{equation*}
\mathrm{R}_{\mathrm{on}}=\frac{1}{\mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}} \frac{\mathrm{~W}}{\mathrm{~L}} \mathrm{~V}_{\mathrm{eff}}} \tag{14.94}
\end{equation*}
$$

Also, using (14.87), the charge change due to the channel charge only caused by turning an n -channel switch off is approximated by

$$
\begin{equation*}
|\Delta \mathrm{V}|=\frac{\mathrm{Q}_{\mathrm{CH}}}{2 \mathrm{C}}=\frac{\mathrm{WLC}_{\mathrm{ox}} \mathrm{~V}_{\mathrm{eff}}}{2 \mathrm{C}} \tag{14.95}
\end{equation*}
$$

For a specified $|\Delta \mathrm{V}|_{\max }$, (14.95) implies that

$$
\begin{equation*}
\mathrm{C}=\frac{\mathrm{WLC}_{\mathrm{ox}} \mathrm{~V}_{\mathrm{eff}}}{2|\Delta \mathrm{~V}|_{\max }} \tag{14.96}
\end{equation*}
$$

Substituting (14.94) and (14.96) into (14.93) gives

$$
\begin{equation*}
\mathrm{f}_{\mathrm{clk}}<\frac{\mu_{\mathrm{n}}|\Delta \mathrm{~V}|_{\max }}{5 \mathrm{~L}^{2}} \tag{14.97}
\end{equation*}
$$

a very simple expression. Thus, the upper frequency limit to charge injection for SC circuits is inversely proportional to $L^{2}$ and is approximately independent of the size of capacitors or the power-supply voltages, assuming the switch sizes are chosen optimally; as technology improves, much higher switching frequencies are attainable. Finally, (14.97) ignores overlap capacitance, so it is somewhat optimistic and should be therefore considered an upper bound on the maximum clocking frequency.

Key Point: Technology scaling permits smaller transistors to offer the same on resistance, thereby reducing charge injection or, for the same charge injection, enabling higher switching frequencies.

#### EXAMPLE 14.7

Assuming the maximum voltage change due to clock feedthrough is 1 mV , what are the maximum clocking frequencies considering only channel charge injection for technologies having minimum channel lengths of $0.8 \mu \mathrm{~m}, 0.35 \mu \mathrm{~m}$, and $0.18 \mu \mathrm{~m}$ in Table 1.5?

#### Solution

Using (14.97) and carrier mobilities obtained from Table 1.5 gives $\mathrm{f}_{\mathrm{cl} \text { }}$, which must be less than $14.8 \mathrm{MHz}, 69 \mathrm{MHz}$, and 196 MHz , respectively, for the three different technologies. Notice the substantial increase in speed for SC circuits as the technology improves.

## 14.7 SWITCHED-CAPACITOR GAIN CIRCUITS

Perhaps the most common nonfiltering analog function is a gain circuit where the output signal is a scaled version of the input. In this section, we shall see that it is possible to realize accurate gain circuits by making use of switched-capacitor techniques. An important application of switched-capacitor gain circuits is in pipelined ana-log-to-digital converters. Specific switched-capacitor circuits that are popular for that application are presented in the chapter on Nyquist-rate A/D converters.

### 14.7.1 Parallel Resistor-Capacitor Circuit

In active-RC circuits, a gain circuit can be realized as parallel combinations of resistors and capacitors in both the feedback and feed-in paths, as shown in Fig. 14.30(a). One of the first switched-capacitor gain circuits uses a similar approach, where the two resistors have been replaced by their switched-capacitor equivalents, as shown in Fig. 14.30(b) [Foxall, 1980]. Using the signal-flow-graph technique of Section 14.2.4, straightforward analysis results in the transfer function for this switched-capacitor gain circuit being given by

$$
\begin{equation*}
H(z)=\frac{V_{\text {out }}(z)}{V_{\text {in }}(z)}=-K \tag{14.98}
\end{equation*}
$$

Unfortunately, this design will also amplify the $1 / \mathrm{f}$ noise and offset voltage of the shown opamp by K. However, it does have the advantage that its output is a continuous waveform that does not incur any large slew-rate requirement (as occurs in the resettable gain circuit discussed next).

### 14.7.2 Resettable Gain Circuit

The next configuration continuously resets an integrating capacitor on each clock cycle, as shown in Fig. 14.31 [Gregorian, 1981]. Here, the voltage across the integrating capacitor, $\mathrm{C}_{2}$, is cleared on each $\phi_{2}$, while on $\phi_{1}$ the input voltage charges $C_{1}$ and the charging current flows across $C_{2}$ at the same time. In this way, the change in charge across $C_{2}, \Delta Q_{C 2}$, equals the change in charge across $C_{1}, \Delta Q_{C 1}$, and therefore, at the end of $\phi_{1}$, the output voltage is related to the input voltage by $\mathrm{V}_{\text {out }} / \mathrm{V}_{\text {in }}=-\mathrm{C}_{1} / \mathrm{C}_{2}$.

In addition, this circuit stores any opamp input-offset voltage across the input and feedback capacitors. When the output is sampled by the succeeding circuit (during $\phi_{1}$ ), the effects of the input-offset voltage of the opamp are cancelled from the output voltage. The elimination of the opamp's input-offset voltage is important for two reasons. One reason is that if the offset voltage is not cancelled, it will also be amplified when the input signal is
image_name:(a)
description:
[
name: R2, type: Resistor, value: R2, ports: {N1: Vout(t), N2: InN(A1)}
name: R2/K, type: Resistor, value: R2/K, ports: {N1: Vin, N2: InN(A1)}
name: C1, type: Capacitor, value: C1, ports: {Np: Vout(t), Nn: InN(A1)}
name: KC1, type: Capacitor, value: KC1, ports: {Np: Vin, Nn: InN(A1)}
name: A1, type: OpAmp, value: A1, ports: {InP: GND, InN: InN(A1), OutP: Vout(t)}
]
extrainfo:The circuit diagram (a) shows an active-RC gain circuit. The output voltage is given by Vout(t) = -KVin(t), indicating an inverting amplifier configuration. The opamp input-offset voltage is stored across the input and feedback capacitors, cancelling it from the output voltage when sampled. This helps in reducing 1/f noise and preventing offset voltage amplification.
image_name:(b)
description:The circuit is a switched-capacitor gain circuit that cancels opamp input-offset voltage. During φ1, the output is sampled, and offset effects are canceled. This reduces 1/f noise and prevents offset voltage amplification.

Fig. 14.30 (a) An active-RC gain circuit. (b) An equivalent switched-capacitor ga in circuit.
image_name:Fig. 14.31
description:The circuit is a resettable gain circuit where the opamp offset voltage is cancelled. It reduces 1/f noise and prevents offset voltage amplification. The gain is determined by the ratio of capacitors C1 and C2, as expressed by the equation Vout(n) = -(C1/C2) * Vin(n). The switches operate in two phases, φ1 and φ2, to sample the input and cancel offset effects.

Fig. 14.31 A resettable gain circuit where opamp offset voltage is cancelled.
amplified and therefore can be troublesome. A second reason (and often more important) is that when the offset voltage is eliminated, $1 / \mathrm{f}$ noise is also reduced. As we saw in Chapter $9,1 / \mathrm{f}$ noise is large at low frequencies and can be a dominant noise source in many MOS circuits. However, when a circuit cancels dc offset voltages, the circuit has, in effect, a high-pass response from the opamp's input terminals to the output voltage. Thus, the 1/f noise is also high-pass filtered and hence reduced. It should be noted here that although there is a high-pass response from the opamp's input terminals to the output voltage, the

Key Point: Switchedcapacitor circuits can use a reset phase to sample and cancel dc offset and very low-frequency (1/f) noise without affecting the circuit's overall dc gain.
response from the overall circuits does not necessarily have a high-pass response.

To see this offset cancellation, consider the gain circuit during $\phi_{2}$ (i.e., when it is being reset) as shown in Fig. 14.32(a). The effect of the input offset voltage is being modelled as a voltage source, $\mathrm{V}_{\text {off }}$, which is placed in series
image_name:Fig. 14.32(a)
description:
[
name: C1, type: Capacitor, value: C1, ports: {Np: Voff, Nn: GND}
name: C2, type: Capacitor, value: C2, ports: {Np: Voff, Nn: GND}
name: A1, type: OpAmp, value: A1, ports: {InP: Voff, InN: Voff, OutP: Voff}
name: Voff, type: VoltageSource, value: Voff, ports: {Np: Voff, Nn: GND}
]
extrainfo:The circuit is a resettable gain circuit used during the reset phase (φ2) to sample and cancel DC offset and low-frequency noise. It includes capacitors C1 and C2, an op-amp A1, and a voltage source Voff to model the input offset voltage.

image_name:(b)
description:
[
name: C1, type: Capacitor, value: C1, ports: {Np: Vin(n), Nn: InN(A1)}
name: C2, type: Capacitor, value: C2, ports: {Np: InN(A1), Nn: Vout(n)}
name: A1, type: OpAmp, value: A1, ports: {InP: Voff, InN: InN(A1), OutP: Vout(n)}
name: Voff, type: VoltageSource, value: Voff, ports: {Np: Voff, Nn: GND}
]
extrainfo:The circuit is a resettable gain circuit used during the reset phase (φ2) to sample and cancel DC offset and low-frequency noise. It includes capacitors C1 and C2, an op-amp A1, and a voltage source Voff to model the input offset voltage. During φ2, both the voltages across C1 and C2 are equal to the op-amp offset voltage, Voff.

Fig. 14.32 The resettable gain circuit (a) during reset $\left(\phi_{2}\right)$, and (b) during valid output $\left(\phi_{1}\right)$.
with one of the opamp inputs. In this case, it is placed in series with the positive input, which results in the analysis being marginally simpler. During $\phi_{2}$, both the voltages across $\mathrm{C}_{1}$ and $\mathrm{C}_{2}$ are equal to the opamp offset voltage, $\mathrm{V}_{\text {off }}$. Next, during $\phi_{1}$ the circuit is configured as shown in Fig. 14.32(b), and at the end of $\phi_{1}$ the voltage across $C_{1}$ is given by $\mathrm{V}_{\mathrm{C}_{1}}(\mathrm{n})=\mathrm{V}_{\text {in }}(\mathrm{n})-\mathrm{V}_{\text {off }}$, while that for $\mathrm{C}_{2}$ is given by $\mathrm{V}_{\mathrm{C}_{2}}(\mathrm{n})=\mathrm{V}_{\text {out }}(\mathrm{n})-\mathrm{V}_{\text {off }}$. Therefore we can write,

$$
\begin{equation*}
\Delta Q_{C_{1}}=C_{1}\left[V_{C_{1}}(n)-\left(-V_{\text {off }}\right)\right]=C_{1} v_{\text {in }}(n) \tag{14.99}
\end{equation*}
$$

and

$$
\begin{equation*}
\mathrm{V}_{\mathrm{C}_{2}}(\mathrm{n})=\mathrm{V}_{\mathrm{C}_{2}}(\mathrm{n}-1 / 2)-\frac{\Delta \mathrm{Q}_{\mathrm{C}_{2}}}{\mathrm{C}_{2}} \tag{14.100}
\end{equation*}
$$

Since the voltage across $C_{2}$ one-half period earlier was $-V_{\text {off }}$ and $\Delta Q_{C 2}=\Delta Q_{C 1}$, we have

$$
\begin{equation*}
V_{\mathrm{C}_{2}}(\mathrm{n})=-\mathrm{V}_{\mathrm{off}}-\frac{\mathrm{C}_{1} \mathrm{~V}_{\mathrm{in}}(\mathrm{n})}{\mathrm{C}_{2}} \tag{14.101}
\end{equation*}
$$

Finally, since one side of $\mathrm{C}_{2}$ is connected to the virtual ground of the opamp, which is at $\mathrm{V}_{\text {off }}$, the output voltage is given by

$$
\begin{align*}
V_{\text {out }}(n) & =V_{\text {off }}+V_{C_{2}}(n) \\
& =V_{\text {off }}+\left(-V_{\text {off }}-\frac{C_{1} v_{\text {in }}(n)}{C_{2}}\right)  \tag{14.102}\\
& =-\left(\frac{C_{1}}{C_{2}}\right) v_{\text {in }}(n)
\end{align*}
$$

Thus, the output voltage is independent of the opamp offset voltage.
Note, however, that the output voltage is only valid during $\phi_{1}$, and it is equal to $\mathrm{V}_{\text {off }}$ during $\phi_{2}$, as shown in Fig. 14.33. The difficulty in realizing this waveform is that the opamp output must slew between ( $\left.-\mathrm{C}_{1} / \mathrm{C}_{2}\right) \mathrm{v}_{\mathrm{in}}$ and a voltage near 0 V each time the clock changes. Clearly, such a waveform requires a very high slew-rate opamp for proper operation.
image_name:Fig. 14.33
description:The graph in Fig. 14.33 is a time-domain waveform representing the output voltage, \( V_{out} \), of a resettable gain circuit over time. The x-axis is labeled "Time," and the y-axis is labeled "\( V_{out} \)," which represents the output voltage.

The waveform is periodic and consists of two distinct phases, \( \phi_1 \) and \( \phi_2 \), which repeat over time. During \( \phi_1 \), the output voltage increases linearly, indicating a period where the circuit is actively amplifying the input signal. This phase is characterized by a positive slope, suggesting a constant rate of increase in voltage.

During \( \phi_2 \), the output voltage abruptly drops to a lower level, \( V_{off} \), which is indicated on the graph. This phase represents a reset period where the output voltage is set to the offset voltage \( V_{off} \), effectively canceling any offset present in the opamp. The transition between \( \phi_1 \) and \( \phi_2 \) is sharp, requiring the opamp to have a high slew rate to transition quickly between these two states.

The waveform repeats this pattern, with the voltage rising during \( \phi_1 \) and resetting during \( \phi_2 \). The overall shape of the waveform is a series of sawtooth-like peaks corresponding to the active amplification phase and flat segments at \( V_{off} \) during the reset phase. This behavior underscores the design's focus on managing the opamp's offset voltage while maintaining a periodic gain cycle.

Fig. 14.33 An example output waveform for the resettable gain circuit.

Finally, note that a programmable gain circuit is easily realized by replacing $C_{1}$ with a programmable capacitor array ${ }^{6}$ (PCA) where the capacitor size is determined by digital signals.

### 14.7.3 Capacitive-Reset Gain Circuit

To eliminate the need for the opamp output to slew to approximately 0 V each clock period yet still cancel the opamp's offset voltage, a capacitive-reset gain circuit can be used. The basic idea of the gain circuit is to couple the opamp's output to the inverting input during the reset phase with a capacitor that has been previously charged to the output voltage. Thus, we shall see that one property of this gain circuit is that the opamp's output need only change by the opamp's offset voltage between clock phases. In addition, since the circuit is insensitive to the opamp's input offset voltage, it also reduces the effect of the opamp's 1/f noise. Finally, it can also be shown (see [Martin, 1987]) that for low-frequency inputs (or for inputs that are constant for at least two clock periods), the errors due to finite gain, A , of the opamp are proportional to $1 / A^{2}$ (rather than the usual $1 / A$ ). Such a result often allows the use of single-stage opamps that are very fast opamps.

The capacitive-reset gain circuit is shown in Fig. 14.34. Capacitor $\mathrm{C}_{4}$ is an optional "deglitching" capacitor [Matsumoto, 1987] used to provide continuous-time feedback during the nonoverlap clock times when all the
image_name:Fig. 14.34
description:The circuit is a switched-capacitor gain circuit with capacitive reset. It can operate as an inverting or non-inverting amplifier depending on the clock signals. The gain is determined by the ratio of capacitors C1 and C2, as shown in the equation: Vout(n) = -(C1/C2) * Vin(n). The optional capacitor C4 is used for deglitching during non-overlapping clock phases.

Fig. 14.34 A gain circuit using capacitive reset ( $C_{4}$ is an optional deglitching capacitor). Depending on the input-stage clock signals, the gain can be either inverting (as shown) or noninverting (input-stage clocks shown in parentheses).

[^3]switches are open. This deglitching technique works well and should be used on almost all switched-capacitor circuits that would otherwise have no feedback connection at some instant of time. This capacitor would normally be small (around 0.5 pF or less).

This gain circuit can be either inverting or noninverting depending on the clock phases of the input stage. While the inverting circuit creates its output as a delay-free version of the input, the output for the noninverting case would be one-half clock cycle behind the input signal.

To see how this capacitive-reset gain circuit operates, consider the inverting circuit during the reset phase of $\phi_{2}$, as shown in Fig. 14.35(a). We have assumed capacitor $\mathrm{C}_{3}$ was charged to the output voltage during the previous $\phi_{1}$ clock phase. Here we see that capacitors $\mathrm{C}_{1}$ and $\mathrm{C}_{2}$ are charged to the opamp's input-offset voltage, $\mathrm{V}_{\mathrm{off}}$, in the same manner as in the resettable gain circuit of Fig. 14.31. The next clock phase of $\phi_{1}$ is shown in Fig. 14.35(b), where we see that the output voltage is independent of the offset voltage in the same manner as the resettable gain circuit. In addition, we see that during $\phi_{1}$, capacitor $\mathrm{C}_{3}$ is charged to the output voltage. Before proceeding, it is of interest to note what happens to the charges on $C_{1}$ and $C_{2}$ when going from phase $\phi_{1}$ to $\phi_{2}$ (i.e., circuit (b) to (a) of Fig. 14.35). Since the charges on $\mathrm{C}_{1}$ and $\mathrm{C}_{2}$ are equal (recall that the charge on $\mathrm{C}_{2}$ was obtained during the charging of $C_{1}$ ), when one side of each of $C_{1}$ and $C_{2}$ are grounded, their charges cancel each other and no charge is dumped onto $\mathrm{C}_{3}$. Therefore, in the circuit of Fig. 14.35(a), the voltage on $\mathrm{C}_{3}$ remains equal to the previous output voltage as shown. It should be noted here that even if the two charges did not precisely cancel, it would only result in the output voltage moving slightly further away from the previous output voltage during $\phi_{2}$ but would not affect the output voltage during $\phi_{1}$.

Finally, this capacitive-reset gain circuit can also realize a differential-to-single-ended gain stage, as shown in Fig. 14.36. Note that the shown circuit indicates that the switches connected around the virtual grounds are disconnected slightly sooner than other switches to reduce nonlinearities due to charge injection. This circuit has a switched-capacitor circuit connected to the positive input of the opamp that not only accepts differential inputs but also, to a first-order approximation, cancels the clock feedthrough of the switches [Martin, 1982].
image_name:(a)
description:
[
name: C1, type: Capacitor, value: C1, ports: {Np: InN(A1), Nn: GND}
name: C2, type: Capacitor, value: C2, ports: {Np: InN(A1), Nn: GND}
name: C3, type: Capacitor, value: C3, ports: {Np: Vout(n-1)+Voff, Nn: InN(A1)}
name: A1, type: OpAmp, value: A1, ports: {InP: Voff, InN: InN(A1), OutP: Vout, OutN: Vout(n-1)+Voff}
name: V_off, type: VoltageSource, value: V_off, ports: {Np: Voff, Nn: GND}
]
extrainfo:The circuit is a differential-to-single-ended gain stage using capacitive reset. The circuit reduces nonlinearities due to charge injection by disconnecting switches around virtual grounds slightly sooner than others. It also cancels clock feedthrough of the switches to a first-order approximation.
image_name:(b)
description:
[
name: C1, type: Capacitor, value: C1, ports: {Np: Vin(n), Nn: InN(A1)}
name: C2, type: Capacitor, value: C2, ports: {Np: Vout(n), Nn: InN(A1)}
name: C3, type: Capacitor, value: C3, ports: {Np: Vout(n), Nn: GND}
name: A1, type: OpAmp, value: A1, ports: {InP: Voff, InN: InN(A1), OutP: Vout(n)}
name: Voff, type: VoltageSource, value: Voff, ports: {Np: Voff, Nn: GND}
]
extrainfo:The circuit is a differential-to-single-ended gain stage using capacitive reset. It includes a switched-capacitor circuit that helps cancel clock feedthrough and reduce nonlinearities. The output voltage is given by Vout(n) = -(C1/C2) * Vin(n).

Fig. 14.35 Capacitive-reset gain circuit. (a) During reset $\left(\phi_{2}\right)$ when the output remains near previous output level. (b) During valid output ( $\phi_{1}$ ) when no offset error is present.
image_name:Fig. 14.36
description:The circuit is a differential-to-single-ended gain stage using capacitive reset. It includes a switched-capacitor circuit that helps cancel clock feedthrough and reduce nonlinearities. The output voltage is given by Vout = (C1/C2) * (Vin+ - Vin-). The circuit uses correlated double sampling (CDS) to minimize errors due to finite offset voltages, 1/f noise, and finite opamp gain.

Fig. 14.36 A differential-to-single-ended gain circuit using capacitive reset.

## 14.8 CORRELATED DOUBLE-SAMPLING TECHNIQUES

The preceding SC gain amplifier is an example of using correlated double sampling (CDS) to minimize errors due to finite offset voltages, $1 / \mathrm{f}$ noise, and finite opamp gain. This technique is generally applicable to SC circuits of many different types [Temes, 1996]. It has been used to realize highly accurate gain amplifiers, sample and holds, and integrators. The basic methodology in all cases is similar: During a calibration phase, the finite input voltage of the opamp is sampled and stored across capacitors; during the operation phase (when the output is being sampled), this error voltage is subtracted from the signal voltage by appropriate switching of the capacitors. A detailed description of CDS techniques is beyond the scope of this text; rather, a couple of examples will be briefly described and the interested reader can consult the tutorial [Temes, 1996] for more information.

A wide-band amplifier that uses CDS, similar to the SC amplifier of Fig. 14.34, but with superior highfrequency operation, is shown in Fig. 14.37. During $\phi_{2}, \mathrm{C}_{1}^{\prime}$ and $\mathrm{C}_{2}^{\prime}$ are used to have

$$
\begin{equation*}
v_{\text {out }} \cong-\frac{\mathrm{C}_{1}^{\prime}}{\mathrm{C}_{2}^{\prime}} \mathrm{v}_{\text {in }} \tag{14.103}
\end{equation*}
$$

but with errors due to finite input-offset voltage, $1 / \mathrm{f}$ noise, and gain. At the same time, the finite opamp input voltage caused by these errors is sampled and stored across $\mathrm{C}_{1}$ and $\mathrm{C}_{2}$. Next, during $\phi_{1}$, this input error voltage is subtracted from the signal (applied to the opamp input) at that time. Assuming that the input voltage and the opamp input error voltages did not change appreciably from $\phi_{2}$ to $\phi_{1}$, errors due to them will be significantly reduced.

The technique can also be used to realize accurate integrators. For example, the SC integrator shown in Fig. 14.38 [Nagaraj, 1986; Ki, 1991] uses an additional capacitor, $\mathrm{C}_{2}^{\prime}$, to sample the opamp input error voltages during $\phi_{1}$. Next, during $\phi_{2}, \mathrm{C}_{2}^{\prime}$ is connected in series with the opamp's inverting input and greatly minimizes the effects of these errors (by a factor of the inverse of the opamp's gain over what would otherwise occur at frequencies substantially less than the sampling frequency). Similar architectures, with an open-loop capacitor in series with the opamp input during the phase when the output is sampled, can also be used for gain amplifiers.

When CDS sampling is used, the opamps should be designed to minimize thermal noise rather than $1 / \mathrm{f}$ noise. This might mean the use of n -channel input transistors rather than p -channel input transistors, for example.
image_name:Fig. 14.37 An SC amplifier with CDS
description:This circuit is a switched-capacitor (SC) amplifier with correlated double sampling (CDS) to minimize errors due to input-offset voltages, 1/f noise, and finite gain. The use of capacitors C1, C2, C1', and C2' along with the operational amplifier helps achieve this error minimization by sampling and holding the input signal.

Fig. 14.37 An SC amplifier with CDS to minimize errors due to input- offset voltages, $1 / f$ noise, and finite gain.
image_name:Fig. 14.37
description:This circuit is a switched-capacitor (SC) amplifier with correlated double sampling (CDS) to minimize errors due to input-offset voltages, 1/f noise, and finite gain. The use of capacitors C1, C2, C1', and C2' along with the operational amplifier helps achieve this error minimization by sampling and holding the input signal.

Fig. 14.38 An SC integrator with CDS to minimize errors due to input-offset voltages, $1 / f$ noise, and finite gain.

When this technique is used in high-order SC filters, often only a couple of stages will have low-frequency gain from the opamp input terminals to the filter outputs and will require CDS circuitry. Other integrators can be more simply realized. This technique has proven to be very useful in applications such as oversampling A/D converters, where accurate integrators are required in the first stage [Hurst, 1989; Rebeschini, 1989] to reduce input-offset voltages and especially $1 / \mathrm{f}$ noise.

## 14.9 OTHER SWITCHED-CAPACITOR CIRCUITS

In this section, we present a variety of other switched-capacitor circuits useful for nonlinear applications. Specifically, we look at an amplitude modulator, full-wave rectifier, peak detector, voltage-controlled oscillator, and sinusoidal oscillator.

### 14.9.1 Amplitude Modulator

Amplitude modulators are used to shift a signal along the frequency axis. For example, to shift an information signal, $\mathrm{m}(\mathrm{t})$, by a carrier frequency, $\omega_{\mathrm{ca}}$, we multiply $\mathrm{m}(\mathrm{t})$ by a sinusoidal signal of frequency, $\omega_{\mathrm{ca}}$, or mathematically,

$$
\begin{equation*}
y(t)=m(t) \times \cos \left(\omega_{c a} t\right) \tag{14.104}
\end{equation*}
$$

image_name:(a)
description:The circuit is a switched-capacitor square-wave modulator, where the input clock phases are controlled by a modulating square wave ϕM. The op-amp A1 is used to amplify the signal, and the circuit uses PMOS and NMOS transistors to switch the capacitors C1, C2, and C3 in response to the clock phases ϕ1 and ϕ2. The modulator shifts the input signal Vin along the frequency axis, as described by the mathematical expression y(t) = m(t) × cos(ωca t). The expressions for ϕA and ϕB indicate the phase control logic used in the modulator.
image_name:(b)
description:This is a switched-capacitor modulator circuit. The circuit uses NMOS transistors to switch the phases ϕA and ϕB, controlled by the carrier frequency ϕca. The circuit is part of an amplitude modulator system, shifting signals along the frequency axis.

Fig. 14.39 (a) A switched-capacitor square-wave modulator where the input clock phases are controlled by the modulating square wave $\phi_{\mathrm{M}}$. (b) A possible circuit realization for $\phi_{\mathrm{A}}$ and $\phi_{\mathrm{B}}$.

Since the Fourier transform of $\cos \left(\omega_{\mathrm{ca}} \mathrm{t}\right)$ is $\pi \delta\left(\omega-\omega_{\mathrm{ca}}\right)+\pi \delta\left(\omega+\omega_{\mathrm{ca}}\right)$, and multiplication in the time domain is equivalent to convolution in the frequency domain, one can show that the spectrum of $\mathrm{y}(\mathrm{t})$ is equal to

$$
\begin{equation*}
Y(\omega)=\frac{1}{2} M\left(\omega+\omega_{\mathrm{ca}}\right)+\frac{1}{2} M\left(\omega-\omega_{\mathrm{ca}}\right) \tag{14.105}
\end{equation*}
$$

Thus, the output spectrum only has power around $\pm \omega_{\text {ca }}$.
However, in many cases it is difficult to realize a sinusoidal signal as well as a linear multiplier. As a result, many modulators make use of a square-wave carrier signal, in which case the output signal is simply

$$
\begin{equation*}
\mathrm{y}(\mathrm{t})=\mathrm{m}(\mathrm{t}) \times \mathrm{S}_{\mathrm{q}}(\mathrm{t})= \pm \mathrm{m}(\mathrm{t}) \tag{14.106}
\end{equation*}
$$

where $\mathrm{S}_{\mathrm{q}}(\mathrm{t})$ is a square wave operating at the carrier frequency whose amplitude has been normalized to 1 . Thus, this approach simply requires a square-wave signal at the carrier frequency determining whether $m(t)$ or $-m(t)$ is passed to the output. The penalty paid here is that rather than $Y(\omega)$ having power located only around $\pm \omega_{\text {ca }}$, there will also be significant power around odd multiples of $\pm \omega_{\mathrm{ca}}$ since a square-wave signal has power at odd harmonics of the fundamental. These extra images can typically be tolerated through the use of additional filtering stages.

A square-wave modulator can be realized using switched-capacitor techniques, as shown in Fig. 14.39. Here, the modulator is realized by making use of the capacitive-reset gain stage of Fig. 14.34. Note that the polarity of the output signal is determined by changing the clock phases of the input-transistor pair through the use of $\phi_{\mathrm{A}}$ and $\phi_{\mathrm{B}}$, which are controlled by the square-wave carrier clock signal $\phi_{\mathrm{ca}}$. When $\phi_{\mathrm{ca}}$ is high, $\phi_{\mathrm{A}}=\phi_{2}$ and $\phi_{\mathrm{B}}=\phi_{1}$, which results in a noninverting output of $\left(\mathrm{C}_{1} / \mathrm{C}_{2}\right) \mathrm{v}_{\mathrm{in}}$. When $\phi_{\mathrm{ca}}$ goes low, the clock phases of $\phi_{\mathrm{A}}, \phi_{\mathrm{B}}$ switch, and the circuit produces an inverting output of $-\left(\mathrm{C}_{1} / \mathrm{C}_{2}\right) \mathrm{v}_{\text {in }}$.

### 14.9.2 Full-Wave Rectifier

A full-wave rectifier produces as its output the absolute value of the input. In other words, if the input is positive the output equals the input, but if the input is negative the output equals an inverted version of the input.

It is possible to realize a full-wave rectifier by making use of an amplitude modulator where, instead of a square-wave carrier signal being used, the output of a comparator controls the polarity of the output signal, as shown in Fig. 14.40. If the input signal is above ground, $\phi_{\text {ca }}$ goes high and the output is equal to a scaled version
of the input. If the input signal is below ground, $\phi_{\mathrm{ca}}$ goes low and the output equals an inverted scaled version of input. For proper operation, the comparator output must change synchronously with the sampling instances. Circuits to achieve this operation are given in [Gregorian, 1986].

### 14.9.3 Peak Detectors

image_name:Fig. 14.40
description:The circuit is a full-wave detector that uses a modulator and an op-amp comparator. The comparator generates a control signal phi_ca based on the input signal Vin, which is used to control the modulator. The output Vout is a full-wave rectified version of the input signal.

Fig. 14.40 A full-wave detector based on the square-wave modulator circuit of Fig. 14.39.

Peak detectors produce as their output the maximum value of an input signal over some time period. While peak detectors will normally have some decaying circuitry associated with them (or a circuit to reset the peak occasionally), here we shall just look at the peak detector circuit itself. Two methods for realizing peak detectors are shown in Fig. 14.41.

In Fig. 14.41(a), a latched comparator is used to determine when $v_{\text {in }}>v_{\text {out }}$. When such a condition occurs, the comparator output goes high and the switch $Q_{1}$ turns on, forcing $\mathrm{v}_{\text {out }}=\mathrm{v}_{\mathrm{in}}$. The comparator is latched here to maintain its speed as well as ensuring that the comparator output is either high or low. Note that this circuit requires that the input signal directly drives $C_{H}$ through $Q_{1}$, and hence buffering may be required. However, this circuit can be reasonably fast since latched comparators can be made to operate quickly and there is no opamp settling involved (only the RC time constant of $Q_{1}$ and $C_{H}$ ).

The circuit of Fig. 14.41(b) requires an opamp (with proper compensation), since it places $Q_{2}$ in a feedback connection. When $\mathrm{v}_{\text {in }}>\mathrm{v}_{\text {out }}$, the opamp output will start to go high, thus turning on $Q_{2}$ and hence turning on the feedback loop. While the feedback loop is on, the high loop gain will force $v_{\text {out }}=v_{\text {in }}$ with a high accuracy. Note that this circuit has a high input impedance as the input signal is applied to the noninverting terminal of an opamp. However, this opamp-based circuit will typically be slower than the comparator-based circuit of Fig. 14.41(a) since one needs to wait for the opamp output to slew and then settle. This slewing time can be minimized by adding circuitry to ensure that the gate of $Q_{2}$ never becomes lower than the output voltage when $Q_{2}$ is not conducting.

### 14.9.4 Voltage-Controlled Oscillator

A voltage-controlled oscillator (VCO) is an oscillator whose frequency can be adjusted through the use of a controlling voltage. As we shall see, the VCO described here generates an output square wave that places the oscillator
image_name:(a)
description:
[
name: A1, type: OpAmp, value: A1, ports: {InP: Vin, InN: Vout,OutP: Out(A1)}
name: Q1, type: NMOS, ports: {S: Vin, D: Vout,G:Out(A1)}
name: C_H, type: Capacitor, value: C_H, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit diagram (a) is a part of a voltage-controlled oscillator (VCO) using a comparator-based approach. The OpAmp is configured as a comparator, and the switch Q1 is controlled by the input voltage Vin. The capacitor CH is used to stabilize the output voltage Vout.
image_name:(b)
description:
[
name: A1, type: OpAmp, value: A1, ports: {InP: Vin, InN: Vout, OutP: Out(A1)}
name: Q2, type: NMOS, ports: {S: Vout, D: VDD, G: Out(A1)}
name: C_H, type: Capacitor, value: C_H, ports: {Np: Vout, Nn: GND}
]
extrainfo:This circuit is a voltage-controlled oscillator (VCO) with an operational amplifier and an NMOS transistor. The op-amp is configured to control the gate of the NMOS, and the capacitor is used to stabilize the output voltage. The VCO generates a square wave output.

Fig. 14.41 Two-peak detectors: (a) latched-comparator approach; (b) continuous-time approach.
alternatively in one of two states and is referred to as a relaxation oscillator. As we shall see in Chapter 19, a VCO is an integral part of a phase-locked loop (PLL).

The basic principle and typical waveforms of the relaxation oscillator are shown in Fig. 14.42 [Martin, 1981] and operate as follows. Assume that $\mathrm{v}_{\text {out }}$ has just toggled low to $-\mathrm{V}_{\mathrm{ss}}$ and node $\mathrm{v}_{\mathrm{x}}$ is now at a level quite a bit higher than zero. On $\phi_{1}, \mathrm{k}_{2} \mathrm{C}$ will be charged up to a voltage of $-\mathrm{V}_{\mathrm{Ss}}$, resulting in a charge value given by

$$
\begin{equation*}
\mathrm{Q}_{\mathrm{k}_{2} \mathrm{C}}=-\mathrm{k}_{2} C \mathrm{~V}_{\mathrm{Ss}} \tag{14.107}
\end{equation*}
$$

image_name:(a)
description:The circuit is a switched-capacitor relaxation oscillator. It uses MOSFETs and capacitors to generate a periodic waveform. The op-amp A1 acts as an integrator, while A2 functions as a comparator. The capacitors k1C, k2C, and C are used to store and transfer charge, controlling the oscillation frequency.

image_name:(b)
description:The graph shown is a time-domain waveform diagram associated with a switched-capacitor relaxation oscillator. It consists of two key waveforms plotted against time: \( V_x \) and \( V_{out} \).

1. **Type of Graph and Function:**
- This is a time-domain waveform graph illustrating voltage changes over time for the oscillator circuit.

2. **Axes Labels and Units:**
- The horizontal axis represents time, but no specific units are provided.
- The vertical axis represents voltage, with specific markers for \( V_x \) and \( V_{out} \).

3. **Overall Behavior and Trends:**
- **\( V_x \) waveform:** This waveform exhibits a staircase pattern, alternating between increasing and decreasing steps. The voltage increases to a peak labeled \( k_1(V_{DD} + V_{SS}) \), then decreases, with a smaller step size labeled \( k_2V_{SS} \) and \( k_2V_{DD} \), indicating charge transfer processes.
- **\( V_{out} \) waveform:** This waveform is a square wave, oscillating between \( V_{DD} \) and \(-V_{SS} \). The period of oscillation is marked as \( T_{osc} \).

4. **Key Features and Technical Details:**
- The staircase pattern in \( V_x \) reflects the integration and charge transfer dynamics of the oscillator, with the steps corresponding to the charge being transferred between capacitors.
- The square wave in \( V_{out} \) indicates a relaxation oscillation, with clear transitions between high and low states.

5. **Annotations and Specific Data Points:**
- The waveform for \( V_x \) includes annotations for the amplitude changes: \( k_1(V_{DD} + V_{SS}) \), \( k_2V_{SS} \), and \( k_2V_{DD} \).
- The square wave \( V_{out} \) is annotated with its oscillation period \( T_{osc} \), representing the time duration for a complete cycle of the waveform.
image_name:(b)
description:The graph consists of two time-domain waveforms, labeled as \( V_x \) and \( V_{out} \), plotted against time.

Upper Graph (\( V_x \)):
- **Type of Graph:** Time-domain waveform.
- **Axes Labels and Units:** The vertical axis represents \( V_x \), and the horizontal axis represents time.
- **Overall Behavior and Trends:** The waveform is a series of step-like increments and decrements, forming a triangular shape over time. This indicates a periodic charging and discharging pattern.
- **Key Features and Technical Details:**
- The waveform has a peak-to-peak amplitude labeled as \( k_1(V_{DD} + V_{SS}) \).
- The step changes are labeled \( k_2V_{DD} \) and \( k_2V_{SS} \), indicating the discrete voltage changes during the waveform.
- The waveform shows a symmetrical triangular shape, suggesting a balanced charge and discharge cycle.

Lower Graph (\( V_{out} \)):
- **Type of Graph:** Time-domain waveform.
- **Axes Labels and Units:** The vertical axis represents \( V_{out} \), and the horizontal axis represents time.
- **Overall Behavior and Trends:** The waveform is a square wave oscillating between \( V_{DD} \) and \( -V_{SS} \), indicating a binary switching output.
- **Key Features and Technical Details:**
- The period of the square wave is marked as \( T_{osc} \), representing the oscillation period of the relaxation oscillator.
- The waveform shows a consistent high and low state duration, indicating a stable oscillation frequency.

General Observations:
- The graphs illustrate the operation of a switched-capacitor relaxation oscillator.
- The \( V_x \) waveform shows the integrator's output, while the \( V_{out} \) waveform shows the comparator's output.
- The periodic behavior in both graphs indicates the transfer of charge and the resulting oscillation frequency determined by the circuit parameters.

Fig. 14.42 A switched-capacitor relaxation oscillator.

Note that the voltage across the unswitched capacitor $\mathrm{k}_{1} \mathrm{C}$ remains unchanged at $-\mathrm{V}_{\mathrm{Ss}}$. Next, as $\phi_{2}$ goes high, the charge on $k_{2} C$ will be transferred to $C$ (while the voltage across unswitched $k_{1} C$ again remains unchanged) and the output will fall by an amount equal to

$$
\begin{equation*}
\Delta \mathrm{v}_{\mathrm{x}}=\frac{\Delta \mathrm{Q}_{\mathrm{C}}}{\mathrm{C}}=\frac{\mathrm{Q}_{\mathrm{k}_{2} \mathrm{C}}}{\mathrm{C}}=-\mathrm{k}_{2} \mathrm{~V}_{\mathrm{Ss}} \tag{14.108}
\end{equation*}
$$

This operation will continue until $\mathrm{v}_{\mathrm{x}}$ reaches zero volts. In effect, $\mathrm{k}_{2} \mathrm{C}$ and C have formed a noninverting dis-crete-time integrator, while capacitor $\mathrm{k}_{1} \mathrm{C}$ does not affect the operation of the circuit. Once $\mathrm{v}_{\mathrm{x}}$ goes below zero, the comparator output will toggle to $V_{D D}$, and at this point a large amount of charge will pass through $k_{1} C$ while the voltage across it changes from $-\mathrm{V}_{\mathrm{SS}}$ to $\mathrm{V}_{\mathrm{DD}}$. This large charge value is equal to

$$
\begin{equation*}
\Delta Q_{k_{1} C}=k_{1} C\left(V_{D D}-\left(-V_{S S}\right)\right) \tag{14.109}
\end{equation*}
$$

and since this charge is drawn across $C$, then $\Delta Q_{C}=\Delta Q_{k_{1} C}$ and node $v_{x}$ drops by an amount equal to

$$
\begin{equation*}
\Delta \mathrm{v}_{\mathrm{x}}=-\frac{\Delta \mathrm{Q}_{\mathrm{C}}}{\mathrm{C}}=-\mathrm{k}_{\mathrm{l}}\left(\mathrm{~V}_{\mathrm{DD}}+\mathrm{V}_{\mathrm{SS}}\right) \tag{14.110}
\end{equation*}
$$

as shown in Fig. 14.42(b). After this time, $\mathrm{v}_{\mathrm{x}}$ will step up in increments of $\mathrm{k}_{2} \mathrm{~V}_{\mathrm{DD}}$ (since $\mathrm{v}_{\text {out }}$ now equals $\mathrm{V}_{\mathrm{DD}}$ ) until $\mathrm{v}_{\mathrm{x}}=0$, at which point a large positive voltage step will occur. Just after this positive step, we will be back at our starting point, and the entire operation will repeat indefinitely.

To derive a formula for the oscillation period $T_{\text {osc }}$, we make the assumption that $k_{1}>>k_{2}$ such that many small steps occur over one-half $T_{\text {osc }}$ period. With this assumption, we can now write that the total number of clock cycles, $\mathrm{T}_{\text {osc }} / \mathrm{T}$, equals the number of steps during negative sloping $\mathrm{v}_{\mathrm{x}}$ plus the number of steps during positive sloping $\mathrm{v}_{\mathrm{x}}$. Mathematically, we have

$$
\begin{equation*}
\frac{T_{\text {osc }}}{T}=\frac{k_{1}\left(V_{D D}+V_{S S}\right)}{k_{2} V_{S S}}+\frac{k_{1}\left(V_{D D}+V_{S S}\right)}{k_{2} V_{D D}} \tag{14.111}
\end{equation*}
$$

Assuming $\mathrm{V}_{\mathrm{DD}}=\mathrm{V}_{\mathrm{SS}}$, we have a 50 percent duty cycle with

$$
\begin{equation*}
\mathrm{T}_{\mathrm{osc}}=4\left(\frac{\mathrm{k}_{1}}{\mathrm{k}_{2}}\right) \mathrm{T} \tag{14.112}
\end{equation*}
$$

or equivalently,

$$
\begin{equation*}
\mathrm{f}_{\mathrm{osc}}=\frac{1}{4}\left(\frac{\mathrm{k}_{2}}{\mathrm{k}_{1}}\right) \mathrm{f} \tag{14.113}
\end{equation*}
$$

This fixed-frequency oscillator can be made voltage controlled by adding an extra feed-in capacitor to the oscillator, $\mathrm{k}_{\text {in }} \mathrm{C}$, as shown in Fig. 14.43. Here, when $\mathrm{V}_{\text {in }}$ is positive, extra charge packets are added into the integrator with the same sign as those for $k_{2} C$, and the circuit reaches $v_{x}=0$ sooner. If $V_{i n}$ is negative, then extra charge packets are added into the integrator with the opposite sign as those for $\mathrm{k}_{2} \mathrm{C}$, and the circuit reaches $\mathrm{v}_{\mathrm{x}}=0$ later. Assuming $\mathrm{k}_{1}>\mathrm{k}_{2}, \mathrm{k}_{\mathrm{in}}$ and $\mathrm{V}_{\mathrm{DD}}=\mathrm{V}_{\mathrm{SS}}$, it is left as an exercise to the reader (Problem 14.25) to show that the frequency of oscillation for the voltage-controlled oscillator of Fig. 14.43 is given by

$$
\begin{equation*}
\mathrm{f}_{\mathrm{osc}}=\frac{1}{4}\left(\frac{\mathrm{k}_{2}}{\mathrm{k}_{1}}+\frac{\mathrm{k}_{\mathrm{in}} \mathrm{~V}_{\mathrm{in}}}{\mathrm{k}_{1} \mathrm{~V}_{\mathrm{DD}}}\right) \mathrm{f} \tag{14.114}
\end{equation*}
$$

### 14.9.5 Sinusoidal Oscillator

In many applications, it is useful to realize an oscillator which produces a nearly sinusoidal output. For example, when a button is pressed on a touch-tone telephone, the signal sent down the telephone line is simply the sum of
image_name:Fig. 14.43
description:The circuit is a voltage-controlled oscillator (VCO) based on a relaxation oscillator design. It uses a combination of PMOS and NMOS transistors, capacitors, and operational amplifiers to generate a sinusoidal output. The circuit includes feedback paths through the use of capacitors and an inverter to stabilize and control the oscillation frequency.

Fig. 14.43 A voltage-controlled oscillator (VCO) based on the relaxation oscillator of Fig. 14.42.
two sinusoidal signals at certain frequencies (the signal is known as a dual-tone multi-frequency (DTMF) signal). Thus, switched-capacitor sinusoidal oscillators could be used to generate the necessary touch-tone signals.

One method of generating a sinusoidal oscillator is shown in Fig. 14.44. Here, a high-Q bandpass filter with center frequency $f_{0}$ is used together with a hard limiter. Assuming some start-up circuit is used to force oscillations to exist, we see that a sinusoidal wave at $\mathrm{v}_{\text {out }}$ results in a square wave at $\mathrm{v}_{1}$ which has a large component at $f_{0}$. The signal $v_{1}$ is filtered by the bandpass filter and thus maintains the sinusoidal signal, $v_{\text {out }}$. The oscillation frequency is set by the center frequency of the bandpass filter, while the sinusoidal amplitude is set by the center frequency gain of the filter and the peak values of the square-wave signal.

A switched-capacitor implementation of this sinusoidal oscillator is shown in Fig. 14.45 [Fleischer, 1985], where the high-Q bandpass filter has been realized using the circuit of Fig. 14.28. The comparator generates signals X and $\overline{\mathrm{X}}$ with the result that the switched-input associated with $\mathrm{V}_{\text {ref }}$ is either positive or negative. The start-up circuit is used to sense when an ac signal is present at $\mathrm{v}_{\text {out }}$. When no ac signal is detected, $\mathrm{v}_{\mathrm{st}}$ is low and the extra capacitors $C_{5}$ and $C_{6}$ form a positive feedback loop which causes oscillations to build up. Once an ac signal is detected, $\mathrm{v}_{\mathrm{st}}$ goes high and the positive feedback loop is broken, thereby allowing oscillations to continue, as discussed previously.
image_name:Fig. 14.44
description:The system block diagram for Fig. 14.44 represents a sinusoidal oscillator that utilizes a bandpass filter. The primary components of this system include:

1. **High-Q Bandpass Filter**: This filter is centered around a frequency \( f_0 \). It is responsible for filtering the input signal \( v_1 \) to allow only a narrow band of frequencies around \( f_0 \) to pass through, enhancing the quality factor (Q) of the signal.

2. **Input Signal \( v_1 \)**: The input to the system is a square wave signal with a period \( T \). This signal is fed into the high-Q bandpass filter.

3. **Output Signal \( v_{out} \)**: The output of the system is a sinusoidal waveform with the same period \( T = 1/f_0 \) as the center frequency of the bandpass filter. This indicates that the system converts the square wave input into a sinusoidal output.

4. **Feedback Loop**: The system includes a feedback loop where the output \( v_{out} \) is fed back into the system, maintaining the oscillation. The feedback mechanism ensures that the oscillations are sustained by reinforcing the signals at the desired frequency \( f_0 \).

5. **Reference Voltage \( V_{ref} \)**: The system also incorporates reference voltages \( V_{ref} \) and \( -V_{ref} \), which are used to stabilize the output and ensure that the oscillations are maintained at a consistent amplitude.

**Flow of Information**: The square wave input \( v_1 \) is processed by the high-Q bandpass filter to allow only the desired frequency \( f_0 \) to pass through. The filtered signal is then output as \( v_{out} \), a sinusoidal wave. This output is fed back into the system to maintain continuous oscillation.

**Overall System Function**: The primary function of this system is to convert a square wave input into a sinusoidal output using a bandpass filter. The high-Q filter and feedback loop ensure that the output is a stable, continuous sinusoidal wave at the desired frequency. This makes the system useful for generating precise sinusoidal signals in various electronic applications.

Fig. 14.44 A sinusoidal oscillator that makes use of a bandpass filter.
image_name:Fig. 14.45 A switched-capacitor implementation of a sinusoidal oscillator.
description:The circuit is a switched-capacitor implementation of a sinusoidal oscillator. It uses capacitors, op-amps, and NMOS transistors to convert a reference voltage into a sinusoidal output. The circuit includes a start-up circuit and a comparator to maintain oscillation. The capacitors CA and CB are set to 1 for specific frequency tuning.

Fig. 14.45 A switched-capacitor implementation of a sinusoidal oscillator.
For examples of other nonfiltering uses of switched-capacitor circuits, the interested reader is referred to [Gregorian, 1986].

## 14.10 KEY POINTS

- Opamp nonidealities such as dc gain, unity-gain frequency and phase-margin, slew-rate, and dc offset impact switched-capacitor circuit performance. [p. 557]
- When signal voltages change very slowly compared with the clock frequency, a switched-capacitor gives rise to an average current inversely proportional to the voltage across it, behaviorally equivalent to a resistor. [p. 561]
- When signal voltages change appreciably from one clock cycle to the next, a discrete-time analysis is needed to accurately predict the input-output behavior of switched-capacitor circuits. [p. 561]
- Each clock cycle, a switched-capacitor integrator samples a quantity of charge proportional to an input voltage and the sampling capacitance, then delivers it to a second integrating capacitor. [p. 562]
- The discrete-time transfer function of a switched-capacitor integrator has a pole at dc, $\mathrm{z}=1$. [p. 563]
- In order to make a switched-capacitor integrator insensitive to the circuit's parasitic capacitances to ground, it is necessary to add two extra switches, for a total of four, on each switched capacitor. [p. 567]
- Both delayed and delay-free integrators can be realized with the same switched-capacitor circuit by changing the clock phases applied to two of the switches. In a fully-differential implementation, both can be configured to provide either positive or negative dc gain. [p. 568]
- Complicated switched-capacitor circuits may be analyzed graphically using a signal-flow-graph representing the opamp stage with an integrating block and replacing each input branch with the corresponding non switched, delayed, or delay-free gain factor. [p. 570]
- Switched capacitors accumulate the thermal noise of the switches. Sampled $\mathrm{kT} / \mathrm{C}$ noise from both clock phases superimpose resulting in a total mean squared input-referred noise of $2 \mathrm{kT} / \mathrm{C}$. [p. 570]
- Beginning with conventional continuous-time active RC filters, and replacing each resistor with a switchedcapacitor results in a discrete-time filter whose frequency response closely approximates that of the original continuous-time filter at frequencies far below the sampling frequency. Once a filter structure is obtained, its precise frequency response is determined through the use of discrete-time analysis. [p. 572]

[^0]:    2. The impulse response of an IIR filter may become so small that, with finite precision arithmetic, it is rounded to zero.
3. It should be noted here that in many other textbooks, the bilinear transform is defined as $s=(2 / T)[(z-1) /(z+1)]$ where $T$ is the sampling period. Here, we have normalized T to 2 since we use the bilinear transform only as a temporary transformation to a continuous-time equivalent, and then we inverse transform the result back to discrete time. Thus, the value of T can be chosen arbitrarily as long as the same value is used in each transformation.
[^1]:    1. BJT input stages are rarely used as they would result in charge leakage due to their nonzero input bias current.
[^2]:    3. When the signal voltage doubles, the signal power goes up by a factor of four. Fully differential circuits would have twice the noise power of single-ended circuits having the same size capacitors due to there being two capacitive networks generating noise. Halving the capacitor size of the differential circuit would result in another doubling in noise power, resulting in a signal-to-noise ratio equal to that of a single-ended circuit having capacitors twice as large.
[^3]:    6. A programmable capacitor array is a capacitor whose size can be digitally controlled. It normally consists of a number of binarily-weighted capacitors having one plate common for all capacitors and the other plate of each capacitor connected through digitally-controlled switches to either a second common node or ground.

- Fully-differential filter implementations offer several advantages over their single-ended counterparts: they allow for the realization of sign inversion (i.e. a gain of -1 ) by simply interchanging wires, reject commonmode noise, and rejecting even-order distortion terms which generally dominate single-ended circuits. [p. 576]
- Although fully-differential circuit implementations require some overhead for additional wiring and commonmode feedback circuitry, if properly designed the overhead should represent a small fraction of the overall circuit. [p. 577]
- Several different discrete-time biquads can be realized by varying the type (i.e., delayed, delay-free) and exact connection of switched-capacitor branches within a two-integrator loop. The choice of which biquad to use depends upon the specific pole and zero locations sought. [p. 584]
- To minimize distortion due to charge injection, switches connected to dc nodes, such as ground, are turned off in advance of other switches. Although there is still some charge injection, it is signal independent. [p. 586]
- Charge injection is most problematic at high switching speeds where low switch on resistances demand wide transistors and small capacitors. [p. 587]
- Technology scaling permits smaller transistors to offer the same on resistance, thereby reducing charge injection or, for the same charge injection, enabling higher switching frequencies. [p. 587]
- Switched-capacitor circuits can use a reset phase to sample and cancel dc offset and very low-frequency (1/f) noise without affecting the circuit's overall dc gain. [p. 589]
