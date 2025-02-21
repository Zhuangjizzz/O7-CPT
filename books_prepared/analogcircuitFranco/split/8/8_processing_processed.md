# Chapter7 Feedback, Stability, and Noise

Chapter Outline
7.1 Negative-Feedback Basics 688
7.2 Effect of Feedback on Distortion, Noise, and Bandwidth 695
7.3 Feedback Topologies and Closed-Loop I/O Resistances 704
7.4 Practical Configurations and the Effect of Loading 714
7.5 Return-Ratio Analysis 741
7.6 Blackman's Impedance Formula and Injection Methods 755
7.7 Stability in Negative-Feedback Circuits 762
7.8 Dominant-Pole Compensation 772
7.9 Frequency Compensation of Monolithic Op Amps 780
7.10 Noise 795

References 811
Problems 811

Feedback in electronics refers to the situation whereby a signal derived from the output port of an amplifier is returned to the input port, where it is combined with the externally applied input signal to create a new signal to be processed by the amplifier itself. The most common forms of combination are addition and subtraction. When the feedback signal is added to the external signal, we have positive feedback, and when it is subtracted we have negative feedback.

In positive feedback the returned signal is designed to reinforce the input signal in such a way as to deliberately drive the amplifier in saturation. Also referred to as regenerative feedback, it is used in the synthesis of digital circuits such as flip flops and Schmitt triggers.

In negative feedback the returned signal is designed to oppose (rather than reinforce) the input signal, this being the reason why it is also referred to as degenerative feedback. This type of feedback is far more interesting than positive feedback because of the many potential advantages it offers. First, it tends to stabilize the gain
against parameter variations and drift of the components making up the amplifier itself. Second, it tends to reduce distortion as well as certain types of noise. Third, it can be used to control the input and output resistances in such a way as to reduce the unwanted effects of loading. Finally, it can be exploited to control the amplifier's dynamics, like extending the bandwidth (broadbanding) and speeding up its transient response.

Like many inventions, negative feedback comes with a price and a risk:

- As we move along we'll see that in order to fully realize the benefits available from this type of feedback we need to start out with a much higher gain than that finally demanded by the application at hand. (The student who has been exposed to the operational amplifier, the most popular amplifier type intended for negativefeedback operation, already knows this.) However, in today's integrated-circuit technology, high-gain amplifiers such as op amps are manufactured readily and inexpensively, so price is generally not much of an issue.
- Far more serious is the fact that negative feedback poses the risk of oscillation. As the signal propagates through the amplifier, it experiences unavoidable delays, collectively referred to as phase lag. If, by the time it returns to the input, the signal has acquired a shift of $-180^{\circ}$, feedback turns from negative to positive. Moreover, if the signal is at least as strong as when it started out, feedback becomes regenerative, resulting in high-frequency oscillation. Though this effect is exploited on purpose in the design of oscillators, it is otherwise undesirable as it may render a circuit totally useless. Mercifully, a variety of techniques have been developed to tame unwanted oscillations. Generally known as frequency compensation techniques, they constitute one of the most fascinating aspects of systems theory as applied to electronics and control.

Negative feedback was conceived in 1928 by Harold Black in his quest to reduce distortion in telephone repeaters. For instance, when using a gain-of-ten voltage amplifier, we expect the circuit to respond to a given input $v_{I}$ with the output $v_{O}=10 v_{I}$. In practice, due to the nonlinearities of the devices making up the amplifier (vacuum tubes then, transistors today), such a relationship holds only in small-signal operation. In large-signal operation an amplifier generally yields a much-distorted output, as we have already seen when transistor amplifiers are being overdriven as in Sections 2.5 and 3.6. We can model this situation by regarding the actual output as consisting of the desired component $10 v_{I}$ plus an unwanted component (or noise) $v_{U}$,

$$
v_{O}=10 v_{I}+v_{U}
$$

In his attempt to reduce $v_{U}$, Harold Black reasoned that if ( $a$ ) we take a fraction of the actual output equal to the reciprocal of the desired gain, or $(1 / 10) v_{O}$ in the present example, (b) we subtract this fraction from the input to create a new signal $v_{E}$ (subsequently named error signal)

$$
v_{E}=v_{I}-\frac{1}{10} v_{O}=v_{I}-\frac{10 v_{I}+v_{U}}{10}=\frac{-v_{U}}{10}
$$

(c) we feed this new signal $v_{E}$ to the amplifier (now renamed error amplifier), and (d) we substantially increase the gain (now called open-loop gain) so that the amplifier
can sustain $v_{O}$ with a vanishingly small $v_{E}$, (or $\left.v_{E} \rightarrow 0\right)$, then also $v_{U}\left(=-10 v_{E}\right)$ will be small, resulting in the virtual elimination of the distortion $v_{U}$ from the output to give

$$
v_{O} \rightarrow 10 v_{I}
$$

It is fascinating that such a terse and disarmingly simple line of reasoning would result in one of the most important inventions of electronics!

Like other revolutionary inventions, negative feedback wasn't immediately accepted by the engineering community because of the risk of oscillation that it posed. However, once this risk became better understood and suitable cures were developed to tame unwanted oscillations, negative feedback became a cornerstone not only in electronic circuit design, but also in such disparate disciplines as automatic control and modeling of biological systems. The student has already been exposed informally to negative feedback in a variety of different situations: op amp circuits use negative feedback; the feedback bias technique stabilizes dc biasing for transistors; emitter/source degeneration is a negative-feedback example designed to stabilize gain against transistor parameter variations. After our informal exposure to negative feedback, we are now ready to tackle it in a thorough and systematic fashion.

CHAPTER HIGHLIGHTS

The chapter begins with basic negative-feedback concepts and terminology, emphasizing the loop gain as a central parameter of a negative feedback system. The curative properties of feedback are illustrated in a variety of situations such as distortion reduction, noise reduction, and broadbanding.

Next, the chapter introduces the four basic negative-feedback topologies and discusses the effect of feedback on gain as well as the input and output resistances. Prerequisite courses have already exposed the student to negative feedback via operational amplifiers, if only informally. This is the right juncture to capitalize on basic op-amp background and expand it to illustrate the different feedback topologies in a more systematic fashion.

In real-life feedback circuits the basic amplifier and the feedback network tend to load each other, so we need suitable methods to investigate the various topologies in the presence of loading. The first such method, known as two-port analysis, is illustrated via a variety of circuit examples, ranging from full-blown op amps and currentfeedback amplifiers, to multi-transistor configurations, to single-transistor stages (the student will finally be able to appreciate the stabilizing effect of already familiar singletransistor feedback schemes such as emitter/source degeneration and feedback bias).

A powerful alternative to two-port analysis, known as return-ratio analysis, is also illustrated in a variety of circuit examples. Directly related to this type of analysis are Blackman's impedance formula and injection methods, which are particularly useful in laboratory measurements and in the course of computer simulations.

The chapter progresses to the study of stability and frequency compensation techniques. After introducing graphical as well as experimental and computer tools to assess the stability of a negative-feedback circuit, the chapter investigates the internal
frequency compensation of the most common op amps discussed in Chapter 5: the bipolar 741-type op amp, and the two-stage and cascode CMOS op amps.

The chapter concludes with noise in integrated circuits. After an introduction to basic noise properties, analytical tools, and noise types, the noise models of diodes and transistors are discussed. The chapter ends with the noise analysis of important circuit configurations such as op amp circuits and differential pairs, both bipolar and CMOS.

The chapter makes abundant use of PSpice both as a verification tool for pa-per-and-pencil calculations and as a software oscilloscope to display critical waveforms, especially when investigating the curative properties on distortion, the complex issues of stability and frequency compensation, or understanding the noise performance of a circuit.

## 7.1 NEGATIVE-FEEDBACK BASICS

Figure 7.1 shows the structure of a negative feedback system. Its main ingredients are an error amplifier and a feedback network. The system receives an external input signal $s_{i}$ (which in an electronic circuit is typically a voltage or a current) and produces in turn an output signal $s_{o}$ (again, a voltage or a current). The feedback network senses $s_{o}$ to produce a scaled version of it, called the feedback signal $s_{f}$, such that

$$
\begin{equation*}
s_{f}=b s_{o} \tag{7.1}
\end{equation*}
$$

where $b$ is called the feedback factor. The feedback signal is then fed to an input summer, where it is subtracted from the input signal to produce a signal called the error signal $s_{\varepsilon}$,

$$
\begin{equation*}
s_{\varepsilon}=s_{i}-s_{f} \tag{7.2}
\end{equation*}
$$

This, in turn, is fed to the error amplifier, thus closing a signal-propagation loop around the amplifier.

As implied by Eq. (7.2), the aim of negative feedback is to reduce the input signal $s_{i}$ to a smaller signal $s_{\varepsilon}$. Were we to $\operatorname{add}$ (rather than subtract) $s_{f}$ to $s_{i}$, then $s_{\varepsilon}$ would be greater than $s_{i}$. After undergoing further magnification by the amplifier, the signal would return to the summer even greater, continuously feeding upon itself until the
image_name:FIGURE 7.1 Block diagram of a negative-feedback circuit
description:The block diagram in FIGURE 7.1 illustrates a negative-feedback circuit. The main components of this system include:

1. **Summer (Σ):** This is the point where the input signal \( s_i \) is combined with the feedback signal \( s_f \). The summer subtracts the feedback signal from the input signal to produce the error signal \( s_\varepsilon \).

2. **Error Amplifier (a):** This block amplifies the error signal \( s_\varepsilon \). The amplification process is characterized by a gain factor \( a \), resulting in the amplified output signal \( s_o \).

3. **Feedback Network (b):** This component takes the output signal \( s_o \) and processes it to produce the feedback signal \( s_f \). The feedback network has a gain factor \( b \) which determines how much of the output signal is fed back to the input.

**Flow of Information:**
- The input signal \( s_i \) enters the system and is combined with the feedback signal \( s_f \) at the summer. The feedback signal is subtracted from the input, generating the error signal \( s_\varepsilon \).
- The error signal \( s_\varepsilon \) is then amplified by the error amplifier with a gain of \( a \) to produce the output signal \( s_o \).
- The output signal \( s_o \) is fed into the feedback network, where it is processed to create the feedback signal \( s_f \), which is then looped back to the summer.

**Labels and Annotations:**
- The diagram labels the input, output, and feedback signals as \( s_i \), \( s_o \), and \( s_f \) respectively.
- The error signal is labeled as \( s_\varepsilon \), and the gains of the amplifier and feedback network are denoted by \( a \) and \( b \).

**Overall System Function:**
The primary function of this negative-feedback circuit is to stabilize the output signal \( s_o \) by reducing the error signal \( s_\varepsilon \). The feedback loop, involving the feedback network and summer, adjusts the input to the error amplifier to minimize deviations in the output, thereby achieving a controlled and stable amplification process. This mechanism is fundamental in applications requiring precise control of signal amplification.

Feedback network
FIGURE 7.1 Block diagram of a negative-feedback circuit.
amplifier is ultimately driven in saturation. Aptly called positive feedback, this form of feedback is used in the synthesis of highly nonlinear circuits such as flip flops and Schmitt triggers. This chapter will deal with negative feedback only.

We now wish to obtain a relationship between the system's output $s_{o}$ and input $s_{i}$. By definition, the error amplifier yields

$$
\begin{equation*}
s_{o}=a S_{\varepsilon} \tag{7.3}
\end{equation*}
$$

where $a$ is the amplifier's gain. Were we to break the feedback loop to make $s_{f}=0$, then the amplifier would yield $s_{o}=a s_{i}$, indicating that $a$ is the gain by which $s_{i}$ would be magnified in the absence of any feedback loop. Consequently, $a$ is called the openloop gain. Combining the above equations,

$$
s_{o}=a\left(s_{i}-s_{f}\right)=a\left(s_{i}-b s_{o}\right)
$$

Collecting and solving for $s_{o}$ gives

$$
\begin{equation*}
s_{o}=A s_{i} \tag{7.4}
\end{equation*}
$$

where

$$
\begin{equation*}
A=\frac{a}{1+a b} \tag{7.5}
\end{equation*}
$$

is the gain by which the overall negative-feedback system amplifies the input $s_{i}$. Aptly called the closed-loop gain, $A\left(=s_{o} / s_{i}\right)$ should not be confused with the open loop gain $a\left(=s_{o} / s_{\varepsilon}\right)$. In fact, to underscore the distinction, we shall use upper-case letters to indicate closed-loop parameters, such as gain and (later) input and output resistances $\left(A, R_{i}, R_{o}\right)$, and lower-case letters to indicate the parameters of the basic error amplifier, aptly called open-loop parameters $\left(a, r_{i}, r_{o}\right)$.

As a signal propagates around the loop, starting, say, at the amplifier's input, it undergoes first magnification by $a$ as it goes through the amplifier, then attenuation by $b$ as it returns through the feed-back network, and finally inversion $(-)$ as it goes through the summer $\Sigma$. The overall gain around the loop is thus $-a b$. The negative of this overall gain is (somewhat improperly) called the loop gain $L$,

$$
\begin{equation*}
L=a b \tag{7.6}
\end{equation*}
$$

As we shall see, $L$ plays a central role in a feedback system. Manipulating Eq. (7.5) as

$$
A=\frac{1}{b} \frac{a b}{1+a b}=\frac{1}{b} \frac{1}{1+1 /(a b)}
$$

allows us to express the closed-loop gain in the insightful alternative form

$$
\begin{equation*}
A=\frac{1}{b} \times \frac{1}{1+1 / L} \tag{7.7}
\end{equation*}
$$

Of particular interest is the condition $L \gg 1$, for then Eq. (7.7) can be approximated as

$$
\begin{equation*}
A \cong \frac{1}{b}\left(1-\frac{1}{L}\right) \cong \frac{1}{b} \tag{7.8}
\end{equation*}
$$

This result alone underscores two of the most important benefits accruing from the use of negative feedback under the condition $L \gg 1$, namely:

- The closed-loop gain $A$ is virtually independent of the open loop gain $a$. This is highly desirable as the open-loop gain $a$ is usually an ill-defined parameter that depends on the parameters of the transistors making up the amplifier. As we know, these parameters vary with the dc biasing conditions, drift with temperature and time, and vary from device to device due to fabrication process variations.
- We can tailor $A$ to a wide variety of applications by a suitable choice of the feedback network. This network is usually implemented with passive components such as resistors and capacitors. By using components of adequate quality, we can make $A$ as predictable, accurate, and stable as needed.
If we regard $1 / L$ as an error term in Eq. (7.8), it is apparent that $L$ gives a measure of how close the actual gain $A$ is to the ideal gain $1 / b$. Specifically, the larger $L$ the better. Since $L=a b$, it follows that to ensure a suitably large $L$ for a given $b$ we need an amplifier with an adequately high gain $a$. In other words, we need to start out with a high open-loop gain $a$ to achieve a much lower but much more stable and predictable closed-loop gain $A$. Since gain drops from $a$ to $a /(1+L)$, we are in affect throwing away gain by the amount of feedback $(1+L)$. Considering the benefits as well as the fact that modern integrated circuit (IC) technology allows for high gains to be achieved readily and inexpensively, this price is well worth paying.

As we move along, we shall refer to the limit $L \rightarrow \infty$ as representing the ideal situation. The corresponding closed-loop gain is then

$$
\begin{equation*}
A_{\text {ideal }}=\lim _{T \rightarrow \infty} A=\frac{1}{b} \tag{7.9}
\end{equation*}
$$

Though the ideal condition is physically unattainable, a circuit designer will strive to approach it within a specified degree of accuracy by ensuring an adequately high loop gain $L$, and hence, by using an amplifier with a correspondingly high open-loop gain $a(=L / b)$.

EXAMPLE 7.1 (a) An engineer is asked to design a voltage amplifier having a closed-loop gain of $10 \mathrm{~V} / \mathrm{V}$ with an error of $1 \%$ or less. What values of $a$ and $b$ are needed? What is the resulting value of $A$ ?
(b) To be on the safe side, the engineer decides to use an amplifier with a gain $a$ ten times as large as that calculated in part (a). What is the resulting value of $A$ ?

#### Solution

(a) Impose $10 \mathrm{~V} / \mathrm{V}=1 / b$, or $b=0.1 \mathrm{~V} / \mathrm{V}$. For a $1 \%$ error we need $1 / L=1 / 100$, so $a=L / b=100 / 0.1=1000 \mathrm{~V} / \mathrm{V}$. Moreover, $A \cong(1 / b) \times(1-1 / L)=$ $10(1-1 / 100)=9.9 \mathrm{~V} / \mathrm{V}$.
(b) Now $L=1000$, so $A \cong 10(1-1 / 1000)=9.99 \mathrm{~V} / \mathrm{V}$, even closer to the ideal value of $10 \mathrm{~V} / \mathrm{V}$.

### The Error Signal $\boldsymbol{s}_{\boldsymbol{\varepsilon}}$ and the Feedback Signal $\boldsymbol{s}_{\boldsymbol{f}}$

Additional properties of negative feedback are readily found by writing

$$
s_{\varepsilon}=\frac{s_{o}}{a}=\frac{A s_{i}}{a}=\frac{a}{1+L} \frac{s_{i}}{a}
$$

or

$$
\begin{equation*}
s_{\varepsilon}=\frac{s_{i}}{1+L} \tag{7.10}
\end{equation*}
$$

Moreover,

$$
s_{f}=b s_{o}=b A s_{i}=b \frac{1}{b} \frac{1}{1+1 / L} s_{i}
$$

which gives

$$
\begin{equation*}
s_{f}=\frac{s_{i}}{1+1 / L} \tag{7.11}
\end{equation*}
$$

These (equivalent) results indicate that for a sufficiently large loop gain (ideally, for $L \rightarrow \infty$ ), the error signal becomes vanishingly small (ideally, $s_{\varepsilon} \rightarrow 0$ ), causing the feedback signal to closely follow the input signal $\left(s_{f} \rightarrow s_{i}\right)$. These properties are worth keeping in mind as we attempt to develop a quick (if approximate) feel for the inner workings of a negative-feedback circuit.

### Gain Desensitivity

Given that the open-loop gain $a$ is an ill-defined parameter because of production variations as well as environmental changes, we wish to investigate the impact of these uncertainties upon the closed-loop gain $A$. To this end, let us differentiate $A$ with respect to $a$ in Eq. (7.5),

$$
\frac{d A}{d a}=\frac{1 \times(1+a b)-a \times b}{(1+a b)^{2}}=\frac{1}{(1+a b)^{2}}=\frac{1}{1+a b} \times \frac{a}{1+a b} \frac{1}{a}=\frac{1}{1+a b} \times \frac{A}{a}
$$

Multiplying both sides by 100da/A and replacing differentials ( $d$ ) with small differences ( $\Delta$ ), we obtain

$$
\begin{equation*}
100 \frac{\Delta A}{A} \cong \frac{1}{1+L}\left(100 \frac{\Delta a}{a}\right) \tag{7.12}
\end{equation*}
$$

This result indicates that the percentage variation in the closed-loop gain $(100 \times \Delta A / A)$ due to a given percentage variation in the open-loop gain $(100 \times$ $\Delta A / A)$ is approximately $(1+L)$ times as small. With $L$ sufficiently large, even an outlandish variation in $a$ will have a minimal effect upon $A$ ! To reflect this stabilizing effect, the amount of feedback $(1+L)$ is also called the gain desensitivity. Once again we observe that the size of $L$ offers a measure of how close a negative-feedback system is to ideal.

EXAMPLE 7.2 Suppose the open-loop gain $a$ of the amplifier of Example 7.1 $a$ has a tolerance of $\pm 20 \%$. Estimate the tolerance of the closed-loop gain A. Repeat, but for Example 7.1 , and comment on your findings.

#### Solution

In Example 7.1 $a$ we have $L=100$, so the approximate tolerance of $A$ is ( $\pm 20 \%$ )/ $(1+100) \cong \pm 0.2 \%$. In Example $7.1 b, L$ is ten times as large, so the tolerance of $A$ will be about ten times as small, or $\pm 0.02 \%$. In either case negative feedback has a dramatic stabilizing effect upon the closed-loop gain $A$.

### A Classic Example: The Non-Inverting Op Amp Configuration

A circuit example conforming exactly to the diagram of Fig. 7.1, and thus embodying all the features discussed so far, is the familiar non-inverting op amp configuration of Fig. 7.2. The op amp combines the roles of error amplifier as well as summer, the latter thanks to the fact that the op amp responds to the difference between its input voltages. The feedback network is a plain voltage divider, giving

$$
\begin{equation*}
b=\frac{v_{f}}{v_{o}}=\frac{R_{1}}{R_{1}+R_{2}}=\frac{1}{1+R_{2} / R_{1}} \tag{7.13}
\end{equation*}
$$

Op amps are deliberately designed to have very high open-loop gains so as to ensure high loop gains, and hence, nearly ideal behavior in negative-feedback operation. In the ideal limit $a \rightarrow \infty$, the circuit would give $L \rightarrow \infty$ and thus $v_{\varepsilon} \rightarrow 0$ and $v_{f} \rightarrow v_{i}$. The closed-loop gain would then take on the ideal value

$$
\begin{equation*}
A_{\text {ideal }}=\frac{v_{o}}{v_{i}}=\frac{1}{b}=1+\frac{R_{2}}{R_{1}} \tag{7.14}
\end{equation*}
$$

image_name:FIGURE 7.2
description:
[
name: Vi, type: VoltageSource, value: Vi, ports: {Np: Vi, Nn: GND}
name: Op amp, type: OpAmp, value: a, ports: {InP: Vi, InN: Vf, OutP: Vo}
name: R1, type: Resistor, value: R1, ports: {N1: Vf, N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: Vo, N2: Vf}
]
extrainfo:This is a non-inverting op amp circuit with a feedback network formed by R1 and R2. The op amp has a high open-loop gain, providing negative feedback to stabilize the closed-loop gain.

FIGURE 7.2 The non-inverting op amp circuit as a classic example of a negative-feedback system.
(a) Let the op amp of Fig. 7.2 be the popular 741-type, whose data sheets report the typical gain $a=200,000 \mathrm{~V} / \mathrm{V}$. Find the closed-loop gain if $R_{1}=1.0 \mathrm{k} \Omega$ and $R_{2}=3.0 \mathrm{k} \Omega$.
(b) Find $v_{o}, v_{f}$ and $v_{\varepsilon}$ if $v_{i}=2.0 \mathrm{~V}$. Comment on your results.
(c) The data sheets also report that because of fabrication process variations, the gain $a$ can be as low as $50,000 \mathrm{~V} / \mathrm{V}$. How does this impact the results found in part (a)? Comment.

#### Solution

(a) We have $b=1 /(1+3)=1 / 4, L=a b=200,000 / 4=50,000$, and $A \cong$ $4(1-1 / 50,000)=3.99992 \mathrm{~V} / \mathrm{V}$. Thanks to the high loop gain, $A$ is very close to $A_{\text {ideal }}(=4.0 \mathrm{~V} / \mathrm{V})$.
(b) We have $v_{o}=A v_{i},=3.99992 \times 2.0=7.99984 \mathrm{~V}, v_{f}=v_{i} /(1+1 / L)=2.0 /$ $(1+1 / 50,000)=1.99996 \mathrm{~V}$, and $v_{\varepsilon}=v_{i} /(1+L) \cong 2.0 / 50,000=40 \times$ $10^{-6} \mathrm{~V}=40 \mu \mathrm{~V}$. For practical purposes, we can state that $v_{o} \cong 8 \mathrm{~V}, v_{f} \cong 2 \mathrm{~V}$, and $v_{\varepsilon} \cong 0$. We observe that just as the voltage divider divides down $v_{o}$ by 4 to give $v_{f}$, the op amp performs the inverse operation, namely, it multiplies up $v_{i}$ by 4 to give $v_{o}$.
(c) We now have $L=a b=50,000 / 4=12,500$, so $A \cong 4(1-1 / 12,500)=$ $3.99968 \mathrm{~V} / \mathrm{V}$. The change in $A$ is insignificant ( $-0.006 \%$ ), and so are the changes in $v_{o}$ and $v_{f}$, both of which continue to be extremely close to their ideal values of 8.0 V and 2.0 V , respectively. However, due to the drop in $a$, we now have $v_{\varepsilon}=v_{o} / a \cong 8 / 50,000=160 \mu \mathrm{~V}$, higher than in part ( $b$ ) but still truly negligible compared to the other voltages in the circuit.
(a) Suitably modify the circuit of Fig. 7.2 so that it amplifies a transducer signal

EXAMPLE 7.4
$v_{i}=5 \mathrm{mV}$ with a closed loop gain of $1000 \mathrm{~V} / \mathrm{V}$.
(b) Assuming a 741-type op amp, estimate $A, v_{o}, v_{f}$, and $v_{\varepsilon}$.
(c) Compare with Example $7.3 a$ and comment.

#### Solution

(a) Imposing $1000=1+R_{2} / R_{1}$ we get $R_{2} / R_{1}=999$. One way to proceed is to leave $R_{1}=1.0 \mathrm{k} \Omega$ and make $R_{2}=999 \mathrm{k} \Omega$. (In practice one would pick the closest standard value of $1.0 \mathrm{M} \Omega$.)
(b) We now have $b \cong 0.001 \mathrm{~V} / \mathrm{V}, L=a b \cong 200,000 \times 0.001=200, A \cong$ $1000(1-1 / 200)=995 \mathrm{~V} / \mathrm{V}, v_{o}=995 \times 5 \mathrm{mV}=4.975 \mathrm{~V}, v_{f}=(5 \mathrm{mV}) /$ $(1+1 / 200)=4.975 \mathrm{mV}$, and $v_{\varepsilon} \cong(5 \mathrm{mV}) /(1+200) \cong 25 \mu \mathrm{~V}$.
(c) Due to the much higher gain $A$ sought, $b$ is much lower compared to Example 7.3a, so the loop gain drops to 200. This implies a $0.5 \%$ deviation of $A$ and $v_{f}$ from their ideal values-still a fairly small deviation. The op amp's input is always $v_{\varepsilon}=v_{o} / a$, that is, the departure of $v_{\varepsilon}$ from its ideal value of 0 V depends only on $v_{o}$ and $a$, regardless of the loop gain $L$.

### A Single-Transistor Example of a Negative-Feedback System

If Fig. 7.2 illustrates feedback around a complex circuit such as an op amp, consisting of many transistors, Fig. 7.3 depicts the opposite extreme of feedback around just one transistor. The latter is a CG amplifier utilizing the voltage divider $R_{1}-R_{2}$ as its feedback network. As long as $\left(R_{1}+R_{2}\right) \gg R_{D}$, we can write

$$
v_{o} \cong-g_{m}\left(R_{D} / / r_{o}\right) v_{g s}=-g_{m}\left(R_{D} / / r_{o}\right) \times\left(v_{g}-v_{s}\right)=g_{m}\left(R_{D} / / r_{o}\right) \times\left(v_{s}-v_{g}\right)
$$

where the body effect has been ignored. This expression is of the type

$$
v_{o}=a\left(v_{i}-v_{f}\right)=a\left(v_{i}-b v_{o}\right)
$$

image_name:(a)
description:
[
name: Vi, type: VoltageSource, value: Vi, ports: {Np: vi, Nn: GND}
name: C, type: Capacitor, value: C, ports: {Np: vs, Nn: vi}
name: ID, type: CurrentSource, value: ID, ports: {Np: vs, Nn: VSS}
name: M1, type: NMOS, ports: {S: vs, D: vd, G: vg}
name: RD, type: Resistor, value: 12kΩ, ports: {N1: vd, N2: VDD}
name: R2, type: Resistor, value: 10MΩ, ports: {N1: vg, N2: vo}
name: R1, type: Resistor, value: 10MΩ, ports: {N1: vg, N2: GND}
]
extrainfo:The circuit is a common-gate amplifier with a voltage divider feedback network. The body effect is ignored in the analysis. The open-loop gain is given by a = gm(RD || ro), and the feedback factor is b = R2/(R1 + R2).

(a)
image_name:(a)
description:
[
name: Vi, type: VoltageSource, ports: {Np: vi, Nn: GND}
name: RD, type: Resistor, value: 12kΩ, ports: {N1: Vo, N2: VDD}
name: R2, type: Resistor, value: 10MΩ, ports: {N1: Vo, N2: vf}
name: R1, type: Resistor, value: 10MΩ, ports: {N1: vf, N2: GND}
name: M1, type: NMOS, ports: {S: Vi, D: Vo, G: vf}
]
extrainfo:The circuit is a common-gate amplifier with a voltage divider feedback network. The open-loop gain is given by a = gm(RD || ro), and the feedback factor is b = R2/(R1 + R2). The body effect is ignored in the analysis. The circuit conforms to a negative-feedback system.

(b)

FIGURE 7.3 (a) A single-transistor circuit as an example of a negative-feedback system, and (b) its ac equivalent.
provided we let $v_{s} \rightarrow v_{i}, v_{g} \rightarrow v_{f}$, and $v_{s g} \rightarrow v_{\varepsilon}$, as depicted in Fig. 7.3b. Also, the openloop gain is $a=g_{m}\left(R_{D} / / r_{o}\right)$, and the feedback factor is

$$
b=\frac{v_{g}}{v_{d}}=\frac{R_{2}}{R_{1}+R_{2}}=\frac{1}{1+R_{2} / R_{1}}
$$

Just like the op amp example above, the present circuit conforms exactly to the diagram of Fig. 7.1.

Let the FET of Fig. 7.3 have $g_{m}=2 \mathrm{~mA} / \mathrm{V}$ and $r_{o}=60 \mathrm{k} \Omega$. Estimate $L$ and $A$, EXAMPLE 7.5 and comment.

#### Solution

We have $a=g_{m}\left(R_{D} / / r_{o}\right)=2(12 / / 60)=20 \mathrm{~V} / \mathrm{V}, b=1 /(1+10 / 10)=1 / 2$, $L=a b=20 / 2=10$, and

$$
A=\frac{1}{b} \frac{1}{1+1 / L}=2 \frac{1}{1+1 / 10}=1.82 \mathrm{~V} / \mathrm{V}
$$

Given the notoriously low voltage gains achievable with FETs, it is not surprising that the loop gain is so low compared to that of an op amp, resulting in a noticeable departure of $A$ from its ideal value of $2 \mathrm{~V} / \mathrm{V}$. Yet, it is instructive to investigate the given single-transistor circuit from a negative-feedback standpoint!

#### Exercise 7.1

As we move along we shall find that negative feedback affects not only the gain, but also the input and output resistances. Using the test method, show that for $R_{1}+R_{2} \gg R_{D}$ in Fig. 7.3, the resistance $R_{i}$ seen looking into the input terminal and the resistance $R_{o}$ seen looking into the output terminal are

$$
R_{i}=\frac{1}{g_{m}}(1+L) \quad R_{o}=\frac{R_{D} / / r_{o}}{1+L}
$$

## 7.2 EFFECT OF FEEDBACK ON DISTORTION, NOISE, AND BANDWIDTH

Equation (7.3) implies a relationship of linear proportionality between output and input, with the proportionality constant representing the open-loop gain $a$. A practical amplifier, such as an IC op amp, is made up of transistors, which are inherently nonlinear devices. Moreover, the amplifier cannot swing its output beyond its own powersupply voltages. Consequently, the voltage transfer curve (VTC) of a practical amplifier is not a straight line, but a nonlinear curve of the type exemplified in Fig. 7.4a (top). As long as operation is restricted in the vicinity of the origin, the curve can be regarded as approximately linear, and its slope, representing the gain $a$, is the steepest there. However, as we move away from the origin, slope progressively decreases until the VTC
image_name:(a)
description:### Type of Graph and Function:
The graph labeled "(a)" consists of two parts: the top graph is a Voltage Transfer Curve (VTC), and the bottom graph represents the open-loop gain of a practical error amplifier.

Axes Labels and Units:
- **Top Graph (VTC):**
- **X-axis:** Input voltage \( v_E \) in millivolts (mV), ranging from -30 mV to 30 mV.
- **Y-axis:** Output voltage \( v_O \) in volts (V), ranging from -10 V to 10 V.
- **Bottom Graph (Open-loop Gain):**
- **X-axis:** Input voltage \( v_E \) in millivolts (mV), same range as the top graph.
- **Y-axis:** Open-loop gain \( a \) in volts per volt (V/V), ranging from 0 to 1000 V/V.

Overall Behavior and Trends:
- **Top Graph (VTC):**
- The curve starts at \( -10 \) V for \( v_E = -30 \) mV and rises steeply through the origin.
- It approaches an asymptote at \( 10 \) V as \( v_E \) increases to 30 mV, indicating saturation.
- The slope is steepest near the origin, indicating the highest gain in this region.
- **Bottom Graph (Open-loop Gain):**
- The gain \( a \) is zero at both ends of the input range (\( v_E = -30 \) mV and \( v_E = 30 \) mV).
- It peaks at the origin, reaching a maximum gain of approximately 1000 V/V.
- The gain decreases symmetrically as \( v_E \) moves away from the origin in either direction.

Key Features and Technical Details:
- **Top Graph (VTC):**
- The curve is nonlinear, with a linear region around the origin where the gain is highest.
- Saturation occurs at \( \pm 10 \) V, beyond which the output does not increase with increasing input.
- **Bottom Graph (Open-loop Gain):**
- The peak gain value is about 1000 V/V at \( v_E = 0 \) mV.
- The gain curve is bell-shaped, indicating that the amplifier is most effective in a narrow range around the origin.

Annotations and Specific Data Points:
- The top graph is labeled "VTC" with an arrow pointing to the curve, and the slope is denoted by \( a \).
- The bottom graph is labeled with an arrow indicating the peak gain value \( a \).
image_name:(b)
description:The graph labeled (b) consists of two plots that depict input and output waveforms over time for a practical amplifier.

1. **Type of Graph and Function:**
- Time-domain waveform graph.

2. **Axes Labels and Units:**
- **Input (Top):**
- X-axis: Time \( t \) in milliseconds (ms), ranging from 0 to 2 ms.
- Y-axis: Input voltage \( v_E \) in millivolts (mV), ranging from -20 mV to 20 mV.
- **Output (Bottom):**
- X-axis: Time \( t \) in milliseconds (ms), ranging from 0 to 2 ms.
- Y-axis: Output voltage \( v_O \) in volts (V), ranging from -10 V to 10 V.

3. **Overall Behavior and Trends:**
- **Input (Top):**
- The input waveform is a triangular wave that oscillates between -20 mV and 20 mV, with peaks at approximately 0.5 ms and 1.5 ms, and zero crossings at 0 ms, 1 ms, and 2 ms.
- **Output (Bottom):**
- The output waveform is a clipped sinusoidal wave with peaks at approximately 0.5 ms and 1.5 ms, and zero crossings at 0 ms, 1 ms, and 2 ms. The waveform is saturated at \( \pm 10 \) V, indicating the limits of the amplifier's output swing.

4. **Key Features and Technical Details:**
- The input waveform is a perfect triangular wave, while the output waveform shows saturation due to the amplifier's power supply limits, resulting in a flattened peak.
- The saturation at \( \pm 10 \) V indicates the maximum output voltage the amplifier can produce.
- The clipping effect in the output waveform is a result of the non-linear characteristics of the amplifier when the input exceeds certain thresholds.

5. **Annotations and Specific Data Points:**
- The time points of interest where the input and output waveforms peak and cross zero are clearly marked by vertical grid lines, providing a reference for understanding the timing of the waveform features.

FIGURE 7.4 (a) The voltage transfer curve (VTC) of a practical error amplifier (top), and its slope (bottom), representing the open-loop gain a. (b) Input (top) and output (bottom) waveforms.
eventually flattens out (or saturates), making the gain $a$ drop to zero. (In the example shown $v_{O}$ saturates at $\pm 10 \mathrm{~V}$.) The open loop gain is now more aptly defined as

$$
\begin{equation*}
a=\frac{d v_{O}}{d v_{E}} \tag{7.15}
\end{equation*}
$$

where $v_{O}$ is the instantaneous voltage at the output and $v_{E}$ the instantaneous error voltage at the input. As shown in Fig. $7.4 a$ (bottom), the gain $a$ reaches its maximum of $1000 \mathrm{~V} / \mathrm{V}$ at the origin, progressively decreasing away from the origin, and finally dropping to zero as the amplifier is driven in saturation.

Because of its nonlinear VTC, a practical amplifier will generally yield a distorted output. This is depicted in Fig. 7.4b for the case of a triangular wave at the input (top). The output (bottom) can be regarded as a magnified version of the input, but with significantly compressed peaks because of the decreased gain there. What are we to do with a nonlinear device of this sort in demanding applications such as highfidelity (hi-fi) audio or precision instrumentation, where distortion is intolerable? As we shall see next, this is another instance where negative feedback comes to our rescue.

Once a nonlinear amplifier is placed inside a negative-feedback loop, a closedloop VTC results, whose slope represents the closed loop gain $A$,

$$
\begin{equation*}
A=\frac{d v_{O}}{d v_{I}} \tag{7.16}
\end{equation*}
$$

where $v_{O}$ and $v_{I}$ are the instantaneous output and input voltages. Rewriting Eq. (7.15) as

$$
\frac{1}{a}=\left[\frac{d v_{O}}{d\left(v_{I}-v_{F}\right)}\right]^{-1}=\frac{d v_{I}-d\left(b v_{O}\right)}{d v_{O}}=\frac{1}{A}-b
$$

and rearranging, we get the familiar result

$$
\begin{equation*}
A=\frac{a}{1+a b}=A_{\text {ideal }} \times \frac{1}{1+1 / L} \tag{7.17}
\end{equation*}
$$

where $A_{\text {ideal }}=1 / b$, and $L=a b$ is the familiar loop gain. This indicates that as long as the open-loop gain $a$ is sufficiently large to ensure an adequately high loop gain $L$, the closed-loop gain $A$ will be fairly close to $A_{\text {ideal }}$, even though the gain $a$ decreases as we move away from the origin. Consequently, negative feedback can linearize the VTC of an amplifier dramatically!

To illustrate, consider the PSpice circuit of Fig. 7.5, where an error amplifier with the nonlinear VTC of Fig. 7.4a is placed inside a negative-feedback loop with $b=R_{1} /\left(R_{1}+R_{2}\right)=1 / 4$. The linearizing properties of negative feedback are demonstrated in Fig. 7.6. Compared to the open-loop VTC of Fig. 7.4a, the closed-loop VTC of Fig. 7.6a is far more linear, and the gain $A$ is close to its ideal value of $1 / b$ $(=4 \mathrm{~V} / \mathrm{V}$ in this example) over a much wider range of output voltages. So long as we restrict circuit operation within this range, the output will be a faithful (magnified-by-four) replica of the input. This is shown in Fig. 7.6 b (top) for the case in which $v_{I}$ is a triangular waveform with peak values of $\pm 2 \mathrm{~V}$, so $v_{O}$ is a fairly undistorted triangular wave with peak values of $\pm 8 \mathrm{~V}$. Even more revealing is the error signal $v_{E}$ displayed in Fig. $7.6 b$ (bottom), because it shows the effort required of the error amplifier to make $v_{O}=4 v_{r}$. It is apparent that in order to compensate for the decrease in its open-loop gain away from the origin, the amplifier suitably pre-distorts its own error signal! Historically, it was precisely to reduce output distortion that Harold Black conceived negative feedback in the first place.

EVALUE $10 *((\exp (2 \mathrm{E} 2 * \mathrm{~V}(\% \mathrm{IN}+, \% \mathrm{IN}-))-1) /(\exp (2 \mathrm{E} 2 * \mathrm{~V}(\% \mathrm{IN}+, \% \mathrm{IN}-))+1))$
image_name:FIGURE 7.5
description:
[
name: VI, type: VoltageSource, value: VI, ports: {Np: VI, Nn: GND}
name: R1, type: Resistor, value: 1.0 kΩ, ports: {N1: VF, N2: GND}
name: R2, type: Resistor, value: 3.0 kΩ, ports: {N1: VF, N2: VO}
name: RL, type: Resistor, value: 10 kΩ, ports: {N1: VO, N2: GND}
name: EAMP, type: OpAmp, value: EAMP, ports: {InP: VE, InN: VF, OutP: VO, OutN: GND}
]
extrainfo:The circuit is a negative-feedback system using an error amplifier to control the output voltage. The feedback network consists of resistors R1 and R2, forming a voltage divider. The load resistor RL is connected from the output to ground. The op-amp EAMP has differential inputs and outputs. The input voltage VI is applied to the non-inverting terminal of the op-amp.

FIGURE 7.5 PSpice circuit to display the waveforms of a negative-feedback system utilizing an error amplifier with the nonlinear VTC of Fig. 7.4a.
image_name:(a)
description:The graph labeled (a) consists of two parts, illustrating the closed-loop voltage transfer characteristic (VTC) and the closed-loop gain for a negative-feedback system using an error amplifier.

1. **Type of Graph and Function:**
- The top part of the graph shows the voltage transfer characteristic (VTC) of the system, which is a plot of output voltage \( v_o \) versus input voltage \( v_I \).
- The bottom part of the graph displays the closed-loop gain \( A \) as a function of the input voltage \( v_I \).

2. **Axes Labels and Units:**
- **Top Graph:**
- **X-axis:** Input \( v_I \) in volts (V), ranging from -2 to 2 volts.
- **Y-axis:** Output \( v_o \) in volts (V), ranging from -10 to 10 volts.
- **Bottom Graph:**
- **X-axis:** Input \( v_I \) in volts (V), ranging from -2 to 2 volts.
- **Y-axis:** Closed-loop gain \( A \) in volts/volt (V/V), ranging from 0 to 4 V/V.

3. **Overall Behavior and Trends:**
- **Top Graph (VTC):**
- The VTC is linear over the input range from -2 to 2 volts, indicating a proportional relationship between input and output voltages. The slope of the line represents the closed-loop gain.
- **Bottom Graph (Closed-loop Gain):**
- The gain \( A \) is relatively constant and high (around 4 V/V) over most of the input range but decreases sharply at the extreme ends of the input range (-2 and 2 volts), suggesting saturation effects.

4. **Key Features and Technical Details:**
- **Top Graph:**
- The linear region indicates a stable feedback system with consistent gain.
- The slope of the VTC represents the gain, which is consistent with the gain shown in the bottom graph.
- **Bottom Graph:**
- The gain \( A \) approaches the maximum value of 4 V/V in the linear region, indicating effective feedback control.
- The sharp decrease in gain at the input extremes suggests the limits of the amplifier's linear operating range.

5. **Annotations and Specific Data Points:**
- The top graph includes an annotation "VTC" indicating the linear portion of the graph and "A" representing the slope.
- The bottom graph includes an annotation "A" at the peak gain level, highlighting the closed-loop gain value.
image_name:(b)
description:The graph labeled as "(b)" consists of two subplots illustrating the behavior of waveforms in a negative-feedback system involving an error amplifier.

1. **Type of Graph and Function:**
- The top subplot is a time-domain waveform graph showing the input and output voltages of the system.
- The bottom subplot is also a time-domain waveform graph displaying the error voltage over time.

2. **Axes Labels and Units:**
- **Top Subplot:**
- The x-axis is labeled "Time t (ms)" and represents time in milliseconds, ranging from 0 to 2 ms.
- The y-axis is labeled "Waveforms (V)" and shows voltage in volts, with a range from -10 V to 10 V.
- **Bottom Subplot:**
- The x-axis is the same as the top subplot, "Time t (ms)", ranging from 0 to 2 ms.
- The y-axis is labeled "Error voltage v_E (mV)" and displays voltage in millivolts, ranging from -10 mV to 10 mV.

3. **Overall Behavior and Trends:**
- **Top Subplot:**
- The waveform for the input voltage \(v_I\) appears as a triangular wave, starting at -10 V, peaking at 10 V, and returning to -10 V, completing one cycle over 1 ms.
- The output voltage \(v_O\) follows a similar triangular pattern but with a phase shift and possibly different amplitude, indicating the effect of the feedback system.
- **Bottom Subplot:**
- The error voltage \(v_E\) also shows a triangular waveform, synchronized with the input and output waveforms, but with a much smaller amplitude, peaking at about ±10 mV.

4. **Key Features and Technical Details:**
- The triangular waveforms indicate a periodic signal with a frequency of approximately 1 kHz (since one full cycle is completed in 1 ms).
- The small amplitude of the error voltage \(v_E\) suggests effective feedback control, minimizing the error between input and output.

5. **Annotations and Specific Data Points:**
- The graph does not include specific numerical annotations or reference lines beyond the axes labels and units.
- The symmetry and periodicity of the waveforms are key features, highlighting the system's response to the input signal and the feedback mechanism's role in reducing error.

FIGURE 7.6 Illustrating the linearizing properties of negative feedback: (a) the closed-loop VTC (top) and its slope (bottom), representing the closed-loop gain $A$; (b) the input and output waveforms (top) and the error waveform (bottom).

### Effect of Negative Feedback on Noise

We now wish to investigate the effect of negative feedback upon disturbances. Henceforth referred to as noise, disturbances may enter the amplifier at the input node $\left(v_{n 1}\right)$, at some intermediate node $\left(v_{n 2}\right)$, or at the output node $\left(v_{n 3}\right)$. As depicted in Fig. 7.7, we use summers to model the points of entry of the various noise components. Moreover, to model the entry of intermediate noise, we split the amplifier into two stages with individual gains $a_{1}$ and $a_{2}$, respectively (clearly, the overall gain is $a=a_{1} \times a_{2}$ ). Starting out at the right and progressively moving toward the left, we write

$$
v_{o}=v_{n 3}+a_{2}\left[v_{n 2}+a_{1}\left(v_{i}+v_{n 1}-b v_{o}\right)\right]
$$

image_name:Figure 7.7
description:The system block diagram, labeled as Figure 7.7, illustrates a model for investigating the effect of negative feedback on voltage noise. The diagram consists of several key components arranged in a sequence to demonstrate how various noise components are introduced and amplified within a feedback loop.

1. **Main Components:**
- **Summers (Σ):** There are three summers in the diagram. These are used to model the entry points of noise components. Each summer adds its respective noise voltage to the signal.
- **Amplifiers (a₁ and a₂):** The system includes two amplifiers, each with gains labeled as \(a₁\) and \(a₂\). These are used to amplify the input signal and the noise components.
- **Feedback Amplifier (b):** A feedback path is present with a gain labeled as \(b\), which is used to provide negative feedback to the system.

2. **Flow of Information or Control:**
- The input voltage \(v_i\) enters the first summer, where it is combined with a noise component \(v_{n1}\) and a feedback voltage \(v_f\) (which is the output voltage \(v_o\) multiplied by the feedback gain \(b\)).
- The output of the first summer is then amplified by the first amplifier with gain \(a₁\).
- The amplified signal is fed into the second summer, where another noise component \(v_{n2}\) is added.
- This combined signal is then amplified by the second amplifier with gain \(a₂\).
- The output of the second amplifier is fed into the third summer, where the final noise component \(v_{n3}\) is added.
- The final output voltage \(v_o\) is taken from the output of the third summer.
- The feedback loop is completed by feeding \(v_o\) back through the feedback amplifier with gain \(b\), producing \(v_f\), which is subtracted at the first summer.

3. **Labels, Annotations, and Key Indicators:**
- Each summer is labeled with a plus sign to indicate the addition of noise components \(v_{n1}, v_{n2}, v_{n3}\).
- The gains of the amplifiers are labeled as \(a₁\) and \(a₂\), with the feedback gain labeled as \(b\).

4. **Overall System Function:**
- The primary function of this system is to model the effect of negative feedback on voltage noise in an amplifier circuit. The arrangement of summers and amplifiers demonstrates how noise is introduced at various stages and how feedback influences the overall output. The closed-loop gain of the system is determined by the product of the individual gains and the feedback factor, effectively amplifying the input signal and the noise terms while stabilizing the system through negative feedback.

FIGURE 7.7 Model to investigate the effect of negative feedback upon voltage noise.
where we have used $v_{f}=b v_{o}$. Collecting, letting $a=a_{1} \times a_{2}$, and solving for $v_{o}$, we get, after minor algebra,

$$
\begin{equation*}
v_{o}=A\left(v_{i}+v_{n 1}+\frac{v_{n 2}}{a_{1}}+\frac{v_{n 3}}{a_{1} \times a_{2}}\right) \tag{7.18}
\end{equation*}
$$

where $A$ is the closed-loop gain of Eq. (7.17). We observe that a negative-feedback circuit amplifies all three noise terms with the same gain $A$ as the useful signal $v_{i}$. However, while $v_{n 1}$ is unchanged, $v_{n 2}$ is divided by $a_{1}$, and $v_{n 3}$ is divided by $a_{1} \times a_{2}$. We summarize this by saying that in a negative-feedback circuit a noise component, reflected to the input, gets divided by the gain(s) of the stage(s) preceding it. This property is often exploited to reduce the effect of a given noise source, such as hum creeping into the power stage of an audio system. If we precede this stage by an additional amplifier with suitably high gain, and we close a negative-feedback loop around the composite circuit, we can make the hum component, reflected to the input, as small as desired compared to the audio signal $v_{i}$, thus raising the signal-tonoise ratio to an acceptable level.

As a dramatic demonstration of the curative properties of negative feedback upon noise, consider the situation of Fig. 7.8a, where a source $v_{I}$ is buffered to a load $R_{L}$ via the Class AB push-pull stage $Q_{1}-Q_{2}$. Ideally, the buffer should give

$$
v_{O(\text { deal })}=v_{I}
$$

image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: VCC, B: VI, E: VO}
name: Q2, type: PNP, ports: {C: VEE, B: VI, E: VO}
name: V1, type: VoltageSource, value: V1, ports: {Np: VI, Nn: GND}
name: RL, type: Resistor, value: 1kΩ, ports: {N1: VO, N2: GND}
]
extrainfo:The circuit is a Class AB push-pull amplifier with a voltage source V1 driving a load resistor RL through transistors Q1 (NPN) and Q2 (PNP). The power supply voltages are VCC (+5V) and VEE (-5V).

(a)
image_name:(b) Input and output waveforms
description:The graph consists of two parts: the top graph shows the input and output waveforms, and the bottom graph illustrates the output noise.

**Top Graph: Input and Output Waveforms**
- **Type of Graph:** Time-domain waveform.
- **Axes Labels and Units:**
- **X-axis:** Time \( t \) in milliseconds (ms), ranging from 0 to 2 ms.
- **Y-axis:** Voltage in volts (V), ranging from -2.0 V to 2.0 V.
- **Overall Behavior and Trends:**
- The input waveform is a sinusoidal wave with peaks at approximately ±2 V.
- The output waveform \( v_O \) follows the input waveform but shows a noticeable distortion around the zero-crossing points due to the dead zone created by the 0.7 V threshold required to turn on the BJTs.
- The ideal output \( v_{O(ideal)} \) is also plotted, showing a perfect sinusoidal shape without distortion.
- **Key Features and Technical Details:**
- The output waveform \( v_O \) deviates from the ideal waveform within the range of -0.7 V to 0.7 V, where the output remains at zero, illustrating the dead zone effect.
- Outside this range, the output approximately matches the input but offset by ±0.7 V, as described in the context.

**Bottom Graph: Output Noise**
- **Type of Graph:** Time-domain waveform.
- **Axes Labels and Units:**
- **X-axis:** Time \( t \) in milliseconds (ms), ranging from 0 to 2 ms.
- **Y-axis:** Output noise voltage \( v_N \) in volts (V), ranging from -2.0 V to 2.0 V.
- **Overall Behavior and Trends:**
- The output noise \( v_N \) shows a rectangular waveform pattern, with distinct flat regions at approximately ±0.7 V.
- **Key Features and Technical Details:**
- The noise waveform indicates the difference between the actual output and the ideal output, highlighting the distortion primarily around the zero-crossing points.
- The noise levels are consistent with the dead zone effect, maintaining a flat level during these periods and returning to zero when the input signal is sufficient to overcome the transistor threshold voltage.
image_name:Output noise
description:The graph titled "Output noise" is a time-domain waveform plot that displays the output noise voltage of a Class AB push-pull amplifier circuit. It is divided into two sections: the top section shows input and output waveforms, while the bottom section focuses on the output noise.

Top Section: Input and Output Waveforms
- **Axes Labels and Units:**
- **X-axis:** Time \( t \) in milliseconds (ms), ranging from 0 to 2 ms.
- **Y-axis:** Voltage (V), ranging from -2 V to 2 V.

- **Overall Behavior and Trends:**
- The plot illustrates two waveforms: the ideal output voltage \( v_{O(ideal)} \) and the actual output voltage \( v_{O} \).
- Both waveforms are sinusoidal with a period of approximately 1 ms, indicating a frequency of about 1 kHz.
- The ideal waveform \( v_{O(ideal)} \) is smooth and continuous, while the actual output \( v_{O} \) shows distortion, particularly around zero crossings.

- **Key Features and Technical Details:**
- The actual output waveform \( v_{O} \) deviates from the ideal waveform \( v_{O(ideal)} \) due to the 0.7 V threshold required to turn on the BJTs, resulting in a dead zone around zero crossings.
- The output voltage \( v_{O} \) is approximately zero for input voltages between -0.7 V and 0.7 V, leading to visible clipping in this range.

Bottom Section: Output Noise
- **Axes Labels and Units:**
- **X-axis:** Time \( t \) in milliseconds (ms), ranging from 0 to 2 ms.
- **Y-axis:** Output noise voltage \( v_{N} \) in volts (V), ranging from -2 V to 2 V.

- **Overall Behavior and Trends:**
- The noise waveform \( v_{N} \) is a stepped waveform with distinct levels, reflecting the difference between the actual and ideal output voltages.
- The waveform is periodic with a period of approximately 1 ms, matching the frequency of the input and output waveforms.

- **Key Features and Technical Details:**
- The noise voltage \( v_{N} \) peaks at approximately ±0.7 V, corresponding to the voltage drop across the BJTs when they turn on.
- The noise waveform highlights the distortion introduced by the dead zone, with distinct flat sections around the zero crossings where the BJTs are not conducting.

This analysis provides a comprehensive understanding of the output noise characteristics in the context of a Class AB push-pull amplifier circuit, illustrating the effects of transistor turn-on thresholds on the output waveform.

(b)

FIGURE 7.8 (a) PSpice circuit simulating a source $v_{\text {, }}$ driving a load $R_{L}$ via a push-pull stage $Q_{1}-Q_{2}$. (b) Input and output waveforms (top), and output noise $v_{N}=v_{0}-v_{\text {O(idea) }}$ (bottom).

However, since it takes about 0.7 V for each BJT to turn on, the circuit gives $v_{O}=0$ for $-0.7 \mathrm{~V}<v_{I}<0.7 \mathrm{~V}, v_{O} \cong v_{I}-0.7 \mathrm{~V}$ for $v_{I}>0.7 \mathrm{~V}$, and $v_{O} \cong v_{I}+0.7 \mathrm{~V}$ for $v_{I}$ $<0.7 \mathrm{~V}$. The waveforms, shown in Fig. $7.8 b$ (top), reveal a much distorted output. In fact, things go as if the non-linearity of the push-pull stage resulted in the injection of the voltage noise

$$
v_{N}=v_{O}-v_{O(\text { ideal })}
$$

depicted in Fig. 7.8b (bottom). We can reduce $v_{N}$ by preceding the buffer by a suitable error amplifier and then closing a negative-feedback loop around the composite circuit. The example depicted in Fig. 7.9a uses an amplifier with gain of only $a=$ $10 \mathrm{~V} / \mathrm{V}$, and a plain wire as the feedback network to yield $b=1 \mathrm{~V} / \mathrm{V}$. The ensuing reduction in distortion can be appreciated by comparing the waveforms of Fig. 7.9b (top and middle) with their counterparts of Fig. $7.8 b$ (top and bottom). One can readily see that the insertion of the amplifier makes the 0.7 -voltage drops appear as if they were reduced to about $(0.7 \mathrm{~V}) / a$, or 0.07 V in our example.
image_name:(a)
description:
[
name: V_I, type: VoltageSource, value: V_I, ports: {Np: V_I, Nn: GND}
name: U1, type: OpAmp, value: 10 V/V, ports: {InP: V_I, InN: V_F, OutP: V_OA, OutN: GND}
name: Q1, type: NPN, ports: {C: V_CC, B: V_OA, E: V_O}
name: Q2, type: PNP, ports: {C: V_EE, B: V_OA, E: V_O}
name: R_L, type: Resistor, value: 1 kΩ, ports: {N1: V_O, N2: GND}
]
extrainfo:The circuit employs an op-amp with a gain of 10 V/V in a negative-feedback configuration to drive a push-pull stage consisting of NPN and PNP transistors. This setup is used to reduce output distortion by minimizing voltage drops across the transistors.

(a)
image_name:I/O waveforms
description:The function graph consists of three subplots, each illustrating different aspects of the circuit's performance over time. The horizontal axis in all graphs is labeled as time \( t \) in milliseconds (ms), ranging from 0 to 2 ms.

1. **Top Subplot: I/O Waveforms**
- **Type of Graph:** Time-domain waveform.
- **Axes Labels and Units:** The vertical axis represents voltage \( V \) in volts, with a range from -2.0 V to 2.0 V.
- **Overall Behavior and Trends:** The plot shows two waveforms: the actual output voltage \( v_O \) and the ideal output voltage \( v_{O(ideal)} \). Both waveforms are sinusoidal with a peak-to-peak amplitude of approximately 4 V, oscillating between -2 V and 2 V.
- **Key Features and Technical Details:** The actual output \( v_O \) closely follows the ideal output \( v_{O(ideal)} \), with minor deviations indicating slight distortion.

2. **Middle Subplot: Output Noise**
- **Type of Graph:** Time-domain waveform.
- **Axes Labels and Units:** The vertical axis represents voltage \( V \) in volts, ranging from -2.0 V to 2.0 V.
- **Overall Behavior and Trends:** The plot shows the output noise \( v_N \), which is the difference between the actual output and the ideal output. The waveform has a smaller amplitude compared to the I/O waveforms, indicating minor noise or distortion.
- **Key Features and Technical Details:** The noise appears periodic and correlates with the peaks and troughs of the input waveform.

3. **Bottom Subplot: Amplifier Waveforms**
- **Type of Graph:** Time-domain waveform.
- **Axes Labels and Units:** The vertical axis represents voltage \( V \) in volts, with a range from -2.0 V to 2.0 V.
- **Overall Behavior and Trends:** This plot shows the amplifier output voltage \( v_{OA} \) and the actual output voltage \( v_O \). The amplifier output \( v_{OA} \) has a higher amplitude and shows more pronounced peaks and troughs compared to \( v_O \).
- **Key Features and Technical Details:** The amplifier output waveform \( v_{OA} \) is more exaggerated, indicating the amplifier's role in driving the push-pull stage and compensating for distortion.
image_name:Output noise
description:The graph titled 'Output noise' is part of a set of three time-domain waveform graphs. Each graph is plotted over a time period ranging from 0 to 2 milliseconds (ms) on the x-axis. The y-axis of each graph represents voltage in volts (V), with a range from -2.0 V to 2.0 V.

1. **Top Graph (I/O Waveforms):**
- This graph compares the actual output voltage $v_O$ with the ideal output voltage $v_{O(ideal)}$. The ideal waveform is depicted as a smooth sine wave oscillating between 2.0 V and -2.0 V, suggesting a perfect sinusoidal input. The actual output waveform $v_O$ closely follows the ideal but shows slight deviations, indicating minor distortions.

2. **Middle Graph (Output Noise):**
- This graph shows the output noise $v_N$, defined as the difference between the actual output voltage $v_O$ and the ideal output voltage $v_{O(ideal)}$. The waveform oscillates around 0 V, with small amplitude variations indicating the presence of noise or distortion. The noise peaks are relatively small, staying well within ±0.5 V, showing that the distortion is minimal.

3. **Bottom Graph (Amplifier Waveforms):**
- This graph displays the amplifier output waveform $v_{OA}$ compared to the actual output $v_O$. The amplifier output $v_{OA}$ shows a more pronounced deviation from the sinusoidal shape, particularly at the peaks and troughs, indicating the amplifier's role in compensating for the distortion and maintaining the output close to the ideal.

Overall, these graphs illustrate the effectiveness of the negative-feedback loop in reducing output distortion, with the amplifier actively adjusting to minimize the difference between the actual and ideal output voltages.
image_name:Amplifier waveforms
description:The graph titled "Amplifier waveforms" consists of three subplots, each depicting a different aspect of the amplifier's performance over time.

1. **Top Plot (I/O waveforms):**
- **Type:** Time-domain waveform.
- **Axes:**
- X-axis: Time \( t \) in milliseconds (ms), ranging from 0 to 2 ms.
- Y-axis: Voltage (V), ranging from -2 V to 2 V.
- **Behavior:**
- The plot shows two waveforms: the ideal output voltage \( v_{O(ideal)} \) and the actual output voltage \( v_O \).
- Both waveforms exhibit a sinusoidal pattern, but the actual output slightly deviates from the ideal, especially noticeable at the peaks.
- The ideal waveform is depicted in light gray, whereas the actual output is in black.

2. **Middle Plot (Output noise):**
- **Type:** Time-domain waveform.
- **Axes:**
- X-axis: Time \( t \) in milliseconds (ms), ranging from 0 to 2 ms.
- Y-axis: Voltage (V), ranging from -2 V to 2 V.
- **Behavior:**
- This plot shows the output noise \( v_N \), defined as the difference between the actual output and the ideal output.
- The noise waveform oscillates around 0 V, indicating minor deviations from the ideal output.
- The amplitude of the noise is relatively small compared to the main signal.

3. **Bottom Plot (Amplifier waveforms):**
- **Type:** Time-domain waveform.
- **Axes:**
- X-axis: Time \( t \) in milliseconds (ms), ranging from 0 to 2 ms.
- Y-axis: Voltage (V), ranging from -2 V to 2 V.
- **Behavior:**
- This plot displays the op-amp output \( v_{OA} \) and the actual output \( v_O \).
- The op-amp output waveform is more pronounced, showing a larger amplitude compared to the actual output.
- The op-amp output is depicted in black, while the actual output is in gray.

**Overall Trends and Key Features:**
- The waveforms indicate a sinusoidal signal being processed by the amplifier circuit.
- The top plot highlights the slight distortion between the ideal and actual outputs, addressed in the feedback loop.
- The middle plot quantifies the output noise, showing minimal deviation.
- The bottom plot illustrates the role of the op-amp in amplifying the signal, with the op-amp output having a larger amplitude than the final output, suggesting a gain reduction through feedback.

(b)

FIGURE 7.9 (a) Preceding the push-pull stage of Fig. 7.8a by an amplifier, and closing a negative-feedback loop around the whole circuit in order to reduce output distortion. (b) Input and output waveforms (top), output noise $v_{N}=v_{O}-v_{\text {O(ideal) }}$ (middle), and the op amp output waveform $v_{O A}$ (bottom).

To fully appreciate the role of the amplifier, it is instructive to display also its output $v_{O A}$, which is shown in Fig. $7.9 b$ (bottom). In its attempt to make $v_{O}$ follow $v_{I}$, the amplifier will have to swing its output $v_{O A}$ about 0.7 V above $v_{O}$ during the positive alternations, and 0.7 V below $v_{o}$ during the negative alternations. In this example we have used an amplifier with a gain of only $10 \mathrm{~V} / \mathrm{V}$, but a unit with much higher gain will reduce distortion in proportion, making $v_{O}$ a much more faithful replica of $v_{I}$. Recall that we have already observed this behavior in connection with the superdiode circuit of Section 1.10. Now we are simply revisiting an already-familiar concept, but from a negative-feedback perspective.
Remark: The goal of the negative-feedback circuit example of Fig. 7.9a is to implement an amplifier with gain $A=1 \mathrm{~V} / \mathrm{V}$ and reduced distortion. To this end, we insert an error amplifier with gain $a=10 \mathrm{~V} / \mathrm{V}$. In so doing we are in effect throwing away a gain-of-ten to achieve only a gain-of-one, but this price is well worth the ensuing reduction in distortion. Needless to say, it is important to distinguish between the basic error amplifier and the overall amplifier resulting from operating the former in conjunction with the negative feedback network (a mere wire in the present example).
