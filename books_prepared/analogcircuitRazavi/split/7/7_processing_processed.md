# 7. CMOS Amplifiers

Most CMOS amplifiers have identical bipolar counterparts and can therefore be analyzed in the same fashion. Our study in this chapter parallels the developments in Chapter 5, identifying both similarities and differences between CMOS and bipolar circuit topologies. It is recommended that the reader review Chapter 5, specifically, Section 5.1. We assume the reader is familiar with concepts such as I/O impedances, biasing, and dc and small-signal analysis. The outline of the chapter is shown below.

General Concepts

- Biasing of MOS Stages
- Realization of Current Sources

MOS Amplifiers

- Common-Source Stage
- Common-Gate Stage
- Source Follower

## 7.1 GENERAL CONSIDERATIONS

### 7.1.1 MOS Amplifier Topologies

Recall from Section 5.3 that the nine possible circuit topologies using a bipolar transistor in fact reduce to three useful configurations. The similarity of bipolar and MOS small-signal models (i.e., a voltage-controlled current source) suggests that the same must hold for MOS amplifiers. In other words, we expect three basic CMOS amplifiers: the "common-source" (CS) stage, the "common-gate" (CG) stage, and the "source follower."

### 7.1.2 Biasing

Depending on the application, MOS circuits may incorporate biasing techniques that are quite different from those described in Chapter 5 for bipolar stages. Most of these techniques are beyond the scope of this book and some methods are studied in Chapter 5. Nonetheless, it is still instructive to apply some of the biasing concepts of Chapter 5 to MOS stages.
image_name:Figure 7.1 MOS stage with biasing
description:
[
name: R1, type: Resistor, value: 4kΩ, ports: {N1: VDD, N2: X}
name: R2, type: Resistor, value: 10kΩ, ports: {N1: X, N2: GND}
name: RS, type: Resistor, value: 1kΩ, ports: {N1: S1, N2: GND}
name: RD, type: Resistor, ports: {N1: VDD, N2: Y}
name: M1, type: NMOS, ports: {S: S1, D: Y, G: X}
name: VDD, type: VoltageSource, value: 1.8V, ports: {Np: VDD, Nn: GND}
]
extrainfo:The circuit is a MOS stage with biasing, using resistors R1 and R2 to set the gate voltage. M1 is an NMOS transistor operating in saturation, with RD connected to VDD and RS to ground. The gate voltage is determined by the voltage divider formed by R1 and R2.

Figure 7.1 MOS stage with biasing.
Consider the circuit shown in Fig. 7.1, where the gate voltage is defined by $R_{1}$ and $R_{2}$. We assume $M_{1}$ operates in saturation. Also, in most bias calculations, we can neglect channel-length modulation. Noting that the gate current is zero, we have

$$
\begin{equation*}
V_{X}=\frac{R_{2}}{R_{1}+R_{2}} V_{D D} \tag{7.1}
\end{equation*}
$$

Since $V_{X}=V_{G S}+I_{D} R_{S}$,

$$
\begin{equation*}
\frac{R_{2}}{R_{1}+R_{2}} V_{D D}=V_{G S}+I_{D} R_{S} \tag{7.2}
\end{equation*}
$$

Also,

$$
\begin{equation*}
I_{D}=\frac{1}{2} \mu_{n} C_{o x} \frac{W}{L}\left(V_{G S}-V_{T H}\right)^{2} \tag{7.3}
\end{equation*}
$$

Equations (7.2) and (7.3) can be solved to obtain $I_{D}$ and $V_{G S}$, either by iteration or by finding $I_{D}$ from Eq. (7.2) and replacing for it in Eq. (7.3):

$$
\begin{equation*}
\left(\frac{R_{2}}{R_{1}+R_{2}} V_{D D}-V_{G S}\right) \frac{1}{R_{S}}=\frac{1}{2} \mu_{n} C_{o x} \frac{W}{L}\left(V_{G S}-V_{T H}\right)^{2} \tag{7.4}
\end{equation*}
$$

That is,

$$
\begin{align*}
V_{G S} & =-\left(V_{1}-V_{T H}\right)+\sqrt{\left(V_{1}-V_{T H}\right)^{2}-V_{T H}^{2}+\frac{2 R_{2}}{R_{1}+R_{2}} V_{1} V_{D D}}  \tag{7.5}\\
& =-\left(V_{1}-V_{T H}\right)+\sqrt{V_{1}^{2}+2 V_{1}\left(\frac{R_{2} V_{D D}}{R_{1}+R_{2}}-V_{T H}\right)} \tag{7.6}
\end{align*}
$$

where

$$
\begin{equation*}
V_{1}=\frac{1}{\mu_{n} C_{o x} \frac{W}{L} R_{S}} \tag{7.7}
\end{equation*}
$$

This value of $V_{G S}$ can then be substituted in Eq. (7.2) to obtain $I_{D}$. Of course, $V_{Y}$ must exceed $V_{X}-V_{T H}$ to ensure operation in the saturation region.

```
Example
7.1
```

Determine the bias current of $M_{1}$ in Fig. 7.1 assuming $V_{T H}=0.5 \mathrm{~V}, \mu_{n} C_{o x}=$ $100 \mu \mathrm{~A} / \mathrm{V}^{2}, W / L=5 / 0.18$, and $\lambda=0$. What is the maximum allowable value of $R_{D}$ for $M_{1}$ to remain in saturation?

Solution We have

$$
\begin{align*}
V_{X} & =\frac{R_{2}}{R_{1}+R_{2}} V_{D D}  \tag{7.8}\\
& =1.286 \mathrm{~V} . \tag{7.9}
\end{align*}
$$

With an initial guess $V_{G S}=1 \mathrm{~V}$, the voltage drop across $R_{S}$ can be expressed as $V_{X}-V_{G S}=286 \mathrm{mV}$, yielding a drain current of $286 \mu \mathrm{~A}$. Substituting for $I_{D}$ in Eq. (7.3) gives the new value of $V_{G S}$ as

$$
\begin{align*}
V_{G S} & =V_{T H}+\sqrt{\frac{2 I_{D}}{\mu_{n} C_{o x} \frac{W}{L}}}  \tag{7.10}\\
& =0.954 \mathrm{~V} \tag{7.11}
\end{align*}
$$

Consequently,

$$
\begin{align*}
I_{D} & =\frac{V_{X}-V_{G S}}{R_{S}}  \tag{7.12}\\
& =332 \mu \mathrm{~A} \tag{7.13}
\end{align*}
$$

and hence

$$
\begin{equation*}
V_{G S}=0.989 \mathrm{~V} \tag{7.14}
\end{equation*}
$$

This gives $I_{D}=297 \mu \mathrm{~A}$.
As seen from the iterations, the solutions converge more slowly than those encountered in Chapter 5 for bipolar circuits. This is due to the quadratic (rather than exponential) $I_{D}-V_{G S}$ dependence. We may therefore utilize the exact result in Eq. (7.6) to avoid lengthy calculations. Since $V_{1}=0.36 \mathrm{~V}$,

$$
\begin{equation*}
V_{G S}=0.974 \mathrm{~V} \tag{7.15}
\end{equation*}
$$

and

$$
\begin{align*}
I_{D} & =\frac{V_{X}-V_{G S}}{R_{S}}  \tag{7.16}\\
& =312 \mu \mathrm{~A} \tag{7.17}
\end{align*}
$$

The maximum allowable value of $R_{D}$ is obtained if $V_{Y}=V_{X}-V_{T H}=0.786 \mathrm{~V}$. That is,

$$
\begin{align*}
R_{D} & =\frac{V_{D D}-V_{Y}}{I_{D}}  \tag{7.18}\\
& =3.25 \mathrm{k} \Omega \tag{7.19}
\end{align*}
$$

Exercise What is the value of $R_{2}$ that places $M_{1}$ at the edge of saturation?

In the circuit of Example 7.1, assume $M_{1}$ is in saturation and $R_{D}=2.5 \mathrm{k} \Omega$ and compute (a) the maximum allowable value of $W / L$ and (b) the minimum allowable value of $R_{S}$ (with $W / L=5 / 0.18$ ). Assume $\lambda=0$.

Solution (a) As $W / L$ becomes larger, $M_{1}$ can carry a larger current for a given $V_{G S}$. With $R_{D}=2.5 \mathrm{k} \Omega$ and $V_{X}=1.286 \mathrm{~V}$, the maximum allowable value of $I_{D}$ is given by

$$
\begin{align*}
I_{D} & =\frac{V_{D D}-V_{Y}}{R_{D}}  \tag{7.20}\\
& =406 \mu \mathrm{~A} . \tag{7.21}
\end{align*}
$$

The voltage drop across $R_{S}$ is then equal to 406 mV , yielding $V_{G S}=1.286 \mathrm{~V}-$ $0.406 \mathrm{~V}=0.88 \mathrm{~V}$. In other words, $M_{1}$ must carry a current of $406 \mu \mathrm{~A}$ with $V_{G S}=0.88 \mathrm{~V}$ :

$$
\begin{align*}
I_{D} & =\frac{1}{2} \mu_{n} C_{o x} \frac{W}{L}\left(V_{G S}-V_{T H}\right)^{2}  \tag{7.22}\\
406 \mu \mathrm{~A} & =\left(50 \mu \mathrm{~A} / \mathrm{V}^{2}\right) \frac{W}{L}(0.38 \mathrm{~V})^{2} \tag{7.23}
\end{align*}
$$

thus,

$$
\begin{equation*}
\frac{W}{L}=56.2 \tag{7.24}
\end{equation*}
$$

(b) With $W / L=5 / 0.18$, the minimum allowable value of $R_{S}$ gives a drain current of $406 \mu \mathrm{~A}$. Since

$$
\begin{align*}
V_{G S} & =V_{T H}+\sqrt{\frac{2 I_{D}}{\mu_{n} C_{o x} \frac{W}{L}}}  \tag{7.25}\\
& =1.041 \mathrm{~V} \tag{7.26}
\end{align*}
$$

the voltage drop across $R_{S}$ is equal to $V_{X}-V_{G S}=245 \mathrm{mV}$. It follows that

$$
\begin{align*}
R_{S} & =\frac{V_{X}-V_{G S}}{I_{D}}  \tag{7.27}\\
& =604 \Omega . \tag{7.28}
\end{align*}
$$

Exercise Repeat the above example if $V_{T H}=0.35 \mathrm{~V}$.

The self-biasing technique of Fig. 5.22 can also be applied to MOS amplifiers. Depicted in Fig. 7.2, the circuit can be analyzed by noting that $M_{1}$ is in saturation (why?) and the voltage drop across $R_{G}$ is zero. Thus,

$$
\begin{equation*}
I_{D} R_{D}+V_{G S}+R_{S} I_{D}=V_{D D} \tag{7.29}
\end{equation*}
$$

Finding $V_{G S}$ from this equation and substituting it in Eq. (7.3), we have

$$
\begin{equation*}
I_{D}=\frac{1}{2} \mu_{n} C_{o x} \frac{W}{L}\left[V_{D D}-\left(R_{S}+R_{D}\right) I_{D}-V_{T H}\right]^{2} \tag{7.30}
\end{equation*}
$$

image_name:Figure 7.2 Self-biased MOS stage
description:
[
name: M1, type: NMOS, ports: {S: s1, D: d1, G: g1}
name: RG, type: Resistor, value: RG, ports: {N1: g1, N2: d1}
name: RD, type: Resistor, value: RD, ports: {N1: d1, N2: VDD}
name: RS, type: Resistor, value: RS, ports: {N1: s1, N2: GND}
]
extrainfo:The circuit is a self-biased NMOS amplifier with M1 in saturation. The voltage drop across RG is zero, indicating no gate current. The drain current ID flows from VDD through RD and M1 to GND.

Figure 7.2 Self-biased MOS stage.
where channel-length modulation is neglected. It follows that

$$
\begin{equation*}
\left(R_{S}+R_{D}\right)^{2} I_{D}^{2}-2\left[\left(V_{D D}-V_{T H}\right)\left(R_{S}+R_{D}\right)+\frac{1}{\mu_{n} C_{o x} \frac{W}{L}}\right] I_{D}+\left(V_{D D}-V_{T H}\right)^{2}=0 \tag{7.31}
\end{equation*}
$$

Example $\quad$ Calculate the drain current of $M_{1}$ in Fig. 7.3 if $\mu_{n} C_{o x}=100 \mu \mathrm{~A} / \mathrm{V}^{2}, V_{T H}=0.5 \mathrm{~V}$, and 7.3 $\lambda=0$. What value of $R_{D}$ is necessary to reduce $I_{D}$ by a factor of two?
image_name:Fig. 7.3
description:
[
name: VDD, type: VoltageSource, value: 1.8V, ports: {Np: VDD, Nn: GND}
name: RD, type: Resistor, value: 1kΩ, ports: {N1: VDD, N2: d1}
name: Resistor, type: Resistor, value: 20kΩ, ports: {N1: d1, N2: g1}
name: M1, type: NMOS, ports: {S: s1, D: d1, G: g1}
name: Resistor, type: Resistor, value: 200Ω, ports: {N1: s1, N2: GND}
]
extrainfo:The circuit is a self-biased NMOS stage with a drain current of 556 μA. The width-to-length ratio (W/L) of the NMOS transistor M1 is 5/0.18.

Figure 7.3 Example of self-biased MOS stage.
Solution Equation (7.31) gives

$$
\begin{equation*}
I_{D}=556 \mu \mathrm{~A} \tag{7.32}
\end{equation*}
$$

To reduce $I_{D}$ to $278 \mu \mathrm{~A}$, we solve Eq. (7.31) for $R_{D}$ :

$$
\begin{equation*}
R_{D}=2.867 \mathrm{k} \Omega \tag{7.33}
\end{equation*}
$$

### 7.1.3 Realization of Current Sources

MOS transistors operating in saturation can act as current sources. As illustrated in Fig. 7.4(a), an NMOS device serves as a current source with one terminal tied to ground, i.e., it draws current from node $X$ to ground. On the other hand, a PMOS transistor
image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: X, G: Vb}
]
extrainfo:The NMOS transistor M1 acts as a current source drawing current from node X to ground.

(a)
image_name:(b)
description:
[
name: M2, type: PMOS, ports: {S: VDD, D: Y, G: Vb}
]
extrainfo:The PMOS transistor M2 acts as a current source, providing current from VDD to node Y. It is controlled by the bias voltage Vb.

(b)
image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: Y, G: Vb}
]
extrainfo:The NMOS transistor M1 is connected with its source to GND, drain to node Y, and gate to Vb. It acts as a current source drawing current from node Y to ground.

(c)
<img class="imgSvg" id = "m38ptgief1wld20dgpt" src="data:image/svg+xml;base64,PHN2ZyBpZD0ic21pbGVzLW0zOHB0Z2llZjF3bGQyMGRncHQiIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyIgdmlld0JveD0iMCAwIDIyNiAxMjMuODM5NDQzMDY5NTE3OTgiIHN0eWxlPSJ3aWR0aDogMjI1Ljc1MDAyNDQ4NjQ3NzI2cHg7IGhlaWdodDogMTIzLjgzOTQ0MzA2OTUxNzk4cHg7IG92ZXJmbG93OiB2aXNpYmxlOyI+PGRlZnM+PGxpbmVhckdyYWRpZW50IGlkPSJsaW5lLW0zOHB0Z2llZjF3bGQyMGRncHQtMSIgZ3JhZGllbnRVbml0cz0idXNlclNwYWNlT25Vc2UiIHgxPSIxNjcuOTk5OTk5OTk5OTQ5MjQiIHkxPSI3NS41NTk2ODUyNjIyNDA3MiIgeDI9IjE4My43NTAwMjQ0ODY0NzcyMyIgeTI9IjQ4LjI3OTg5OTE4MDM0OTA4NCI+PHN0b3Agc3RvcC1jb2xvcj0iY3VycmVudENvbG9yIiBvZmZzZXQ9IjIwJSI+PC9zdG9wPjxzdG9wIHN0b3AtY29sb3I9ImN1cnJlbnRDb2xvciIgb2Zmc2V0PSIxMDAlIj48L3N0b3A+PC9saW5lYXJHcmFkaWVudD48bGluZWFyR3JhZGllbnQgaWQ9ImxpbmUtbTM4cHRnaWVmMXdsZDIwZGdwdC0zIiBncmFkaWVudFVuaXRzPSJ1c2VyU3BhY2VPblVzZSIgeDE9IjEzNi40OTk5OTk5OTk5NjE5NCIgeTE9Ijc1LjU1OTY1Njk4NzYyNjM0IiB4Mj0iMTY3Ljk5OTk5OTk5OTk0OTI0IiB5Mj0iNzUuNTU5Njg1MjYyMjQwNzIiPjxzdG9wIHN0b3AtY29sb3I9ImN1cnJlbnRDb2xvciIgb2Zmc2V0PSIyMCUiPjwvc3RvcD48c3RvcCBzdG9wLWNvbG9yPSJjdXJyZW50Q29sb3IiIG9mZnNldD0iMTAwJSI+PC9zdG9wPjwvbGluZWFyR3JhZGllbnQ+PGxpbmVhckdyYWRpZW50IGlkPSJsaW5lLW0zOHB0Z2llZjF3bGQyMGRncHQtNSIgZ3JhZGllbnRVbml0cz0idXNlclNwYWNlT25Vc2UiIHgxPSIxMTcuNDE0NjE2NDY3MzQ2MjYiIHkxPSI5Ny4yNzY0NjAwNTM3NTM3NyIgeDI9IjEzMC4wMTQ2MzYwNTY1Njg2MyIgeTI9Ijc1LjQ1MjYzMTE4ODI0MDQ1Ij48c3RvcCBzdG9wLWNvbG9yPSJjdXJyZW50Q29sb3IiIG9mZnNldD0iMjAlIj48L3N0b3A+PHN0b3Agc3RvcC1jb2xvcj0iY3VycmVudENvbG9yIiBvZmZzZXQ9IjEwMCUiPjwvc3RvcD48L2xpbmVhckdyYWRpZW50PjxsaW5lYXJHcmFkaWVudCBpZD0ibGluZS1tMzhwdGdpZWYxd2xkMjBkZ3B0LTciIGdyYWRpZW50VW5pdHM9InVzZXJTcGFjZU9uVXNlIiB4MT0iMTIwLjc0OTk3NTUxMzQzMzk1IiB5MT0iMTAyLjgzOTQ0MzA2OTUxNzk4IiB4Mj0iMTM2LjQ5OTk5OTk5OTk2MTk0IiB5Mj0iNzUuNTU5NjU2OTg3NjI2MzQiPjxzdG9wIHN0b3AtY29sb3I9ImN1cnJlbnRDb2xvciIgb2Zmc2V0PSIyMCUiPjwvc3RvcD48c3RvcCBzdG9wLWNvbG9yPSJjdXJyZW50Q29sb3IiIG9mZnNldD0iMTAwJSI+PC9zdG9wPjwvbGluZWFyR3JhZGllbnQ+PGxpbmVhckdyYWRpZW50IGlkPSJsaW5lLW0zOHB0Z2llZjF3bGQyMGRncHQtOSIgZ3JhZGllbnRVbml0cz0idXNlclNwYWNlT25Vc2UiIHgxPSIxMjAuNzUwMDI0NDg2NTAyNTUiIHkxPSI0OC4yNzk4NDI2MzExMjAzMSIgeDI9IjEzNi40OTk5OTk5OTk5NjE5NCIgeTI9Ijc1LjU1OTY1Njk4NzYyNjM0Ij48c3RvcCBzdG9wLWNvbG9yPSJjdXJyZW50Q29sb3IiIG9mZnNldD0iMjAlIj48L3N0b3A+PHN0b3Agc3RvcC1jb2xvcj0iY3VycmVudENvbG9yIiBvZmZzZXQ9IjEwMCUiPjwvc3RvcD48L2xpbmVhckdyYWRpZW50PjxsaW5lYXJHcmFkaWVudCBpZD0ibGluZS1tMzhwdGdpZWYxd2xkMjBkZ3B0LTExIiBncmFkaWVudFVuaXRzPSJ1c2VyU3BhY2VPblVzZSIgeDE9Ijg5LjI0OTk3NTUxMzQ0NjY3IiB5MT0iMTAyLjgzOTQxNDc5NDkwMzY2IiB4Mj0iMTIwLjc0OTk3NTUxMzQzMzk1IiB5Mj0iMTAyLjgzOTQ0MzA2OTUxNzk4Ij48c3RvcCBzdG9wLWNvbG9yPSJjdXJyZW50Q29sb3IiIG9mZnNldD0iMjAlIj48L3N0b3A+PHN0b3Agc3RvcC1jb2xvcj0iY3VycmVudENvbG9yIiBvZmZzZXQ9IjEwMCUiPjwvc3RvcD48L2xpbmVhckdyYWRpZW50PjxsaW5lYXJHcmFkaWVudCBpZD0ibGluZS1tMzhwdGdpZWYxd2xkMjBkZ3B0LTEzIiBncmFkaWVudFVuaXRzPSJ1c2VyU3BhY2VPblVzZSIgeDE9IjkyLjQwMDAxOTM5NzA4MzQxIiB5MT0iNTMuOTQ5ODE3MTgzOTY1MTMiIHgyPSIxMTcuNjAwMDE5Mzk3MDczMjUiIHkyPSI1My45NDk4Mzk4MDM2NTY1OTQiPjxzdG9wIHN0b3AtY29sb3I9ImN1cnJlbnRDb2xvciIgb2Zmc2V0PSIyMCUiPjwvc3RvcD48c3RvcCBzdG9wLWNvbG9yPSJjdXJyZW50Q29sb3IiIG9mZnNldD0iMTAwJSI+PC9zdG9wPjwvbGluZWFyR3JhZGllbnQ+PGxpbmVhckdyYWRpZW50IGlkPSJsaW5lLW0zOHB0Z2llZjF3bGQyMGRncHQtMTUiIGdyYWRpZW50VW5pdHM9InVzZXJTcGFjZU9uVXNlIiB4MT0iODkuMjUwMDI0NDg2NTE1MjYiIHkxPSI0OC4yNzk4MTQzNTY1MDU5OSIgeDI9IjEyMC43NTAwMjQ0ODY1MDI1NSIgeTI9IjQ4LjI3OTg0MjYzMTEyMDMxIj48c3RvcCBzdG9wLWNvbG9yPSJjdXJyZW50Q29sb3IiIG9mZnNldD0iMjAlIj48L3N0b3A+PHN0b3Agc3RvcC1jb2xvcj0iY3VycmVudENvbG9yIiBvZmZzZXQ9IjEwMCUiPjwvc3RvcD48L2xpbmVhckdyYWRpZW50PjxsaW5lYXJHcmFkaWVudCBpZD0ibGluZS1tMzhwdGdpZWYxd2xkMjBkZ3B0LTE3IiBncmFkaWVudFVuaXRzPSJ1c2VyU3BhY2VPblVzZSIgeDE9Ijc5Ljk4NTM2NDEzNTUwNDMxIiB5MT0iNzUuNDUyNTg2MjgxNjI1NTciIHgyPSI5Mi41ODUzNDQ1NDYyNzE4MSIgeTI9Ijk3LjI3NjQzNzc2NjgzMDM4Ij48c3RvcCBzdG9wLWNvbG9yPSJjdXJyZW50Q29sb3IiIG9mZnNldD0iMjAlIj48L3N0b3A+PHN0b3Agc3RvcC1jb2xvcj0iY3VycmVudENvbG9yIiBvZmZzZXQ9IjEwMCUiPjwvc3RvcD48L2xpbmVhckdyYWRpZW50PjxsaW5lYXJHcmFkaWVudCBpZD0ibGluZS1tMzhwdGdpZWYxd2xkMjBkZ3B0LTE5IiBncmFkaWVudFVuaXRzPSJ1c2VyU3BhY2VPblVzZSIgeDE9IjczLjQ5OTk5OTk5OTk4NzMxIiB5MT0iNzUuNTU5NjAwNDM4Mzk3NjciIHgyPSI4OS4yNDk5NzU1MTM0NDY2NyIgeTI9IjEwMi44Mzk0MTQ3OTQ5MDM2NiI+PHN0b3Agc3RvcC1jb2xvcj0iY3VycmVudENvbG9yIiBvZmZzZXQ9IjIwJSI+PC9zdG9wPjxzdG9wIHN0b3AtY29sb3I9ImN1cnJlbnRDb2xvciIgb2Zmc2V0PSIxMDAlIj48L3N0b3A+PC9saW5lYXJHcmFkaWVudD48bGluZWFyR3JhZGllbnQgaWQ9ImxpbmUtbTM4cHRnaWVmMXdsZDIwZGdwdC0yMSIgZ3JhZGllbnRVbml0cz0idXNlclNwYWNlT25Vc2UiIHgxPSI3My40OTk5OTk5OTk5ODczMSIgeTE9Ijc1LjU1OTYwMDQzODM5NzY3IiB4Mj0iODkuMjUwMDI0NDg2NTE1MjYiIHkyPSI0OC4yNzk4MTQzNTY1MDU5OSI+PHN0b3Agc3RvcC1jb2xvcj0iY3VycmVudENvbG9yIiBvZmZzZXQ9IjIwJSI+PC9zdG9wPjxzdG9wIHN0b3AtY29sb3I9ImN1cnJlbnRDb2xvciIgb2Zmc2V0PSIxMDAlIj48L3N0b3A+PC9saW5lYXJHcmFkaWVudD48bGluZWFyR3JhZGllbnQgaWQ9ImxpbmUtbTM4cHRnaWVmMXdsZDIwZGdwdC0yMyIgZ3JhZGllbnRVbml0cz0idXNlclNwYWNlT25Vc2UiIHgxPSI3My41MDAwNDg5NzMwNTU5IiB5MT0iMjEiIHgyPSI4OS4yNTAwMjQ0ODY1MTUyNiIgeTI9IjQ4LjI3OTgxNDM1NjUwNTk5Ij48c3RvcCBzdG9wLWNvbG9yPSJjdXJyZW50Q29sb3IiIG9mZnNldD0iMjAlIj48L3N0b3A+PHN0b3Agc3RvcC1jb2xvcj0iY3VycmVudENvbG9yIiBvZmZzZXQ9IjEwMCUiPjwvc3RvcD48L2xpbmVhckdyYWRpZW50PjxsaW5lYXJHcmFkaWVudCBpZD0ibGluZS1tMzhwdGdpZWYxd2xkMjBkZ3B0LTI1IiBncmFkaWVudFVuaXRzPSJ1c2VyU3BhY2VPblVzZSIgeDE9IjQyIiB5MT0iNzUuNTU5NTcyMTYzNzgzMzIiIHgyPSI3My40OTk5OTk5OTk5ODczMSIgeTI9Ijc1LjU1OTYwMDQzODM5NzY3Ij48c3RvcCBzdG9wLWNvbG9yPSJjdXJyZW50Q29sb3IiIG9mZnNldD0iMjAlIj48L3N0b3A+PHN0b3Agc3RvcC1jb2xvcj0iY3VycmVudENvbG9yIiBvZmZzZXQ9IjEwMCUiPjwvc3RvcD48L2xpbmVhckdyYWRpZW50PjwvZGVmcz48bWFzayBpZD0idGV4dC1tYXNrLW0zOHB0Z2llZjF3bGQyMGRncHQiPjxyZWN0IHg9IjAiIHk9IjAiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiIGZpbGw9IndoaXRlIj48L3JlY3Q+PGNpcmNsZSBjeD0iMTgzLjc1MDAyNDQ4NjQ3NzIzIiBjeT0iNDguMjc5ODk5MTgwMzQ5MDg0IiByPSI3Ljg3NSIgZmlsbD0iYmxhY2siPjwvY2lyY2xlPjxjaXJjbGUgY3g9IjQyIiBjeT0iNzUuNTU5NTcyMTYzNzgzMzIiIHI9IjcuODc1IiBmaWxsPSJibGFjayI+PC9jaXJjbGU+PGNpcmNsZSBjeD0iNzMuNTAwMDQ4OTczMDU1OSIgY3k9IjIxIiByPSI3Ljg3NSIgZmlsbD0iYmxhY2siPjwvY2lyY2xlPjwvbWFzaz48c3R5bGU+CiAgICAgICAgICAgICAgICAuZWxlbWVudC1tMzhwdGdpZWYxd2xkMjBkZ3B0IHsKICAgICAgICAgICAgICAgICAgICBmb250OiAxNHB4IEhlbHZldGljYSwgQXJpYWwsIHNhbnMtc2VyaWY7CiAgICAgICAgICAgICAgICAgICAgYWxpZ25tZW50LWJhc2VsaW5lOiAnbWlkZGxlJzsKICAgICAgICAgICAgICAgIH0KICAgICAgICAgICAgICAgIC5zdWItbTM4cHRnaWVmMXdsZDIwZGdwdCB7CiAgICAgICAgICAgICAgICAgICAgZm9udDogOC40cHggSGVsdmV0aWNhLCBBcmlhbCwgc2Fucy1zZXJpZjsKICAgICAgICAgICAgICAgIH0KICAgICAgICAgICAgPC9zdHlsZT48ZyBtYXNrPSJ1cmwoI3RleHQtbWFzay1tMzhwdGdpZWYxd2xkMjBkZ3B0KSI+PGxpbmUgeDE9IjE2Ny45OTk5OTk5OTk5NDkyNCIgeTE9Ijc1LjU1OTY4NTI2MjI0MDcyIiB4Mj0iMTgzLjc1MDAyNDQ4NjQ3NzIzIiB5Mj0iNDguMjc5ODk5MTgwMzQ5MDg0IiBzdHlsZT0ic3Ryb2tlLWxpbmVjYXA6cm91bmQ7c3Ryb2tlLWRhc2hhcnJheTpub25lO3N0cm9rZS13aWR0aDoxLjI2IiBzdHJva2U9InVybCgnI2xpbmUtbTM4cHRnaWVmMXdsZDIwZGdwdC0xJykiPjwvbGluZT48bGluZSB4MT0iMTM2LjQ5OTk5OTk5OTk2MTk0IiB5MT0iNzUuNTU5NjU2OTg3NjI2MzQiIHgyPSIxNjcuOTk5OTk5OTk5OTQ5MjQiIHkyPSI3NS41NTk2ODUyNjIyNDA3MiIgc3R5bGU9InN0cm9rZS1saW5lY2FwOnJvdW5kO3N0cm9rZS1kYXNoYXJyYXk6bm9uZTtzdHJva2Utd2lkdGg6MS4yNiIgc3Ryb2tlPSJ1cmwoJyNsaW5lLW0zOHB0Z2llZjF3bGQyMGRncHQtMycpIj48L2xpbmU+PGxpbmUgeDE9IjExNy40MTQ2MTY0NjczNDYyNiIgeTE9Ijk3LjI3NjQ2MDA1Mzc1Mzc3IiB4Mj0iMTMwLjAxNDYzNjA1NjU2ODYzIiB5Mj0iNzUuNDUyNjMxMTg4MjQwNDUiIHN0eWxlPSJzdHJva2UtbGluZWNhcDpyb3VuZDtzdHJva2UtZGFzaGFycmF5Om5vbmU7c3Ryb2tlLXdpZHRoOjEuMjYiIHN0cm9rZT0idXJsKCcjbGluZS1tMzhwdGdpZWYxd2xkMjBkZ3B0LTUnKSI+PC9saW5lPjxsaW5lIHgxPSIxMjAuNzQ5OTc1NTEzNDMzOTUiIHkxPSIxMDIuODM5NDQzMDY5NTE3OTgiIHgyPSIxMzYuNDk5OTk5OTk5OTYxOTQiIHkyPSI3NS41NTk2NTY5ODc2MjYzNCIgc3R5bGU9InN0cm9rZS1saW5lY2FwOnJvdW5kO3N0cm9rZS1kYXNoYXJyYXk6bm9uZTtzdHJva2Utd2lkdGg6MS4yNiIgc3Ryb2tlPSJ1cmwoJyNsaW5lLW0zOHB0Z2llZjF3bGQyMGRncHQtNycpIj48L2xpbmU+PGxpbmUgeDE9IjEyMC43NTAwMjQ0ODY1MDI1NSIgeTE9IjQ4LjI3OTg0MjYzMTEyMDMxIiB4Mj0iMTM2LjQ5OTk5OTk5OTk2MTk0IiB5Mj0iNzUuNTU5NjU2OTg3NjI2MzQiIHN0eWxlPSJzdHJva2UtbGluZWNhcDpyb3VuZDtzdHJva2UtZGFzaGFycmF5Om5vbmU7c3Ryb2tlLXdpZHRoOjEuMjYiIHN0cm9rZT0idXJsKCcjbGluZS1tMzhwdGdpZWYxd2xkMjBkZ3B0LTknKSI+PC9saW5lPjxsaW5lIHgxPSI4OS4yNDk5NzU1MTM0NDY2NyIgeTE9IjEwMi44Mzk0MTQ3OTQ5MDM2NiIgeDI9IjEyMC43NDk5NzU1MTM0MzM5NSIgeTI9IjEwMi44Mzk0NDMwNjk1MTc5OCIgc3R5bGU9InN0cm9rZS1saW5lY2FwOnJvdW5kO3N0cm9rZS1kYXNoYXJyYXk6bm9uZTtzdHJva2Utd2lkdGg6MS4yNiIgc3Ryb2tlPSJ1cmwoJyNsaW5lLW0zOHB0Z2llZjF3bGQyMGRncHQtMTEnKSI+PC9saW5lPjxsaW5lIHgxPSI5Mi40MDAwMTkzOTcwODM0MSIgeTE9IjUzLjk0OTgxNzE4Mzk2NTEzIiB4Mj0iMTE3LjYwMDAxOTM5NzA3MzI1IiB5Mj0iNTMuOTQ5ODM5ODAzNjU2NTk0IiBzdHlsZT0ic3Ryb2tlLWxpbmVjYXA6cm91bmQ7c3Ryb2tlLWRhc2hhcnJheTpub25lO3N0cm9rZS13aWR0aDoxLjI2IiBzdHJva2U9InVybCgnI2xpbmUtbTM4cHRnaWVmMXdsZDIwZGdwdC0xMycpIj48L2xpbmU+PGxpbmUgeDE9Ijg5LjI1MDAyNDQ4NjUxNTI2IiB5MT0iNDguMjc5ODE0MzU2NTA1OTkiIHgyPSIxMjAuNzUwMDI0NDg2NTAyNTUiIHkyPSI0OC4yNzk4NDI2MzExMjAzMSIgc3R5bGU9InN0cm9rZS1saW5lY2FwOnJvdW5kO3N0cm9rZS1kYXNoYXJyYXk6bm9uZTtzdHJva2Utd2lkdGg6MS4yNiIgc3Ryb2tlPSJ1cmwoJyNsaW5lLW0zOHB0Z2llZjF3bGQyMGRncHQtMTUnKSI+PC9saW5lPjxsaW5lIHgxPSI3OS45ODUzNjQxMzU1MDQzMSIgeTE9Ijc1LjQ1MjU4NjI4MTYyNTU3IiB4Mj0iOTIuNTg1MzQ0NTQ2MjcxODEiIHkyPSI5Ny4yNzY0Mzc3NjY4MzAzOCIgc3R5bGU9InN0cm9rZS1saW5lY2FwOnJvdW5kO3N0cm9rZS1kYXNoYXJyYXk6bm9uZTtzdHJva2Utd2lkdGg6MS4yNiIgc3Ryb2tlPSJ1cmwoJyNsaW5lLW0zOHB0Z2llZjF3bGQyMGRncHQtMTcnKSI+PC9saW5lPjxsaW5lIHgxPSI3My40OTk5OTk5OTk5ODczMSIgeTE9Ijc1LjU1OTYwMDQzODM5NzY3IiB4Mj0iODkuMjQ5OTc1NTEzNDQ2NjciIHkyPSIxMDIuODM5NDE0Nzk0OTAzNjYiIHN0eWxlPSJzdHJva2UtbGluZWNhcDpyb3VuZDtzdHJva2UtZGFzaGFycmF5Om5vbmU7c3Ryb2tlLXdpZHRoOjEuMjYiIHN0cm9rZT0idXJsKCcjbGluZS1tMzhwdGdpZWYxd2xkMjBkZ3B0LTE5JykiPjwvbGluZT48bGluZSB4MT0iNzMuNDk5OTk5OTk5OTg3MzEiIHkxPSI3NS41NTk2MDA0MzgzOTc2NyIgeDI9Ijg5LjI1MDAyNDQ4NjUxNTI2IiB5Mj0iNDguMjc5ODE0MzU2NTA1OTkiIHN0eWxlPSJzdHJva2UtbGluZWNhcDpyb3VuZDtzdHJva2UtZGFzaGFycmF5Om5vbmU7c3Ryb2tlLXdpZHRoOjEuMjYiIHN0cm9rZT0idXJsKCcjbGluZS1tMzhwdGdpZWYxd2xkMjBkZ3B0LTIxJykiPjwvbGluZT48bGluZSB4MT0iNzMuNTAwMDQ4OTczMDU1OSIgeTE9IjIxIiB4Mj0iODkuMjUwMDI0NDg2NTE1MjYiIHkyPSI0OC4yNzk4MTQzNTY1MDU5OSIgc3R5bGU9InN0cm9rZS1saW5lY2FwOnJvdW5kO3N0cm9rZS1kYXNoYXJyYXk6bm9uZTtzdHJva2Utd2lkdGg6MS4yNiIgc3Ryb2tlPSJ1cmwoJyNsaW5lLW0zOHB0Z2llZjF3bGQyMGRncHQtMjMnKSI+PC9saW5lPjxsaW5lIHgxPSI0MiIgeTE9Ijc1LjU1OTU3MjE2Mzc4MzMyIiB4Mj0iNzMuNDk5OTk5OTk5OTg3MzEiIHkyPSI3NS41NTk2MDA0MzgzOTc2NyIgc3R5bGU9InN0cm9rZS1saW5lY2FwOnJvdW5kO3N0cm9rZS1kYXNoYXJyYXk6bm9uZTtzdHJva2Utd2lkdGg6MS4yNiIgc3Ryb2tlPSJ1cmwoJyNsaW5lLW0zOHB0Z2llZjF3bGQyMGRncHQtMjUnKSI+PC9saW5lPjwvZz48Zz48dGV4dCB4PSIxNzguNTAwMDI0NDg2NDc3MjMiIHk9IjUzLjUyOTg5OTE4MDM0OTA4NCIgY2xhc3M9ImVsZW1lbnQtbTM4cHRnaWVmMXdsZDIwZGdwdCIgZmlsbD0iY3VycmVudENvbG9yIiBzdHlsZT0iCiAgICAgICAgICAgICAgICB0ZXh0LWFuY2hvcjogc3RhcnQ7CiAgICAgICAgICAgICAgICB3cml0aW5nLW1vZGU6IGhvcml6b250YWwtdGI7CiAgICAgICAgICAgICAgICB0ZXh0LW9yaWVudGF0aW9uOiBtaXhlZDsKICAgICAgICAgICAgICAgIGxldHRlci1zcGFjaW5nOiBub3JtYWw7CiAgICAgICAgICAgICAgICBkaXJlY3Rpb246IGx0cjsKICAgICAgICAgICAgIj48dHNwYW4gc3R5bGU9IgogICAgICAgICAgICAgICAgdW5pY29kZS1iaWRpOiBwbGFpbnRleHQ7CiAgICAgICAgICAgICAgICB3cml0aW5nLW1vZGU6IGxyLXRiOwogICAgICAgICAgICAgICAgbGV0dGVyLXNwYWNpbmc6IG5vcm1hbDsKICAgICAgICAgICAgICAgIHRleHQtYW5jaG9yOiBtaWRkbGU7CiAgICAgICAgICAgICI+WTY8L3RzcGFuPjwvdGV4dD48dGV4dCB4PSIxODMuNzUwMDI0NDg2NDc3MjMiIHk9IjQ4LjI3OTg5OTE4MDM0OTA4NCIgY2xhc3M9ImRlYnVnIiBmaWxsPSIjZmYwMDAwIiBzdHlsZT0iCiAgICAgICAgICAgICAgICBmb250OiA1cHggRHJvaWQgU2Fucywgc2Fucy1zZXJpZjsKICAgICAgICAgICAgIj48L3RleHQ+PHRleHQgeD0iMTY3Ljk5OTk5OTk5OTk0OTI0IiB5PSI3NS41NTk2ODUyNjIyNDA3MiIgY2xhc3M9ImRlYnVnIiBmaWxsPSIjZmYwMDAwIiBzdHlsZT0iCiAgICAgICAgICAgICAgICBmb250OiA1cHggRHJvaWQgU2Fucywgc2Fucy1zZXJpZjsKICAgICAgICAgICAgIj48L3RleHQ+PHRleHQgeD0iMTM2LjQ5OTk5OTk5OTk2MTk0IiB5PSI3NS41NTk2NTY5ODc2MjYzNCIgY2xhc3M9ImRlYnVnIiBmaWxsPSIjZmYwMDAwIiBzdHlsZT0iCiAgICAgICAgICAgICAgICBmb250OiA1cHggRHJvaWQgU2Fucywgc2Fucy1zZXJpZjsKICAgICAgICAgICAgIj48L3RleHQ+PHRleHQgeD0iMTIwLjc0OTk3NTUxMzQzMzk1IiB5PSIxMDIuODM5NDQzMDY5NTE3OTgiIGNsYXNzPSJkZWJ1ZyIgZmlsbD0iI2ZmMDAwMCIgc3R5bGU9IgogICAgICAgICAgICAgICAgZm9udDogNXB4IERyb2lkIFNhbnMsIHNhbnMtc2VyaWY7CiAgICAgICAgICAgICI+PC90ZXh0Pjx0ZXh0IHg9Ijg5LjI0OTk3NTUxMzQ0NjY3IiB5PSIxMDIuODM5NDE0Nzk0OTAzNjYiIGNsYXNzPSJkZWJ1ZyIgZmlsbD0iI2ZmMDAwMCIgc3R5bGU9IgogICAgICAgICAgICAgICAgZm9udDogNXB4IERyb2lkIFNhbnMsIHNhbnMtc2VyaWY7CiAgICAgICAgICAgICI+PC90ZXh0Pjx0ZXh0IHg9IjczLjQ5OTk5OTk5OTk4NzMxIiB5PSI3NS41NTk2MDA0MzgzOTc2NyIgY2xhc3M9ImRlYnVnIiBmaWxsPSIjZmYwMDAwIiBzdHlsZT0iCiAgICAgICAgICAgICAgICBmb250OiA1cHggRHJvaWQgU2Fucywgc2Fucy1zZXJpZjsKICAgICAgICAgICAgIj48L3RleHQ+PHRleHQgeD0iNDcuMjUiIHk9IjgwLjgwOTU3MjE2Mzc4MzMyIiBjbGFzcz0iZWxlbWVudC1tMzhwdGdpZWYxd2xkMjBkZ3B0IiBmaWxsPSJjdXJyZW50Q29sb3IiIHN0eWxlPSIKICAgICAgICAgICAgICAgIHRleHQtYW5jaG9yOiBzdGFydDsKICAgICAgICAgICAgICAgIHdyaXRpbmctbW9kZTogaG9yaXpvbnRhbC10YjsKICAgICAgICAgICAgICAgIHRleHQtb3JpZW50YXRpb246IG1peGVkOwogICAgICAgICAgICAgICAgbGV0dGVyLXNwYWNpbmc6IG5vcm1hbDsKICAgICAgICAgICAgICAgIGRpcmVjdGlvbjogcnRsOyB1bmljb2RlLWJpZGk6IGJpZGktb3ZlcnJpZGU7CiAgICAgICAgICAgICI+PHRzcGFuIHN0eWxlPSIKICAgICAgICAgICAgICAgIHVuaWNvZGUtYmlkaTogcGxhaW50ZXh0OwogICAgICAgICAgICAgICAgd3JpdGluZy1tb2RlOiBsci10YjsKICAgICAgICAgICAgICAgIGxldHRlci1zcGFjaW5nOiBub3JtYWw7CiAgICAgICAgICAgICAgICB0ZXh0LWFuY2hvcjogc3RhcnQ7CiAgICAgICAgICAgICI+WTg8L3RzcGFuPjwvdGV4dD48dGV4dCB4PSI0MiIgeT0iNzUuNTU5NTcyMTYzNzgzMzIiIGNsYXNzPSJkZWJ1ZyIgZmlsbD0iI2ZmMDAwMCIgc3R5bGU9IgogICAgICAgICAgICAgICAgZm9udDogNXB4IERyb2lkIFNhbnMsIHNhbnMtc2VyaWY7CiAgICAgICAgICAgICI+PC90ZXh0Pjx0ZXh0IHg9Ijg5LjI1MDAyNDQ4NjUxNTI2IiB5PSI0OC4yNzk4MTQzNTY1MDU5OSIgY2xhc3M9ImRlYnVnIiBmaWxsPSIjZmYwMDAwIiBzdHlsZT0iCiAgICAgICAgICAgICAgICBmb250OiA1cHggRHJvaWQgU2Fucywgc2Fucy1zZXJpZjsKICAgICAgICAgICAgIj48L3RleHQ+PHRleHQgeD0iNjguMjUwMDQ4OTczMDU1OSIgeT0iMjYuMjUiIGNsYXNzPSJlbGVtZW50LW0zOHB0Z2llZjF3bGQyMGRncHQiIGZpbGw9ImN1cnJlbnRDb2xvciIgc3R5bGU9IgogICAgICAgICAgICAgICAgdGV4dC1hbmNob3I6IHN0YXJ0OwogICAgICAgICAgICAgICAgd3JpdGluZy1tb2RlOiBob3Jpem9udGFsLXRiOwogICAgICAgICAgICAgICAgdGV4dC1vcmllbnRhdGlvbjogbWl4ZWQ7CiAgICAgICAgICAgICAgICBsZXR0ZXItc3BhY2luZzogbm9ybWFsOwogICAgICAgICAgICAgICAgZGlyZWN0aW9uOiBsdHI7CiAgICAgICAgICAgICI+PHRzcGFuIHN0eWxlPSIKICAgICAgICAgICAgICAgIHVuaWNvZGUtYmlkaTogcGxhaW50ZXh0OwogICAgICAgICAgICAgICAgd3JpdGluZy1tb2RlOiBsci10YjsKICAgICAgICAgICAgICAgIGxldHRlci1zcGFjaW5nOiBub3JtYWw7CiAgICAgICAgICAgICAgICB0ZXh0LWFuY2hvcjogbWlkZGxlOwogICAgICAgICAgICAiPlk0PC90c3Bhbj48L3RleHQ+PHRleHQgeD0iNzMuNTAwMDQ4OTczMDU1OSIgeT0iMjEiIGNsYXNzPSJkZWJ1ZyIgZmlsbD0iI2ZmMDAwMCIgc3R5bGU9IgogICAgICAgICAgICAgICAgZm9udDogNXB4IERyb2lkIFNhbnMsIHNhbnMtc2VyaWY7CiAgICAgICAgICAgICI+PC90ZXh0Pjx0ZXh0IHg9IjEyMC43NTAwMjQ0ODY1MDI1NSIgeT0iNDguMjc5ODQyNjMxMTIwMzEiIGNsYXNzPSJkZWJ1ZyIgZmlsbD0iI2ZmMDAwMCIgc3R5bGU9IgogICAgICAgICAgICAgICAgZm9udDogNXB4IERyb2lkIFNhbnMsIHNhbnMtc2VyaWY7CiAgICAgICAgICAgICI+PC90ZXh0PjwvZz48L3N2Zz4="/>
(d)

Figure 7.4 (a) NMOS device operating as a current source, (b) PMOS device operating as a current source, (c) PMOS topology not operating as a current source, (d) NMOS topology not operating as a current source.
[Fig. 7.4(b)] draws current from $V_{D D}$ to node $Y$. If $\lambda=0$, these currents remain independent of $V_{X}$ or $V_{Y}$ (so long as the transistors are in saturation).

It is important to understand that only the drain terminal of a MOSFET can draw a dc current and still present a high impedance. Specifically, NMOS or PMOS devices configured as shown in Figs. 7.4(c) and (d) do not operate as current sources because variation of $V_{X}$ or $V_{Y}$ directly changes the gate-source voltage of each transistor, thus changing the drain current considerably. From another perspective, the small-signal model of these two structures is identical to that of the diode-connected devices in Fig. 6.34, revealing a small-signal impedance of only $1 / g_{m}($ if $\lambda=0)$ rather than infinity.

## 7.2 COMMON-SOURCE STAGE

### 7.2.1 CS Core

Shown in Fig. 7.5(a), the basic CS stage is similar to the common-emitter topology, with the input applied to the gate and the output sensed at the drain. For small signals, $M_{1}$ converts the input voltage variations to proportional drain current changes, and $R_{D}$ transforms the drain currents to the output voltage. If channel-length modulation is neglected, the small-signal model in Fig. 7.5(b) yields $v_{\text {in }}=v_{1}$ and $v_{\text {out }}=-g_{m} v_{1} R_{D}$. That is,

$$
\begin{equation*}
\frac{v_{\text {out }}}{v_{\text {in }}}=-g_{m} R_{D} \tag{7.34}
\end{equation*}
$$

a result similar to that obtained for the common emitter stage in Chapter 5.
image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: Vin}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout}
name: gmV1, type: VoltageControlledCurrentSource, ports: {Np: Vin, Nn: GND}
]
extrainfo:This is a common-source amplifier circuit with an NMOS transistor. The input voltage is applied to the gate of M1, and the output is taken from the drain. The resistor RD is connected between VDD and the drain of M1, forming the load. The voltage-controlled current source represents the transconductance of the MOSFET in the small-signal model.
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: Vin}
name: RD, type: Resistor, value: RD, ports: {N1: Vout, N2: GND}
name: gmV1, type: VoltageControlledCurrentSource, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit diagram (b) represents the small-signal model of a common-source amplifier. The NMOS transistor M1 converts input voltage variations to drain current changes, and the resistor RD transforms these drain currents to output voltage. The voltage-controlled current source gmV1 models the transconductance of the NMOS transistor.

Figure 7.5 (a) Common-source stage, (b) small-signal mode.

The voltage gain of the CS stage is also limited by the supply voltage. Since $g_{m}=$ $\sqrt{2 \mu_{n} C_{o x}(W / L) I_{D}}$, we have

$$
\begin{equation*}
A_{v}=-\sqrt{2 \mu_{n} C_{o x} \frac{W}{L} I_{D}} R_{D}, \tag{7.35}
\end{equation*}
$$

concluding that if $I_{D}$ or $R_{D}$ is increased, so is the voltage drop across $R_{D}\left(=I_{D} R_{D}\right){ }^{1}$ For $M_{1}$ to remain in saturation,

$$
\begin{equation*}
V_{D D}-R_{D} I_{D}>V_{G S}-V_{T H} \tag{7.36}
\end{equation*}
$$

that is,

$$
\begin{equation*}
R_{D} I_{D}<V_{D D}-\left(V_{G S}-V_{T H}\right) \tag{7.37}
\end{equation*}
$$

Example Calculate the small-signal voltage gain of the CS stage shown in Fig. 7.6 if $I_{D}=1 \mathrm{~mA}$, 7.4 $\mu_{n} C_{o x}=100 \mu \mathrm{~A} / \mathrm{V}^{2}, V_{T H}=0.5 \mathrm{~V}$, and $\lambda=0$. Verify that $M_{1}$ operates in saturation.
image_name:Figure 7.6
description:
[
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: Vin}
name: RD, type: Resistor, value: 1k, ports: {N1: VDD, N2: Vout}
name: VDD, type: VoltageSource, value: 1.8V, ports: {Np: VDD, Nn: GND}
]
extrainfo:The circuit is a common-source (CS) amplifier stage with NMOS M1. The resistor RD is connected between the drain of M1 and VDD, and the source of M1 is grounded. The gate of M1 is connected to Vin, and the output is taken from the drain, labeled as Vout. The voltage supply is 1.8V.

Figure 7.6 Example of CS stage.
Solution We have

$$
\begin{align*}
g_{m} & =\sqrt{2 \mu_{n} C_{o x} \frac{W}{L} I_{D}}  \tag{7.38}\\
& =\frac{1}{300 \Omega} . \tag{7.39}
\end{align*}
$$

Thus,

$$
\begin{align*}
A_{v} & =-g_{m} R_{D}  \tag{7.40}\\
& =3.33 \tag{7.41}
\end{align*}
$$

To check the operation region, we first determine the gate-source voltage:

$$
\begin{align*}
V_{G S} & =V_{T H}+\sqrt{\frac{2 I_{D}}{\mu_{n} C_{o x} \frac{W}{L}}}  \tag{7.42}\\
& =1.1 \mathrm{~V} \tag{7.43}
\end{align*}
$$

[^4]The drain voltage is equal to $V_{D D}-R_{D} I_{D}=0.8 \mathrm{~V}$. Since $V_{G S}-V_{T H}=0.6 \mathrm{~V}$, the device indeed operates in saturation and has a margin of 0.2 V with respect to the triode region. For example, if $R_{D}$ is doubled with the intention of doubling $A_{v}$, then $M_{1}$ enters the triode region and its transconductance drops.

Exercise What value of $V_{T H}$ places $M_{1}$ at the edge of saturation?

Since the gate terminal of MOSFETs draws a zero current (at very low frequencies), we say the CS amplifier provides a current gain of infinity. By contrast, the current gain of a common-emitter stage is equal to $\beta$.

Let us now compute the I/O impedances of the CS amplifier. Since the gate current is zero (at low frequencies),

$$
\begin{equation*}
R_{i n}=\infty \tag{7.44}
\end{equation*}
$$

a point of contrast to the CE stage (whose $R_{i n}$ is equal to $r_{\pi}$ ). The high input impedance of the CS topology plays a critical role in many analog circuits.

The similarity between the small-signal equivalents of CE and CS stages indicates that the output impedance of the CS amplifier is simply equal to

$$
\begin{equation*}
R_{\text {out }}=R_{D} \tag{7.45}
\end{equation*}
$$

This is also seen from Fig. 7.7.
image_name:Figure 7.8
description:
[
name: V1, type: VoltageSource, value: V1, ports: {Np: V1, Nn: GND}
name: g_mv1, type: VoltageControlledCurrentSource, ports: {Np: V1, Nn: Vx}
name: RD, type: Resistor, value: RD, ports: {N1: Vx, N2: GND}
name: Vx, type: VoltageSource, value: Vx, ports: {Np: Vx, Nn: GND}
]
extrainfo:The circuit is a small-signal model of a common-source amplifier with channel-length modulation. The voltage source V1 provides the input signal, while the voltage-controlled current source g_mv1 models the transconductance of the MOSFET. RD is the load resistor, and Vx is the output voltage across the load.

Figure 7.7 Output impedance of CS stage.

In practice, channel-length modulation may not be negligible, especially if $R_{D}$ is large. The small-signal model of CS topology is therefore modified as shown in Fig. 7.8, revealing that

$$
\begin{align*}
A_{v} & =-g_{m}\left(R_{D} \| r_{O}\right)  \tag{7.46}\\
R_{\text {in }} & =\infty  \tag{7.47}\\
R_{\text {out }} & =R_{D} \| r_{O} . \tag{7.48}
\end{align*}
$$

In other words, channel-length modulation and the Early effect impact the CS and CE stages, respectively, in a similar manner.
image_name:Figure 7.8
description:
[
name: v1, type: VoltageSource, value: v1, ports: {Np: Vx, Nn: GND}
name: g_m v1, type: VoltageControlledCurrentSource, value: g_m v1, ports: {Np: GND, Nn: Vx}
name: ro, type: Resistor, value: ro, ports: {N1: Vx, N2: Vx}
name: RD, type: Resistor, value: RD, ports: {N1: Vx, N2: GND}
name: vx, type: VoltageSource, value: vx, ports: {Np: Vx, Nn: GND}
]
extrainfo:The circuit is a small-signal model of a common source amplifier with channel-length modulation. It includes a voltage-controlled current source, resistors, and voltage sources. The voltage gain is affected by the parallel combination of RD and ro.

Figure 7.8 Effect of channel-length modulation on CS stage.

Example
7.5

Assuming $M_{1}$ operates in saturation, determine the voltage gain of the circuit depicted in Fig. 7.9(a) and plot the result as a function of the transistor channel length while other parameters remain constant.
image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: Vin}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: Vout}
name: I1, type: CurrentSource, ports: {Np: VDD, Nn: Vout}
]
extrainfo:The circuit is a common source amplifier with channel-length modulation. The voltage gain is determined by the transconductance (gm) and the output resistance (ro) of the NMOS transistor M1. The ideal current source provides an infinite small-signal resistance.

(a)
image_name:(b)
description:The graph is a plot of voltage gain (A_v) versus device channel length (L) for a common source amplifier. The x-axis represents the channel length (L), and the y-axis represents the voltage gain (A_v). Both axes are on a linear scale.

The graph shows a curve that starts at a lower gain value and increases as the channel length increases. This indicates that the voltage gain of the amplifier is positively correlated with the channel length of the device. The curve suggests a nonlinear relationship, where the rate of increase in gain diminishes as the channel length becomes larger, possibly approaching an asymptotic value.

There are no specific annotations, markers, or numerical values provided on the graph. The overall trend highlights the impact of channel length modulation on the gain of the amplifier, where longer channel lengths lead to higher gains due to increased output resistance (r_O). This behavior aligns with the equation A_v = -g_m * r_O, where r_O is inversely proportional to the channel length modulation parameter (λ)."}

(b)

Figure 7.9 (a) CS stage with ideal current source as a load, (b) gain as a function of device channel length.

Solution The ideal current source presents an infinite small-signal resistance, allowing the use of Eq. (7.46) with $R_{D}=\infty$ :

$$
\begin{equation*}
A_{v}=-g_{m} r_{O} \tag{7.49}
\end{equation*}
$$

This is the highest voltage gain that a single transistor can provide. Writing $g_{m}=$ $\sqrt{2 \mu_{n} C_{o x}(W / L) I_{D}}$ and $r_{O}=\left(\lambda I_{D}\right)^{-1}$, we have

$$
\begin{equation*}
\left|A_{v}\right|=\frac{\sqrt{2 \mu_{n} C_{o x} \frac{W}{L}}}{\lambda \sqrt{I_{D}}} \tag{7.50}
\end{equation*}
$$

This result may imply that $\left|A_{v}\right|$ falls as $L$ increases, but recall from Chapter 6 that $\lambda \propto L^{-1}$ :

$$
\begin{equation*}
\left|A_{v}\right| \propto \sqrt{\frac{2 \mu_{n} C_{o x} W L}{I_{D}}} \tag{7.51}
\end{equation*}
$$

Consequently, $\left|A_{v}\right|$ increases with $L$ [Fig. 7.9(b)].

Repeat the above example if a resistor of value $R_{1}$ is tied between the gate and drain of $M_{1}$.

### 7.2.2 CS Stage With Current-Source Load

As seen in the above example, the tradeoff between the voltage gain and the voltage headroom can be relaxed by replacing the load resistor with a current source. The observations made in relation to Fig. 7.4(b) therefore suggest the use of a PMOS device as the load of an NMOS CS amplifier [Fig. 7.10(a)].

Let us determine the small-signal gain and output impedance of the circuit. Having a constant gate-source voltage, $M_{2}$ simply behaves as a resistor equal to its

Did you know?

The intrinsic gain, $g_{m} r_{0}$, of MOSFETs has fallen with technology scaling, i.e., as the minimum channellength has gone from about $10 \mu \mathrm{~m}$ in the 1960s to 25 nm today. Due to severe channel-length modulation, the intrinsic gain of these shortchannel devices is on the order of 5 to 10 , making it difficult to achieve a high voltage gain in many analog circuits. This issue has prompted extensive research on analog design using low-gain building blocks. For example, the analog-to-digital converter that digitizes the image in your camera may need an op amp with a gain of 4,000 but must now be designed with a gain of only 20 .
image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: Vin}
name: M2, type: PMOS, ports: {S: VDD, D: Vout, G: Vb}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
name: V1, type: VoltageSource, value: V1, ports: {Np: V1, Nn: GND}
name: gm2V1, type: VoltageControlledCurrentSource, ports: {Np: GND, Nn: Vout}
name: ro1, type: Resistor, value: ro1, ports: {N1: Vout, N2: GND}
name: ro2, type: Resistor, value: ro2, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit is a common-source (CS) stage using a PMOS device as a current source. The output impedance is defined by the parallel combination of ro1 and ro2.
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: Vin}
name: M2, type: PMOS, ports: {S: VDD, D: Vout, G: Vb}
name: V1, type: VoltageSource, value: V1, ports: {Np: V1, Nn: GND}
name: ro1, type: Resistor, value: ro1, ports: {N1: Vout, N2: GND}
name: gm2, type: VoltageControlledCurrentSource, value: gm2, ports: {Np: GND, Nn: Vout}
name: ro2, type: Resistor, value: ro2, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit is a common-source (CS) amplifier stage using an NMOS transistor (M1) with a PMOS current source (M2). The output is taken at Vout. The small-signal model includes a voltage-controlled current source (gm2) and resistors ro1 and ro2, which define the output impedance.

Figure 7.10 (a) CS stage using a PMOS device as a current source, (b) small-signal model.
output impedance [Fig. 7.10(b)] because $v_{1}=0$ and hence $g_{m 2} v_{1}=0$. Thus, the drain node of $M_{1}$ sees both $r_{O 1}$ and $r_{O 2}$ to ac ground. Equations (7.46) and (7.48) give

$$
\begin{align*}
A_{v} & =-g_{m 1}\left(r_{O 1} \| r_{O 2}\right)  \tag{7.52}\\
R_{\text {out }} & =r_{O 1} \| r_{O 2} \tag{7.53}
\end{align*}
$$

Example Figure 7.11 shows a PMOS CS stage using an NMOS current source load. Compute the 7.6 voltage gain of the circuit.
image_name:Figure 7.11
description:
[
name: M2, type: PMOS, ports: {S: VDD, D: Vout, G: Vin}
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: Vb}
]
extrainfo:The circuit is a common-source amplifier with a PMOS load and NMOS driver. The input is at Vin, and the output is at Vout. Vb is the bias voltage for the NMOS transistor M1.

Figure 7.11 CS stage using an NMOS device as current source.

Solution Transistor $M_{2}$ generates a small-signal current equal to $g_{m 2} v_{i n}$, which then flows through $r_{O 1} \| r_{O 2}$, producing $v_{o u t}=-g_{m 2} v_{i n}\left(r_{O 1} \| r_{O 2}\right)$. Thus,

$$
\begin{equation*}
A_{v}=-g_{m 2}\left(r_{O 1} \| r_{O 2}\right) \tag{7.54}
\end{equation*}
$$

Exercise Calculate the gain if the circuit drives a loads resistance equal to $R_{L}$.

### 7.2.3 CS Stage With Diode-Connected Load

In some applications, we may use a diode-connected MOSFET as the drain load. Illustrated in Fig. 7.12(a), such a topology exhibits only a moderate gain due to the relatively low impedance of the diode-connected device (Section 7.1.3). With $\lambda=0, M_{2}$ acts as a smallsignal resistance equal to $1 / g_{m 2}$, and Eq. (7.34) yields

$$
\begin{align*}
A_{v} & =-g_{m 1} \cdot \frac{1}{g_{m 2}}  \tag{7.55}\\
& =-\frac{\sqrt{2 \mu_{n} C_{o x}(W / L)_{1} I_{D}}}{\sqrt{2 \mu_{n} C_{o x}(W / L)_{2} I_{D}}}  \tag{7.56}\\
& =-\sqrt{\frac{(W / L)_{1}}{(W / L)_{2}}} . \tag{7.57}
\end{align*}
$$

image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: Vin}
name: M2, type: NMOS, ports: {S: VDD, D: Vout, G: Vout}
]
extrainfo:The circuit is a MOS stage using a diode-connected NMOS load, providing moderate gain due to the low impedance of the diode-connected device. The gain is determined by the dimensions of M1 and M2 and is independent of process parameters and drain current.
image_name:(b)
description:
[
name: Q1, type: NPN, ports: {C: Vout, B: Vin, E: GND}
name: Q2, type: NPN, ports: {C: VCC, B: Vout, E: Vout}
]
extrainfo:The circuit (b) is a bipolar counterpart of a MOS stage using a diode-connected load. The voltage gain is limited to unity.
image_name:(c)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: Vin}
name: rO1, type: Resistor, value: rO1, ports: {N1: Vout, N2: GND}
name: rO2, type: Resistor, value: rO2, ports: {N1: Vout, N2: GND}
name: 1/gm2, type: CurrentSource, value: 1/gm2, ports: {Np: GND, Nn: Vout}
]
extrainfo:The circuit is a simplified MOS stage using a diode-connected load, providing moderate gain. The gain is determined by the dimensions of the transistors and is independent of process parameters and drain current.

Figure 7.12 (a) MOS stage using a diode-connected load, (b) bipolar counterpart, (c) simplified circuit of (a).

Interestingly, the gain is given by the dimensions of $M_{1}$ and $M_{2}$ and remains independent of process parameters $\mu_{n}$ and $C_{o x}$ and the drain current, $I_{D}$.

The reader may wonder why we did not consider a common-emitter stage with a diodeconnected load in Chapter 5. Shown in Fig. 7.12(b), such a circuit is not used because it provides a voltage gain of only unity:

$$
\begin{align*}
A_{v} & =-g_{m 1} \cdot \frac{1}{g_{m 2}}  \tag{7.58}\\
& =-\frac{I_{C 1}}{V_{T}} \cdot \frac{1}{I_{C 2} / V_{T}}  \tag{7.59}\\
& \approx-1 . \tag{7.60}
\end{align*}
$$

The contrast between Eqs. (7.57) and (7.60) arises from a fundamental difference between MOS and bipolar devices: transconductance of the former depends on device dimensions whereas that of the latter does not.

A more accurate expression for the gain of the stage in Fig. 7.12(a) must take channellength modulation into account. As depicted in Fig. 7.12(c), the resistance seen at the drain is now equal to $\left(1 / g_{m 2}\right)\left\|r_{O 2}\right\| r_{O 1}$, and hence

$$
\begin{equation*}
A_{v}=-g_{m 1}\left(\frac{1}{g_{m 2}}\left\|r_{O 2}\right\| r_{O 1}\right) \tag{7.61}
\end{equation*}
$$

Similarly, the output resistance of the stage is given by

$$
\begin{equation*}
R_{\text {out }}=\frac{1}{g_{m 2}}\left\|r_{O 2}\right\| r_{O 1} \tag{7.62}
\end{equation*}
$$

| Example |  |
| :---: | :---: |
| 7.7 | Determine the voltage gain of the circuit shown in Fig. 7.13(a) if $\lambda \neq 0$. |

image_name:Figure 7.13
description:
[
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: Vin}
name: M2, type: PMOS, ports: {S: VDD, D: Vout, G: Vout}
]
extrainfo:The circuit is a common-source amplifier with a diode-connected PMOS load. The input is applied to the gate of M1, and the output is taken from the drain of M1. M2 is configured as a diode-connected load.

Figure 7.13 CS stage with diode-connected PMOS device.

Solution This stage is similar to that in Fig. 7.12(a), but with NMOS devices changed to PMOS transistors: $M_{1}$ serves as a common-source device and $M_{2}$ as a diode-connected load. Thus,

$$
\begin{equation*}
A_{v}=-g_{m 2}\left(\frac{1}{g_{m 1}}\left\|r_{O 1}\right\| r_{O 2}\right) \tag{7.63}
\end{equation*}
$$

Exercise Repeat the above example if the gate of $M_{1}$ is tied to a constant voltage equal to 0.5 V .

### 7.2.4 CS Stage With Degeneration

Recall from Chapter 5 that a resistor placed in series with the emitter of a bipolar transistor alters characteristics such as gain, I/O impedances, and linearity. We expect similar results for a degenerated CS amplifier.
image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: Vin}
name: RD, type: Resistor, value: RD, ports: {N1: Vout, N2: VDD}
name: RS, type: Resistor, value: RS, ports: {N1: GND, N2: Vout}
]
extrainfo:This is a common-source amplifier with source degeneration. The NMOS transistor M1 is connected with its source to ground through the resistor RS, and its drain to the output Vout through the resistor RD. The gate is connected to the input Vin. The circuit is powered by VDD.

(a)
image_name:(b)
description:
[
name: V1, type: VoltageSource, value: V1, ports: {Np: Vin, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: GND, N2: V1}
name: gmV1, type: VoltageControlledCurrentSource, ports: {Np: V1, Nn: Vout}
name: RD, type: Resistor, value: RD, ports: {N1: Vout, N2: GND}
]
extrainfo:This is a small-signal model of a common-source amplifier with source degeneration. The voltage source V1 provides the input voltage Vin. The resistor RS is connected to ground, and the current source gmV1 represents the transconductance in the circuit. The output is taken across the resistor RD, which is also connected to ground.

(b)

Figure 7.14 (a) CS stage with degeneration, (b) small-signal model.

Figure 7.14 depicts the stage along with its small-signal equivalent (if $\lambda=0$ ). As with the bipolar counterpart, the degeneration resistor sustains a fraction of the input voltage change. From Fig. 7.14(b), we have

$$
\begin{equation*}
v_{\text {in }}=v_{1}+g_{m} v_{1} R_{S} \tag{7.64}
\end{equation*}
$$

and hence

$$
\begin{equation*}
v_{1}=\frac{v_{i n}}{1+g_{m} R_{S}} \tag{7.65}
\end{equation*}
$$

Since $g_{m} v_{1}$ flows through $R_{D}, v_{\text {out }}=-g_{m} v_{1} R_{D}$ and

$$
\begin{align*}
\frac{v_{\text {out }}}{v_{\text {in }}} & =-\frac{g_{m} R_{D}}{1+g_{m} R_{S}}  \tag{7.66}\\
& =-\frac{R_{D}}{\frac{1}{g_{m}}+R_{S}} \tag{7.67}
\end{align*}
$$

a result identical to that expressed by Eq. (5.157) for the bipolar counterpart.

Example 7.8
image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: Vin}
name: M2, type: PMOS, ports: {S: VDD, D: Vout, G: GND}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout}
]
extrainfo:The circuit is a common-source stage with degeneration, using M1 as an NMOS and M2 as a PMOS. M2 is diode-connected, providing feedback. The output is taken across RD.

(a)
image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: Vin}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout}
name: S1, type: Resistor, value: 1/gm2, ports: {N1: GND, N2: GND}
]
extrainfo:The circuit is a common-source stage with degeneration, using M1 as an NMOS. The output is taken across RD. The resistor S1 represents a source degeneration resistor with a value of 1/gm2.

(b)

Figure 7.15 (a) Example of CS stage with degeneration, (b) simplified circuit.
Solution Transistor $M_{2}$ serves as a diode-connected device, presenting an impedance of $1 / g_{m 2}$ [Fig. 7.15(b)]. The gain is therefore given by Eq. (7.67) if $R_{S}$ is replaced with $1 / g_{m 2}$ :

$$
\begin{equation*}
A_{v}=-\frac{R_{D}}{\frac{1}{g_{m 1}}+\frac{1}{g_{m 2}}} . \tag{7.68}
\end{equation*}
$$

Exercise
What happens if $\lambda \neq 0$ for $M_{2}$ ?

In parallel with the developments in Chapter 5, we may study the effect of a resistor appearing in series with the gate (Fig. 7.16). However, since the gate current is zero (at low frequencies), $R_{G}$ sustains no voltage drop and does not affect the voltage gain or the I/O impedances.

Effect of Transistor Output Impedance As with the bipolar counterparts, the inclusion of the transistor output impedance complicates the analysis and is studied in Problem 7.32. Nonetheless, the output impedance of the degenerated CS stage plays a critical role in analog design and is worth studying here.

Figure 7.17 shows the small-signal equivalent of the circuit. Since $R_{S}$ carries a current equal to $i_{X}$ (why?), we have $v_{1}=-i_{X} R_{S}$. Also, the current through $r_{O}$ is equal to
image_name:Figure 7.16 CS stage with gate resistance
description:
[
name: M1, type: NMOS, ports: {S: s1, D: Vout, G: g1}
name: RG, type: Resistor, value: RG, ports: {N1: Vin, N2: g1}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout}
name: RS, type: Resistor, value: RS, ports: {N1: s1, N2: GND}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
]
extrainfo:The circuit is a common-source (CS) stage with a gate resistance RG and degeneration resistance RS. It is used to amplify input signals applied at Vin, with the output taken at Vout. The NMOS transistor M1 is the active device in the amplification process.

Figure 7.16 CS stage with gate resistance.
image_name:Figure 7.17 Output impedance of CS stage with degeneration
description:
[
name: V1, type: VoltageSource, value: V1, ports: {Np: v1, Nn: -Vi}
name: RS, type: Resistor, value: RS, ports: {N1: -Vi, N2: GND}
name: gmV1, type: VoltageControlledCurrentSource, ports: {Np: -Vi, Nn: -Vi}
name: ro, type: Resistor, value: ro, ports: {N1: Vx, N2: -Vi}
name: Vx, type: VoltageSource, value: Vx, ports: {Np: Vx, Nn: GND}
]
extrainfo:The circuit diagram represents the output impedance of a common-source (CS) stage with degeneration. It includes a voltage source V1, a resistor RS, a voltage-controlled current source gmV1, a resistor ro, and a voltage source Vx. The diagram illustrates the relationship between the current ix and voltage vx in the context of the CS stage.

Figure 7.17 Output impedance of CS stage with degeneration.
$i_{X}-g_{m} v_{1}=i_{X}-g_{m}\left(-i_{X} R_{S}\right)=i_{X}+g_{m} i_{X} R_{S}$. Adding the voltage drops across $r_{O}$ and $R_{S}$ and equating the result to $v_{X}$, we have

$$
\begin{equation*}
r_{O}\left(i_{X}+g_{m} i_{X} R_{S}\right)+i_{X} R_{S}=v_{X} \tag{7.69}
\end{equation*}
$$

and hence

$$
\begin{align*}
\frac{v_{X}}{i_{X}} & =r_{O}\left(1+g_{m} R_{S}\right)+R_{S}  \tag{7.70}\\
& =\left(1+g_{m} r_{O}\right) R_{S}+r_{O}  \tag{7.71}\\
& \approx g_{m} r_{O} R_{S}+r_{O} \tag{7.72}
\end{align*}
$$

Alternatively, we observe that the model in Fig. 7.17 is similar to its bipolar counterpart in Fig. 5.46(a) but with $r_{\pi}=\infty$. Letting $r_{\pi} \rightarrow \infty$ in Eqs. (5.196) and (5.197) yields the same results as above. As expected from our study of the bipolar degenerated stage, the MOS version also exhibits a "boosted" output impedance.

Compute the output resistance of the circuit in Fig. 7.18(a) if $M_{1}$ and $M_{2}$ are identical.
image_name:Figure 7.18 (a)
description:
[
name: M1, type: NMOS, ports: {S: sig2, D: d1, G: Vb}
name: M2, type: NMOS, ports: {S: GND, D: sig2, G: sig2}
name: Rout, type: Resistor, value: Rout, ports: {N1: d1, N2: Vout}
]
extrainfo:The circuit is a common-source stage with degeneration using two NMOS transistors. M2 is diode-connected.

(a)
image_name:Figure 7.18 (a)
description:
[
name: M1, type: NMOS, ports: {S: s1, D: d1, G: Vb}
name: M2, type: NMOS, ports: {S: GND, D: s1, G: s1}
name: Rout, type: Resistor, value: Rout, ports: {N1: d1, N2: Vout}
]
extrainfo:The circuit is a common-source stage with degeneration using two NMOS transistors. M2 is diode-connected. The output resistance is calculated using the formula for Rout.

(b)

Figure 7.18 (a) Example of CS stage with degeneration, (b) simplified circuit.

Solution The diode-connected device $M_{2}$ can be represented by a small-signal resistance of $\left(1 / g_{m 2}\right) \| r_{O 2} \approx 1 / g_{m 2}$. Transistor $M_{1}$ is degenerated by this resistance, and from Eq. (7.70):

$$
\begin{equation*}
R_{o u t}=r_{O 1}\left(1+g_{m 1} \frac{1}{g_{m 2}}\right)+\frac{1}{g_{m 2}} \tag{7.73}
\end{equation*}
$$

which, since $g_{m 1}=g_{m 2}=g_{m}$, reduces to

$$
\begin{align*}
R_{\text {out }} & =2 r_{O 1}+\frac{1}{g_{m}}  \tag{7.74}\\
& \approx 2 r_{O 1} . \tag{7.75}
\end{align*}
$$

Exercise Do the results remain unchanged if $M_{2}$ is replaced with a diode-connected PMOS device?

Example Determine the output resistance of the circuit in Fig. 7.19(a) and compare the result with
7.10 that in the above example. Assume $M_{1}$ and $M_{2}$ are in saturation.
image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: s1d2, D: d1, G: Vb2}
name: M2, type: NMOS, ports: {S: GND, D: s1d2, G: Vb1}
name: Rout, type: Resistor, value: Rout, ports: {N1: d1, N2: Vout}
name: d1, type: Diode, ports: {Na: Vout, Nc: d1}
]
extrainfo:The circuit is a common-source stage with NMOS transistors M1 and M2, and a diode-connected load. M2 acts as a source degeneration resistor for M1. The output is taken across Rout.

(a)
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: s1, D: d1, G: GND}
name: rO1, type: Resistor, value: rO1, ports: {N1: d1, N2: s1}
name: rO2, type: Resistor, value: rO2, ports: {N1: s1, N2: GND}
name: d1, type: Diode, ports: {Na: Vout, Nc: d1}
name: Rout, type: Resistor, value: Rout, ports: {N1: d1, N2: Vout}
]
extrainfo:The circuit is a common-source stage with NMOS transistor M1 and a diode-connected load. Resistors rO1 and rO2 are connected to the source of M1, with rO2 connected to ground. The output is taken across Rout, connected to the diode.

(b)

Figure 7.19 (a) Example of CS stage with degeneration, (b) simplified circuit.

Solution With its gate-source voltage fixed, transistor $M_{2}$ operates as a current source, introducing a resistance of $r_{O 2}$ from the source of $M_{1}$ to ground [Fig. 7.19(b)].

Equation (7.71) can therefore be written as

$$
\begin{align*}
R_{\text {out }} & =\left(1+g_{m 1} r_{O 1}\right) r_{O 2}+r_{O 1}  \tag{7.76}\\
& \approx g_{m 1} r_{O 1} r_{O 2}+r_{O 1} \tag{7.77}
\end{align*}
$$

Assuming $g_{m 1} r_{O 2} \gg 1$ (which is valid in practice), we have

$$
\begin{equation*}
R_{\text {out }} \approx g_{m 1} r_{O 1} r_{O 2} \tag{7.78}
\end{equation*}
$$

We observe that this value is quite higher than that in Eq. (7.75).

Exercise Repeat the above example for the PMOS counterpart of the circuit.

### 7.2.5 CS Core With Biasing

The effect of the simple biasing network shown in Fig. 7.1 is similar to that analyzed for the bipolar stage in Chapter 5. Depicted in Fig. 7.20(a) along with an input coupling capacitor (assumed a short circuit), such a circuit no longer exhibits an infinite input impedance:

$$
\begin{equation*}
R_{\text {in }}=R_{1} \| R_{2} \tag{7.79}
\end{equation*}
$$

image_name:(a)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: R1, type: Resistor, value: R1, ports: {N1: VDD, N2: g1}
name: R2, type: Resistor, value: R2, ports: {N1: g1, N2: GND}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout}
name: RS, type: Resistor, value: RS, ports: {N1: s1, N2: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: Vin, Nn: g1}
name: M1, type: NMOS, ports: {S: s1, D: Vout, G: g1}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
]
extrainfo:The circuit is a common-source (CS) amplifier with biasing network, input coupling capacitor, and a load resistor RD. The NMOS transistor M1 is used for amplification. R1 and R2 form a voltage divider for biasing the gate of M1. The input signal is AC-coupled via C1. The output is taken across RD, and RS provides source degeneration for stability.
image_name:(b)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: RG, type: Resistor, value: RG, ports: {N1: Vin, N2: X}
name: R1, type: Resistor, value: R1, ports: {N1: VDD, N2: g}
name: R2, type: Resistor, value: R2, ports: {N1: g, N2: GND}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout}
name: RS, type: Resistor, value: RS, ports: {N1: S1, N2: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: X, Nn: g}
name: M1, type: NMOS, ports: {S: S1, D: Vout, G: g}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
]
extrainfo:The circuit is a common-source NMOS amplifier with a gate resistor RG added for biasing. The input is capacitively coupled through C1, and the output is taken from the drain of M1. RS provides source degeneration, and RD is the load resistor.
image_name:(c)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: RG, type: Resistor, value: RG, ports: {N1: Vin, N2: x}
name: R1, type: Resistor, value: R1, ports: {N1: VDD, N2: g}
name: R2, type: Resistor, value: R2, ports: {N1: g, N2: GND}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout}
name: RS, type: Resistor, value: RS, ports: {N1: s1, N2: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: x, Nn: g}
name: C2, type: Capacitor, value: C2, ports: {Np: s1, Nn: GND}
name: M1, type: NMOS, ports: {S: s1, D: Vout, G: g}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
]
extrainfo:The circuit diagram (c) is a common-source amplifier with an NMOS transistor (M1) and a bypass capacitor (C2) connected across RS for AC signals. The input is AC-coupled through C1, and the gate bias is set by R1 and R2. The output is taken from the drain of M1.

Figure 7.20 (a) CS stage with input coupling capacitor, (b) inclusion of gate resistance, (c) use of bypass capacitor.

Thus, if the circuit is driven by a finite source impedance [Fig. 7.20(b)], the voltage gain falls to

$$
\begin{equation*}
A_{v}=\frac{R_{1} \| R_{2}}{R_{G}+R_{1} \| R_{2}} \cdot \frac{-R_{D}}{\frac{1}{g_{m}}+R_{S}} \tag{7.80}
\end{equation*}
$$

where $\lambda$ is assumed to be zero.
As mentioned in Chapter 5, it is possible to utilize degeneration for bias point stability but eliminate its effect on the small-signal performance by means of a bypass capacitor [Fig. 7.20(c)]. Unlike the case of bipolar realization, this does not alter the input impedance of the CS stage:

$$
\begin{equation*}
R_{\text {in }}=R_{1} \| R_{2} \tag{7.81}
\end{equation*}
$$

but raises the voltage gain:

$$
\begin{equation*}
A_{v}=-\frac{R_{1} \| R_{2}}{R_{G}+R_{1} \| R_{2}} g_{m} R_{D} \tag{7.82}
\end{equation*}
$$

Example Design the CS stage of Fig. 7.20(c) for a voltage gain of 5, an input impedance of $50 \mathrm{k} \Omega$,
7.11 and a power budget of 5 mW . Assume $\mu_{n} C_{o x}=100 \mu \mathrm{~A} / \mathrm{V}^{2}, V_{T H}=0.5 \mathrm{~V}, \lambda=0$, and $V_{D D}=1.8 \mathrm{~V}$. Also, assume a voltage drop of 400 mV across $R_{S}$.

Solution The power budget along with $V_{D D}=1.8 \mathrm{~V}$ implies a maximum supply current of 2.78 mA . As an initial guess, we allocate 2.7 mA to $M_{1}$ and the remaining $80 \mu \mathrm{~A}$ to $R_{1}$ and $R_{2}$. It follows that

$$
\begin{equation*}
R_{S}=148 \Omega \tag{7.83}
\end{equation*}
$$

As with typical design problems, the choice of $g_{m}$ and $R_{D}$ is somewhat flexible so long as $g_{m} R_{D}=5$. However, with $I_{D}$ known, we must ensure a reasonable value for $V_{G S}$, e.g., $V_{G S}=1 \mathrm{~V}$. This choice yields

$$
\begin{align*}
g_{m} & =\frac{2 I_{D}}{V_{G S}-V_{T H}}  \tag{7.84}\\
& =\frac{1}{92.6 \Omega} \tag{7.85}
\end{align*}
$$

and hence

$$
\begin{equation*}
R_{D}=463 \Omega \tag{7.86}
\end{equation*}
$$

Writing

$$
\begin{equation*}
I_{D}=\frac{1}{2} \mu_{n} C_{o x} \frac{W}{L}\left(V_{G S}-V_{T H}\right)^{2} \tag{7.87}
\end{equation*}
$$

gives

$$
\begin{equation*}
\frac{W}{L}=216 \tag{7.88}
\end{equation*}
$$

With $V_{G S}=1 \mathrm{~V}$ and a $400-\mathrm{mV}$ drop across $R_{S}$, the gate voltage reaches 1.4 V , requiring that

$$
\begin{equation*}
\frac{R_{2}}{R_{1}+R_{2}} V_{D D}=1.4 \mathrm{~V} \tag{7.89}
\end{equation*}
$$

which, along with $R_{i n}=R_{1} \| R_{2}=50 \mathrm{k} \Omega$, yields

$$
\begin{align*}
& R_{1}=64.3 \mathrm{k} \Omega  \tag{7.90}\\
& R_{2}=225 \mathrm{k} \Omega . \tag{7.91}
\end{align*}
$$

We must now check to verify that $M_{1}$ indeed operates in saturation. The drain voltage is given by $V_{D D}-I_{D} R_{D}=1.8 \mathrm{~V}-1.25 \mathrm{~V}=0.55 \mathrm{~V}$. Since the gate voltage is equal to 1.4 V , the gate-drain voltage difference exceeds $V_{T H}$, driving $M_{1}$ into the triode region!

How did our design procedure lead to this result? For the given $I_{D}$, we have chosen an excessively large $R_{D}$, i.e., an excessively small $g_{m}$ (because $g_{m} R_{D}=5$ ), even though $V_{G S}$ is reasonable. We must therefore increase $g_{m}$ so as to allow a lower value for $R_{D}$. For example, suppose we halve $R_{D}$ and double $g_{m}$ by increasing $W / L$ by a factor of four:

$$
\begin{align*}
\frac{W}{L} & =864  \tag{7.92}\\
g_{m} & =\frac{1}{46.3 \Omega} \tag{7.93}
\end{align*}
$$

The corresponding gate-source voltage is obtained from (7.84):

$$
\begin{equation*}
V_{G S}=250 \mathrm{mV} \tag{7.94}
\end{equation*}
$$

yielding a gate voltage of 650 mV .
Is $M_{1}$ in saturation? The drain voltage is equal to $V_{D D}-R_{D} I_{D}=1.17 \mathrm{~V}$, a value higher than the gate voltage minus $V_{T H}$. Thus, $M_{1}$ operates in saturation.

Exercise Repeat the above example for a power budget of 3 mW and $V_{D D}=1.2 \mathrm{~V}$.

## 7.3 COMMON-GATE STAGE

Shown in Fig. 7.21, the CG topology resembles the common-base stage studied in Chapter 5 . Here, if the input rises by a small value, $\Delta V$, then the gate-source voltage of $M_{1}$ decreases by the same amount, thereby lowering the drain current by $g_{m} \Delta V$ and
image_name:Figure 7.21 Common-gate stage
description:
[
name: M1, type: NMOS, ports: {S: Vin, D: Vout, G: Vb}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
]
extrainfo:This is a common-gate amplifier circuit. The input is applied to the source of the NMOS transistor M1, and the output is taken from the drain. The gate of M1 is connected to a bias voltage Vb. The resistor RD is connected between VDD and the drain of M1. The circuit is used for amplifying voltage signals.

Figure 7.21 Common-gate stage.
raising $V_{\text {out }}$ by $g_{m} \Delta V R_{D}$. That is, the voltage gain is positive and equal to

$$
\begin{equation*}
A_{v}=g_{m} R_{D} \tag{7.95}
\end{equation*}
$$

The CG stage suffers from voltage headroom-gain trade-offs similar to those of the CB topology. In particular, to achieve a high gain, a high $I_{D}$ or $R_{D}$ is necessary, but the drain voltage, $V_{D D}-I_{D} R_{D}$, must remain above $V_{b}-V_{T H}$ to ensure $M_{1}$ is saturated.

Example A microphone having a dc level of zero drives a CG stage biased at $I_{D}=0.5 \mathrm{~mA}$. If 7.12 $W / L=50, \mu_{n} C_{o x}=100 \mu \mathrm{~A} / \mathrm{V}^{2}, V_{T H}=0.5 \mathrm{~V}$, and $V_{D D}=1.8 \mathrm{~V}$, determine the maximum allowable value of $R_{D}$ and hence the maximum voltage gain. Neglect channellength modulation.

Solution With $W / L$ known, the gate-source voltage can be determined from

$$
\begin{equation*}
I_{D}=\frac{1}{2} \mu_{n} C_{o x} \frac{W}{L}\left(V_{G S}-V_{T H}\right)^{2} \tag{7.96}
\end{equation*}
$$

as

$$
\begin{equation*}
V_{G S}=0.947 \mathrm{~V} \tag{7.97}
\end{equation*}
$$

For $M_{1}$ to remain in saturation,

$$
\begin{equation*}
V_{D D}-I_{D} R_{D}>V_{b}-V_{T H} \tag{7.98}
\end{equation*}
$$

and hence

$$
\begin{equation*}
R_{D}<2.71 \mathrm{k} \Omega \tag{7.99}
\end{equation*}
$$

Also, the above value of $W / L$ and $I_{D}$ yield $g_{m}=(447 \Omega)^{-1}$ and

$$
\begin{equation*}
A_{v} \leq 6.06 \tag{7.100}
\end{equation*}
$$

Figure 7.22 summarizes the allowable signal levels in this design. The gate voltage can be generated using a resistive divider similar to that in Fig. 7.20(a).

Exercise If a gain of 10 is required, what value should be chosen for $W / L$ ?
image_name:Figure 7.22
description:
[
name: M1, type: NMOS, ports: {S: Vin, D: Vout, G: Vb}
name: RD, type: Resistor, value: RD, ports: {N1: Vout, N2: VDD}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
]
extrainfo:The circuit represents a common-gate (CG) stage with an NMOS transistor M1. The gate voltage Vb is 0.947 V, and Vb - Vth is 0.447 V. The output voltage is taken across RD, and the input is applied to the source of M1.

Figure 7.22 Signal levels in CG stage.

We now compute the I/O impedances of the CG stage, expecting to obtain results similar to those of the CB topology. Neglecting channel-length modulation for now, we have from Fig. 7.23(a) $v_{1}=-v_{X}$ and

$$
\begin{align*}
i_{X} & =-g_{m} v_{1}  \tag{7.101}\\
& =g_{m} v_{X} \tag{7.102}
\end{align*}
$$

That is,

$$
\begin{equation*}
R_{i n}=\frac{1}{g_{m}} \tag{7.103}
\end{equation*}
$$

a relatively low value. Also, from Fig. 7.23(b), $v_{1}=0$ and hence

$$
\begin{equation*}
R_{\text {out }}=R_{D} \tag{7.104}
\end{equation*}
$$

an expected result because the circuits of Figs. 7.23(b) and 7.7 are identical.

Let us study the behavior of the CG stage in the presence of a finite source impedance (Fig. 7.24) but still with $\lambda=0$. In a manner similar to that depicted in Chapter 5 for the CB topology, we write

$$
\begin{align*}
v_{X} & =\frac{\frac{1}{g_{m}}}{\frac{1}{g_{m}}+R_{S}} v_{i n}  \tag{7.105}\\
& =\frac{1}{1+g_{m} R_{S}} v_{i n} \tag{7.106}
\end{align*}
$$

image_name:(a)
description:
[
name: V1, type: VoltageSource, value: V1, ports: {Np: V1, Nn: GND}
name: Vx, type: VoltageSource, value: Vx, ports: {Np: Vx, Nn: GND}
name: gmV1, type: VoltageControlledCurrentSource, ports: {Np: X, Nn: Vx}
name: RD, type: Resistor, value: RD, ports: {N1: X, N2: GND}
]
extrainfo:The circuit is a common-gate stage with a voltage source V1 supplying the input voltage. The voltage-controlled current source gmV1 is controlled by V1 and outputs current through RD to ground. Vx is used as a feedback voltage source.
image_name:(b)
description:
[
name: v1, type: VoltageSource, value: v1, ports: {Np: X, Nn: GND}
name: RD, type: Resistor, value: RD, ports: {N1: X, N2: GND}
name: vx, type: VoltageSource, value: vx, ports: {Np: Vx, Nn: GND}
]
extrainfo:The circuit diagram (b) is a common-gate stage with a voltage source V1, a resistor RD, and a voltage source Vx. The current source gmV1 is connected to node X, which is common to V1 and RD. Vx is connected to the output node, providing feedback.

Did you know?

The common-gate stage is sometimes used as a low-noise RF amplifier, e.g., at the input of your WiFi receiver. This topology is attractive because its low input impedance allows simple "impedance matching" with the antenna. However, with the reduction of the intrinsic gain, $g_{m} r_{O}$, as a result of scaling, the input impedance, $R_{i n}$, is now too high! It can be shown that with channel-length modulation

$$
R_{i n}=\frac{R_{D}+r_{0}}{1+g_{m} r_{0}}
$$

which reduces to $1 / g_{m}$ if $g_{m} r_{0} \gg 1$ and $R_{D} \ll r_{0}$. Since neither of these conditions holds anymore, the CG stage presents new challenges to RF designers.
image_name:Figure 7.24 Simplification of CG stage with signal source resistance
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: X}
name: M1, type: NMOS, ports: {S: X, D: Vout, G: Vb}
name: RD, type: Resistor, value: RD, ports: {N1: Vout, N2: VDD}
name: 1/gm, type: VoltageControlledCurrentSource, value: 1/gm, ports: {Np: X, Nn: GND}
]
extrainfo:The circuit is a simplified common-gate (CG) stage with source resistance Rs. It includes a voltage source Vin, an NMOS transistor M1, and resistors RD and RS. The stage also includes a voltage-controlled current source with transconductance 1/gm. The output voltage is taken across RD.

Figure 7.24 Simplification of CG stage with signal source resistance.

Thus,

$$
\begin{align*}
\frac{v_{\text {out }}}{v_{\text {in }}} & =\frac{v_{\text {out }}}{v_{X}} \cdot \frac{v_{X}}{v_{\text {in }}}  \tag{7.107}\\
& =\frac{g_{m} R_{D}}{1+g_{m} R_{S}}  \tag{7.108}\\
& =\frac{R_{D}}{\frac{1}{g_{m}}+R_{S}} \tag{7.109}
\end{align*}
$$

The gain is therefore equal to that of the degenerated CS stage except for a negative sign.
In contrast to the common-source stage, the CG amplifier exhibits a current gain of unity: the current provided by the input voltage source simply flows through the channel and emerges from the drain node.

The analysis of the common-gate stage in the general case, i.e., including both channellength modulation and a finite source impedance, is beyond the scope of this book (Problem 7.42). However, we can make two observations. First, a resistance appearing in series with the gate terminal [Fig. 7.25(a)] does not alter the gain or I/O impedances (at low frequencies) because it sustains a zero potential drop-as if its value were zero. Second, the output resistance of the CG stage in the general case [Fig. 7.25(b)] is identical to that of the degenerated CS topology:

$$
\begin{equation*}
R_{\text {out }}=\left(1+g_{m} r_{O}\right) R_{S}+r_{O} \tag{7.110}
\end{equation*}
$$

image_name:Figure 7.25 (a)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout}
name: RG, type: Resistor, value: RG, ports: {N1: G, N2: Vb}
name: M1, type: NMOS, ports: {S: Vin, D: Vout, G: G}
name: RS, type: Resistor, value: RS, ports: {N1: GND, N2: S1}
name: ro, type: Resistor, value: ro, ports: {N1: S1, N2: d1}
name: Rout, type: Resistor, value: Rout, ports: {N1: d1, N2: di}
name: di, type: Diode, ports: {Na: di, Nc: GND}
]
extrainfo:Figure 7.25(a) shows a common-gate (CG) amplifier stage with a gate resistance RG. Figure 7.25(b) depicts the output resistance of the CG stage with a source degeneration resistor RS and output resistance Rout.
image_name:Figure 7.25 (b)
description:
[
name: RS, type: Resistor, value: RS, ports: {N1: GND, N2: S1}
name: ro, type: Resistor, value: ro, ports: {N1: S1, N2: d1}
name: Rout, type: Resistor, value: Rout, ports: {N1: d1, N2: di}
name: M1, type: NMOS, ports: {S: GND, D: d1, G: di}
name: di, type: Diode, ports: {Na: di, Nc: GND}
]
extrainfo:The circuit in Figure 7.25(b) is a common-gate (CG) stage with an output resistance network. It includes a resistor RS connected to ground, a resistor ro connected between S1 and d1, and a resistor Rout connected to the diode di. The NMOS transistor M1 has its source connected to ground, drain connected to d1, and gate connected to di. The diode di is connected to ground.

Figure 7.25 (a) CG stage with gate resistance, (b) output resistance of CG stage.

Example 7.13

For the circuit shown in Fig. 7.26(a), calculate the voltage gain if $\lambda=0$ and the output impedance if $\lambda>0$.
image_name:Figure 7.26 (a)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: X}
name: M1, type: NMOS, ports: {S: X, D: Vout, G: Vb}
name: M2, type: NMOS, ports: {S: GND, D: X, G: Vb}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout}
]
extrainfo:This is a common-gate amplifier stage with NMOS transistors M1 and M2. M1 is configured with its source connected to node X and its drain to Vout, while M2 has its source at ground and its drain at node X. The input voltage is applied at Vin, and the output is taken from Vout. RD provides the load at the output. The gate voltage Vb is common to both NMOS transistors.

(a)
image_name:(b)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: Rs, type: Resistor, value: Rs, ports: {N1: Vin, N2: Vx}
name: 1/gm1, type: Resistor, value: 1/gm1, ports: {N1: Vx, N2: GND}
name: 1/gm2, type: Resistor, value: 1/gm2, ports: {N1: Vx, N2: GND}
]
extrainfo:This circuit represents the equivalent input network of a common-gate amplifier stage. The input voltage is applied at Vin, and the node Vx is the intermediate node where the resistors Rs, 1/gm1, and 1/gm2 converge. Both resistors 1/gm1 and 1/gm2 are connected to ground.

(b)
image_name:Figure 7.26 (b)
description:
[
name: Rs, type: Resistor, ports: {N1: Vin, N2: S1}
name: r01, type: Resistor, ports: {N1: S1, N2: D1}
name: M1, type: NMOS, ports: {S: GND, D: D1, G: S1}
name: rO2, type: Resistor, ports: {N1: S1, N2: GND}
name: d1, type: CurrentSource, ports: {Np: D1, Nn: GND}
name: Rout1, type: Resistor, ports: {N1: D1, N2: Vout}
]
extrainfo:This circuit is the equivalent input network of a common-gate amplifier stage. Rs, r01, and Rout1 are resistors, M1 is an NMOS transistor, and d1 is a current source. The node S1 is the intermediate node where these components converge.

(c)

Figure 7.26 (a) Example of CG stage, (b) equivalent input network, (c) calculation of output resistance.

Solution
We first compute $v_{X} / v_{i n}$ with the aid of the equivalent circuit depicted in Fig. 7.26(b):

$$
\begin{align*}
\frac{v_{X}}{v_{i n}} & =\frac{\frac{1}{g_{m 2}} \| \frac{1}{g_{m 1}}}{\frac{1}{g_{m 2}} \| \frac{1}{g_{m 1}}+R_{S}}  \tag{7.111}\\
& =\frac{1}{1+\left(g_{m 1}+g_{m 2}\right) R_{S}} \tag{7.112}
\end{align*}
$$

Noting that $v_{\text {out }} / v_{X}=g_{m 1} R_{D}$, we have

$$
\begin{equation*}
\frac{v_{\text {out }}}{v_{\text {in }}}=\frac{g_{m 1} R_{D}}{1+\left(g_{m 1}+g_{m 2}\right) R_{S}} \tag{7.113}
\end{equation*}
$$

To compute the output impedance, we first consider $R_{\text {out } 1}$, as shown in Fig. 7.26(c), which from Eq. (7.110) is equal to

$$
\begin{align*}
& R_{\text {out } 1}=\left(1+g_{m 1} r_{O 1}\right)\left(\frac{1}{g_{m 2}}\left\|r_{O 2}\right\| R_{S}\right)+r_{O 1}  \tag{7.114}\\
& \approx g_{m 1} r_{O 1}\left(\frac{1}{g_{m 2}} \| R_{S}\right)+r_{O 1} \tag{7.115}
\end{align*}
$$

The overall output impedance is then given by

$$
\begin{align*}
R_{\text {out }} & =R_{\text {out } 1} \| R_{D}  \tag{7.116}\\
& \approx\left[g_{m 1} r_{O 1}\left(\frac{1}{g_{m 2}} \| R_{S}\right)+r_{O 1}\right] \| R_{D} \tag{7.117}
\end{align*}
$$

Exercise Calculate the output impedance if the gate of $M_{2}$ is tied to a constant voltage.

### 7.3.1 CG Stage With Biasing

Following our study of the CB biasing in Chapter 5, we surmise the CG amplifier can be biased as shown in Fig. 7.27. Providing a path for the bias current to ground, resistor $R_{3}$ lowers the input impedance-and hence the voltage gain-if the signal source exhibits a finite output impedance, $R_{S}$.
image_name:Figure 7.27 CG stage with biasing
description:
[
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: X}
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: X}
name: C1, type: Capacitor, value: C1, ports: {Np: Vin, Nn: X}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout}
name: R1, type: Resistor, value: R1, ports: {N1: VDD, N2: g1}
name: R2, type: Resistor, value: R2, ports: {N1: g1, N2: GND}
name: R3, type: Resistor, value: R3, ports: {N1: X, N2: GND}
name: g1, type: VoltageSource, value: g1, ports: {Np: g1, Nn: X}
]
extrainfo:The circuit is a Common Gate (CG) amplifier stage with biasing. The input is applied at Vin, and the output is taken at Vout. The NMOS transistor M1 is used in the CG configuration, with its source connected to ground and its gate connected to node X. The biasing is provided by resistors R1, R2, and R3, with a voltage source g1 setting the gate voltage. The load resistor RD connects the drain to VDD, and the input signal is AC coupled through capacitor C1.

Figure 7.27 CG stage with biasing.

Since the impedance seen to the right of node $X$ is equal to $R_{3} \|\left(1 / g_{m}\right)$, we have

$$
\begin{align*}
\frac{v_{\text {out }}}{v_{\text {in }}} & =\frac{v_{X}}{v_{\text {in }}} \cdot \frac{v_{\text {out }}}{v_{X}}  \tag{7.118}\\
& =\frac{R_{3} \|\left(1 / g_{m}\right)}{R_{3} \|\left(1 / g_{m}\right)+R_{S}} \cdot g_{m} R_{D} \tag{7.119}
\end{align*}
$$

where channel-length modulation is neglected. As mentioned earlier, the voltage divider consisting of $R_{1}$ and $R_{2}$ does not affect the small-signal behavior of the circuit (at low frequencies).

Design the common-gate stage of Fig. 7.27 for the following parameters: $v_{\text {out }} /$ $v_{i n}=5, R_{S}=0, R_{3}=500 \Omega, 1 / g_{m}=50 \Omega$, power budget $=2 \mathrm{~mW}, V_{D D}=1.8 \mathrm{~V}$. Assume $\mu_{n} C_{o x}=100 \mu \mathrm{~A} / \mathrm{V}^{2}, V_{T H}=0.5 \mathrm{~V}$, and $\lambda=0$.

Solution From the power budget, we obtain a total supply current of 1.11 mA . Allocating $10 \mu \mathrm{~A}$ to the voltage divider, $R_{1}$ and $R_{2}$, we leave 1.1 mA for the drain current of $M_{1}$. Thus, the voltage drop across $R_{3}$ is equal to 550 mV .

We must now compute two interrelated parameters: $W / L$ and $R_{D}$. A larger value of $W / L$ yields a greater $g_{m}$, allowing a lower value of $R_{D}$. As in Example 7.11, we choose an initial value for $V_{G S}$ to arrive at a reasonable guess for $W / L$. For example, if $V_{G S}=0.8 \mathrm{~V}$, then $W / L=244$, and $g_{m}=2 I_{D} /\left(V_{G S}-V_{T H}\right)=(136.4 \Omega)^{-1}$, dictating $R_{D}=682 \Omega$ for $v_{\text {out }} / v_{\text {in }}=5$.

Let us determine whether $M_{1}$ operates in saturation. The gate voltage is equal to $V_{G S}$ plus the drop across $R_{3}$, amounting to 1.35 V . On the other hand, the drain voltage is given by $V_{D D}-I_{D} R_{D}=1.05 \mathrm{~V}$. Since the drain voltage exceeds $V_{G}-V_{T H}, M_{1}$ is indeed in saturation.

The resistive divider consisting of $R_{1}$ and $R_{2}$ must establish a gate voltage equal to 1.35 V while drawing $10 \mu \mathrm{~A}$ :

$$
\begin{align*}
\frac{V_{D D}}{R_{1}+R_{2}} & =10 \mu \mathrm{~A}  \tag{7.120}\\
\frac{R_{2}}{R_{1}+R_{2}} V_{D D} & =1.35 \mathrm{~V} \tag{7.121}
\end{align*}
$$

It follows that $R_{1}=45 \mathrm{k} \Omega$ and $R_{2}=135 \mathrm{k} \Omega$.
If $W / L$ cannot exceed 100 , what voltage gain can be achieved?

Suppose in Example 7.14, we wish to minimize $W / L$ (and hence transistor capacitances).
7.15 What is the minimum acceptable value of $W / L$ ?

Solution For a given $I_{D}$, as $W / L$ decreases, $V_{G S}-V_{T H}$ increases. Thus, we must first compute the maximum allowable $V_{G S}$. We impose the condition for saturation as

$$
\begin{equation*}
V_{D D}-I_{D} R_{D}>V_{G S}+V_{R 3}-V_{T H} \tag{7.122}
\end{equation*}
$$

where $V_{R 3}$ denotes the voltage drop across $R_{3}$, and set $g_{m} R_{D}$ to the required gain:

$$
\begin{equation*}
\frac{2 I_{D}}{V_{G S}-V_{T H}} R_{D}=A_{v} \tag{7.123}
\end{equation*}
$$

Eliminating $R_{D}$ from Eqs. (7.122) and (7.123) gives:

$$
\begin{equation*}
V_{D D}-\frac{A_{v}}{2}\left(V_{G S}-V_{T H}\right)>V_{G S}-V_{T H}+V_{R 3} \tag{7.124}
\end{equation*}
$$

and hence

$$
\begin{equation*}
V_{G S}-V_{T H}<\frac{V_{D D}-V_{R 3}}{\frac{A_{v}}{2}+1} \tag{7.125}
\end{equation*}
$$

In other words,

$$
\begin{equation*}
W / L>\frac{2 I_{D}}{\mu_{n} C_{o x}\left(2 \frac{V_{D D}-V_{R 3}}{A_{v}+2}\right)^{2}} \tag{7.126}
\end{equation*}
$$

It follows that

$$
\begin{equation*}
W / L>172.5 . \tag{7.127}
\end{equation*}
$$

Exercise Repeat the above example for $A_{v}=10$.

## 7.4 SOURCE FOLLOWER

The MOS counterpart of the emitter follower is called the "source follower" (or the "common-drain" stage) and shown in Fig. 7.28. The amplifier senses the input at the gate and produces the output at the source, with the drain tied to $V_{D D}$. The circuit's behavior is similar to that of the bipolar counterpart.
image_name:Figure 7.28 Source follower
description:
[
name: M1, type: NMOS, ports: {S: Vout, D: VDD, G: Vin}
name: RL, type: Resistor, value: RL, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit is a source follower (common-drain) configuration using an NMOS transistor. The input is applied to the gate of the NMOS, and the output is taken from the source, providing a voltage level shift.

Figure 7.28 Source follower.

### 7.4.1 Source Follower Core

If the gate voltage of $M_{1}$ in Fig. 7.28 is raised by a small amount, $\Delta V_{i n}$, the gate-source voltage tends to increase, thereby raising the source current and hence the output voltage. Thus, $V_{\text {out }}$ "follows" $V_{\text {in }}$. Since the dc level of $V_{\text {out }}$ is lower than that of $V_{\text {in }}$ by $V_{G S}$, we say the follower can serve as a "level shift" circuit. From our analysis of emitter followers in Chapter 5, we expect this topology to exhibit a subunity gain, too.

Figure 7.29(a) depicts the small-signal equivalent of the source follower, including channel-length modulation. Recognizing that $r_{O}$ appears in parallel with $R_{L}$, we have

$$
\begin{equation*}
g_{m} v_{1}\left(r_{O} \| R_{L}\right)=v_{\text {out }} \tag{7.128}
\end{equation*}
$$

Also,

$$
\begin{equation*}
v_{\text {in }}=v_{1}+v_{\text {out }} \tag{7.129}
\end{equation*}
$$

It follows that

$$
\begin{align*}
\frac{v_{\text {out }}}{v_{\text {in }}} & =\frac{g_{m}\left(r_{O} \| R_{L}\right)}{1+g_{m}\left(r_{O} \| R_{L}\right)}  \tag{7.130}\\
& =\frac{r_{O} \| R_{L}}{\frac{1}{g_{m}}+r_{O} \| R_{L}} \tag{7.131}
\end{align*}
$$

The voltage gain is therefore positive and less than unity. It is desirable to maximize $R_{L}$ (and $r_{O}$ ).

As with emitter followers, we can view the above result as voltage division between a resistance equal to $1 / g_{m}$ and another equal to $r_{O} \| R_{L}$ [Fig. 7.29(b)]. Note, however, that a resistance placed in series with the gate does not affect Eq. (7.131) (at low frequencies) because it sustains a zero drop.
image_name:(b)
description:
[
name: Vin, type: VoltageSource, ports: {Np: Vin, Nn: GND}
name: gmV1, type: VoltageControlledCurrentSource, ports: {Np: GND, Nn: Vout}
name: rO, type: Resistor, value: rO, ports: {N1: GND, N2: Vout}
name: RL, type: Resistor, value: RL, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit is a source follower configuration with a voltage-controlled current source and resistive load. The voltage gain is positive but less than unity.

(a)
image_name:(a)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: 1/gm, type: Resistor, value: 1/gm, ports: {N1: Vin, N2: Vout}
name: RL||ro, type: Resistor, value: RL||ro, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit is a source follower configuration with a voltage-controlled current source and resistive load. The voltage gain is positive but less than unity.

(b)

Example
7.16

A source follower is realized as shown in Fig. 7.30(a), where $M_{2}$ serves as a current source. Calculate the voltage gain of the circuit.
image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: Vout, D: VDD, G: Vin}
name: M2, type: NMOS, ports: {S: GND, D: Vout, G: Vb}
]
extrainfo:The circuit is a source follower configuration with a voltage-controlled current source and resistive load. The voltage gain is positive but less than unity. M1 acts as the main transistor providing the output voltage at Vout, and M2 serves as a current source.

(a)
image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: Vout, D: GND, G: Vin}
name: rO1, type: Resistor, value: rO1, ports: {N1: GND, N2: Vout}
name: rO2, type: Resistor, value: rO2, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit is a source follower configuration with NMOS M1 providing the output voltage at Vout. Resistors rO1 and rO2 form part of the load, with rO2 connected to ground. The voltage gain is positive but less than unity.

(b)

Figure 7.30 (a) Follower with ideal current source, (b) simplified circuit.

Solution Since $M_{2}$ simply presents an impedance of $r_{O 2}$ from the output node to ac ground [Fig. 7.30(b)], we substitute $R_{L}=r_{O 2}$ in Eq. (7.131):

$$
\begin{equation*}
A_{v}=\frac{r_{O 1} \| r_{O 2}}{\frac{1}{g_{m 1}}+r_{O 1} \| r_{O 2}} \tag{7.132}
\end{equation*}
$$

If $r_{O 1} \| r_{O 2} \gg 1 / g_{m 1}$, then $A_{v} \approx 1$.

Exercise Repeat the above example if a resistance of value $R_{S}$ is placed in series with the source of $M_{2}$.

Example
7.17

Design a source follower to drive a $50-\Omega$ load with a voltage gain of 0.5 and a power budget of 10 mW . Assume $\mu_{n} C_{o x}=100 \mu \mathrm{~A} / \mathrm{V}^{2}, V_{T H}=0.5 \mathrm{~V}, \lambda=0$, and $V_{D D}=1.8 \mathrm{~V}$.

Solution With $R_{L}=50 \Omega$ and $r_{O}=\infty$ in Fig. 7.28, we have

$$
\begin{equation*}
A_{v}=\frac{R_{L}}{\frac{1}{g_{m}}+R_{L}} \tag{7.133}
\end{equation*}
$$

and hence

$$
\begin{equation*}
g_{m}=\frac{1}{50 \Omega} . \tag{7.134}
\end{equation*}
$$

The power budget and supply voltage yield a maximum supply current of 5.56 mA . Using this value for $I_{D}$ in $g_{m}=\sqrt{2 \mu_{n} C_{o x}(W / L) I_{D}}$ gives

$$
\begin{equation*}
W / L=360 . \tag{7.135}
\end{equation*}
$$

Exercise What voltage gain can be achieved if the power budget is raised to 15 mW ?
image_name:Figure 7.31 Output resistance of source follower
description:
[
name: M1, type: NMOS, ports: {S: GND, D: s1, G: GND}
name: ro, type: Resistor, value: ro, ports: {N1: s1, N2: GND}
name: RL, type: Resistor, value: RL, ports: {N1: s1, N2: GND}
]
extrainfo:The circuit diagram shows a source follower configuration with NMOS transistor M1. The output resistance is calculated as the parallel combination of 1/gm, ro, and RL. The source node s1 connects to both resistors ro and RL, which are grounded at the other end.

Figure 7.31 Output resistance of source follower.

It is instructive to compute the output impedance of the source follower. ${ }^{2}$ As illustrated in Fig. 7.31, $R_{\text {out }}$ consists of the resistance seen looking up into the source in parallel with that seen looking down into $R_{L}$. With $\lambda \neq 0$, the former is equal to $\left(1 / g_{m}\right) \| r_{O}$, yielding

$$
\begin{align*}
R_{\text {out }} & =\frac{1}{g_{m}}\left\|r_{O}\right\| R_{L}  \tag{7.136}\\
& \approx \frac{1}{g_{m}} \| R_{L} . \tag{7.137}
\end{align*}
$$

In summary, the source follower exhibits a very high input impedance and a relatively low output impedance, thereby providing buffering capability.
image_name:Figure 7.32 Source follower with input and output coupling capacitors
description:
[
name: C1, type: Capacitor, value: C1, ports: {Np: Vin, Nn: g1}
name: C2, type: Capacitor, value: C2, ports: {Np: s1, Nn: Vout}
name: RG, type: Resistor, value: RG, ports: {N1: g1, N2: VDD}
name: RS, type: Resistor, value: RS, ports: {N1: s1, N2: GND}
name: M1, type: NMOS, ports: {S: s1, D: VDD, G: g1}
]
extrainfo:The circuit is a source follower with input and output coupling capacitors, providing high input impedance and low output impedance. The NMOS transistor M1 operates in saturation with the gate and drain voltages equal.

Figure 7.32 Source follower with input and output coupling capacitors.

### 7.4.2 Source Follower With Biasing

The biasing of source followers is similar to that of emitter followers (Chapter 5). Figure 7.32 depicts an example where $R_{G}$ establishes a dc voltage equal to $V_{D D}$ at the gate of $M_{1}$ (why?) and $R_{S}$ sets the drain bias current. Note that $M_{1}$ operates in saturation because the gate and drain voltages are equal. Also, the input impedance of the circuit has dropped from infinity to $R_{G}$.

Let us compute the bias current of the circuit. With a zero voltage drop across $R_{G}$, we have

$$
\begin{equation*}
V_{G S}+I_{D} R_{S}=V_{D D} . \tag{7.138}
\end{equation*}
$$

[^5]Neglecting channel-length modulation, we write

$$
\begin{align*}
I_{D} & =\frac{1}{2} \mu_{n} C_{o x} \frac{W}{L}\left(V_{G S}-V_{T H}\right)^{2}  \tag{7.139}\\
& =\frac{1}{2} \mu_{n} C_{o x} \frac{W}{L}\left(V_{D D}-I_{D} R_{S}-V_{T H}\right)^{2} . \tag{7.140}
\end{align*}
$$

The resulting quadratic equation can be solved to obtain $I_{D}$.

Design the source follower of Fig. 7.32 for a drain current of 1 mA and a voltage gain of 0.8 . Assume $\mu_{n} C_{o x}=100 \mu \mathrm{~A} / \mathrm{V}^{2}, V_{T H}=0.5 \mathrm{~V}, \lambda=0, V_{D D}=1.8 \mathrm{~V}$, and $R_{G}=50 \mathrm{k} \Omega$.

Solution The unknowns in this problem are $V_{G S}, W / L$, and $R_{S}$. The following three equations can be formed:

$$
\begin{align*}
I_{D} & =\frac{1}{2} \mu_{n} C_{o x} \frac{W}{L}\left(V_{G S}-V_{T H}\right)^{2}  \tag{7.141}\\
I_{D} R_{S}+V_{G S} & =V_{D D}  \tag{7.142}\\
A_{v} & =\frac{R_{S}}{\frac{1}{g_{m}}+R_{S}} . \tag{7.143}
\end{align*}
$$

If $g_{m}$ is written as $2 I_{D} /\left(V_{G S}-V_{T H}\right)$, then Eqs. (7.142) and (7.143) do not contain $W / L$ and can be solved to determine $V_{G S}$ and $R_{S}$. With the aid of Eq. (7.142), we write Eq. (7.143) as

$$
\begin{align*}
A_{v} & =\frac{R_{S}}{\frac{V_{G S}-V_{T H}}{2 I_{D}}+R_{S}}  \tag{7.144}\\
& =\frac{2 I_{D} R_{S}}{V_{G S}-V_{T H}+2 I_{D} R_{S}}  \tag{7.145}\\
& =\frac{2 I_{D} R_{S}}{V_{D D}-V_{T H}+I_{D} R_{S}} \tag{7.146}
\end{align*}
$$

Thus,

$$
\begin{align*}
R_{S} & =\frac{V_{D D}-V_{T H}}{I_{D}} \frac{A_{v}}{2-A_{v}}  \tag{7.147}\\
& =867 \Omega . \tag{7.148}
\end{align*}
$$

and

$$
\begin{align*}
V_{G S} & =V_{D D}-I_{D} R_{S}  \tag{7.149}\\
& =V_{D D}-\left(V_{D D}-V_{T H}\right) \frac{A_{v}}{2-A_{v}}  \tag{7.150}\\
& =0.933 \mathrm{~V} \tag{7.151}
\end{align*}
$$

It follows from Eq. (7.141) that

$$
\begin{equation*}
\frac{W}{L}=107 \tag{7.152}
\end{equation*}
$$

Exercise What voltage gain can be achieved if $W / L$ cannot exceed 50?

Equation (7.140) reveals that the bias current of the source follower varies with the supply voltage. To avoid this effect, integrated circuits bias the follower by means of a current source (Fig. 7.33).
image_name:Figure 7.33 Source follower with biasing
description:
[
name: RG, type: Resistor, ports: {N1: VDD, N2: g1}
name: C1, type: Capacitor, ports: {Np: Vin, Nn: g1}
name: M1, type: NMOS, ports: {S: s1d2, D: VDD, G: g1}
name: C2, type: Capacitor, ports: {Np: s1d2, Nn: Vout}
name: S1, type: CurrentSource, ports: {Np: s1, Nn: GND}
name: M2, type: NMOS, ports: {S: GND, D: s1d2, G: Vb}
]
extrainfo:The circuit is a source follower with biasing, where M1 and M2 form a cascode stage. The biasing is provided by a current source (S1) and a bias voltage (Vb) for M2. The circuit aims to stabilize the bias current against variations in the supply voltage (VDD).

Figure 7.33 Source follower with biasing.

## 7.5 SUMMARY AND ADDITIONAL EXAMPLES

In this chapter, we have studied three basic CMOS building blocks, namely, the commonsource stage, the common-gate stage, and the source follower. As observed throughout the chapter, the small-signal behavior of these circuits is quite similar to that of their bipolar counterparts, with the exception of the high impedance seen at the gate terminal. We have noted that the biasing schemes are also similar, with the quadratic $I_{D}-V_{G S}$ relationship supplanting the exponential $I_{C}-V_{B E}$ characteristic.

In this section, we consider a number of additional examples to solidify the concepts introduced in this chapter, emphasizing analysis by inspection.

Example Calculate the voltage gain and output impedance of the circuit shown in Fig. 7.34(a).
image_name:(a)
description:
[
name: M1, type: PMOS, ports: {S: VDD, D: Vout, G: Vin}
name: M2, type: NMOS, ports: {S: GND, D: Vout, G: Vb}
name: M3, type: NMOS, ports: {S: Vout, D: GND, G: Vout}
]
extrainfo:The circuit is a common-source (CS) amplifier stage with PMOS M1 as the input device. M2 acts as a current source, and M3 is diode-connected. The output is taken from the drain of M1.

(a)
image_name:(a)
description:
[
name: M1, type: PMOS, ports: {S: VDD, D: Vout, G: Vin}
name: rO1, type: Resistor, value: rO1, ports: {N1: VDD, N2: Vout}
name: rO2, type: Resistor, value: rO2, ports: {N1: Vout, N2: GND}
name: rO3, type: Resistor, value: rO3, ports: {N1: Vout, N2: GND}
name: 1/gm3, type: Resistor, value: 1/gm3, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit is a common-source amplifier stage with PMOS M1 as the input device. M2 acts as a current source, and M3 is diode-connected. The output is taken from the drain of M1.

(b)

Figure 7.34 (a) Example of CS stage, (b) simplified circuit.

Solution We identify $M_{1}$ as a common-source device because it senses the input at its gate and generates the output at its drain. Transistors $M_{2}$ and $M_{3}$ therefore act as the load, with the former serving as a current source and the latter as a diode-connected device. Thus, $M_{2}$ can be replaced with a small-signal resistance equal to $r_{O 2}$, and $M_{3}$ with another equal to $\left(1 / g_{m 3}\right) \| r_{O 3}$. The circuit now reduces to that depicted in Fig. 7.34(b), yielding

$$
\begin{equation*}
A_{v}=-g_{m 1}\left(\frac{1}{g_{m 3}}\left\|r_{O 1}\right\| r_{O 2} \| r_{O 3}\right) \tag{7.153}
\end{equation*}
$$

and

$$
\begin{equation*}
R_{o u t}=\frac{1}{g_{m 3}}\left\|r_{O 1}\right\| r_{O 2} \| r_{O 3} \tag{7.154}
\end{equation*}
$$

Note that $1 / g_{m 3}$ is dominant in both expressions.

Exercise Repeat the above example if $M_{2}$ is converted to a diode-connected device.

Example Compute the voltage gain of the circuit shown in Fig. 7.35(a). Neglect channel-length 7.20 modulation in $M_{1}$.
image_name:Figure 7.35 (a)
description:
[
name: M3, type: PMOS, ports: {S: VDD, D: s1g3d3, G: s1g3d3}
name: M1, type: PMOS, ports: {S: s1g3d3, D: Vout, G: Vin}
name: M2, type: NMOS, ports: {S: GND, D: Vout, G: Vb}
]
extrainfo:The circuit is a common-source amplifier with M3 as a diode-connected PMOS, M1 as a PMOS, and M2 as an NMOS. The input is Vin, the output is Vout, and M2 is biased by Vb. M3 provides a load for M1.

(a)
image_name:Figure 7.35 (a)
description:
[
name: M1, type: PMOS, ports: {S: S1, D: Vout, G: Vin}
name: S1, type: VoltageSource, value: S1, ports: {Np: VDD, Nn: S1}
name: 1/gm3 || rO3, type: Resistor, value: 1/gm3 || rO3, ports: {N1: S1, N2: VDD}
name: rO2, type: Resistor, value: rO2, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit is a common-source amplifier with a PMOS transistor M1. The input is Vin, the output is Vout, and the load is provided by a combination of a voltage source S1 and a resistor 1/gm3 || rO3. The resistor rO2 connects the output to ground.

(b)

Figure 7.35 (a) Example of CS stage, (b) simplified circuit.

Solution Operating as a CS stage and degenerated by the diode-connected device $M_{3}$, transistor $M_{1}$ drives the current-source load, $M_{2}$. Simplifying the amplifier to that in Fig. 7.35(b), we have

$$
\begin{equation*}
A_{v}=-\frac{r_{O 2}}{\frac{1}{g_{m 1}}+\frac{1}{g_{m 3}} \| r_{O 3}} \tag{7.155}
\end{equation*}
$$

Exercise Repeat the above example if the gate of $M_{3}$ is tied to a constant voltage.

Example Determine the voltage gain of the amplifiers illustrated in Fig. 7.36. For simplicity, assume
7.21 $r_{O 1}=\infty$ in Fig. 7.36(b).
image_name:(a)
description:
[
name: M2, type: PMOS, ports: {S: VDD, D: Vout, G: Vin}
name: M1, type: NMOS, ports: {S: S1, D: Vout, G: Vb}
name: RS, type: Resistor, value: RS, ports: {N1: S1, N2: GND}
]
extrainfo:The circuit is a common-source amplifier stage with a PMOS load (M2) and an NMOS transistor (M1) with source degeneration by resistor RS. The input is applied at Vin, and the output is taken at Vout.

(a)
image_name:(a)
description:
[
name: M2, type: PMOS, ports: {S: VDD, D: Vout, G: Vb2}
name: M1, type: NMOS, ports: {S: S1, D: Vout, G: Vb1}
name: RS, type: Resistor, value: RS, ports: {N1: S1, N2: Vin}
]
extrainfo:The circuit is a common-source amplifier stage with a PMOS load (M2) and an NMOS transistor (M1) with source degeneration by resistor RS. The input is applied at Vin, and the output is taken at Vout.

(b)

Figure 7.36 Examples of (a) CS and (b) CG stages.

Solution Degenerated by $R_{S}$, transistor $M_{1}$ in Fig. 7.36(a) presents an impedance of $\left(1+g_{m 1} r_{O 1}\right) R_{S}+r_{O 1}$ to the drain of $M_{2}$. Thus the total impedance seen at the drain is equal to $\left[\left(1+g_{m 1} r_{O 1}\right) R_{S}+r_{O 1}\right] \| r_{O 2}$, giving a voltage gain of

$$
\begin{equation*}
A_{v}=-g_{m 2}\left\{\left[\left(1+g_{m 1} r_{O 1}\right) R_{S}+r_{O 1}\right] \| r_{O 1}\right\} \tag{7.156}
\end{equation*}
$$

In Fig. 7.36(b), $M_{1}$ operates as a common-gate stage and $M_{2}$ as the load, obtaining Eq. (7.109):

$$
\begin{equation*}
A_{v 2}=\frac{r_{O 2}}{\frac{1}{g_{m 1}}+R_{S}} \tag{7.157}
\end{equation*}
$$

Exercise Replace $R_{S}$ wit a diode-connected device and repeat the analysis.

Calculate the voltage gain of the circuit shown in Fig. 7.37(a) if $\lambda=0$.
image_name:(a)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: M1, type: NMOS, ports: {S: GND, D: s1s2, G: Vin}
name: M2, type: NMOS, ports: {S: s1s2, D: Vout, G: Vb}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout}
name: I1, type: CurrentSource, value: I1, ports: {Np: s1s2, Nn: GND}
]
extrainfo:The circuit is a composite stage with M1 operating as a source follower and M2 as a common-gate stage. The voltage gain of the circuit is given by the expression A_v = RD / (1/g_m1 + 1/g_m2). A current named I1 flows from the node labeled s1s2 to ground.
image_name:(b)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: M1, type: NMOS, ports: {S: GND, D: s1s2, G: Vin}
name: M2, type: NMOS, ports: {S: s1s2, D: Vout, G: Vb}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout}
name: I1, type: CurrentSource, value: I1, ports: {Np: s1s2, Nn: GND}
]
extrainfo:The circuit is a composite stage with M1 operating as a source follower and M2 as a common-gate stage. The node s1s2 is a shared source connection between M1 and M2, with M2 providing the load for M1.

Figure 7.37 (a) Example of a composite stage, (b) simplified circuit.

Solution In this circuit, $M_{1}$ operates as a source follower and $M_{2}$ as a CG stage (why?). A simple method of analyzing the circuit is to replace $v_{i n}$ and $M_{1}$ with a Thevenin equivalent. From Fig. 7.29(b), we derive the model depicted in Fig. 7.37(b). Thus,

$$
\begin{equation*}
A_{v}=\frac{R_{D}}{\frac{1}{g_{m 1}}+\frac{1}{g_{m 2}}} \tag{7.158}
\end{equation*}
$$

Exercise What happens if a resistance of value $R_{1}$ is placed in series with the drain of $M_{1}$ ?

Example The circuit of Fig. 7.38 produces two outputs. Calculate the voltage gain from the input 7.23 to $Y$ and to $X$. Assume $\lambda=0$ for $M_{1}$.
image_name:Figure 7.38
description:
[
name: M1, type: NMOS, ports: {S: X, D: Y, G: Vin}
name: M2, type: PMOS, ports: {S: VDD, D: X, G: GND}
name: M3, type: NMOS, ports: {S: Y, D: Vout2, G: VDD}
name: M4, type: PMOS, ports: {S: VDD, D: Y, G: Vb}
]
extrainfo:The circuit in Figure 7.38 is a composite stage with two outputs, Vout1 and Vout2. M1 and M2 form a source follower configuration, while M3 and M4 are connected to the output node Y. The circuit operates with VDD as the power supply and GND as the ground reference.

Figure 7.38 Example of composite stage.

Solution For $V_{\text {out } 1}$, the circuit serves as a source follower. The reader can show that if $r_{O 1}=\infty$, then $M_{3}$ and $M_{4}$ do not affect the source follower operation. Exhibiting a smallsignal impedance of $\left(1 / g_{m 2}\right) \| r_{O 2}$, transistor $M_{2}$ acts as a load for the follower, yielding from Eq. (7.131)

$$
\begin{equation*}
\frac{v_{\text {out } 1}}{v_{\text {in }}}=\frac{\frac{1}{g_{m 2}} \| r_{O 2}}{\frac{1}{g_{m 2}} \| r_{O 2}+\frac{1}{g_{m 1}}} \tag{7.159}
\end{equation*}
$$

For $V_{\text {out } 2}, M_{1}$ operates as a degenerated CS stage with a drain load consisting of the diode-connected device $M_{3}$ and the current source $M_{4}$. This load impedance is equal to $\left(1 / g_{m 3}\right)\left\|r_{O 3}\right\| r_{O 4}$, resulting in

$$
\begin{equation*}
\frac{v_{\text {out } 2}}{v_{i n}}=-\frac{\frac{1}{g_{m 3}}\left\|r_{O 3}\right\| r_{O 4}}{\frac{1}{g_{m 1}}+\frac{1}{g_{m 2}} \| r_{O 2}} \tag{7.160}
\end{equation*}
$$

Exercise Which one of the two gains is higher? Explain intuitively why.

## 7.6 CHAPTER SUMMARY

- The impedances seen looking into the gate, drain, and source of a MOSFET are equal to infinity, $r_{O}$ (with source grounded), and $1 / g_{m}$ (with gate grounded), respectively.
- In order to obtain the required small-signal MOS parameters such as $g_{m}$ and $r_{O}$, the transistor must be "biased," i.e., carry a certain drain current and sustain certain gate-source and drain-source voltages. Signals simply perturb these conditions.
- Biasing techniques establish the required gate voltage by means of a resistive path to the supply rails or the output node (self-biasing).
- With a single transistor, only three amplifier topologies are possible: common-source and common-gate stages and source followers.
- The CS stage provides a moderate voltage gain, a high input impedance, and a moderate output impedance.
- Source degeneration improves the linearity but lowers the voltage gain.
- Source degeneration raises the output impedance of CS stages considerably.
- The CG stage provides a moderate voltage gain, a low input impedance, and a moderate output impedance.
- The voltage gain expressions for CS and CG stages are similar but for a sign.
- The source follower provides a voltage gain less than unity, a high input impedance, and a low output impedance, serving as a good voltage buffer.
