# 4. Frequency Response of Electronic Circuits

Historically, electronic circuits were characterized by exciting them with an oscillator's output, and then with an oscilloscope determining how the circuit affected the magnitude and phase of its input signal. In general, this technique is only appropriate for linear circuits. However, it is also useful for non-linear circuits containing transistors when the signals are small enough that the transistors can be adequately characterized by their operating points and small linear changes about their operating points; that is, the nonlinear transistors can be accurately described using small-signal analysis. The use of this technique for characterizing electronic circuits has led to the application of frequency-domain techniques to the analysis of most any linear or weakly non-linear system, a technique that is now ubiquitous in system analysis.

## 4.1 FREQUENCY RESPONSE OF LINEAR SYSTEMS

Consider a linear time-invariant system with transfer function $\mathrm{H}(\mathrm{s})$ being excited by an input signal having Laplace transform $\mathrm{X}_{\text {in }}(\mathrm{s}) .{ }^{1}$ The Laplace transform of the output signal, $\mathrm{X}_{\text {out }}(\mathrm{s})$, is given by

In the time domain, assuming $\mathrm{x}_{\mathrm{in}}(\mathrm{t})$ is the inverse Laplace transform of $\mathrm{X}_{\mathrm{in}}(\mathrm{s})$, and $\mathrm{h}(\mathrm{t})$ is the inverse Laplace Transform of $\mathrm{H}(\mathrm{s})$ (often called its impulse response), we have

$$
\begin{equation*}
\mathrm{x}_{\mathrm{out}}(\mathrm{t})=\mathrm{x}_{\mathrm{in}}(\mathrm{t}) \cdot \mathrm{h}(\mathrm{t})=\int_{-\infty} \mathrm{x}_{\mathrm{in}}(\tau) \mathrm{h}(\mathrm{t}-\tau) \mathrm{d} \tau \tag{4.2}
\end{equation*}
$$

That is, the output signal is the convolution of the input signal with the impulse response of the system's transfer function.

The merit of frequency-domain analysis is that for particular inputs it is often easier to use (4.1) and the inverse Laplace Transform to calculate the expected output of a circuit rather than (4.2). Examples of this are when the inputs are pure sinusoids, or step inputs.

Only certain types of transfer functions arise in the ordinary course of analog circuit analysis. Since the inputs and outputs are generally voltages or currents in the circuit, $\mathrm{x}_{\mathrm{in}}$ and $\mathrm{x}_{\text {out }}$ are always real-valued. Hence, the impulse response $h(t)$ is also always real-valued. Furthermore, we will restrict our discussion to circuits comprising lumped elements: resistors, capacitors, independent and dependent voltage and current sources. ${ }^{2}$ The transfer

[^4]functions of such circuits may always be written in rational form with real-valued coefficients. That is, as a ratio of polynomials in the Laplace Transform variable, s.
\$\$

$$
\begin{equation*}
H(s)=\frac{a_{0}+a_{1} s+\ldots+a_{m} s^{m}}{1+b_{1} s+\ldots+b_{n} s^{n}} \tag{4.3}
\end{equation*}
$$

In (4.3), all of the coefficients $a_{i}$ and $b_{i}$ are real. Normally, $m \leq n$. When the transfer function is stable, all of the $b_{i}$ will be positive.

Transfer functions may also be written as a ratio of products of first-order terms,

$$
\begin{align*}
H(s) & =K \frac{\left(s+z_{1}\right)\left(s+z_{2}\right) \ldots\left(s+z_{m}\right)}{\left(s+\omega_{1}\right)\left(s+\omega_{2}\right) \ldots\left(s+\omega_{n}\right)} \\
& =a_{0} \frac{\left(1+\frac{s}{z_{1}}\right)\left(1+\frac{s}{z_{2}}\right) \ldots\left(1+\frac{s}{z_{m}}\right)}{\left(1+\frac{s}{\omega_{1}}\right)\left(1+\frac{s}{\omega_{2}}\right) \ldots\left(1+\frac{s}{\omega_{n}}\right)} \tag{4.4}
\end{align*}
$$

where $\mathrm{K}=\mathrm{a}_{\mathrm{m}} / \mathrm{b}_{\mathrm{n}}$. These are often referred to as root form since the roots of the numerator (zeros) and denominator (poles) are clearly visible. However, to be exact note that $\mathbf{z}_{i}$ and $\omega_{i}$ are not the actual roots of the numerator and denominator; rather they are equal to the negative roots. Hence, the transfer functions zeros are $-\mathbf{z}_{1},-\mathbf{z}_{2} \ldots$ and the poles are $-\omega_{1},-\omega_{2} \ldots$. It is also common to refer to the frequencies of the zeros and poles which are always positive quantities, $\left|\mathbf{z}_{1}\right|,\left|\mathbf{z}_{2}\right| \ldots$ and $\left|\omega_{1}\right|,\left|\omega_{2}\right| \ldots$, since these are physical frequencies of significance in describing the

Key Point: The transfer functions in analog circuits throughout this text:
a) are rational with $\mathrm{m} \leq \mathrm{n}$
b) have real-valued coefficients, $\mathrm{a}_{\mathrm{i}}$ and $\mathrm{b}_{\mathrm{i}}$ c) have poles and zeros that are either real or appear in complex-conjugate pairs Furthermore, if the system is stable, d) all denominator coefficients $b_{i}>0$ e) the real part of all poles will be negative
system's input-output behavior.

For transfer functions of systems with real-valued inputs and outputs, all zeros and poles will be either real or occur in complex-conjugate pairs. Further, the real parts of all the poles will be positive for stable transfer functions.

### 4.1.1 Magnitude and Phase Response

The output of an oscillator can often be characterized as a sinusoidal signal given by

$$
\begin{equation*}
x_{i n}(t)=A_{i n} \cos \left(\omega_{i n} t\right)=A_{i n} \frac{\left(e^{j \omega_{i n} t}+e^{-j \omega_{i n} t}\right)}{2} \tag{4.5}
\end{equation*}
$$

where Euler's relation has been used

$$
\begin{equation*}
e^{j x}=\cos (x)+j \sin (x) \tag{4.6}
\end{equation*}
$$

and

$$
\begin{equation*}
\mathrm{j}=\sqrt{-1} \tag{4.7}
\end{equation*}
$$

is a purely imaginary number of unit magnitude.
In the frequency domain, $\mathrm{X}_{\mathrm{in}}(\mathrm{s})$ consists of two impulses, one at

$$
\begin{equation*}
s=j \omega_{\text {in }} \tag{4.8}
\end{equation*}
$$

and one at

$$
\begin{equation*}
s=-j \omega_{\mathrm{in}} \tag{4.9}
\end{equation*}
$$

with each impulse having a magnitude $A_{i n} / 2$.
The output of a linear system having such an input also consists of two impulses in the frequency domain, but now each impulse will be multiplied by $\mathrm{H}(\mathrm{s})$ where $\mathrm{s}=\mathrm{j} \omega_{\text {in }}$ for the positive frequency impulse and $s=-\mathrm{j} \omega_{\text {in }}$ for the negative frequency impulse. After taking the inverse Laplace Transform of the output signal, it is seen that

$$
\begin{equation*}
x_{\text {out }}(t)=\frac{A_{\text {in }}}{2}\left(e^{j \omega_{\text {in }} t} H\left(j \omega_{\text {in }}\right)+e^{-j \omega_{\text {in }} t} H\left(-j \omega_{\text {in }}\right)\right) \tag{4.10}
\end{equation*}
$$

The transfer function evaluated on the imaginary axis, $\mathrm{H}\left(\mathrm{j} \omega_{\mathrm{in}}\right)$, is its frequency response which may written in terms of its magnitude response $\left|\mathrm{H}\left(\mathrm{j} \omega_{\text {in }}\right)\right|$ and phase response $\phi=\angle \mathrm{H}\left(\mathrm{j} \omega_{\text {in }}\right)$.

$$
\begin{equation*}
H\left(j \omega_{i n}\right)=\left|H\left(j \omega_{i n}\right)\right| e^{j \phi} \tag{4.11}
\end{equation*}
$$

Furthermore, for systems with real-valued inputs and outputs,

$$
\begin{equation*}
\mathrm{H}\left(-\mathrm{j} \omega_{\mathrm{in}}\right)=\left|\mathrm{H}\left(\mathrm{j} \omega_{\mathrm{in}}\right)\right| \mathrm{e}^{-\mathrm{j} \phi} \tag{4.12}
\end{equation*}
$$

Substituting (4.11) and (4.12) into (4.10) gives

$$
\begin{align*}
x_{\text {out }}(t) & =\frac{A_{\text {in }}}{2}\left|H\left(j \omega_{\text {in }}\right)\right|\left(e^{j \omega_{\text {in }}} e^{j \phi}+e^{-j \omega_{\text {in }} t} e^{-j \phi}\right) \\
& =\frac{A_{\text {in }}}{2}\left|H\left(j \omega_{\text {in }}\right)\right|\left(e^{j\left(\omega_{\text {in }} t+\phi\right)}+e^{-j\left(\omega_{\text {in }} t \phi\right)}\right)  \tag{4.13}\\
& =A_{\text {in }}\left|H\left(j \omega_{\text {in }}\right)\right| \cos \left(\omega_{\text {in }} t+\phi\right)
\end{align*}
$$

The development just presented has been given in terms of the Laplace transform variable s for the particular case where $s=j \omega_{i n}$. Alternatively, it is often presented in terms of Fourier Transforms which are equivalent to Laplace Transforms with $s=j \omega_{i n}$. However, when using Fourier Transforms, the j symbol denoting that the frequency is complex is usually omitted. For example, (4.11) would normally be written as

$$
\begin{equation*}
\mathrm{H}\left(\omega_{\mathrm{in}}\right)=\left|\mathrm{H}\left(\omega_{\mathrm{in}}\right)\right| \mathrm{e}^{\mathrm{j} \phi} \tag{4.14}
\end{equation*}
$$

where $\phi=\angle \mathrm{H}\left(\omega_{\text {in }}\right)$.

Key Point: When a linear circuit is excited with a sinusoid, the output will be a sinusoid at the same frequency. Its magnitude will equal to the input magnitude multiplied by the magnitude response $\left|\mathrm{H}\left(\omega_{\text {in }}\right)\right|$. The phase difference between the output and input sinusoids will equal the phase response $\angle \mathrm{H}\left(\omega_{\text {in }}\right)$. Magnitude responses are often expressed in units of decibels, $20 \log _{10}|\mathrm{H}(\omega)| \mathrm{dB}$.

The interpretation of (4.14) is as follows: When a linear electronic circuit is excited with the output of a sinusoidal oscillator, the output of the circuit will also be a sinusoid at the same frequency. The magnitude of the output sinusoid will be equal to the magnitude of the input sinusoid multiplied by $\left|H\left(\omega_{\mathrm{in}}\right)\right|$ where $H\left(\omega_{\mathrm{in}}\right)$ is the frequency response of the circuit. The phase difference between the output sinusoid and the input sinusoid will be equal to $\phi=\angle \mathrm{H}\left(\omega_{\mathrm{in}}\right)$.

Magnitude response is often expressed in units of decibels (dB),

$$
20 \log _{10}|\mathrm{H}(\omega)| \mathrm{dB}
$$

Decibels are a convenient unit since the magnitude response of two linear systems in series is the sum of the two magnitude responses when expressed in dB. Specifically, two systems with frequency responses $H_{1}(\omega)$ and $H_{2}(\omega)$ connected in series will have an overall frequency response $H_{1}(\omega) \cdot H_{2}(\omega)$. Expressed in decibels,

$$
20 \log _{10}\left(\left|\mathrm{H}_{1}(\omega)\right|\left|\mathrm{H}_{2}(\omega)\right|\right) \mathrm{dB}=20 \log _{10}\left|\mathrm{H}_{1}(\omega)\right| \mathrm{dB}+20 \log _{10}\left|\mathrm{H}_{2}(\omega)\right| \mathrm{dB}
$$

#### EXAMPLE 4.1

If the magnitude response of a linear system is doubled, how much does it increase in dB ? What if the magnitude response is increased by an order of magnitude?

#### Solution

If the magnitude response of the original system is $20 \log _{10}|H(\omega)| \mathrm{dB}$, once it is doubled it becomes

$$
\begin{aligned}
20 \log _{10}(2|\mathrm{H}(\omega)|) \mathrm{dB} & =20 \log _{10}|\mathrm{H}(\omega)| \mathrm{dB}+20 \log _{10} 2 \mathrm{~dB} \\
& =20 \log _{10} \mathrm{H}(\omega) \mid \mathrm{dB}+6.02 \mathrm{~dB} \\
& \cong 20 \log _{10} \mathrm{H}(\omega) \mid \mathrm{dB}+6 \mathrm{~dB}
\end{aligned}
$$

If increased by an order of magnitude, it becomes

$$
\begin{aligned}
20 \log _{10}(10|\mathrm{H}(\omega)|) \mathrm{dB} & =20 \log _{10}|\mathrm{H}(\omega)| \mathrm{dB}+20 \log _{10} 10 \mathrm{~dB} \\
& =20 \log _{10}|\mathrm{H}(\omega)| \mathrm{dB}+20 \mathrm{~dB}
\end{aligned}
$$

Hence, doubling a magnitude response implies an increase of 6 dB and increasing it by one order of magnitude implies an increase of 20 dB . In general, a change in $|H(\omega)|$ by a multiplicative factor $|A|$ can be expressed in decibels by adding $20 \log _{10}|\mathrm{~A}| \mathrm{dB}$.

### 4.1.2 First-Order Circuits

A first-order transfer function has a first order denominator, $\mathrm{n}=1$. For example,

$$
\begin{equation*}
\mathrm{H}(\mathrm{~s})=\frac{\mathrm{A}_{0}}{1+\frac{\mathrm{s}}{\omega_{0}}} \tag{4.15}
\end{equation*}
$$

is a first-order low-pass transfer function. It is the most-commonly encountered transfer function in electronic circuits. It arises naturally when a resistance and capacitance are combined. It is also often used as a simple model of more complex circuits, such as operational amplifiers; when used in this way, $\omega_{0}$ is referred to as a dominant pole and (4.15) is a dominant-pole approximation.

#### EXAMPLE 4.2

Consider a linear circuit having a transfer function given by (4.15), where $\mathrm{A}_{0}=10$ and $\omega_{0}=2 \pi \times 100 \mathrm{rad} . / \mathrm{s}$. Find the magnitude and phase of the output sinusoid assuming the input sinusoid has a peak voltage of 1 V and zero phase for the frequencies $10 \mathrm{~Hz}, 100 \mathrm{~Hz}$, and 1 kHz .

#### Solution

We can re-write (4.15) with $s=j \omega$ using Fourier Transforms as

$$
\begin{equation*}
H(\omega)=\frac{A_{0}}{1+j \frac{\omega}{\omega_{0}}}=\frac{A_{0}}{\sqrt{1+\left(\frac{\omega}{\omega_{0}}\right)^{2}}} e^{j \phi} \tag{4.16}
\end{equation*}
$$

where

$$
\begin{equation*}
\phi=-\tan ^{-1}\left(\frac{\omega}{\omega_{0}}\right) \tag{4.17}
\end{equation*}
$$

Note that

$$
\begin{equation*}
|H(\omega)|=\frac{A_{0}}{\sqrt{1+\left(\frac{\omega}{\omega_{0}}\right)^{2}}} \tag{4.18}
\end{equation*}
$$

Using (4.17) and (4.18), for the case $f=10 \mathrm{~Hz}$, where $\omega=2 \pi f=628.3 \mathrm{rad}$, we have

$$
\begin{equation*}
|H(\omega)|=\frac{10}{\sqrt{1+\left(\frac{2 \pi f}{2 \pi f_{0}}\right)^{2}}}=\frac{10}{\sqrt{1+\left(\frac{f}{f_{0}}\right)^{2}}}=\frac{10}{\sqrt{1+\left(\frac{10}{100}\right)^{2}}}=9.95=19.96 \mathrm{~dB} \tag{4.19}
\end{equation*}
$$

The phase shift is given by

$$
\begin{equation*}
\phi=-\tan ^{-1}\left(\frac{10}{100}\right)=-5.7^{\circ} \tag{4.20}
\end{equation*}
$$

The fact that the phase difference between the input and output is negative, implies the output sinusoid comes after the input sinusoid by $-5.7^{\circ}$, or in other words "lags" the input sinusoid. For $f_{i n}=100 \mathrm{~Hz}$, we have

$$
\begin{equation*}
|\mathrm{H}(\omega)|=\frac{10}{\sqrt{2}}=0.7071 \times 10=20 \mathrm{~dB}-3.01 \mathrm{~dB} \tag{4.21}
\end{equation*}
$$

and

$$
\begin{equation*}
\phi=-\tan ^{-1}(1)=-45^{\circ} \tag{4.22}
\end{equation*}
$$

Note that at $f_{i n}=f_{0}$ or equivalently, for $\omega_{i n}=\omega_{0}$, the magnitude response is 3 dB below its low-frequency value, and the phase is delayed by $-45^{\circ}$. Finally, for $f_{i n}=1 \mathrm{kHz}$, we have

$$
\begin{equation*}
\mathrm{H}(\omega) \left\lvert\,=\frac{10}{\sqrt{1+\left(\frac{\mathrm{f}}{\mathrm{f}_{0}}\right)^{2}}}=\frac{10}{\sqrt{1+\left(\frac{1000}{100}\right)^{2}}}=\frac{10}{10.05}=20 \mathrm{~dB}-20.04 \mathrm{~dB}=-0.04 \mathrm{~dB}\right. \tag{4.23}
\end{equation*}
$$

and

$$
\begin{equation*}
\phi=-\tan ^{-1}\left(\frac{1000}{10}\right)=-1.47 \mathrm{rad}=-84^{\circ} \tag{4.24}
\end{equation*}
$$

Thus, the gain is approximately 20 dB less than its low-frequency value and the phase shift is approaching $-90^{\circ}$.

#### Step Response of First-Order Circuits

Another common means of characterizing linear circuits is to excite them with step inputs. This would normally be done in practice by exciting them with a square wave having a low-enough frequency (or equivalently longenough period), so the circuit settles between edges, and therefore each edge effectively excites the circuit similar to a step input.

Consider a step input $\mathrm{x}_{\mathrm{in}}(\mathrm{t})=\mathrm{A}_{\mathrm{in}} \mathrm{u}(\mathrm{t})$ where $\mathrm{u}(\mathrm{t})$, the step-input function, is defined as

$$
\mathrm{u}(\mathrm{t})= \begin{cases}0, & \mathrm{t} \leq 0  \tag{4.25}\\ 1, & \mathrm{t}>0\end{cases}
$$

The step function $u(t)$ has a Laplace transform given by

$$
\begin{equation*}
U(s)=\frac{1}{s} \tag{4.26}
\end{equation*}
$$

Therefore, the Laplace transform of the output of a linear system having transfer function $\mathrm{H}(\mathrm{s})$ and a step input is given by

$$
\begin{equation*}
X_{\text {out }}(\mathrm{s})=A_{\text {in }} \frac{H(s)}{s} \tag{4.27}
\end{equation*}
$$

This is normally easy to calculate especially since any rational $\mathrm{H}(\mathrm{s})$ may be expressed as a sum of first-order terms using residues [James, 2004].

Consider the special case were a first-order low-pass filter has a transfer function given by

$$
\begin{equation*}
\mathrm{H}(\mathrm{~s})=\frac{\mathrm{A}_{0}}{1+\frac{\mathrm{s}}{\omega_{0}}} \tag{4.28}
\end{equation*}
$$

Using (4.27), we have

$$
\begin{equation*}
X_{\text {out }}(s)=\frac{A_{\text {in }}}{s} \frac{A_{0}}{1+\frac{s}{\omega_{0}}} \tag{4.29}
\end{equation*}
$$

Equation (4.29) can be rewritten in terms of its residues as

$$
\begin{equation*}
X_{\text {out }}(\mathrm{s})=\mathrm{A}_{\text {in }} \mathrm{A}_{0}\left[\frac{1}{\mathrm{~s}}-\frac{1}{\mathrm{~s}+\omega_{0}}\right] \tag{4.30}
\end{equation*}
$$

It is now simple to take the Inverse Laplace Transform to get

$$
\begin{equation*}
\mathrm{x}_{\text {out }}(\mathrm{t})=\mathrm{u}(\mathrm{t}) \mathrm{A}_{\text {in }} \mathrm{A}_{0}\left[1-\mathrm{e}^{-\mathrm{t} / \mathrm{t}}\right] \tag{4.31}
\end{equation*}
$$

where $\tau=1 / \omega_{0}$.

In a similar manner it is straight-forward to show that a general first-order circuit having a transfer function given by

$$
\begin{equation*}
H(s)=A_{0}\left(\frac{1+\frac{s}{\omega_{z}}}{1+\frac{s}{\omega_{0}}}\right) \tag{4.32}
\end{equation*}
$$

and subjected to a step input has an output with Laplace transform

$$
\begin{equation*}
X_{\text {out }}(s)=\frac{A_{\text {in }} A_{0}}{s}\left(\frac{1+\frac{s}{\omega_{z}}}{1+\frac{s}{\omega_{0}}}\right) \tag{4.33}
\end{equation*}
$$

Hence, the system's step response is

$$
\begin{equation*}
\mathrm{x}_{\text {out }}(\mathrm{t})=\mathrm{u}(\mathrm{t}) \mathrm{A}_{\text {in }} \mathrm{A}_{0}\left[1-\left(1-\frac{\omega_{0}}{\omega_{z}}\right) \mathrm{e}^{-\mathrm{t} / \mathrm{t}}\right] \tag{4.34}
\end{equation*}
$$

where $\tau=1 / \omega_{0}$
Note that the step response for $t$ very slightly greater than 0 is denoted by $\mathrm{x}_{\text {out }}\left(0^{+}\right)$and using (4.34) is easily found to be given by

$$
\begin{equation*}
\mathrm{x}_{\text {out }}\left(0^{+}\right)=\mathrm{A}_{\text {in }} \mathrm{A}_{0} \frac{\omega_{0}}{\omega_{z}} \tag{4.35}
\end{equation*}
$$

This is easily verified using the Laplace transform property

$$
\begin{equation*}
x_{\text {out }}\left(0^{+}\right)=\lim _{s \rightarrow \infty} s X_{\text {out }}(s)=\lim _{s \rightarrow \infty} H(s) A_{\text {in }}=A_{\text {in }} A_{0} \frac{\omega_{0}}{\omega_{z}} \tag{4.36}
\end{equation*}
$$

together with equation (4.33). In a similar manner, it is easily found that after a long time, when the first-order circuit has settled, its response denoted $\mathrm{x}_{\text {out }}(\infty)$ is given by

$$
\begin{equation*}
\mathrm{x}_{\text {out }}(\infty)=\mathrm{A}_{\text {in }} \mathrm{A}_{0} \tag{4.37}
\end{equation*}
$$

Once again, this can be verified using the Laplace Transform property

$$
\begin{equation*}
\mathrm{X}_{\text {out }}(\infty)=\lim _{\mathrm{s} \rightarrow 0} \mathrm{~s} \mathrm{X}_{\text {out }}(\mathrm{s})=\lim _{\mathrm{s} \rightarrow 0} \mathrm{H}(\mathrm{~s}) \mathrm{A}_{\text {in }} \tag{4.38}
\end{equation*}
$$

together with (4.33). Using (4.34), (4.35) and (4.38), one can derive the general equation giving the step response of any first-order circuit as

$$
\begin{equation*}
x(t)=x(\infty)-\left[x(\infty)-x\left(0^{+}\right)\right] e^{-t / \tau} \tag{4.39}
\end{equation*}
$$

#### EXAMPLE 4.3

Consider the first-order lowpass circuit shown in Fig. 4.1. Assume $R=1 \mathrm{k} \Omega$ and $C=1 \mathrm{nF}$. Find the -3 dB frequency of the circuit and the time constant of the circuit. Assuming the input signal is a $0.5-\mathrm{V}$ step input at time 0 , what is the output voltage at $1.5 \mu \mathrm{~s}$ ? How long does it take for the circuit to settle within $70 \%$ of its final value?

#### Solution

The transfer function of this circuit is easily found using the admittance divider formula; that is

$$
\begin{equation*}
H(s)=\frac{V_{\text {out }}(s)}{V_{\text {in }}(s)}=\frac{G_{1}(s)}{G_{1}(s)+G_{2}(s)} \tag{4.40}
\end{equation*}
$$

where $\mathrm{G}_{1}(\mathrm{~s})$ is the interconnecting admittance between the input and output and the denominator is the sum of all admittances connected to the output node (in this case $G_{1}(s)+G_{2}(s)$ ). For this case, we have $G_{1}(s)=1 / R$ and $\mathrm{G}_{2}(\mathrm{~s})=\mathrm{sC}$ and therefore

$$
\begin{equation*}
H(s)=\frac{1 / R}{s C+1 / R}=\frac{1}{1+s R C} \tag{4.41}
\end{equation*}
$$

The -3 dB frequency in radians per second is given by

$$
\begin{equation*}
\omega_{0}=\frac{1}{\mathrm{RC}}=\frac{1}{1 \times 10^{3} 1 \times 10^{-9}}=1 \times 10^{6} \mathrm{rad} / \mathrm{sec} \tag{4.42}
\end{equation*}
$$

In Hz , the -3 dB frequency is given by

$$
\begin{equation*}
\mathrm{f}_{-3 \mathrm{~dB}}=\frac{1}{2 \pi} \frac{1}{\mathrm{RC}} \cong 159 \mathrm{kHz} \tag{4.43}
\end{equation*}
$$

The circuit time constant is given by

$$
\begin{equation*}
\tau=\frac{1}{\omega_{0}}=R C=1 \mu \mathrm{~s} \tag{4.44}
\end{equation*}
$$

Next, using (4.31), we have the output voltage at $1.5 \mu \mathrm{~s}$ given by

$$
\begin{equation*}
\mathrm{x}_{\text {out }}(\mathrm{t})=0.5\left[1-\mathrm{e}^{-1.5 \times 10^{-6} / 1 \times 10^{-6}}\right]=0.5\left[1-\mathrm{e}^{-1.5}\right]=0.39 \mathrm{~V} \tag{4.45}
\end{equation*}
$$

For the circuit to settle within $70 \%$ of its final value, we need

$$
\begin{equation*}
1-\mathrm{e}^{-\mathrm{t} / \tau}=0.7 \tag{4.46}
\end{equation*}
$$

image_name:Fig. 4.1 A RC first-order lowpass circuit
description:
[
name: Vin, type: VoltageSource, ports: {Np: Vin, Nn: GND}
name: R, type: Resistor, value: R, ports: {N1: Vin, N2: Vout}
name: C, type: Capacitor, value: C, ports: {Np: Vout, Nn: GND}
]
extrainfo:This is a first-order RC lowpass filter circuit with an input voltage source Vin, a resistor R, and a capacitor C. The output voltage is taken across the capacitor.

Fig. 4.1 A RC first-order lowpass circuit.
which implies

$$
\begin{equation*}
\mathrm{t}=\tau \ln \left(\frac{1}{1-0.7}\right)=1.2 \tau=1.2 \mu \mathrm{~s} \tag{4.47}
\end{equation*}
$$

#### EXAMPLE 4.4

Consider the first-order circuit shown in Fig. 4.2. Find equations for the transfer function and for the stepresponse. What constraint is necessary and sufficient for the step-response to be an ideal step? For the special case of $\mathrm{C}_{1}=5 \mathrm{pF}, \mathrm{C}_{2}=10 \mathrm{pF}, \mathrm{R}_{1}=2 \mathrm{k} \Omega$, and $\mathrm{R}_{2}=10 \mathrm{k} \Omega$, plot the step response assuming the input signal is a 2 V step.

#### Solution

The transfer function can once again be found using the admittance-divider formula. We have

$$
\begin{align*}
H(s) & =\frac{V_{\text {out }}(s)}{V_{\text {in }}(s)}=\frac{s C_{1}+1 / R_{1}}{s C_{1}+1 / R_{1}+s C_{2}+1 / R_{2}} \\
& =\left(\frac{R_{2}}{R_{1}+R_{2}}\right)\left[\frac{1+s R_{1} C_{1}}{1+s \frac{\left(R_{1} R_{2}\right)}{\left(R_{1}+R_{2}\right)}\left(C_{1}+C_{2}\right)}\right] \tag{4.48}
\end{align*}
$$

Equation (4.48) can be re-written in the same form as (4.32) with the substitutions

$$
\begin{gather*}
A_{0}=\frac{R_{2}}{R_{1}+R_{2}}  \tag{4.49}\\
\tau_{z}=\omega_{z}^{-1}=R_{1} C_{1} \tag{4.50}
\end{gather*}
$$

and

$$
\begin{equation*}
\tau_{0}=\omega_{0}^{-1}=\frac{\left(\mathrm{R}_{1} \mathrm{R}_{2}\right)}{\left(\mathrm{R}_{1}+\mathrm{R}_{2}\right)}\left(\mathrm{C}_{1}+\mathrm{C}_{2}\right)=\left(\mathrm{R}_{1} \| \mathrm{R}_{2}\right)\left(\mathrm{C}_{1}+\mathrm{C}_{2}\right) \tag{4.51}
\end{equation*}
$$

Fig. 4.2 A RC first-order circuit.
image_name:Fig. 4.2 A RC first-order circuit
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: Vin, N2: Vout}
name: C1, type: Capacitor, value: C1, ports: {Np: Vin, Nn: Vout}
name: R2, type: Resistor, value: R2, ports: {N1: Vout, N2: GND}
name: C2, type: Capacitor, value: C2, ports: {Np: Vout, Nn: GND}
]
extrainfo:This is an RC first-order circuit with a high-pass filter configuration. The input voltage is applied at Vin and the output is taken at Vout. The circuit consists of resistors R1 and R2, and capacitors C1 and C2. The ground node is connected to the lower terminal of R2 and C2.

In order for the step response (given by (4.34)) to be an ideal step, we need $\omega_{z}=\omega_{0}$. Using (4.50) and (4.51), we see the necessary conditions are

$$
\begin{equation*}
\mathrm{R}_{1} \mathrm{C}_{1}=\left(\mathrm{R}_{1} \| \mathrm{R}_{2}\right)\left(\mathrm{C}_{1}+\mathrm{C}_{2}\right) \tag{4.52}
\end{equation*}
$$

which implies

$$
\begin{equation*}
\frac{\mathrm{C}_{2}}{\mathrm{C}_{1}}=\frac{\mathrm{R}_{1}}{\mathrm{R}_{2}} \tag{4.53}
\end{equation*}
$$

For the case, of $\mathrm{C}_{1}=5 \mathrm{pF}, \mathrm{C}_{2}=10 \mathrm{pF}, \mathrm{R}_{1}=2 \mathrm{k} \Omega$, and $\mathrm{R}_{2}=10 \mathrm{k} \Omega$, we have $\mathrm{A}_{0}=0.833$, $\omega_{z}=1 \times 10^{8} \mathrm{rad}$, and $\omega_{0}=4 \times 10^{7} \mathrm{rad}$. Using (4.36) and (4.48), we see

$$
\begin{equation*}
\mathrm{x}_{\mathrm{out}}\left(0^{+}\right)=\mathrm{A}_{\mathrm{in}} \lim _{s \rightarrow \infty} \mathrm{H}(\mathrm{~s})=\mathrm{A}_{\mathrm{in}} \frac{\mathrm{C}_{1}}{\mathrm{C}_{1}+\mathrm{C}_{2}}=2\left(\frac{5 \mathrm{pF}}{5 \mathrm{pF}+10 \mathrm{pF}}\right)=0.67 \mathrm{~V} \tag{4.54}
\end{equation*}
$$

and

$$
\begin{equation*}
\mathrm{x}_{\mathrm{out}}(\infty)=\mathrm{A}_{\mathrm{in}} \lim _{\mathrm{s} \rightarrow 0} \mathrm{H}(\mathrm{~s})=\mathrm{A}_{\mathrm{in}} \frac{\mathrm{R}_{2}}{\mathrm{R}_{1}+\mathrm{R}_{2}}=2\left(\frac{10 \mathrm{k} \Omega}{2 \mathrm{k} \Omega+10 \mathrm{k} \Omega}\right)=1.67 \mathrm{~V} \tag{4.55}
\end{equation*}
$$

The circuit time constant is $1 / \omega_{0}=25 \mathrm{~ns}$. Using these values, it is possible to sketch the step response as shown in Fig. 4.3. In one time constant, the output voltage has settled to within $22 \%$ of its total change (i.e. $\left.\mathrm{x}_{\text {out }}(\infty)-\left(\mathrm{x}_{\text {out }}(\infty)-\mathrm{x}_{\text {out }}\left(0^{+}\right)\right) \mathrm{e}^{-1}=1.67 \mathrm{~V}-1 \mathrm{~V} \cdot \mathrm{e}^{-1}=1.30 \mathrm{~V}\right)$.

#### EXAMPLE 4.5

Consider an amplifier having a small signal transfer function that approximately is given by

$$
\begin{equation*}
\mathrm{A}(\mathrm{~s})=\frac{\mathrm{A}_{0}}{1+\frac{\mathrm{s}}{\omega_{-\mathrm{diB}}}} \tag{4.56}
\end{equation*}
$$

image_name:Fig. 4.3 The 2-V step-response of the circuit of Fig. 4.2
description:The graph depicted is a time-domain waveform representing the step-response of a circuit, specifically labeled as Fig. 4.3. The x-axis is time, denoted as 't', measured in nanoseconds (ns), while the y-axis represents the output voltage, \( x_{out}(t) \), measured in volts (V).

**Axes Labels and Units:**
- **X-axis:** Time \( (t) \), in nanoseconds (ns).
- **Y-axis:** Output voltage \( x_{out}(t) \), in volts (V).

**Overall Behavior and Trends:**
The graph illustrates a step-response starting at approximately 0.67 V. The voltage rises sharply, indicating a rapid response to a step input, and then gradually approaches a steady-state value. The curve initially rises steeply and then transitions into a more gradual slope before leveling off.

**Key Features and Technical Details:**
- **Initial Voltage:** Approximately 0.67 V.
- **Intermediate Voltage:** At around 25 ns, the voltage reaches approximately 1.30 V.
- **Final Steady-State Voltage:** The output stabilizes at 1.67 V.
- **Response Time:** The significant change in voltage occurs within the first 25 ns, after which the output stabilizes.

**Annotations and Specific Data Points:**
- The graph includes horizontal dashed lines at 0.67 V and 1.30 V, indicating key voltage levels during the step-response.
- A vertical dashed line marks the time at 25 ns, highlighting the time it takes for the voltage to reach the intermediate level before stabilizing.

This graph provides a clear visualization of how the circuit responds to a 2-V step input, showing the transition from initial to final voltage levels and the time dynamics involved in this process.

Fig. 4.3 The 2-V step-response of the circuit of Fig. 4.2.

What is the approximate unity-gain frequency and the phase shift at the unity-gain frequency for $\mathrm{A}_{0}=1 \times 10^{5}$ and $\omega_{-3 \mathrm{~dB}}=1 \times 10^{3}$ ?

#### Solution

At frequencies $s=j \omega » j \omega_{-3 d B}$, which is the case for most signal frequencies, the $s$ term in the denominator dominates and we have

$$
\begin{equation*}
A(s) \cong \frac{A_{0} \omega_{-3 d B}}{s} \tag{4.57}
\end{equation*}
$$

and the open-loop transfer function of the amplifier is very similar to that of an ideal integrator. The magnitude of the Fourier Transform is found by substituting $s=j \omega$ and taking the magnitude. To find the unity gain frequency, this magnitude should be set to unity and then $\omega$ (often called $\omega_{\text {ta }}$ ) should be solved for. We have

$$
\begin{equation*}
\left|\frac{\mathrm{A}_{0} \omega_{-3 \mathrm{~dB}}}{\omega_{\mathrm{ta}}}\right|=1 \tag{4.58}
\end{equation*}
$$

Key Point: For a firstorder lowpass transfer function with dc gain $\mathrm{A}_{0}>>1$, the unity gain frequency is $\omega_{\mathrm{ta}} \approx \mathrm{A}_{0} \omega_{-3 \mathrm{~dB}}$ and $\angle \mathrm{A}\left(\omega_{\mathrm{ta}}\right) \approx 90^{\circ}$.
which implies

$$
\begin{equation*}
\omega_{\mathrm{ta}} \cong \mathrm{~A}_{0} \omega_{-3 \mathrm{~dB}} \tag{4.59}
\end{equation*}
$$

The phase shift of the transfer function is given by

$$
\begin{equation*}
\angle \mathrm{A}(\omega)=-\tan \left(\frac{\omega}{\omega_{-3 \mathrm{AB}}}\right)^{-1} \tag{4.60}
\end{equation*}
$$

Noting that since $A_{0}$ » 1 , we have $\omega / \omega_{-3 \mathrm{~dB}}$ » 1 , and therefore

$$
\begin{equation*}
\angle \mathrm{A}\left(\omega_{\mathrm{ta}}\right) \cong-90^{\circ} \tag{4.61}
\end{equation*}
$$

For this example, using (4.59) and (4.61), we have $\omega_{\mathrm{ta}} \cong 1 \times 10^{8}$ rad.

### 4.1.3 Second-Order Low-Pass Transfer Functions with Real Poles

Second-order low-pass transfer functions are often encountered when characterizing electronic circuits. For example, operational amplifiers with feedback, and perhaps being inadequately compensated, are often modelled as second-order low-pass functions. Three alternative formulations for second-order low-pass transfer functions (assuming a real numerator) are

$$
\begin{align*}
H(s) & =\frac{K}{\left(1+s \tau_{1}\right)\left(1+s \tau_{2}\right)} \\
& =\frac{K}{\left(1+\frac{s}{\omega_{\mathrm{p} 1}}\right)\left(1+\frac{s}{\omega_{\mathrm{p} 2}}\right)}  \tag{4.62}\\
& =\frac{\mathrm{K} \omega_{\mathrm{p} 1} \omega_{\mathrm{p} 2}}{\left(\mathrm{~s}+\omega_{\mathrm{p} 1}\right)\left(\mathrm{s}+\omega_{\mathrm{p} 2}\right)}
\end{align*}
$$

The coefficients $\tau_{1}, \tau_{2}$ or $\omega_{\mathrm{p} 1}, \omega_{\mathrm{p} 2}$ are either real and positive, or occur in complex-conjugate pairs. The transfer function may also be written in the form

$$
\begin{equation*}
H(s)=\frac{K \omega_{p 1} \omega_{p 2}}{\omega_{p 1} \omega_{p 2}+s\left(\omega_{p 1}+\omega_{p 2}\right)+s^{2}} \tag{4.63}
\end{equation*}
$$

Equation (4.63) may be written in the alternative (and popular) form

$$
\begin{equation*}
H(s)=\frac{K \omega_{0}^{2}}{\omega_{0}^{2}+s \frac{\omega_{0}}{Q}+s^{2}} \tag{4.64}
\end{equation*}
$$

Here, parameter $\omega_{0}$ is called the resonant frequency, parameter Q is called the Q -factor ${ }^{3}$ [Sedra, 2009], and K is the dc gain of the transfer function. This latter form (4.64) is often preferred by experienced designers because it has no complex-valued coefficients, even in cases where the poles $-\omega_{\mathrm{p} 1}$ and $-\omega_{\mathrm{p} 2}$ are a complex-conjugate pair.

We will for now consider only the special case where $\omega_{\mathrm{p} 1}<\omega_{\mathrm{p} 2}$ are both real and distinct. We can set the denominator of (4.64), $D(s)$, equal to the denominator of (4.62), and we have

$$
\begin{align*}
D(s) & =\omega_{0}^{2}+s \frac{\omega_{0}}{Q}+s^{2} \\
& =\left(\omega_{\mathrm{p} 1}+\mathrm{s}\right)\left(\omega_{\mathrm{p} 2}+\mathrm{s}\right)  \tag{4.65}\\
& =\omega_{\mathrm{p} 1} \omega_{\mathrm{p} 2}+\mathrm{s}\left(\omega_{\mathrm{p} 1}+\omega_{\mathrm{p} 2}\right)+\mathrm{s}^{2}
\end{align*}
$$

Equating the coefficients yields

$$
\begin{equation*}
\omega_{0}^{2}=\omega_{p 1} \omega_{p 2} \tag{4.66}
\end{equation*}
$$

and

$$
\begin{equation*}
\frac{\omega_{0}}{Q}=\omega_{p 1}+\omega_{p 2} \tag{4.67}
\end{equation*}
$$

Solving (4.66) and (4.67), we get

$$
\begin{equation*}
\omega_{\mathrm{p} 1}, \omega_{\mathrm{p} 2}=\frac{\omega_{0}}{2 \mathrm{Q}}\left(1 \pm \sqrt{1-4 \mathrm{Q}^{2}}\right) \tag{4.68}
\end{equation*}
$$

We can also express the frequency response of (4.62) as

$$
\begin{equation*}
H(s)=\frac{K}{\sqrt{1+\left(\frac{\omega}{\omega_{\mathrm{p} 1}}\right)^{2}} \sqrt{1+\left(\frac{\omega}{\omega_{\mathrm{p} 2}}\right)^{2}}} \mathrm{e}^{\mathrm{j} \phi} \tag{4.69}
\end{equation*}
$$

where

$$
\begin{equation*}
\phi=-\tan ^{-1}\left(\frac{\omega}{\omega_{\mathrm{p} 1}}\right)-\tan \left(\frac{\omega}{\omega_{\mathrm{p} 2}}\right) \tag{4.70}
\end{equation*}
$$

This form clearly shows $|H(\omega)|$ and $\angle H(\omega)$.
3. The Q -factor is $1 / 2$ times the inverse of the damping-factor. The damping-factor is an alternative method of indicating the pole locations in second-order transfer-functions.

#### Widely-Spaced Real Poles

For the special case of real poles $\omega_{\mathrm{p} 1} \ll \omega_{\mathrm{p} 2}$, we have Q « 1 , and we can make the approximation

$$
\begin{equation*}
\sqrt{1-4 Q^{2}} \cong 1-2 Q^{2} \tag{4.71}
\end{equation*}
$$

Using (4.71) and (4.68) gives

$$
\begin{align*}
\omega_{\mathrm{p} 1} & \cong \omega_{0} \mathrm{Q}  \tag{4.72}\\
\omega_{\mathrm{p} 2} & \cong \frac{\omega_{0}}{\mathrm{Q}} \tag{4.73}
\end{align*}
$$

Using (4.69) and (4.70), it is possible to simply approximate the magnitude and phase response of low-pass transfer functions in a number of different frequency regions. For $\omega$ « $\omega_{p}$, we have $|H(\omega)|=K$. At $\omega=\omega_{p}$, we have $H\left(\omega_{p 1}\right)=K / \sqrt{2}$, and $\angle H(\omega)=-45^{\circ}$. Next, for $\omega_{p 1} \ll \omega \ll \omega_{p 2}$, we have

$$
\begin{equation*}
|H(\omega)| \cong \frac{K \omega_{p 1}}{\omega} \tag{4.74}
\end{equation*}
$$

If we express the magnitude response in terms of decibels ( dB ),

$$
\begin{equation*}
|H(\omega)|_{\mathrm{dB}} \cong 20 \log \left(K \omega_{\mathrm{p} 1}\right)-20 \log (\omega) \tag{4.75}
\end{equation*}
$$

Thus, the magnitude response is decreasing -20 dB for every decade increase in $\omega$. In addition, in this region, we have $\angle H(\omega) \cong-90^{\circ}$. Next, at $\omega=\omega_{\mathrm{p} 2}$, we have

$$
\begin{equation*}
\left|H\left(\omega_{\mathrm{p} 2}\right)\right| \cong \frac{\mathrm{K} \omega_{\mathrm{p} 1}}{\sqrt{2} \omega_{\mathrm{p} 2}} \tag{4.76}
\end{equation*}
$$

and $\angle \mathrm{H}(\omega)=-135^{\circ}$. The final region is when $\omega_{\mathrm{p} 2} \ll \omega$. In this region, we have

$$
\begin{equation*}
|H(\omega)| \cong \frac{K \omega_{p 1} \omega_{p 2}}{\omega^{2}} \tag{4.77}
\end{equation*}
$$

Expressing the magnitude gain in dB , we have

$$
\begin{equation*}
|H(\omega)|_{\mathrm{dB}} \cong 20 \log \left(K \omega_{\mathrm{p} 1} \omega_{\mathrm{p} 2}\right)-40 \log (\omega) \tag{4.78}
\end{equation*}
$$

and we see the gain is decreasing -40 dB for every decade increase in $\omega$. In this region, we also have $\angle \mathrm{H}(\omega) \cong-180^{\circ}$.

#### Step Response

The step response for a second-order low-pass transfer function can be found by expanding (4.62) into partial fractions (or residues). It is not too difficult to show that

$$
\begin{equation*}
\mathrm{H}(\mathrm{~s})=\mathrm{K}\left[\frac{\omega_{\mathrm{p} 2}}{\omega_{\mathrm{p} 2}-\omega_{\mathrm{p} 1}} \frac{\omega_{\mathrm{p} 1}}{s+\omega_{\mathrm{p} 1}}-\frac{\omega_{\mathrm{p} 1}}{\omega_{\mathrm{p} 2}-\omega_{\mathrm{p} 1}} \frac{\omega_{\mathrm{p} 2}}{s+\omega_{\mathrm{p} 2}}\right] \tag{4.79}
\end{equation*}
$$

Equivalently, in terms of time constants $\tau_{1}=1 / \omega_{\mathrm{p} 1}$ and $\tau_{2}=1 / \omega_{\mathrm{p} 2}$

$$
\begin{equation*}
\mathrm{H}(\mathrm{~s})=\mathrm{K}\left[\frac{\tau_{1}}{\tau_{1}-\tau_{2}} \frac{1}{1+\mathrm{s} \tau_{1}}-\frac{\tau_{2}}{\tau_{1}-\tau_{2}} \frac{1}{1+\mathrm{s} \tau_{2}}\right] \tag{4.80}
\end{equation*}
$$

It is now straightforward to express the step response of the second-order system as the sum of the individual step responses of two first-order systems. We have

$$
\begin{equation*}
x_{o u t}(t)=A_{i n} \frac{K \omega_{p 2}}{\omega_{\mathrm{p} 2}-\omega_{p 1}}\left[1-e^{-t \omega_{\mathrm{p}}}\right]-A_{i n} \frac{K \omega_{\mathrm{p} 1}}{\omega_{\mathrm{p} 2}-\omega_{\mathrm{p} 1}}\left[1-\mathrm{e}^{-\mathrm{t} \omega_{\mathrm{p} 2}}\right] \tag{4.81}
\end{equation*}
$$

and we see the step response is composed of two first-order modes.
For the case of widely-spaced real poles $\omega_{\mathrm{p} 1}$ « $\omega_{\mathrm{p} 2}$, we see that the second term in (4.81) settles much more quickly then the first. Hence, for $t$ » $1 / \omega_{p 2}$,

$$
\begin{equation*}
x_{\text {out }}(t) \cong A_{i n} \frac{K \omega_{p 2}}{\omega_{p 2}-\omega_{p 1}}\left[1-e^{-t \omega_{p 1}}\right]-A_{i n} \frac{K \omega_{p 1}}{\omega_{p 2}-\omega_{p 1}} \cong A_{i n} K\left[1-e^{-t \omega_{p 1}}\right] \tag{4.82}
\end{equation*}
$$

The system exhibits a first-order step response with the slower time constant, $1 / \omega_{\mathrm{p} 1}$.

### 4.1.4 Bode Plots

The observations made in Section 4.1.3 are the basis of a methodology useful for constructing approximate plots of the magnitude response (in dB ) and phase response (in degrees) versus log frequency. These plots are called Bode Plots; they are used extensively to graphically represent a circuit's frequency response and for the analysis of feedback systems.

The method for Bode plots of stable low-pass transfer functions having only real poles (i.e. where the order of the numerator $m=0$, hence $N(s)=K$ ) is summarized by the following rules:
a. At very low frequencies both the magnitude and phase plots are constant (horizontal lines) at $20 \log _{10}|\mathrm{H}(0)| \mathrm{dB}$ and $0^{\circ}$ respectively.
b. As the frequency becomes larger than a pole frequency, the slope of the magnitude response changes by $-20 \mathrm{~dB} /$ decade.
c. Each pole contributes an additional $-45^{\circ}$ phase shift at the frequency of the pole. At frequencies substantially higher than a pole frequency, it contributes an additional $-90^{\circ}$.

Key Point: Transfer functions with only real-valued poles and numerator order zero have monotonically decreasing magnitude and phase response plots with each pole contributing an additional -20 dB/decade slope in the magnitude response, and an additional $-90^{\circ}$ phase shift.

#### EXAMPLE 4.6

Sketch a bode plot for a second-order low-pass transfer function (4.62) with $\mathrm{K}=1 \times 10^{4}$, $\omega_{\mathrm{p} 1}=10 \mathrm{rad} / \mathrm{s}$, and $\omega_{\mathrm{p} 2}=1000 \mathrm{rad} / \mathrm{s}$.

#### Solution

The transfer function is

$$
H(s)=\frac{1 \times 10^{4}}{\left(1+\frac{s}{10}\right)\left(1+\frac{s}{1000}\right)}
$$

Following the procedure, the magnitude response is constant for low frequencies at a value of $20 \log _{10}|\mathrm{H}(0)|=20 \log _{10} 10^{4}=80 \mathrm{~dB}$ (step a). The slope then decreases to $-20 \mathrm{~dB} /$ decade at $\omega_{\mathrm{p} 1}=10 \mathrm{rad} / \mathrm{s}$ and to $-40 \mathrm{~dB} /$ decade at $\omega_{\mathrm{p} 2}=10^{3} \mathrm{rad} / \mathrm{s}$ (step b). The phase response starts at $0^{\circ}$ (step a) and decreases to $-45^{\circ}$ at $\omega_{\mathrm{p} 1}=10,-90^{\circ}$ at $\omega_{\mathrm{p} 1} \ll \omega \ll \omega_{\mathrm{p} 2}$, to $-135^{\circ}$ at $\omega_{\mathrm{p} 2}=10^{3} \mathrm{rad} / \mathrm{s}$, and finally to $-180^{\circ}$ at $\omega \gg \omega_{\mathrm{p} 2}$ (step c). The plots in Fig. 4.4 result.

The methodology described above may be generalized to handle any rational transfer function where all zeros and poles are purely real. It is easiest to have $\mathrm{H}(\mathrm{s})$ written in root form, (4.4).
a. Find a frequency $\omega_{\text {mid }}$ where the number of poles at lower frequencies, $\omega_{1}, \omega_{2} \ldots \omega_{k}$, equals the number of zeros at lower frequencies, $\mathbf{z}_{1}, \mathbf{z}_{2} \ldots \mathbf{z}_{\mathrm{k}}$. Begin the magnitude response plot with a flat (constant) region around $\omega_{\text {mid }}$ at a value of

$$
20 \log _{10}\left|\mathrm{H}\left(\omega_{\text {mid }}\right)\right| \cong 20 \log \left(\mathrm{~K} \frac{\left|\mathrm{z}_{(\mathrm{K}+1)}\right| \ldots\left|\mathrm{z}_{\mathrm{m}}\right|}{\left|\omega_{(\mathrm{K}+1)}\right| \ldots\left|\omega_{\mathrm{n}}\right|}\right)
$$

Begin the phase response plot at $\angle \mathrm{H}\left(\omega_{\text {mid }}\right) \cong 0^{\circ}$.
b. Moving from $\omega_{\text {mid }}$ to the right along the magnitude response plot (to higher frequencies), each time the frequency becomes greater than a pole frequency, $\omega_{i}$ with $i>k$, the slope of the magnitude response changes by $-20 \mathrm{~dB} /$ decade. Each time the frequency becomes greater than a zero frequency, $\left|z_{i}\right|$ with $\mathrm{i}>\mathrm{k}$, the slope of the magnitude response changes by $+20 \mathrm{~dB} /$ decade.
c. Moving from $\omega_{\text {mid }}$ to the left along the magnitude response plot (to lower frequencies), each time the frequency becomes less than a pole frequency, $\omega_{i}$ with $i \leq k$, the slope of the magnitude response changes by $+20 \mathrm{~dB} /$ decade. Each time the frequency becomes less than a zero frequency, $\left|\mathbf{z}_{\mathrm{i}}\right|$ with $\mathrm{i} \leq \mathrm{k}$, the slope of the magnitude response changes by $-20 \mathrm{~dB} /$ decade.
d. Moving from $\omega_{\text {mid }}$ to the right along the phase response plot (to higher frequencies), an additional $-45^{\circ}$ phase shift is introduced at the frequency of each pole, $\omega_{i}$ with $i>k$, and right-half plane zero, $\left|z_{i}\right|$ with $\mathrm{i}>\mathrm{k}$ and $\mathrm{z}_{\mathrm{i}}<0$; at frequencies substantially higher than the pole and zero frequencies an additional $-90^{\circ}$ phase shift is contributed. At each left-half-plane zero encountered, $\left|z_{i}\right|$ with $i>k$ and $z_{i}>0$, an

Fig. 4.4 Magnitude gain (in dB) and phase versus $\omega$ on a logarithmic scale.
image_name:Fig. 4.4 Magnitude gain (in dB) and phase versus ω on a logarithmic scale
description:The graph in Fig. 4.4 is a Bode plot, which consists of two separate plots: the magnitude plot and the phase plot, both plotted against frequency on a logarithmic scale.

Magnitude Plot:
- **Axes:**
- The vertical axis represents the magnitude of the transfer function \(|H(\omega)|\) in decibels (dB).
- The horizontal axis represents the frequency \(\omega\) on a logarithmic scale.

- **Behavior and Trends:**
- The magnitude starts at 80 dB for low frequencies.
- There is a break point at approximately \(\omega = 10^1\), where the slope of the magnitude plot changes.
- Initially, the slope is \(-20\) dB per decade.
- After this break point, the slope increases to \(-40\) dB per decade at around \(\omega = 10^3\).

- **Key Features:**
- The plot shows two distinct linear regions with different slopes, indicating the presence of poles in the system.
- The change in slope suggests a transition from one pole to two poles.

Phase Plot:
- **Axes:**
- The vertical axis represents the phase angle \(\angle H(\omega)\) in degrees.
- The horizontal axis represents the frequency \(\omega\) on a logarithmic scale.

- **Behavior and Trends:**
- The phase starts near 0° at low frequencies.
- As frequency increases, the phase decreases, passing through \(-90°\) and approaching \(-180°\) at higher frequencies.

- **Key Features:**
- The phase plot indicates phase shifts associated with the poles in the system.
- The gradual decrease in phase aligns with the increasing negative slope observed in the magnitude plot.

Annotations and Specific Data Points:
- The magnitude plot is annotated with slope indicators showing \(-20\) dB/dec and \(-40\) dB/dec.
- The break points in the magnitude plot correspond to changes in the phase plot, indicating the frequencies at which poles affect the system's response.

additional $+45^{\circ}$ phase shift is introduced at the frequency $\left|\mathbf{z}_{\mathrm{i}}\right|$, and an additional $+90^{\circ}$ phase shift is contributed at frequencies substantially higher.
e. Moving from $\omega_{\text {mid }}$ to the left along the phase response plot (to lower frequencies), an additional $+45^{\circ}$ phase shift is introduced at the frequency of each pole, $\omega_{i}$ with $i \leq k$, and right-half plane zero, $\left|z_{i}\right|$ with $\mathrm{i} \leq \mathrm{k}$ and $\mathrm{z}_{\mathrm{i}}<0$; at frequencies substantially lower than the pole and zero frequencies an additional $+90^{\circ}$ phase shift is contributed. At each left-half-plane zero encountered, $\left|z_{i}\right|$ with $i \leq k$ and $z_{i}>0$, an additional $-45^{\circ}$ phase shift is introduced at the frequency $\left|z_{i}\right|$, and an additional $-90^{\circ}$ phase shift is contributed at frequencies substantially lower.

#### EXAMPLE 4.7

Find the transfer function of the opamp circuit shown in Fig. 4.5 and sketch its Bode plots.

#### Solution

Since $C_{1}$ is five orders of magnitude larger than $C_{2}$, there is a wide range of frequencies where $C_{1}$ can be assumed to be a short circuit and $\mathrm{C}_{2}$ can be approximated by an open circuit. ${ }^{4}$ In this frequency range, called midband, we have simply a noninverting opamp configuration with a gain of $\left(1+R_{2} / R_{1}\right)$.

At moderately-low frequencies where $C_{1}$ is having an effect, $C_{2}$ can certainly be treated as an open circuit since it is so small. The circuit at these frequencies appears like the simplified circuit shown in Fig. 4.6. The transfer function at these frequencies is found by analyzing this simplified circuit. The closed-loop transfer function is given by

$$
\begin{equation*}
\mathrm{H}(\mathrm{~s})=\frac{\mathrm{V}_{\text {out }}(\mathrm{s})}{\mathrm{V}_{\text {in }}(\mathrm{s})}=1+\frac{\mathrm{Z}_{2}(\mathrm{~s})}{\mathrm{Z}_{1}(\mathrm{~s})} \tag{4.83}
\end{equation*}
$$

image_name:Fig. 4.5
description:
[
name: A1, type: OpAmp, value: A1, ports: {InP: Vin, InN: InN(A1), OutP: Vout}
name: R1, type: Resistor, value: 100Ω, ports: {N1: InN(A1), N2: R1_C1}
name: R2, type: Resistor, value: 2kΩ, ports: {N1: InN(A1), N2: Vout}
name: C1, type: Capacitor, value: 100nF, ports: {Np: R1_C1, Nn: GND}
name: C2, type: Capacitor, value: 1pF, ports: {Np: InN(A1), Nn: Vout}
]
extrainfo:The circuit is a feedback configuration often used for stereo power amplifiers. It includes a capacitor C1 that acts as an open circuit at low frequencies to maintain unity gain at DC, minimizing clicks due to DC offsets. Capacitor C2 limits the high frequency response.

Fig. 4.5 The feedback configuration often used for stereo power amplifiers.
4. The reason for including $\mathrm{C}_{1}$ is that at very-very-low frequencies, it operates as an open circuit. Thus, at dc, the gain is only unity. The low gain at d.c. (of unity) helps minimize bothersome "clicks" due to d.c. offsets inherent in the amplifier that would be amplified by the large gain if $\mathrm{C}_{1}$ had not been included. The capacitor $\mathrm{C}_{2}$ limits the high frequency response. It also helps stabilize the opamp, but this is beyond the scope of the current subject.

Fig. 4.6 A simplified circuit that has the same frequency response as Fig. 4.5 for low and mid-band frequencies.
image_name:Fig. 4.6
description:
[
name: A1, type: OpAmp, value: A1, ports: {InP: Vin, InN: InN(A1), OutP: Vout}
name: R1, type: Resistor, value: 100Ω, ports: {N1: InN(A1), N2: r1_c1}
name: R2, type: Resistor, value: 2kΩ, ports: {N1: InN(A1), N2: Vout}
name: C1, type: Capacitor, value: 100nF, ports: {Np: r1_c1, Nn: GND}
]
extrainfo:The circuit is a simplified op-amp configuration with low and mid-band frequency response. The gain at DC is unity, which minimizes DC offset clicks. C1 limits high frequency response and stabilizes the op-amp.

where

$$
\begin{equation*}
Z_{1}(s)=R_{1}+\frac{1}{s C_{1}} \tag{4.84}
\end{equation*}
$$

and

$$
\begin{equation*}
Z_{2}(s)=R_{2} \tag{4.85}
\end{equation*}
$$

We have

$$
\begin{equation*}
H(s)=\frac{R_{1}+R_{2}+\frac{1}{s C_{1}}}{R_{1}+\frac{1}{s C_{1}}}=\frac{1+s\left(R_{1}+R_{2}\right) C_{1}}{1+s R_{1} C_{1}} \tag{4.86}
\end{equation*}
$$

We see the simplified circuit is first order with a zero at

$$
\begin{equation*}
\omega_{z 1}=\frac{1}{\left(R_{1}+R_{2}\right) C_{1}}=4.76 \mathrm{krad} / \mathrm{sec} \tag{4.87}
\end{equation*}
$$

and a pole at

$$
\begin{equation*}
\omega_{\mathrm{p} 1}=\frac{1}{\mathrm{R}_{1} \mathrm{C}_{1}}=100 \mathrm{krad} / \mathrm{sec} \tag{4.88}
\end{equation*}
$$

Note that as the frequency gets large, $\omega \gg \omega_{\mathrm{zl}}, \omega_{\mathrm{p} 1}$, the result in (4.86) becomes the same as that obtained earlier by inspection for mid-band frequencies.

$$
\begin{equation*}
\mathrm{H}(\mathrm{~s}) \cong 1+\frac{\mathrm{R}_{2}}{\mathrm{R}_{1}} \tag{4.89}
\end{equation*}
$$

image_name:Fig. 4.7
description:
[
name: A1, type: OpAmp, value: A1, ports: {InP: Vin, InN: InN, InN(A1): Vout, OutN: Vout}
name: R1, type: Resistor, value: 100Ω, ports: {N1: InN(A1), N2: GND}
name: R2, type: Resistor, value: 2kΩ, ports: {N1: InN(A1), N2: Vout}
name: C2, type: Capacitor, value: 1pF, ports: {Np: InN(A1), Nn: Vout}
]
extrainfo:The circuit is a simplified feedback amplifier with an operational amplifier, resistors, and a capacitor forming feedback loops. The circuit is designed to have a specific frequency response, with Z1 and Z2 representing impedance components in the feedback network.

Fig. 4.7 A simplified circuit that has the same frequency response as that in Fig. 4.5 for mid-band and high frequencies.

At mid and high-frequencies, when $\mathrm{C}_{1}$ can be certainly be treated as a short-circuit, the response of the circuit is very close to that of the simplified circuit shown in Fig. 4.7. We now have

$$
\begin{equation*}
Z_{1}(s)=R_{1} \tag{4.90}
\end{equation*}
$$

and

$$
\begin{equation*}
Z_{2}(s)=\frac{1}{1 / R_{2}+s C_{2}} \tag{4.91}
\end{equation*}
$$

Using (4.83), we have (after a little algebra)

$$
\begin{align*}
H(s) & =\frac{Y_{1}(s)+Y_{2}(s)}{Y_{2}(s)} \\
& =\frac{\frac{1}{R_{1}}+\frac{1}{R_{2}}+s C_{2}}{\frac{1}{R_{2}}+s C_{2}}  \tag{4.92}\\
& =\left(\frac{R_{1}+R_{2}}{R_{1}}\right)\left(\frac{1+s\left(R_{1} \| R_{2}\right) C_{2}}{1+s R_{2} C_{2}}\right)
\end{align*}
$$

Key Point: When a circuit has one or more capacitors with relatively very large value, one may consider those capacitors shortcircuited to see how the circuit behaves at higher frequencies. Similarly, when one or more capacitors have relatively very small value, the circuit may be considered with those capacitors open-circuited to understand its operation at lower frequencies.

We see the simplified circuit is again first order with a zero at

$$
\begin{equation*}
\omega_{z 2}=\frac{1}{\left(R_{1} \| R_{2}\right) C_{2}}=1.05 \times 10^{8} \mathrm{rad} / \mathrm{sec} \tag{4.93}
\end{equation*}
$$

and a pole at

$$
\begin{equation*}
\omega_{\mathrm{p} 2}=\frac{1}{\mathrm{R}_{2} \mathrm{C}_{2}}=5 \times 10^{6} \mathrm{rad} / \mathrm{sec} \tag{4.94}
\end{equation*}
$$

Once again the mid-band gain may be found by evaluating (4.92) at low frequencies, $\omega \ll \omega_{\mathrm{z2}}, \omega_{\mathrm{p} 2}$ resulting in $H(s) \cong 1+\left(R_{2} / R_{1}\right)$.

An alternative approach would be to consider the actual circuit of Fig. 4.5 that is valid at all frequencies and substitute

$$
\begin{equation*}
\mathrm{Z}_{1}(\mathrm{~s})=\mathrm{R}_{1}+\frac{1}{\mathrm{sC}} \tag{4.95}
\end{equation*}
$$

and

$$
\begin{equation*}
Z_{2}(s)=\frac{1}{1 / R_{2}+s C_{2}} \tag{4.96}
\end{equation*}
$$

directly into (4.83) without simplifying. After some algebra, we get

$$
\begin{equation*}
H(s)=\frac{1+s\left[\left(R_{1}+R_{2}\right) C_{1}+R_{2} C_{2}\right]+s^{2} R_{1} R_{2} C_{1} C_{2}}{\left(1+s R_{1} C_{1}\right)\left(1+s R_{2} C_{2}\right)} \tag{4.97}
\end{equation*}
$$

If we now make the assumption that the numerator, $\mathrm{N}(\mathrm{s})$, has two widely separated zeros $\omega_{\mathrm{z} 1}$ « $\omega_{\mathrm{z2}}$, then we may express the numerator as

$$
\begin{align*}
\mathrm{N}(\mathrm{~s}) & =\left(1+\frac{\mathrm{s}}{\omega_{\mathrm{z} 1}}\right)\left(1+\frac{\mathrm{s}}{\omega_{\mathrm{z} 2}}\right) \\
& =1+\mathrm{s}\left(\frac{1}{\omega_{\mathrm{z} 1}}+\frac{1}{\omega_{\mathrm{z} 2}}\right)+\frac{\mathrm{s}^{2}}{\omega_{\mathrm{z} 1} \omega_{\mathrm{z} 2}}  \tag{4.98}\\
& \cong 1+\frac{\mathrm{s}}{\omega_{\mathrm{z} 1}}+\frac{\mathrm{s}^{2}}{\omega_{\mathrm{z} 1} \omega_{\mathrm{z} 2}}
\end{align*}
$$

Equating (4.98) and (4.97) and solving for $\omega_{\mathrm{z} 1}$ and $\omega_{\mathrm{z2}}$, we get

$$
\begin{gather*}
\omega_{z 1} \cong \frac{1}{\left(R_{1}+R_{2}\right) C_{1}+R_{2} C_{2}} \cong \frac{1}{\left(R_{1}+R_{2}\right) C_{1}}  \tag{4.99}\\
\omega_{z 2} \cong \frac{1}{\omega_{z 1} R_{1} R_{2} C_{1} C_{2}} \cong \frac{R_{1}+R_{2}}{R_{1} R_{2} C_{2}}=\frac{1}{\left(R_{1} \| R_{2}\right) C_{2}} \tag{4.100}
\end{gather*}
$$

We also have two widely-spaced poles given by

$$
\begin{align*}
& \omega_{\mathrm{p} 1}=\frac{1}{\mathrm{R}_{1} \mathrm{C}_{1}}  \tag{4.101}\\
& \omega_{\mathrm{p} 2}=\frac{1}{\mathrm{R}_{2} \mathrm{C}_{2}} \tag{4.102}
\end{align*}
$$

Hence, we have the same poles and zeros that were obtained by separate analysis of the low-frequency circuit in Fig. 4.6 and the high-frequency circuit in Fig. 4.7.

Following the procedure for sketching Bode plots, we begin at mid-band frequencies $\omega_{\mathrm{p} 1}$ « $\omega$ « $\omega_{\mathrm{p} 2}$. Here, the gain as given by (4.89) is 21 and the magnitude of the bode plot is constant at 26.4 dB while the phase is constant at $0^{\circ}$. Moving to higher frequencies, we first encounter the pole $\omega_{\mathrm{p} 2}$ and then the zero $\omega_{\mathrm{z2}}$. Moving to lower frequencies, we first encounter the pole $\omega_{\mathrm{p} 1}$ and then the zero $\omega_{\mathrm{z} 1}$. The resulting Bode plot is shown in Fig. 4.8.
image_name:Fig. 4.8
description:The graph in Fig. 4.8 is a Bode plot, consisting of two parts: the magnitude plot and the phase plot.

1. **Magnitude Plot**:
- **Type**: Logarithmic scale Bode plot.
- **Axes**:
- The vertical axis represents the magnitude in decibels (dB).
- The horizontal axis represents frequency in a logarithmic scale, ranging from $10^2$ to $10^8$.
- **Behavior and Trends**:
- The plot starts at 0 dB for low frequencies.
- It rises with a slope of +20 dB/decade after encountering the zero at $\omega_{z1}$.
- The magnitude remains constant at 20 dB between $\omega_{p1}$ and $\omega_{p2}$.
- It decreases with a slope of -20 dB/decade after $\omega_{p2}$.
- **Key Features**:
- Shows a constant gain of 20 dB over a certain frequency range.
- Critical points are marked at $\omega_{z1}$, $\omega_{p1}$, $\omega_{p2}$, and $\omega_{z2}$.

2. **Phase Plot**:
- **Axes**:
- The vertical axis represents phase in degrees.
- The horizontal axis is the same logarithmic frequency scale.
- **Behavior and Trends**:
- The phase starts at 0° at low frequencies.
- It increases to a peak near 90° after $\omega_{z1}$.
- The phase then decreases, passing through 0° again and reaching -90°.
- **Key Features**:
- The phase response shows typical behavior of a system with zeros and poles affecting the phase angle.
- The phase shifts correspond to the locations of poles and zeros on the frequency axis.

Fig. 4.8 Approximate magnitude and phase responses of the circuit of Fig. 4.5.

### 4.1.5 Second-Order Low-Pass Transfer Functions with Complex Poles

Consider the second-order low-pass transfer function in (4.62) when the two poles are complex-valued and conjugate pairs, $\omega_{\mathrm{p} 1}=\omega_{\mathrm{p} 2}{ }^{*}$. Using (4.68), we see this case occurs when $\mathrm{Q}>1 / 2$ and we have

$$
\begin{equation*}
\omega_{\mathrm{p} 1}, \omega_{\mathrm{p} 2}=\frac{\omega_{0}}{2 \mathrm{Q}}\left[1 \pm \mathrm{j} \sqrt{4 Q^{2}-1}\right] \equiv \omega_{\mathrm{r}} \pm j \omega_{\mathrm{q}} \tag{4.103}
\end{equation*}
$$

Hence,

$$
\begin{equation*}
\omega_{\mathrm{r}}=\frac{\omega_{0}}{2 \mathrm{Q}} \tag{4.104}
\end{equation*}
$$

and

$$
\begin{equation*}
\omega_{q}=\frac{\omega_{0}}{2 Q} \sqrt{4 Q^{2}-1} \tag{4.105}
\end{equation*}
$$

Furthermore,

$$
\begin{equation*}
\left|\omega_{\mathrm{p} 1}\right|=\left|\omega_{\mathrm{p} 2}\right|=\frac{\omega_{0}}{2 \mathrm{Q}}\left[1+4 \mathrm{Q}^{2}-1\right]^{1 / 2}=\omega_{0} \tag{4.106}
\end{equation*}
$$

The pole locations on the complex s-plane are illustrated in Fig. 4.9. The step response can now be found by substituting (4.103) into (4.81).

$$
\begin{align*}
x_{\text {out }}(t) & =\frac{A_{\text {in }} K}{-2 j \omega_{q}}\left[\left(\omega_{r}-j \omega_{q}\right)\left(1-e^{-\omega_{r} t} e^{-j \omega_{q} t}\right)-\left(\omega_{r}+j \omega_{q}\right) e^{-\omega_{r} t} e^{j \omega_{q}^{t}}\right] \\
& =\frac{A_{\text {in }} K}{2 j \omega_{q}}\left(j \omega_{q}\left[2-e^{-\omega_{r} t}\left(e^{j \omega_{q} t}+e^{-j \omega_{q} t}\right)\right]-\omega_{r}\left[e^{-\omega_{r} t}\left(e^{j \omega_{q} t}-e^{-j \omega_{q} t}\right)\right]\right) \\
& =A_{i n} K\left[1-e^{-\omega_{r} t} \cos \left(\omega_{q} t\right)-\frac{\omega_{r}}{\omega_{q}} e^{-\omega_{r} t} \sin \left(\omega_{q} t\right)\right] \\
& =A_{\text {in }} K\left[1-A_{s} e^{-\omega_{r} t} \cos \left(\omega_{q} t+\theta\right)\right] \tag{4.107}
\end{align*}
$$

Fig. 4.9 The complex-conjugate pole locations of a second-order stable transfer function with $\mathrm{Q}>0.5$.
image_name:Fig. 4.9
description:The graph in Fig. 4.9 is a pole-zero plot of a second-order stable transfer function with a quality factor (Q) greater than 0.5. This type of graph is typically used in control systems and signal processing to represent the locations of poles and zeros in the complex plane.

1. **Type of Graph and Function**: The graph is a pole-zero plot, specifically focusing on the pole locations of a second-order system.

2. **Axes Labels and Units**: The horizontal axis represents the real part of the complex frequency, while the vertical axis represents the imaginary part. The units are typically in radians per second (ω).

3. **Overall Behavior and Trends**: The graph shows two poles, denoted by crosses (X), located symmetrically about the real axis. The poles are complex conjugates, indicating an oscillatory response in the system. The distance from the origin to the poles represents the natural frequency of the system (ω₀), while the angle from the negative real axis to the pole represents the phase angle, which is related to the damping factor.

4. **Key Features and Technical Details**:
- The poles are located at a distance ω₀ from the origin.
- The real part of the pole is at -ω₀/2Q, indicating the damping ratio of the system.
- The angle between the negative real axis and the line connecting the origin to the pole is labeled as cos⁻¹(1/2Q), representing the phase angle.
- The imaginary part of the poles is determined by the distance along the vertical axis.

5. **Annotations and Specific Data Points**:
- Two poles are marked as -ωₚ₁ and -ωₚ₂.
- The angle and distances are labeled to show the relationship between Q, ω₀, and the pole locations.

This plot provides insight into the stability and dynamic response of the system, with the pole locations indicating how the system will respond to different inputs.

Fig. 4.10 The step responses of a secondorder low-pass circuit for (a) $\mathrm{Q}<0.5$ (b) $Q=0.5$, and (c) $. Q>0.5$
image_name:Fig. 4.10
description:The graph in Fig. 4.10 illustrates the step responses of a second-order low-pass circuit for different values of the quality factor \(Q\). The plot is a time-domain waveform, showing how the output \(x_{out}(t)\) evolves over time after a step input is applied.

1. **Axes Labels and Units**:
- The horizontal axis represents time \(t\), but specific units are not provided. It is likely in seconds or milliseconds depending on the context of the system.
- The vertical axis represents the output \(x_{out}(t)\) of the system, which could be voltage or another similar measure, though units are not specified.

2. **Overall Behavior and Trends**:
- Three distinct curves are shown, labeled (a), (b), and (c), corresponding to different values of the quality factor \(Q\).
- Curve (a) represents the step response for \(Q < 0.5\), showing a smooth exponential rise to a steady state without overshoot.
- Curve (b) corresponds to \(Q = 0.5\), where the response rises to the steady state more quickly than (a), with minimal overshoot.
- Curve (c) illustrates the response for \(Q > 0.5\), showing an oscillatory behavior with overshoot before settling into a steady state. This curve demonstrates a damped sinusoidal oscillation that takes longer to settle compared to the other curves.

3. **Key Features and Technical Details**:
- The system's behavior changes significantly with different \(Q\) values, affecting the speed and nature of the response.
- For \(Q < 0.5\), the system is overdamped, leading to a slower response without oscillations.
- At \(Q = 0.5\), the system is critically damped, achieving the fastest response without overshoot.
- For \(Q > 0.5\), the system is underdamped, resulting in oscillations due to the presence of complex conjugate poles.

4. **Annotations and Specific Data Points**:
- The curves are annotated with labels (a), (b), and (c) to indicate the corresponding \(Q\) values.
- The critical points such as the maximum overshoot in the underdamped case (c) are not numerically specified but are visually evident as peaks above the steady state level.

This graph provides insight into how the quality factor \(Q\) influences the dynamic response of a second-order low-pass filter, highlighting the trade-off between speed of response and overshoot/oscillations.

where $A_{s}=\sqrt{2-4 Q^{2}}$ and $\theta=\tan ^{-1} \sqrt{4 Q^{2}-1}$. Thus, we see the step response has a sinusoidal term whose envelope exponentially decreases with a time constant equal to the inverse of the real parts of the poles, $1 / \omega_{\mathrm{r}}=2 \mathrm{Q} / \omega_{0}$. Hence, a system with high Q -factor will exhibit oscillations that persist for a long time. The oscillatory frequency of the sinusoids are determined by the imaginary parts of the poles.

It is also possible to determine the peak of the step response by solving

$$
\begin{equation*}
\frac{d}{d \mathrm{t}} \mathrm{x}_{\text {out }}(\mathrm{t})=0 \tag{4.108}
\end{equation*}
$$

for time, t. In general, there may be multiple solutions to (4.108), but since the envelope of the oscillations is decaying, the solution with the smallest magnitude $|t|$ is the time of the highest peak in the step response. The height is obtained by evaluating (4.107) at this time,

$$
\begin{equation*}
\left.\mathrm{x}_{\text {out }}(\mathrm{t})\right|_{\max }=\mathrm{A}_{\text {in }} \mathrm{K} \mathrm{e}^{-\left(\frac{\pi}{\sqrt{\mathrm{Q}^{2}-1}}\right)} \tag{4.109}
\end{equation*}
$$

Equation (4.109) is valid only for $\mathrm{Q}>0.5$. For $\mathrm{Q} \leq 0.5$, the poles are real-valued and there is no overshoot. The borderline case $\mathrm{Q}=0.5$ is called a maximally-damped response. These different cases have been plotted approximately in Fig. 4.10.

## 4.2 FREQUENCY RESPONSE OF ELEMENTARY TRANSISTOR CIRCUITS

When analyzing electronic circuits containing transistors to determine their frequency response, a small-signal analysis is implicitly assumed since only linearized systems can have a well defined frequency response. Given this assumption, the procedure is the same one outlined at the very beginning of Chapter 3, except that the circuit's parasitic capacitances are included to capture the circuit's high-frequency limitations.

### 4.2.1 High-Frequency MOS Small-Signal Model

The small-signal high-frequency model for MOS transistors takes the low-frequency model and adds parasitic capacitances to model the charge-storage effects of MOS transistors. These effects were covered in detail in Chapter 1 , but the salient points are repeated here in sufficient detail to permit basic frequency analysis of MOS transistor circuits.

A cross-sectional view of a MOS transistor showing the parasitic capacitances is shown in Fig. 4.11. The high-frequency model for MOS transistors in the active region is shown in Fig. 4.12. The largest capacitance in the model is the gate-source capacitance $\mathrm{C}_{\text {gs }}$. For a transistor with width W and gate length L , its value can be estimated with the approximate formula

$$
\begin{equation*}
\mathrm{C}_{\mathrm{gs}}=\frac{2}{3} \mathrm{WLC}_{\mathrm{ox}}+\mathrm{C}_{\mathrm{ov}} \tag{4.110}
\end{equation*}
$$

where $C_{o v}$ is the gate to source or drain overlap capacitance and $C_{o x}$ is the gate capacitance per unit area. The capacitance $\mathrm{C}_{g d}$ is primarily due to the overlap capacitance,

$$
\begin{equation*}
C_{g d}=C_{o v} \tag{4.111}
\end{equation*}
$$

The other capacitances in the small-signal model are due to the depletion capacitances of reverse-biased junctions. We have

$$
\begin{equation*}
C_{s b}=\left(A_{s}+W L\right) C_{j s}+P_{s} C_{j-s w} \tag{4.112}
\end{equation*}
$$

image_name:Fig. 4.11
description:The image labeled as Fig. 4.11 depicts a cross-section of an n-channel MOS transistor, illustrating the small-signal capacitances associated with the device. The diagram is detailed and includes several key components and annotations:

1. **Components and Structure:**
- **Polysilicon Gate:** The top structure is labeled as polysilicon, which forms the gate of the transistor. It is situated above the channel region.
- **Source and Drain Regions:** These are denoted as n+ regions, indicating heavily doped n-type semiconductor areas. They are separated by the channel region under the polysilicon gate.
- **Substrate:** The base of the structure is a p-type substrate, labeled as p- substrate, with a p+ field implant at the edges.
- **Oxide Layer (SiO2):** Surrounding the polysilicon gate, there is an insulating oxide layer.

2. **Connections and Interactions:**
- **Capacitances:**
- **C_gs (Gate-Source Capacitance):** This is shown between the gate and the source region, indicating the capacitance due to the gate-source overlap.
- **C_gd (Gate-Drain Capacitance):** This is the capacitance between the gate and the drain, primarily due to the overlap capacitance (C_ov).
- **C'_sb (Source-Bulk Capacitance):** Connected to the source and the bulk (substrate), representing the depletion capacitance.
- **C'_db (Drain-Bulk Capacitance):** Connected to the drain and the bulk, another depletion capacitance.
- **C_s-sw and C_d-sw (Source and Drain Sidewall Capacitances):** These are sidewall capacitances associated with the source and drain junctions.
- **Voltage Annotations:**
- **V_SB = 0:** The source-bulk voltage is grounded.
- **V_GS > V_tn:** Indicates that the gate-source voltage is greater than the threshold voltage.
- **V_DG > -V_tn:** Signifies that the drain-gate voltage is above a certain threshold.

3. **Labels and Annotations:**
- **L_ov:** This denotes the overlap length between the gate and the source/drain regions.
- **Material Annotations:**
- **Al (Aluminum):** Used for contacts to the source and drain regions.
- **p+ Field Implant:** Enhances the isolation between the devices on the chip.

This diagram is a detailed representation of the small-signal model of an n-channel MOS transistor, highlighting the various capacitances and their interactions within the device. It provides a clear view of how signals and voltages are managed in the transistor's active region.

Fig. 4.11 A cross-section of an n-channel MOS transistor showing the small signal capacitances.
image_name:Fig. 4.12
description:
[
name: Cgs, type: Capacitor, value: Cgs, ports: {Np: Vg, Nn: "Vs"}
name: Cgd, type: Capacitor, value: Cgd, ports: {Np: Vg, Nn: Vd}
name: Csb, type: Capacitor, value: Csb, ports: {Np: "Vs", Nn: GND}
name: Cdb, type: Capacitor, value: Cdb, ports: {Np: Vd, Nn: GND}
name: gmvgs, type: VoltageControlledCurrentSource, ports: {Np: Vd, Nn: "Vs"}
name: gsvs, type: VoltageControlledCurrentSource, ports: {Np: "Vs", Nn: Vd}
name: rds, type: Resistor, value: rds, ports: {N1: Vd, N2: "Vs"}
]
extrainfo:This circuit represents the high-frequency model of an n-channel MOS transistor in the active region, highlighting the various capacitances and voltage-controlled current sources that manage signals and voltages.

Fig. 4.12 The high-frequency model for MOS transistors in the active region.
where $A_{s}$ is the area of the source junction, $P_{s}$ is the effective perimeter of the source junction, and $C_{i s}$ and $\mathrm{C}_{\mathrm{j} \text {-sw }}$ are the per-unit-area and per-unit-length capacitances formed underneath and around the side-walls of the source junction region. The effective area used for the source junction in (4.112) has the channel area added (i.e. WL ) as the source junction and the channel are electrically connected with low impedance. The equation for the drain-bulk capacitance is similar.

$$
\begin{equation*}
C_{d b}=A_{d} C_{j d}+P_{d} C_{j-s w} \tag{4.113}
\end{equation*}
$$

The effective drain junction does not include the area of the channel (i.e. WL). Both $\mathrm{C}_{\mathrm{js}}$ and $\mathrm{C}_{\mathrm{jd}}$ are inversely proportional to $\sqrt{1+\mathrm{V}_{\mathrm{SB}} \text { or } \mathrm{DB} / \Phi_{0}}$. This accounts for the increase in depletion region thickness with increasing reverse bias on the source and drain body junctions. Since $V_{D B}>V_{S B}$ in active mode, $C_{j d}$ will be slightly less than $C_{j s}$.

### 4.2.2 Common-Source Amplifier

A common-source amplifier is shown in Fig. 4.13. It is here driven by a voltage source $\mathrm{v}_{\mathrm{in}}$ with source resistance $R_{s}$, although this may of course be the Thevenin equivalent of a input current source having the same source

Fig. 4.13 A common-source amplifier.
image_name:Fig. 4.13 A common-source amplifier
description:
[
name: Q3, type: PMOS, ports: {S: VDD, D: P, G: P}
name: Q2, type: PMOS, ports: {S: VDD, D: Vout, G: P}
name: Q1, type: NMOS, ports: {S: GND, D: Vout, G: g1}
name: I_bias, type: CurrentSource, value: I_bias, ports: {Np: P, Nn: GND}
name: R_s, type: Resistor, value: R_s, ports: {N1: Vin, N2: g1}
name: C_L, type: Capacitor, value: C_L, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is a common-source amplifier with a PMOS load and NMOS driver. It includes a bias current source (I_bias) connected to the PMOS transistors. The input is fed through a resistor (R_s) to the gate of the NMOS (Q1). The output is taken at Vout, which is also connected to a load capacitor (C_L).

GND
image_name:Fig. 4.14
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: Rs, type: Resistor, value: Rs, ports: {N1: Vin, N2: V1}
name: Cgs1, type: Capacitor, value: Cgs1, ports: {Np: V1, Nn: GND}
name: Cgd1, type: Capacitor, value: Cgd1, ports: {Np: V1, Nn: Vout}
name: gm1Vgs1, type: VoltageControlledCurrentSource, ports: {N1: Vout, N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: Vout, N2: GND}
name: C2, type: Capacitor, value: C2, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is a small-signal model for high-frequency analysis of a common-source amplifier. It includes parasitic capacitances Cgs1 and Cgd1, a voltage-controlled current source gm1Vgs1, and a load resistor R2 and capacitor C2 at the output.

Fig. 4.14 A small-signal model for high-frequency analysis of the common-source amplifier.
resistance. It is assumed that the bias voltage of the input signal is such that both $Q_{1}$ and $Q_{2}$ are in the active region. Based on this assumption, a small-signal equivalent circuit for high-frequency analysis of the commonsource amplifier of Fig. 4.13 is shown in Fig. 4.14. Here, $C_{g s 1}$ is the gate-to-source capacitance of $Q_{1}$ and $C_{g d 1}$ is the gate-to-drain capacitance of $Q_{1}$. Note that it has been assumed that the output capacitance of the input signal source can be ignored. The capacitance $\mathrm{C}_{2}$ is made up of the parallel connection of the drain-to-bulk capacitances of $Q_{1}$ and $Q_{2}$, the gate-drain capacitance of $Q_{2}$, and the load capacitance $C_{\llcorner }$.

$$
\begin{equation*}
\mathrm{C}_{2}=\mathrm{C}_{\mathrm{db} 1}+\mathrm{C}_{\mathrm{db} 2}+\mathrm{C}_{\mathrm{gd} 2}+\mathrm{C}_{\mathrm{L}} \tag{4.114}
\end{equation*}
$$

Similarly, $R_{2}$ is the parallel combination of $r_{d s 1}$ and $r_{\mathrm{ds} 2}$, both small-signal resistances between the output node and small-signal ground.

$$
\begin{equation*}
R_{2}=r_{d s 1} \| r_{d s 2} \tag{4.115}
\end{equation*}
$$

The frequency response of the small-signal circuit may be obtained by nodal analysis. To avoid making circuit equation errors, a consistent methodology should be maintained when writing nodal equations. Here, the first term is always the node at which the currents are being summed. Multiplying this node voltage is the sum of all admittances connected to the node. The next negative terms are the adjacent node voltages with each being multiplied by the connecting admittance. The last terms are any current sources with a positive sign being used if the current sources flow out of the node. Thus, the nodal equation at $\mathrm{V}_{1}$ is

$$
\begin{equation*}
v_{1}\left(G_{s}+s C_{g s 1}+s C_{g d 1}\right)-v_{\text {in }} G_{s}-v_{\text {out }} s C_{g d 1}=0 \tag{4.116}
\end{equation*}
$$

where $G_{s}=1 / R_{s}{ }^{5}$. Also, at the output node, we have

$$
\begin{equation*}
v_{\text {out }}\left(G_{2}+s C_{g d 1}+s C_{2}\right)-v_{1} s C_{g d 1}+g_{m 1} v_{1}=0 \tag{4.117}
\end{equation*}
$$

where we have used $v_{1}=v_{g s 1}$. From (4.117), we have

$$
\begin{equation*}
v_{1}=v_{\text {out }} \frac{\left[G_{2}+s\left(C_{g d 1}+C_{2}\right)\right]}{-g_{m 1}+s C_{g d 1}} \tag{4.118}
\end{equation*}
$$

Substituting (4.118) into (4.116) gives

$$
\begin{equation*}
v_{\text {out }} \frac{\left[G_{2}+s\left(C_{g d 1}+C_{2}\right)\right]\left[G_{s}+s\left(C_{g s 1}+C_{g d 1}\right)\right]}{-g_{m 1}+s C_{g d 1}}-v_{\text {out }} s C_{g d 1}=v_{\text {in }} G_{s} \tag{4.119}
\end{equation*}
$$

5. Whenever a variable is designated $G_{i}$, it is implicitly assumed that it is an admittance and that $G_{i}=1 / R_{i}$, where $R_{i}$ is the resistance of the same component.
which implies

$$
\begin{align*}
& v_{\text {out }}\left\{\begin{array}{c}
G_{s} G_{2}+s\left[G_{2}\left(C_{g \mathrm{~s} 1}+C_{g d 1}\right)+G_{s}\left(C_{g d 1}+C_{2}\right)+g_{m 1} C_{g d 1}\right] \\
+s^{2}\left[\left(C_{g s 1}+C_{g d 1}\right)\left(C_{g d 1}+C_{2}\right)-C_{g d 1}^{2}\right]
\end{array}\right\}  \tag{4.120}\\
& =-v_{i n} G_{s}\left(g_{m 1}-s C_{g d 1}\right)
\end{align*}
$$

Continuing, we have

$$
\begin{equation*}
A(s)=\frac{v_{\text {out }}}{v_{\text {in }}}=\frac{-g_{m 1} R_{2}\left(1-s \frac{C_{\text {gd }}}{g_{m 1}}\right)}{1+s a+s^{2} b} \tag{4.121}
\end{equation*}
$$

where

$$
\begin{equation*}
\mathrm{a}=\mathrm{R}_{\mathrm{s}}\left[\mathrm{C}_{\mathrm{gs} 1}+\mathrm{C}_{\mathrm{gd} 1}\left(1+\mathrm{g}_{\mathrm{m} 1} \mathrm{R}_{2}\right)\right]+\mathrm{R}_{2}\left(\mathrm{C}_{\mathrm{gd} 1}+\mathrm{C}_{2}\right) \tag{4.122}
\end{equation*}
$$

and

$$
\begin{equation*}
\mathrm{b}=\mathrm{R}_{\mathrm{s}} \mathrm{R}_{2}\left(\mathrm{C}_{\mathrm{gd} 1} \mathrm{C}_{\mathrm{gs} 1}+\mathrm{C}_{\mathrm{gs} 1} \mathrm{C}_{2}+\mathrm{C}_{\mathrm{gd} 1} \mathrm{C}_{2}\right) \tag{4.123}
\end{equation*}
$$

This result may seem surprisingly complex for a single-transistor circuit, but several important features are revealed by careful consideration of (4.121) - (4.123).

The low frequency gain is obtained by substituting $\mathrm{s}=0$ into (4.121) and is, as expected,

$$
\begin{equation*}
A_{0}=-g_{m 1} R_{2} \tag{4.124}
\end{equation*}
$$

Assuming the poles are real and widely separated with $\omega_{\mathrm{p} 1}$ « $\omega_{\mathrm{p} 2}$, the denominator can be expressed as

$$
\begin{equation*}
\mathrm{D}(\mathrm{~s})=\left(1+\frac{\mathrm{s}}{\omega_{\mathrm{p} 1}}\right)\left(1+\frac{\mathrm{s}}{\omega_{\mathrm{p} 2}}\right) \cong 1+\frac{\mathrm{s}}{\omega_{\mathrm{p} 1}}+\frac{\mathrm{s}^{2}}{\omega_{\mathrm{p} 1} \omega_{\mathrm{p} 2}} \tag{4.125}
\end{equation*}
$$

Equating the coefficients of (4.125) with those of the denominator of (4.121), we have

$$
\begin{gather*}
\omega_{p 1} \cong \frac{1}{a}=\frac{1}{R_{s}\left[C_{g s 1}+C_{g d 1}\left(1+g_{m 1} R_{2}\right)\right]+R_{2}\left(C_{g d 1}+C_{2}\right)}  \tag{4.126}\\
\omega_{p 2} \cong \frac{1}{\omega_{p 1} b} \tag{4.127}
\end{gather*}
$$

Substituting (4.123) and (4.126) into (4.127), we have

$$
\begin{equation*}
\omega_{\mathrm{p} 2} \cong \frac{\mathrm{~g}_{\mathrm{m} 1} \mathrm{C}_{\mathrm{gd} 1}}{\mathrm{C}_{\mathrm{g} 1} \mathrm{C}_{\mathrm{gd} 1}+\mathrm{C}_{\mathrm{gs} 1} C_{2}+\mathrm{C}_{\mathrm{gd} 1} C_{2}} \tag{4.128}
\end{equation*}
$$

Finally, at high frequencies the zero can be important.

$$
\begin{equation*}
\omega_{\mathrm{z}}=-\frac{g_{\mathrm{m} 1}}{\mathrm{C}_{\mathrm{gd} 1}} \tag{4.129}
\end{equation*}
$$

Intuitively, the zero is caused because at high frequencies $C_{g d 1}$ shorts the gate and drain of $Q_{1}$ together, providing a direct path from the amplifier's input to output. Hence, as frequency increases beyond $\left|\omega_{z}\right|$, the circuit appears to have one less node and one less pole. As a result the roll-off in magnitude response provided by the poles is stifled and the slope of $|A(\omega)|_{d B}$ increases by $+20 \mathrm{~dB} /$ decade. Because the sign of $\omega_{z}$ is negative, the zero is in the right
half-plane and therefore causes phase lag rather than phase lead. This is important when compensating CMOS opamps having common-source stages.

Since $\omega_{\mathrm{p} 1} \ll \omega_{\mathrm{p} 2}, \omega_{\mathrm{z}}$, a dominant-pole approximation may be applied for frequencies $\omega \ll \omega_{\mathrm{p} 2}, \omega_{\bar{\nu}}$

$$
\begin{equation*}
A(s) \cong \frac{A_{0}}{1+\frac{s}{\omega_{p 1}}}=\frac{-g_{m} R_{2}}{1+s\left\{R_{s}\left[C_{g s 1}+C_{g d 1}\left(1+g_{m 1} R_{2}\right)\right]+R_{2}\left(C_{g d 1}+C_{2}\right)\right\}} \tag{4.130}
\end{equation*}
$$

and the $3-\mathrm{dB}$ bandwidth is approximately the dominant pole frequency.

$$
\begin{equation*}
\omega_{-3 \mathrm{~dB}} \cong \omega_{\mathrm{p} 1}=\frac{1}{R_{\mathrm{s}}\left[C_{\mathrm{gs} 1}+C_{g \mathrm{~d} 1}\left(1+\mathrm{g}_{\mathrm{m} 1} R_{2}\right)\right]+\mathrm{R}_{2}\left(\mathrm{C}_{\mathrm{gd} 1}+\mathrm{C}_{2}\right)} \tag{4.131}
\end{equation*}
$$

For the special case where the load capacitance and therefore $\mathrm{C}_{2}$ is large, we have

$$
\begin{gather*}
\omega_{\mathrm{p} 1} \cong \frac{1}{\mathrm{R}_{2} \mathrm{C}_{2}}  \tag{4.132}\\
\omega_{\mathrm{p} 2} \cong \frac{\mathrm{C}_{\mathrm{gd} 1}}{\mathrm{C}_{\mathrm{gs} 1}+\mathrm{C}_{\mathrm{gd} 1}} \frac{\mathrm{~g}_{\mathrm{m} 1}}{\mathrm{C}_{2}} \tag{4.133}
\end{gather*}
$$

Note that both $\omega_{\mathrm{p} 2}$ and $\omega_{\mathrm{z}}$ are proportional to the transistor's transconductance $\mathrm{g}_{\mathrm{m} 1}$; having a large transconductance is important in minimizing the detrimental effects of the second pole and the zero by pushing them to higher frequencies.

The high-frequency analysis of the common-source amplifier illustrates the critical importance of utilizing approximations in analog circuits, both to expedite analysis and to build intuition. The next two subsections present the two most important approximations invoked for the high-frequency analysis of analog circuits, and apply them to the common-source amplifier.

### 4.2.3 Miller Theorem and Miller Effect

Key Point: The frequencyresponse of the commonsource amplifier has 2 poles and 1 zero. The complexity of the analysis illustrates the importance of making approximations and simplifications in the high-frequency analysis of analog circuits.

The most commonly presented method for analyzing common-source amplifiers to determine their -3 dB frequency is based on the Miller theorem. This theorem states that the two circuits shown in Fig. 4.15 are equivalent if $Y_{1}$ and $Y_{2}$ are chosen appropriately. Specifically, if

$$
\begin{equation*}
Y_{1}(s)=Y(s)(1+A) \tag{4.134}
\end{equation*}
$$

and

$$
\begin{equation*}
\mathrm{Y}_{2}(\mathrm{~s})=\mathrm{Y}(\mathrm{~s})\left(1+\frac{1}{\mathrm{~A}}\right) \tag{4.135}
\end{equation*}
$$

then the current through $\mathrm{Y}_{1}$ is

$$
\begin{aligned}
\mathrm{I}_{1} & =\mathrm{Y}_{1}(\mathrm{~s}) \mathrm{V}_{1} \\
& =\mathrm{Y}(\mathrm{~s})(1+\mathrm{A}) \mathrm{V}_{1} \\
& =\mathrm{Y}(\mathrm{~s})\left(\mathrm{V}_{1}+\mathrm{AV} \mathrm{~V}_{1}\right) \\
& =\mathrm{Y}(\mathrm{~s})\left(\mathrm{V}_{1}-\mathrm{V}_{2}\right) \\
& =\mathrm{I}
\end{aligned}
$$

image_name:(a)
description:
[
name: Y, type: Other, ports: {N1: Out (-A), N2: In (-A)}
name: -A, type: OpAmp, value: -A, ports: {InP: In (-A), InN: GND, OutP: Out (-A), OutN: GND}
]
extrainfo:The circuit diagram (a) illustrates the use of an operational amplifier with feedback through an element Y. The voltage at the input of the op-amp is V1, and the output voltage is V2 = -AV1. The circuit demonstrates the Miller theorem, which states that the equivalent circuit can be transformed as shown in diagram (b) with Y1 and Y2.
image_name:(b)
description:
[
name: Y1, type: Other, ports: {N1: In(-A), N2: GND}
name: -A, type: OpAmp, value: -A, ports: {InP: In(-A), InN: GND, OutP: Out(-A), OutN: GND}
name: Y2, type: Other, ports: {N1: Out(-A), N2: GND}
]
extrainfo:The circuit diagram (b) illustrates the application of Miller's theorem, where the admittance Y is split into two components Y1 and Y2 connected to ground. The op-amp -A inverts and amplifies the input voltage V1, producing an output V2 = -AV1.

Fig. 4.15 The Miller theorem states that circuit (a) and (b) are equivalent assuming $Y_{1}$ and $Y_{2}$ are chosen appropriately.
and the current through $Y_{2}$ is

$$
\begin{aligned}
\mathrm{I}_{2} & =\mathrm{Y}_{2}(\mathrm{~s}) \mathrm{V}_{2} \\
& =\mathrm{Y}(\mathrm{~s})\left(1+\frac{1}{\mathrm{~A}}\right) \mathrm{V}_{2} \\
& =\mathrm{Y}(\mathrm{~s})\left(\mathrm{V}_{2}+\frac{1}{\mathrm{~A}} \mathrm{~V}_{2}\right) \\
& =\mathrm{Y}(\mathrm{~s})\left(\mathrm{V}_{2}-\mathrm{V}_{1}\right) \\
& =-\mathrm{I}
\end{aligned}
$$

Hence, in both circuits the currents leaving nodes $\mathrm{V}_{1}$ and $\mathrm{V}_{2}$ through the impedance branches are the same, so all nodal equations are identical and analysis of the two circuits will produce the same results.

#### EXAMPLE 4.8

What is the input impedance of an ideal voltage amplifier with gain -A and a capacitor C connecting the input and output?

#### Solution

This is a straightforward application of Miller Theorem to the case where $\mathrm{Y}(\mathrm{s})=1 / \mathrm{sC}$. Additional insight is gained by recognizing that any capacitance C may be represented by two capacitors in series, as shown in Fig. 4.16.
image_name:Fig. 4.16
description:The circuit diagram shows the equivalence of a single capacitor C with two capacitors C1 and C2 in series, where C1 = (1+A)C and C2 = (1+1/A)C. This is an application of Miller Theorem.

Fig. 4.16 Equivalence of a capacitance C and two series capacitors, $\mathrm{C}_{1}$ and $\mathrm{C}_{2}$.

$$
\begin{align*}
& C_{1}=(1+A) C  \tag{4.136}\\
& C_{2}=\left(1+\frac{1}{A}\right) C \tag{4.137}
\end{align*}
$$

This is true for any constant A since

$$
\frac{C_{1} C_{2}}{C_{1}+C_{2}}=\frac{(1+A) C \cdot\left(1+\frac{1}{A}\right) C}{(1+A) C+\left(1+\frac{1}{A}\right) C}=\frac{\left(A+2+\frac{1}{A}\right) C^{2}}{\left(A+2+\frac{1}{A}\right) C}=C
$$

When $C$ is split into $C_{1}$ and $C_{2}$ as shown in Fig. 4.16, a new (fictitious) node is created at $V_{x}$ whose potential is a simple voltage division between $\mathrm{V}_{1}$ and $\mathrm{V}_{2}$.

$$
\begin{equation*}
\mathrm{V}_{\mathrm{x}}=\mathrm{V}_{1}+\frac{\mathrm{C}_{2}}{\mathrm{C}_{1}+\mathrm{C}_{2}}\left(\mathrm{~V}_{2}-\mathrm{V}_{1}\right) \tag{4.138}
\end{equation*}
$$

In this case, $C$ is connected around an ideal voltage amplifier with gain $-A$, so $V_{2}=-A V_{1}$. Substituting this, along with (4.136) and (4.137) into (4.138) gives the interesting result,

$$
\begin{aligned}
V_{x} & =V_{1}+\left(\frac{\left(1+\frac{1}{A}\right) C}{(1+A) C+\left(1+\frac{1}{A}\right) C}\right)\left(-A V_{1}-V_{1}\right) \\
& =V_{1}-\left(\frac{\left(1+\frac{1}{A}\right)(A+1) C}{(1+A) C+\left(1+\frac{1}{A}\right) C}\right) V_{1}=0
\end{aligned}
$$

Hence, choosing $C_{1}$ and $C_{2}$ as in (4.136) and (4.137) provides a perfect voltage-division ratio to ensure that the node $\mathrm{V}_{\mathrm{x}}$ remains at zero potential (i.e. ground) at all times. The equivalency is illustrated in Fig. 4.17. A similar procedure may be applied to any complex admittance $\mathrm{Y}(\mathrm{s})$, providing an alternate proof of the Miller Theorem.

Clearly, the input impedance $Z_{\text {in }}$ is the capacitance $C_{1}=(1+A) C$, a much larger value than the actual capacitor C when the gain $|A|$ is large. This amplification of $C$ by the gain of an inverting amplifier is called the Miller effect, and C is the Miller capacitor.

Intuitively, the Miller effect may be understood as follows. When the voltage at the amplifier input changes by $\Delta \mathrm{V}_{1}$, the voltage across the Miller capacitor changes by $(1+\mathrm{A}) \Delta \mathrm{V}_{1}$. Thus, whatever source is driving $\mathrm{V}_{1}$ must deliver a charge $(1+\mathrm{A}) \Delta \mathrm{V}_{1} \mathrm{C}$ to the Miller capacitor-the same charge that would be required by a grounded capacitor with the much larger value $(1+\mathrm{A}) \mathrm{C}$.
image_name:Fig. 4.17
description:
[{'name': 'C', 'type': 'Capacitor', 'value': 'C', 'ports': {'Np': 'V1', 'Nn': 'V2'}}, {'name': '-A', 'type': 'OpAmp', 'value': '-A', 'ports': {'InP': 'V1', 'InN': 'V2', 'OutP': 'V2'}}]
[{'name': 'C1', 'type': 'Capacitor', 'value': '(1+A)C', 'ports': {'Np': 'V1', 'Nn': 'Vx'}}, {'name': 'C2', 'type': 'Capacitor', 'value': '(1+1/A)C', 'ports': {'Np': 'Vx', 'Nn': 'V2'}}, {'name': '-A', 'type': 'OpAmp', 'value': '-A', 'ports': {'InP': 'V1', 'InN': 'V2', 'OutP': 'V2'}}]
extrainfo:The circuit demonstrates the Miller effect, where the capacitance appears larger at the input due to the feedback through the op-amp. The effective input impedance is Zin = 1/s(1+A)C, and Vx is grounded.

Fig. 4.17 The application of the Miller theorem to a capacitance across an ideal voltage amplifier results in a large effective input capacitance.

Key Point: When a capacitor connects the input and output of a high-gain inverting amplifier, it appears much larger at the input than it really is. This Miller effect is often responsible for the dominant pole of such amplifiers and, hence, is useful for obtaining a quick estimate of bandwidth.

The power of the Miller theorem is that it greatly simplifies the analysis for the dominant pole of a circuit having a capacitor between the input and output of an inverting high-gain amplifier, as we shall see. However, the Miller theorem is not used when estimating the second pole of amplifiers. At frequencies where capacitive loading at node $\mathrm{V}_{2}$, which is responsible for the second pole, becomes appreciable, the gain between nodes $\mathrm{V}_{1}$ and $\mathrm{V}_{2}$ starts to decrease. Hence, $|A(\omega)|$ may no longer be assumed constant and application of the Miller theorem is difficult.

The Miller theorem can be used to simplify the analysis of the small-signal circuit of Fig. 4.14. The simplified circuit is shown in Fig. 4.18. This simplification is based on noting that the low-frequency gain between $\mathrm{v}_{1}$ and $\mathrm{v}_{\text {out }}$ is

$$
\begin{equation*}
\frac{v_{\text {out }}}{v_{1}} \equiv-A=-g_{\mathrm{m} 1} R_{2} \tag{4.139}
\end{equation*}
$$

The admittance $Y$ bridging $v_{1}$ and $v_{\text {out }}$ is $Y(s)=s C_{g d 1}$. Therefore, we have

$$
\begin{equation*}
Y_{1}(s)=s C_{g d 1}(1+A)=s C_{g d 1}\left(1+g_{m 1} R_{2}\right) \tag{4.140}
\end{equation*}
$$

image_name:Fig. 4.18
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: Rs, type: Resistor, value: Rs, ports: {N1: Vin, N2: V1}
name: Cgs1, type: Capacitor, value: Cgs1, ports: {Np: V1, Nn: GND}
name: Cgd1, type: Capacitor, value: Cgd1, ports: {Np: V1, Nn: Vout}
name: gm1Vgs1, type: VoltageControlledCurrentSource, ports: {Np: Vout, Nn: GND}
name: R2, type: Resistor, value: R2, ports: {N1: Vout, N2: GND}
name: C2, type: Capacitor, value: C2, ports: {Np: Vout, Nn: Vout}
]
extrainfo:This is a simplified small-signal model for a common-source amplifier using the Miller theorem. The circuit includes a voltage source Vin, resistors Rs and R2, capacitors Cgs1, Cgd1, and C2, and a voltage-controlled current source gm1Vgs1. The admittance bridging V1 and Vout is represented by capacitors with modified values using Miller's theorem.

Fig. 4.18 A simplified small-signal model for the common-source amplifier applying the Miller theorem.
and

$$
\begin{equation*}
Y_{2}(s)=s C_{g d 1}\left(1+\frac{1}{A}\right)=s C_{g d 1}\left(1+\frac{1}{g_{m 1} R_{2}}\right) \tag{4.141}
\end{equation*}
$$

It is now evident that the transfer function from $v_{\text {in }}$ to $v_{1}$ has a low-frequency pole which certainly dominates over any others because of the large capacitance there.

$$
\begin{equation*}
\frac{v_{1}}{v_{\text {in }}}(s) \cong \frac{1}{1+\frac{s}{\omega_{\mathrm{p} 1}}} \tag{4.142}
\end{equation*}
$$

where

$$
\begin{equation*}
\omega_{\mathrm{p} 1}=\frac{1}{R_{s}\left[C_{g s 1}+C_{g d 1}\left(1+g_{m 1} R_{2}\right)\right]} \tag{4.143}
\end{equation*}
$$

The estimate for the -3 dB frequency of the circuit is then given by

$$
\begin{equation*}
\omega_{-3 \mathrm{~dB}} \cong \omega_{\mathrm{p} 1}=\frac{1}{R_{s}\left[C_{g s 1}+C_{g d 1}\left(1+g_{m 1} R_{2}\right)\right]} \tag{4.144}
\end{equation*}
$$

This is in agreement with the result obtained by nodal analysis in (4.131) except that terms related to the output node, $\mathrm{R}_{2}\left(\mathrm{C}_{\mathrm{gd} 1}+\mathrm{C}_{2}\right)$, are here ignored. Because the size of $\mathrm{C}_{\mathrm{gd} 1}$ is effectively multiplied by one plus the gain of the amplifier, the importance of having $\mathrm{C}_{\mathrm{gd} 1}$ small is obvious.

As a final note regarding the Miller theorem, this technique of realizing a large grounded capacitor by placing a smaller capacitor between the input and output of a high-gain inverting amplifier may be used to effectively realize large grounded on-chip capacitors.

### 4.2.4 Zero-Value Time-Constant Analysis

The most common and powerful technique for the high-frequency analysis of complex circuits is the zero-value time-constant analysis technique [Gray, 2009]. It is very powerful in estimating a circuit's bandwidth with minimal complication and also in determining which nodes are most important and need to have their associated timeconstants minimized. Generally, the approach is to calculate a time-constant for each capacitor in the circuit by assuming all other capacitors are zero, then sum all the time constants to provide a single overall time constant. Beginning with the small-signal equivalent circuit, the procedure is as follows.
a. Set all independent sources to zero. That is, make all voltage sources into short circuits and all current sources into open circuits.
b. For each capacitor $C_{k}$ in turn, with all other capacitors taken to be zero (making them open circuits), find a corresponding time-constant. To do this, replace the capacitor in question with a voltage source, and then calculate the resistance "seen by that capacitor," $\mathrm{R}_{\mathrm{k}}$, by taking the ratio of the voltage source to the current flowing from it. Note that in this analysis step, there are no capacitors in the circuit. The corresponding time-constant is then simply the capacitor

Key Point: The method of zero-value timeconstants estimates the dominant pole and, hence, bandwidth of complex circuits by analyzing several simpler circuits at dc.
multiplied by the resistance it sees: $\tau_{k}=R_{k} C_{k}$.
c. The -3 dB frequency for the complete circuit is approximated by one over the sum of the individual capacitor time-constants. ${ }^{6}$

$$
\begin{equation*}
\omega_{-3 \mathrm{~dB}} \cong \frac{1}{\sum \tau_{\mathrm{k}}}=\frac{1}{\sum \mathrm{R}_{\mathrm{k}} \mathrm{C}_{\mathrm{k}}} \tag{4.145}
\end{equation*}
$$

This procedure is best understood by way of example.

#### EXAMPLE 4.9

Perform a zero-value time-constant analysis on the common-source amplifier.

#### Solution

Begin with the small-signal equivalent circuit in Fig. 4.14. Set $\mathbf{v}_{\text {in }}=0$. There are three capacitances in the circuit: $\mathrm{C}_{\mathrm{gs}}, \mathrm{C}_{2}$, and $\mathrm{C}_{\mathrm{gdl}}$. We shall consider each in turn.

To compute the time-constant for $\mathrm{C}_{\mathrm{gs} 1}$, set $\mathrm{C}_{2}=0$ and $\mathrm{C}_{\mathrm{gd} 1}=0$ making them open circuits. Then replace $\mathrm{C}_{\mathrm{gs} 1}$ with a test voltage source, $\mathrm{v}_{1}$. The resulting small-signal circuit, shown in Fig. 4.19(a), must then be analyzed to find $R_{1}=v_{1} / i_{1}$. The analysis is trivial, yielding $R_{1}=R_{s}$ and the first time constant,

$$
\begin{equation*}
\tau_{1}=R_{s} C_{g s 1} \tag{4.146}
\end{equation*}
$$

For the capacitor $\mathrm{C}_{2}$, open-circuit both $\mathrm{C}_{g \mathrm{~s} 1}$ and $\mathrm{C}_{\mathrm{gd} 1}$ and apply a test voltage $\mathrm{v}_{2}$ at the output resulting in the small-signal circuit in Fig. $4.19(b)$. Note that there is no current in $R_{s}$ so that $v_{g s 1}=0$ and $g_{m 1} v_{g s 1}=0$. The result follows straightforwardly:

$$
\begin{equation*}
\tau_{2}=\mathrm{R}_{2} \mathrm{C}_{2} \tag{4.147}
\end{equation*}
$$

The analysis for $\mathrm{C}_{\mathrm{gd} 1}$ is slightly more involved. The circuit of Fig. 4.19(c) can be redrawn as shown there. In this transformation, the reference or "ground" node was changed. (Which node is called "ground" is arbitrary in an analysis.) Also, the direction and sign of the voltage-controlled current-source were changed. The perceptive reader might notice that the resulting circuit is essentially the same as that used previously to find the output resistance of a source-degenerated current-source. We have

$$
\begin{equation*}
v_{y}=i_{3} R_{s} \tag{4.148}
\end{equation*}
$$

A nodal equation at $\mathbf{v}_{3}$ gives

$$
\begin{equation*}
v_{3} G_{2}-v_{y} G_{2}-g_{m 1} v_{y}-i_{3}=0 \tag{4.149}
\end{equation*}
$$

Substituting (4.148) into (4.149) and solving for $v_{3} / \mathrm{i}_{3}$ gives

$$
\begin{equation*}
R_{3} \equiv \frac{v_{3}}{i_{3}}=R_{s}\left(1+g_{m 1} R_{2}\right)+R_{2} \tag{4.150}
\end{equation*}
$$

Hence, the final time constant is

$$
\begin{equation*}
\tau_{3}=\left[R_{s}\left(1+g_{m 1} R_{2}\right)+R_{2}\right] C_{g d 1} \tag{4.151}
\end{equation*}
$$

Taking the -3 dB frequency as the inverse of the sum of the time constants results in,

$$
\begin{align*}
\omega_{-3 \mathrm{~dB}} & \cong \frac{1}{R_{s} C_{g s 1}+R_{2} C_{2}+\left[R_{s}\left(1+g_{m 1} R_{2}\right)+R_{2}\right] C_{g d 1}}  \tag{4.152}\\
& =\frac{1}{R_{s}\left[C_{g s 1}+C_{g d 1}\left(1+g_{m 1} R_{2}\right)\right]+R_{2}\left[C_{2}+C_{g d 1}\right]}
\end{align*}
$$

6. This procedure exactly calculates the coefficient of the " $s$ " term in the denominator, $\mathrm{b}_{1}$ in (4.3). The approximation is in assuming that higher-order terms in the denominator and any zeros can be ignored around the -3 dB frequency so that the denominator is approximately $\left(1+b_{1} s\right)$ and the -3 dB frequency is approximately $1 / b_{1}$.
image_name:(a)
description:
[
name: Rs, type: Resistor, value: Rs, ports: {N1: GND, N2: GND}
name: V1, type: VoltageSource, value: V1, ports: {Np: GND, Nn: GND}
]
extrainfo:The diagram represents a simplified small-signal schematic for determining the zero-value time-constant of C_gsl in a common-source amplifier configuration. It includes a resistor Rs and a voltage source V1 connected to ground.
image_name:(b)
description:
[
name: Rs, type: Resistor, value: Rs, ports: {N1: GND, N2: LOAD}
name: V1, type: VoltageSource, value: V1, ports: {Np: LOAD, Nn: GND}
]
extrainfo:The circuit diagram (b) represents a simplified small-signal schematic for determining the zero-value time-constant of a component with the label 'LOAD'. The voltage source V1 is connected across the resistor Rs and the node labeled 'LOAD', with both components connected to the ground (GND). The small-signal voltage across the load is set to zero (vgs1 = 0).
image_name:(c)
description:
[
name: Rs, type: Resistor, value: Rs, ports: {N1: GND, N2: Vy}
name: Vg1, type: VoltageSource, value: Vg1, ports: {Np: Vg1, Nn: GND}
name: gm1Vg1, type: VoltageControlledCurrentSource, ports: {Np: Vy, Nn: GND}
name: R2, type: Resistor, value: R2, ports: {N1: Vy, N2: GND}
]
extrainfo:This is a simplified small-signal schematic for determining the zero-value time-constant of a common-source amplifier configuration. The circuit includes a voltage-controlled current source and is used for analyzing the zero-value time constant.

Fig. 4.19 Analysis of a common-source amplifier by the method of zero-value time constants. The complete small-signal schematic appears in Fig. 4.14. (a) The simplified small-signal schematic for determining the zero-value time-constant of $\mathrm{C}_{\mathrm{gsl}}$. (b) Simplified small-signal schematic for determining the zero-value time-constant of $\mathrm{C}_{2}$. (c) Two equivalent small-signal schematics for determining the zero-value time-constant of $\mathrm{C}_{\mathrm{gd} 1}$.

The bandwidth estimate in (4.152) is exactly the same as (4.131), which was obtained by performing a nodal analysis of the complete circuit and then applying a dominant-pole approximation. ${ }^{7}$

[^5]If the load capacitance is very large, the time constant at the output, $\tau_{2}$, dominates and (4.152) reduces to

$$
\begin{equation*}
\omega_{-3 \mathrm{~dB}} \cong \frac{1}{\mathrm{R}_{2} \mathrm{C}_{2}} \tag{4.153}
\end{equation*}
$$

However, often in analog integrated circuits, the first term in the denominator of (4.152) dominates, yielding the same expression obtained by applying the Miller Theorem and neglecting the output node:

$$
\begin{equation*}
\omega_{-3 \mathrm{~dB}} \cong \frac{1}{R_{s}\left[C_{g s 1}+C_{g d 1}(1+A)\right]} \tag{4.154}
\end{equation*}
$$

where $A=g_{m 1} R_{2}$ is the magnitude of the low-frequency gain.

#### EXAMPLE 4.10

Assume all transistors have $\mathrm{W} / \mathrm{L}=100 \mu \mathrm{~m} / 1.6 \mu \mathrm{~m}$ in Fig. 4.13, and use the transistor parameters listed in Table 1.5 for the $0.8-\mu \mathrm{m}$ CMOS technology in Table 1.5. Also assume that $\mathrm{I}_{\text {bias }}=100 \mu \mathrm{~A}, \mathrm{R}_{\mathrm{s}}=180 \mathrm{k} \Omega$, $\mathrm{C}_{\mathrm{L}}=0.3 \mathrm{pF}, \mathrm{C}_{\mathrm{gs} 1}=0.2 \mathrm{pF}, \mathrm{C}_{\mathrm{gd} 1}=0.015 \mathrm{pF}, \mathrm{C}_{\mathrm{db} 1}=20 \mathrm{fF}, \mathrm{C}_{\mathrm{gd} 2}=22 \mathrm{fF}$, and $\mathrm{C}_{\mathrm{db} 2}=36 \mathrm{fF}$. Estimate the 3 dB frequency of the common-source amplifier of Fig. 4.13.

#### Solution

We have

$$
\begin{equation*}
\mathrm{R}_{2}=\mathrm{r}_{\mathrm{ds} 1} \| \mathrm{r}_{\mathrm{ds} 2}=77 \mathrm{k} \Omega \tag{4.155}
\end{equation*}
$$

and

$$
\begin{equation*}
\mathrm{C}_{2}=\mathrm{C}_{\mathrm{L}}+\mathrm{C}_{\mathrm{db} 1}+\mathrm{C}_{\mathrm{db} 2}+\mathrm{C}_{\mathrm{gd} 2}=0.38 \mathrm{pF} \tag{4.156}
\end{equation*}
$$

The terms involving $R_{s}$, namely $R_{s}\left[C_{g s 1}+C_{g d 1}(1+A)\right]$, are equal to $0.26 \mu \mathrm{~s}$. The terms involving $R_{2}$, namely $\mathrm{R}_{2}\left(\mathrm{C}_{\mathrm{gd} 1}+\mathrm{C}_{2}\right)$ are equal to $0.03 \mu \mathrm{~s}$. The -3 dB frequency (in hertz) is approximately.

$$
\begin{align*}
\mathrm{f}_{-3 \mathrm{~dB}} & \cong \frac{1}{2 \pi} \frac{1}{\mathrm{R}_{\mathrm{in}}\left[\mathrm{C}_{\mathrm{gs} 1}+\mathrm{C}_{\mathrm{gd} 1}\left(1+\mathrm{g}_{\mathrm{m} 1} \mathrm{R}_{2}\right)\right]+\mathrm{R}_{2}\left(\mathrm{C}_{\mathrm{gd} 1}+\mathrm{C}_{2}\right)} \\
& =550 \mathrm{kHz} \tag{4.157}
\end{align*}
$$

### 4.2.5 Common-Source Design Examples

When parasitic MOS capacitances limit the high-frequency response of an amplifier, its bandwidth can be improved by sizing the offending transistor(s) as small as possible. For a fixed current, this implies that the device will exhibit a relatively high value of $\mathrm{V}_{\text {eff }}$. However, operation under very high values of $\mathrm{V}_{\text {eff }}$ is generally avoided since it requires higher dc voltage drops to appear across the transistors to keep them in active mode, and also causes mobility degradation which can decrease amplifier gain.

#### EXAMPLE 4.11

We are to design the common source amplifier in Fig. 4.13 to provide a gain of 20 while driving a capacitive load of $C_{L}=100 \mathrm{fF}$ with maximal bandwidth. The transistor parameters are those listed in Table 1.5 for the $0.18-\mu \mathrm{m}$ CMOS technology. The input source resistance is $R_{s}=40 \mathrm{k} \Omega$ and the supply voltage is 1.8 V . The ideal current source $\mathrm{I}_{\text {bias }} \operatorname{sinks} 50 \mu \mathrm{~A}$ and the total power consumption is to be less than 1 mW .

#### Solution

An approximate expression for the bandwidth $\omega_{-3 \mathrm{~dB}}$ is given in (4.152). In this example, the load capacitance is modest and the source resistance high, so the Miller effect is likely to be the major limitation in the amplifier's bandwidth. To maximize $\omega_{-3 \mathrm{~dB}}$ we wish to minimize the Miller capacitance $\mathrm{C}_{\mathrm{gd} 1}=\mathrm{C}_{\mathrm{ov} 1}$ which requires us to use a

SPICE! Try simulating this design using the provided netlist.
small device width, $\mathrm{W}_{1}$. As we saw in Chapter 1 , this implies relatively large values of $\mathrm{V}_{\text {eff }, 1}$ However, to avoid mobility degradation (which would make it difficult to obtain the targeted gain), we restrict ourselves to a maximum effective gate-source voltage of

$$
\mathrm{V}_{\mathrm{eff}, 1}=\frac{1}{2 \theta}=\frac{1}{2 \cdot 1.7 \mathrm{~V}^{-1}} \cong 300 \mathrm{mV}
$$

If we ensure that $L_{1}$ «L ${ }_{2}$, then $r_{d s 2}$ » $r_{d s 1}$ so that $R_{2} \cong r_{d s 1}$ in (4.124). Hence, the dc gain $A_{0} \cong-g_{m 1} r_{d s 1}$ is approximately equal to the intrinsic gain of $Q_{1}$,

$$
\begin{equation*}
A_{0} \cong-g_{\mathrm{m} 1} r_{\mathrm{ds} 1}=-\frac{2 \mathrm{I}_{\mathrm{D} 1}}{\mathrm{~V}_{\mathrm{eff}, 1}} \cdot \frac{1}{\lambda \mathrm{I}_{\mathrm{D} 1}}=-\frac{2 \mathrm{~L}_{1}}{\lambda \mathrm{~L}_{1} \mathrm{~V}_{\mathrm{eff}, 1}} \tag{4.158}
\end{equation*}
$$

where we have made a coarse approximation in assuming $r_{\mathrm{ds} 1}=1 / \lambda \mathrm{I}_{\mathrm{D} \text {-sat }} \cong 1 / \lambda \mathrm{I}_{\mathrm{D}}$. Substituting the value $\lambda L_{1}=0.08 \mu \mathrm{~m} / \mathrm{V}$ from Table 1.5 along with $\mathrm{V}_{\text {eff }, 1}=300 \mathrm{mV}$ and $\left|A_{0}\right|=20$ into (4.158) allows us to solve for the device length.

$$
\mathrm{L}_{1}=\left|\mathrm{A}_{0}\right| \lambda \mathrm{L}_{1} \mathrm{~V}_{\mathrm{eff}, 1}=(20 / 2) \cdot 0.08 \mu \mathrm{~m} / \mathrm{V} \cdot 0.3 \mathrm{~V}=0.24 \mu \mathrm{~m}
$$

Note that increasing the drain current while maintaining $\mathrm{V}_{\text {eff, } 1}=300 \mathrm{mV}$ will increase $\mathrm{g}_{\mathrm{m} 1}$ and reduce $\mathrm{r}_{\mathrm{ds} 1}$ roughly in proportion resulting in approximately the same gain but a smaller $R_{2}$ in the denominator of $\omega_{-3 \mathrm{~dB}}$ in (4.152). Hence, bandwidth is maximized by using all of the available current. In this case, for a total power consumption of 1 mW and reserving $\mathrm{I}_{\text {bias }}=50 \mu \mathrm{~A}$ of current for the biasing transistor $\mathrm{Q}_{3}$,

$$
\mathrm{I}_{\mathrm{D} 1}=\frac{1 \mathrm{~mW}}{1.8 \mathrm{~V}}-50 \mu \mathrm{~A} \cong 500 \mu \mathrm{~A}
$$

From the desired drain current, gate length, and $\mathrm{V}_{\text {eff }, 1}$ we may compute the required gate width

$$
\begin{gathered}
\mathrm{I}_{\mathrm{D} 1}=\frac{1}{2} \mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}} \frac{\mathrm{~W}_{1}}{\mathrm{~L}_{1}} \mathrm{~V}_{\mathrm{eff}, 1}^{2} \\
\Rightarrow \mathrm{~W}_{1}=\frac{2 \mathrm{I}_{\mathrm{D} 1} \mathrm{~L}_{1}}{\mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}} \mathrm{~V}_{\mathrm{eff}, 1}^{2}}=\frac{2 \cdot 500 \mu \mathrm{~A} \cdot 0.24 \mu \mathrm{~m}}{270 \mu \mathrm{~A} / \mathrm{V}^{2}(0.3 \mathrm{~V})^{2}} \cong 10 \mu \mathrm{~m}
\end{gathered}
$$

To ensure $L_{2}$ » $L_{1}$, we take $L_{2}=3 L_{1}=0.72 \mu \mathrm{~m}$. Since they have the same drain currents, the width of $Q_{2}$ may be conveniently taken 3 times that of $Q_{1}$, although this is not critical.

$$
\mathrm{W}_{2}=3 \cdot 10 \mu \mathrm{~m}=30 \mu \mathrm{~m}
$$

Finally, $Q_{3}$ is sized to provide the desired current ratio in the current mirror formed with $Q_{2}$.

$$
\begin{gathered}
\mathrm{L}_{3}=\mathrm{L}_{2}=0.72 \mu \mathrm{~m} \\
\mathrm{~W}_{3}=\mathrm{W}_{2} \cdot\left(\frac{50 \mu \mathrm{~A}}{500 \mu \mathrm{~A}}\right)=3 \mu \mathrm{~m}
\end{gathered}
$$

When the Miller effect is dominant, as in Example 4.11, the amplifier bandwidth is maximized by taking a small device width and high $\mathrm{V}_{\text {eff }}$ for common-source transistor $\mathrm{Q}_{1}$. However, large device widths and small values of $\mathrm{V}_{\text {eff }}$ are preferable when a large load capacitance causes the output time constant to dominate.

#### EXAMPLE 4.12

We wish to design the common source amplifier in Fig. 4.13 with minimal power consumption while providing a $3-\mathrm{dB}$ bandwidth of 5 MHz and a gain of at least 20 using the transistor parameters listed in Table 1.5 for the 0.18 $\mu \mathrm{m}$ CMOS technology with $C_{L}=10 \mathrm{pF}$ and $R_{s}=1 \mathrm{k} \Omega$. The ideal current source $I_{\text {bias }}$ is $50 \mu \mathrm{~A}$.

#### Solution

In this case, the load capacitance is large and the source resistance lower than in Example 4.11. The output time constant will dominate.

$$
\begin{equation*}
\omega_{-3 \mathrm{~dB}} \cong 1 /\left(\mathrm{r}_{\mathrm{ds}, 1}| | \mathrm{r}_{\mathrm{ds}, 2}\right) \mathrm{C}_{\mathrm{L}}=2 \pi \cdot 5 \cdot 10^{6} \mathrm{rad} / \mathrm{sec} \tag{4.159}
\end{equation*}
$$

Substituting the fixed $C_{L}=10 \mathrm{pF}$ into (4.159) yields,

$$
\left(\mathrm{r}_{\mathrm{ds}, 1}| | \mathrm{r}_{\mathrm{ds}, 2}\right)=3.2 \mathrm{k} \Omega
$$

Note that $\left(r_{d s, 1}| | r_{d s, 2}\right)=1 / I_{D}\left(\lambda_{1}+\lambda_{2}\right)$. To minimize $I_{D}$ and, hence, power consumption we require large $\lambda_{1}$ and $\lambda_{2}$ which in turn demands small $L_{1}$ and $L_{2}$. Therefore, we use the minimum possible in this CMOS process.

$$
\mathrm{L}_{1}=\mathrm{L}_{2}=0.18 \mu \mathrm{~m}
$$

Using the values for $\lambda \mathrm{L}$ from Table 1.5,

$$
\lambda_{1}=\lambda_{2}=(0.08 \mu \mathrm{~m} / \mathrm{V}) / 0.18 \mu \mathrm{~m}=0.44 \mathrm{~V}^{-1}
$$

From this, the required drain current is found.

$$
\mathrm{I}_{\mathrm{D}}=\frac{1}{\mathrm{r}_{\mathrm{ds}} \cdot \lambda} \cong 350 \mu \mathrm{~A}
$$

The result has been rounded to the nearest integer multiple of the bias current, $50 \mu \mathrm{~A}$, in order to simplify the current mirror design. To meet the gain requirement,

$$
\begin{gathered}
\left|A_{0}\right| \cong g_{\mathrm{m} 1}\left(r_{d s, 1}| | r_{d s, 2}\right)=\frac{2 I_{D}}{V_{\text {eff }, 1}} \cdot \frac{1}{\left(\lambda_{1}+\lambda_{2}\right) I_{D}}=\frac{2}{V_{\text {eff }, 1}} \cdot \frac{1}{\left(\lambda_{1}+\lambda_{2}\right)}>20 \\
\Rightarrow V_{\text {eff }, 1}<\frac{2}{20\left(0.44 \mathrm{~V}^{-1}+0.44 \mathrm{~V}^{-1}\right)}=114 \mathrm{mV}
\end{gathered}
$$

For some margin, we take $\mathrm{V}_{\text {eff, } 1}=100 \mathrm{mV}$ and the resulting transistor width is

$$
W_{1}=\frac{2 I_{D 1} L_{1}}{\mu_{\mathrm{n}} C_{\mathrm{ox}} V_{\text {eff }, 1}^{2}}=\frac{2 \cdot 355 \mu \mathrm{~A} \cdot 0.18 \mu \mathrm{~m}}{270 \mu \mathrm{~A} / \mathrm{V}^{2}(0.1 \mathrm{~V})^{2}} \cong 47 \mu \mathrm{~m}
$$

The width of $Q_{2}$ may be chosen the same, $\mathrm{W}_{2}=47 \mu \mathrm{~m}$ and the size of $\mathrm{Q}_{3}$ chosen to provide the correct current ratio in the current mirror formed by $Q_{2}$ and $Q_{3}$ :

$$
\begin{aligned}
& \frac{\left(W_{3} / L_{3}\right)}{\left(W_{2} / L_{2}\right)}=\frac{50 \mu \mathrm{~A}}{350 \mu \mathrm{~A}} \\
\Rightarrow L_{3}= & 0.18 \mu \mathrm{~m} \text { and } W_{3}=6.7 \mu \mathrm{~m}
\end{aligned}
$$

Note that the gain of the amplifier in Example 4.12 is maximized by increasing $W_{1}$ to operate $Q_{1}$ near subthreshold.

### 4.2.6 Common-Gate Amplifier

The frequency response of the common-gate stage is usually superior to that of the common-source stage for two reasons. First, there is no Miller Capacitance coupling from the input node to the high-gain output node. Second, assuming $R_{L}$ is not considerably larger than $r_{d s}$, the common-gate stage exhibits a low input resistance at the source node. The small-signal circuit of a common-gate amplifier being driven by a small signal Norton-equivalent input current source, $\mathrm{l}_{\mathrm{in}}$, is shown in Fig. 4.20. All parasitic capacitances between the drain and small-signal ground have been combined into $C_{2}$ and the body-effect may be included by an additional transconductane $g_{s}$ in parallel with $g_{m}$. We will use the technique of zero-value time-constant analysis to estimate the bandwidth of this amplifier.

First we will estimate the time-constant associated with $\mathrm{C}_{\mathrm{gs}}$ by analysis of the circuit in Fig. 4.21 where the input source and all other capacitances have been set equal to zero. The capacitor $C_{g s}$ is connected between the source and small-signal ground and may, therefore, include $\mathrm{C}_{\mathrm{sb}}$. The small-signal resistance seen by it is simply the resistance seen at the source, $R_{1}=r_{\text {in }} \| R_{s}$. The input resistance of the common-gate amplifier was previously shown to be
image_name:Fig. 4.20
description:
[
name: Cgs, type: Capacitor, value: Cgs, ports: {Np: GND, Nn: vs}
name: Iin, type: CurrentSource, value: Iin, ports: {Np: GND, Nn: vs}
name: Rs, type: Resistor, value: Rs, ports: {N1: Vs, N2: GND}
name: gmvgs, type: VoltageControlledCurrentSource, value: gmvgs, ports: {Np: Vout, Nn: Vs}
name: rds, type: Resistor, value: rds, ports: {N1: Vs, N2: Vout}
name: C2, type: Capacitor, value: Cds+CL+Cgd, ports: {Np: Vout, Nn: GND}
name: RL, type: Resistor, value: RL, ports: {N1: Vout, N2: GND}
]
extrainfo:This is a small-signal model of a common-gate amplifier focusing on the time constant of Cgs. The voltage-controlled current source gmvgs models the transconductance of the MOSFET. The circuit is used to analyze the resistance seen by Cgs, which is rin parallel with Rs.

Fig. 4.20 The high-frequency small-signal model for a common-gate amplifier.
image_name:Fig. 4.21
description:
[
name: v1, type: VoltageSource, value: v1, ports: {Np: GND, Nn: Vs}
name: Rs, type: Resistor, value: Rs, ports: {N1: Vs, N2: GND}
name: rds, type: Resistor, value: rds, ports: {N1: Vs, N2: P}
name: RL, type: Resistor, value: RL, ports: {N1: P, N2: GND}
name: g_m v_s, type: VoltageControlledCurrentSource, ports: {Np: Vs, Nn: P}
]
extrainfo:This circuit represents a high-frequency small-signal model for a common-gate amplifier. It focuses on analyzing the time constant of Cgs and the resistance seen by Cgs, which is rin parallel with Rs. The voltage-controlled current source models the transconductance of the MOSFET.

Fig. 4.21 A simplified small-signal model for computing the time-constant of $\mathrm{C}_{\mathrm{gs}}$.

$$
\begin{equation*}
r_{\text {in }} \cong \frac{1}{g_{m}}\left(1+\frac{R_{\mathrm{L}}}{r_{d s}}\right) \tag{4.160}
\end{equation*}
$$

Under the assumption that $R_{L}$ is not too much bigger than $r_{d s}$, we have

$$
\begin{equation*}
R_{1}=r_{\text {in }}\left\|R_{s} \cong \frac{1}{g_{m}}\right\| R_{s} \cong \frac{1}{g_{m}} \tag{4.161}
\end{equation*}
$$

Thus, the time-constant associated with $\mathrm{C}_{\mathrm{gs}}$ is

$$
\begin{equation*}
\tau_{1}=\left(r_{i n} \| R_{s}\right) C_{g s} \cong \frac{C_{g s}}{g_{m}} \tag{4.162}
\end{equation*}
$$

This assumes $r_{i n}$ « $R_{s}$, but in the event this assumption is not justified, the time constant would be smaller and therefore less important.

Consider next the resistance seen-by $\mathrm{C}_{2}$ with all other capacitances set to zero. Once again this capacitor is grounded. The resistance seen by it is

$$
\begin{equation*}
\mathrm{R}_{2}=\mathrm{R}_{\mathrm{L}} \| \mathrm{r}_{\mathrm{d} 1} \tag{4.163}
\end{equation*}
$$

where $r_{d 1}$ is the resistance looking into the drain with source-degeneration resistor $R_{S}$ in place. From our previous analysis of the output impedance of a source-degenerated current source at low frequencies, we know this resistance is given by

$$
\begin{equation*}
r_{d 1}=r_{d s}\left(1+g_{m} R_{s}\right) \tag{4.164}
\end{equation*}
$$

Often, this impedance will be much greater than $R_{L}$ in which case $R_{2} \cong R_{L}$ and

$$
\begin{equation*}
\tau_{2}=\left(R_{L} \| r_{d 1}\right) C_{2} \cong R_{L} C_{2} \tag{4.165}
\end{equation*}
$$

The -3 dB frequency will be approximately given by $1 /\left(\tau_{1}+\tau_{2}\right)$. Note the absence of any time constants having capacitive terms effectively multiplied by the low-frequency gain of the amplifier unlike the common-source stage. Whereas in the common-source amplifier $\mathrm{C}_{\mathrm{gd}}$ appears between two nodes related by a large negative gain, in the common-gate amplifier $\mathrm{C}_{\mathrm{gd}}$ is grounded so there is no Miller effect. This results in significantly superior high-frequency operation.

In the next section we will see that by combining a common-gate stage with a common-source stage, even further improvements are achieved. This combination mitigates the Miller effect, like the common-gate stage, but has the high input impedance of the common-source stage.

Key Point: All small-signal capacitances in the commongate amplifier are (small-signal) grounded. Hence there is no Miller effect and it can provide high-frequency performance superior to that of the commonsource amplifier, although with much lower input resistance.

## 4.3 CASCODE GAIN STAGE

We next consider the frequency response of the cascode amplifiers shown in Fig. 4.22. Comparing the telescopic cascode of Fig. 4.22(a) and the folded cascode of Fig. 4.22(b), we see that the folded-cascode amplifier suffers from smaller carrier mobility in the common gate transistor $\mathrm{Q}_{2}$. This results in a lower transconductance, $\mathrm{g}_{\mathrm{m} 2}$, a larger time-constant associated with $\mathrm{C}_{\mathrm{gs2}}$, as seen in (4.162), and generally lower bandwidth.

Recall that a major reason for the popularity of cascode stages is that they can have quite large gain for a single stage due to the large impedances at the output. Normally this high gain is obtained without any degradation in speed, or sometimes with an improvement in speed. If, on the other hand, the current source at the output node has a modest or low output resistance (typical when they are realized with just a simple resistor) the cascode stage can provide improved bandwidth without any degradation in gain, or sometimes a small improvement in gain.
image_name:(a)
description:
[
name: Ibias, type: CurrentSource, value: Ibias, ports: {Np: LOAD, Nn: Vout}
name: Q2, type: NMOS, ports: {S: d1s2, D: Vout, G: Vbias}
name: Q1, type: NMOS, ports: {S: GND, D: d1s2, G: g1}
name: Rs, type: Resistor, value: Rs, ports: {N1: Vin, N2: g1}
name: CL, type: Capacitor, value: CL, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit diagram (a) is a telescopic cascode amplifier. It consists of two NMOS transistors Q1 and Q2. The current source Ibias provides biasing for the amplifier. The output is taken at Vout, and the input is applied at Vin through a resistor Rs. The capacitor CL is connected at the output to stabilize the circuit.
image_name:(b)
description:
[
name: Q1, type: NMOS, ports: {S: GND, D: P, G: g1}
name: Q2, type: NMOS, ports: {S: P, D: Vout, G: Vbias}
name: Ibias1, type: CurrentSource, value: Ibias1, ports: {Np: LOAD, Nn: P}
name: Ibias2, type: CurrentSource, value: Ibias2, ports: {Np: Vout, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: Vin, N2: g1}
name: CL, type: Capacitor, value: CL, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is a folded-cascode amplifier with NMOS transistors Q1 and Q2. It uses a resistor RS for input and a capacitor CL for output stabilization. The current sources Ibias1 and Ibias2 provide biasing for the amplifier stage.

Fig. 4.22 (a) A telescopic cascode amplifier and (b) a folded-cascode amplifier.
image_name:Fig. 4.23
description:
[
name: Rs, type: Resistor, value: Rs, ports: {N1: Vin, N2: Vg1}
name: Cgs1, type: Capacitor, value: Cgs1, ports: {Np: Vg1, Nn: GND}
name: Cgd1, type: Capacitor, value: Cgd1, ports: {Np: Vg1, Nn: Vs2}
name: g_m1v_g1, type: VoltageControlledCurrentSource, ports: {Np: Vs2, Nn: GND}
name: r_ds1, type: Resistor, value: r_ds1, ports: {N1: Vs2, N2: GND}
name: g_m2v_s2, type: VoltageControlledCurrentSource, ports: {Np: Vs2, Nn: Vout}
name: r_ds2, type: Resistor, value: r_ds2, ports: {N1: Vout, N2: Vs2}
name: Cs2, type: Capacitor, value: Cs2, ports: {Np: Vs2, Nn: GND}
name: Cout, type: Capacitor, value: Cout, ports: {Np: Vout, Nn: GND}
name: RL, type: Resistor, value: RL, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit is a small-signal model of a folded-cascode amplifier gain stage. It features a high output resistance and potentially high gain, with reduced Miller effect and short-channel effects. The available output voltage swing is reduced.

Fig. 4.23 The small-signal model of the cascode gain stage.

Key Point: The cascode gain stage uses a common-gate transistor $\mathrm{Q}_{2}$ to reduce the $\mathrm{V}_{\mathrm{DS}}$ variations on a commonsource transistor $\mathrm{Q}_{1}$. The result is high output resistance providing potentially high gain, a reduced Miller effect, and reduced short-channel effects. However, the available output voltage swing is reduced.

The exact high-frequency analysis of a cascode gain stage is usually left to simulation on a computer, however an approximate analysis based on zerovalue time-constants is not too complicated. As before, in the zero-value timeconstant analysis all independent sources are set to zero (i.e. here, $\mathrm{v}_{\mathrm{in}}$ is set to 0 volts) and each capacitor is considered in turn with all other capacitors set to zero. The corresponding time-constants are found and labeled $\tau_{\mathrm{k}}$. Then the -3 dB frequency, $\omega_{-3 \mathrm{~dB}}$, is estimated to be one over the sum of all the timeconstants. This technique gives some insight into the relative importance of each capacitor in determining the overall -3 dB frequency.

The small-signal model being analyzed is shown in Fig. 4.23 where the total capacitance at the output node, $\mathrm{C}_{\text {out }}$, is the parallel combination of $\mathrm{C}_{\mathrm{gd} 2}+\mathrm{C}_{\mathrm{db} 2}$, the load capacitance $\mathrm{C}_{\mathrm{L}}$, and the output capacitance of the bias current source, $\mathrm{C}_{\text {bias }}$.

$$
\begin{equation*}
C_{\text {out }}=C_{g d 2}+C_{d b 2}+C_{L}+C_{\text {bias }} \tag{4.166}
\end{equation*}
$$

All capacitances at the source of $Q_{2}$ are combined into

$$
\begin{equation*}
C_{s 2}=C_{d b 1}+C_{s b 2}+C_{g s 2} \tag{4.167}
\end{equation*}
$$

The resistance seen by $C_{\text {out }}$ is the amplifier's output resistance, $R_{\text {out }}$. Hence, the output time-constant is

$$
\begin{equation*}
\tau_{\text {out }}=R_{\text {out }} C_{\text {out }}=\left(r_{\text {d } 2} \| R_{L}\right) C_{\text {out }} \tag{4.168}
\end{equation*}
$$

The resistance seen by $C_{g s 1}$ is $R_{s}$ and the corresponding time-constant is simply

$$
\begin{equation*}
\tau_{g s 1}=C_{g s 1} R_{s} \tag{4.169}
\end{equation*}
$$

The resistance seen by $C_{s 2}$ is the parallel combination of $r_{\text {in2 }}$ defined in (3.51) and $r_{d s 1}$.

$$
\begin{equation*}
g_{\mathrm{s} 2}=1 / \mathrm{r}_{\mathrm{s} 2}=\mathrm{g}_{\mathrm{in} 2}+\mathrm{g}_{\mathrm{ds} 1} \tag{4.170}
\end{equation*}
$$

Hence, its time constant is

$$
\begin{equation*}
\tau_{\mathrm{s} 2}=\left(\mathrm{r}_{\mathrm{i} 2} \| \mathrm{r}_{\mathrm{ds} 1}\right) \mathrm{C}_{\mathrm{s} 2}=\frac{\mathrm{C}_{\mathrm{s} 2}}{\mathrm{~g}_{\mathrm{in} 2}+\mathrm{g}_{\mathrm{ds} 1}} \tag{4.171}
\end{equation*}
$$

The calculation of the time-constant corresponding to $\mathrm{C}_{\mathrm{gd} 1}$ is more involved, but identical to that performed for $C_{g d 1}$ in the common-source amplifier in Example 4.10. The result is given by (4.151) where $R_{2}$ is the total resistance at the drain of $Q_{1}$, in this case given by $r_{\text {in } 2} \| r_{\text {ds } 1}$.

$$
\begin{array}{r}
\tau_{g d 1}=\left\{R_{s}\left[1+g_{m 1}\left(r_{i n 2} \| r_{d s 1}\right)\right]+\left(r_{i n} \| r_{d s 1}\right)\right\} C_{g d 1}  \tag{4.172}\\
\cong R_{s}\left[1+g_{m 1}\left(r_{i n 2} \| r_{d s 1}\right)\right] C_{g d 1}
\end{array}
$$

The approximation in (4.172) assumes $\mathrm{g}_{\mathrm{m} 1} \mathrm{R}_{\mathrm{s}}$ » . Since the low-frequency gain from $\mathrm{v}_{\mathrm{g} 1}$ to $\mathrm{v}_{\mathrm{s} 2}$ is $-g_{m 1}\left(r_{i n 2} \| r_{d s 1}\right)$, you may recognize this time constant as a manifestation of the Miller effect. Notice that $C_{g d 1}$ is multiplied by one minus the low-frequency gain between the two nodes it bridges, as illustrated in Fig. 4.24. If $\mathrm{R}_{\mathrm{s}}$ is large, say on the order of a transistor output impedance $r_{d s}$, and $I_{\text {bias }}$ has an output impedance on the order of $g_{m} r_{d s}^{2}$, then this time-constant is approximately given by

$$
\begin{equation*}
\tau_{\mathrm{gd} 1} \approx \mathrm{C}_{\mathrm{gd} 1} \frac{\mathrm{~g}_{\mathrm{m}} \mathrm{r}_{\mathrm{ds}}^{2}}{2} \tag{4.173}
\end{equation*}
$$

which is almost as large as the corresponding time-constant for a common-source amplifier-a fact not well known.

The sum of the time-constants is then given by

$$
\begin{align*}
\tau_{\text {total }}= & \tau_{\text {out }}+\tau_{\text {gs } 1}+\tau_{s 2}+\tau_{\text {gd } 1} \\
\approx & \left(g_{m 2} r_{d s 1} r_{\text {s } 2} \| R_{L}\right) C_{\text {out }}+C_{g s 1} R_{s}+  \tag{4.174}\\
& +\left(r_{\text {in } 2} \| r_{d s 1}\right) C_{s 2}+R_{s}\left[1+g_{m 1}\left(r_{\text {in } 2} \| r_{d s 1}\right)\right] C_{g d 1}
\end{align*}
$$

The -3 dB frequency is estimated to be one over this time-constant (i.e. $\omega_{-3 \mathrm{~dB}}=1 / \tau_{\text {total }}$ ).

### EXAMPLE 4.13

Estimate the -3 dB frequency of the cascode amplifier of Fig. 4.22(a). Assume that the current source $\mathrm{I}_{\text {bias }}$ has a high output impedance, on the order of $R_{L} \approx g_{m-p} r_{\mathrm{ds}-\mathrm{p}}^{2}$. Further assume that for all transistors, $g_{m}=1 \mathrm{~mA} / \mathrm{V}$,
image_name:Fig. 4.24
description:
[
name: Q1, type: NMOS, ports: {S: GND, D: Vs2, G: Vg1}
name: Q2, type: NMOS, ports: {S: Vs2, D: LOAD, G: GND}
name: Rs, type: Resistor, value: Rs, ports: {N1: Vin, N2: Vg1}
name: Cgd1, type: Capacitor, value: Cgd1, ports: {Np: Vs2, Nn: Vg1}
]
extrainfo:The circuit is a cascode amplifier with two NMOS transistors Q1 and Q2. Q1 is connected to the input voltage Vin through a resistor Rs. The gate of Q2 is grounded, and its drain is connected to the load. The capacitor Cgd1 is connected between the drain of Q1 and its gate. The source of Q1 is grounded.

Fig. 4.24 The Miller effect for the calculation of the zero-value time-constant $\tau_{\text {gd } 1}$ in a cascode amplifier.
$\mathrm{r}_{\mathrm{ds}}=100 \mathrm{k} \Omega, \mathrm{C}_{\mathrm{gs}}=0.2 \mathrm{pF}, \mathrm{C}_{\mathrm{gd}}=15 \mathrm{fF}, \mathrm{C}_{\mathrm{sb}}=40 \mathrm{fF}$, and $\mathrm{C}_{\mathrm{db}}=20 \mathrm{fF}$. The other component values are $\mathrm{R}_{\mathrm{s}}=180 \mathrm{k} \Omega, \mathrm{C}_{\mathrm{L}}=5 \mathrm{pF}$, and $\mathrm{C}_{\text {bias }}=20 \mathrm{fF}$.

### Solution

The time-constants associated with each capacitor are evaluated and summed to form the bandwidth estimate. First note that

$$
\begin{gather*}
\mathrm{C}_{\mathrm{s} 2}=\mathrm{C}_{\mathrm{db} 1}+\mathrm{C}_{\mathrm{sb} 2}+\mathrm{C}_{\mathrm{gs} 2}=0.26 \mathrm{pF}  \tag{4.175}\\
\mathrm{C}_{\mathrm{out}}=\mathrm{C}_{\mathrm{gd} 2}+\mathrm{C}_{\mathrm{db} 2}+\mathrm{C}_{\mathrm{L}}+\mathrm{C}_{\mathrm{bias}}=5.055 \mathrm{pF}
\end{gather*}
$$

It was shown in Section 3.7 that when $I_{\text {bias }}$ has high output resistance, $r_{\text {in } 2} \approx r_{d s}$. Hence, we have

$$
\begin{gather*}
\tau_{\mathrm{gs} 1}=\mathrm{R}_{\mathrm{s}} \mathrm{C}_{\mathrm{gs} 1}=36 \mathrm{~ns} \\
\tau_{\mathrm{gd} 1} \approx \frac{\mathrm{~g}_{\mathrm{m}} \mathrm{r}_{\mathrm{ds}}^{2}}{2} C_{\mathrm{gd} 1}=75 \mathrm{~ns}  \tag{4.176}\\
\tau_{\mathrm{s} 2} \approx \frac{r_{\mathrm{ds}}}{2} C_{\mathrm{s} 2}=13 \mathrm{~ns} \\
\tau_{\text {out }} \approx\left(\mathrm{g}_{\mathrm{m}} \mathrm{r}_{\mathrm{ds}}^{2} \| \mathrm{g}_{\mathrm{m}} \mathrm{r}_{\mathrm{ds}}^{2}\right) C_{\text {out }}=25.3 \mu \mathrm{~s}
\end{gather*}
$$

An estimate of the -3 dB bandwidth is obtained by taking the inverse of the sum of all time constants in (4.176),

$$
\begin{equation*}
\omega_{-3 \mathrm{~dB}} \cong \frac{1}{\tau_{\mathrm{gs} 1}+\tau_{\mathrm{gd} 1}+\tau_{\mathrm{s} 2}+\tau_{\mathrm{out}}}=2 \pi \times 6.3 \mathrm{kHz} \tag{4.177}
\end{equation*}
$$

When used to provide a large low-frequency gain, the cascode amplifier must be biased by a high-quality current source, $I_{\text {bias }}$ whose output resistance is on the order of $R_{L} \approx g_{m-p} r_{d s-p}^{2}$. In that case, the overall gain is

$$
\begin{equation*}
A_{v} \approx-\frac{1}{2} g_{\mathrm{m}}^{2} r_{\mathrm{ds}}^{2}=-\frac{1}{2}\left(\frac{g_{m}}{g_{d s}}\right)^{2} \tag{4.178}
\end{equation*}
$$

and the output resistance is

$$
\begin{equation*}
\mathrm{R}_{\text {out }}=\mathrm{R}_{\mathrm{L}} \| \mathrm{r}_{\mathrm{d} 2} \approx \frac{1}{2} \mathrm{~g}_{\mathrm{m}} \mathrm{r}_{\mathrm{ds}}^{2} \tag{4.179}
\end{equation*}
$$

When designed for large output resistance like this, and especially when there is a large load capacitance $C_{L}$, the output time constant $\tau_{\text {out }}$ expressed in (4.168) will generally dominate over all others. We can substitute $R_{\text {out }} \approx \mathrm{g}_{\mathrm{m}} \mathrm{r}_{\mathrm{ds}}^{2} / 2$ into (4.168) to obtain a rough estimate of this time constant,

$$
\begin{equation*}
\tau_{\text {out }} \approx \mathrm{g}_{\mathrm{m}} \mathrm{r}_{\mathrm{ds}}^{2} \mathrm{C}_{\text {out }} / 2 \tag{4.180}
\end{equation*}
$$

and the -3 dB frequency is approximately equal to its inverse,

$$
\begin{equation*}
\omega_{-3 \mathrm{~dB}} \cong \frac{1}{\tau_{\text {out }}}=\frac{1}{\mathrm{R}_{\text {out }} C_{\text {out }}} \approx \frac{2 \mathrm{~g}_{\mathrm{ds}}^{2}}{\mathrm{~g}_{\mathrm{m}} \mathrm{C}_{\text {out }}} \tag{4.181}
\end{equation*}
$$

### EXAMPLE 4.14

Reconsider Example 4.13, but this time neglect all time constants other than the output time constant.

### Solution

Using (4.181) to obtain a bandwidth estimate yields an almost identical result to that obtained in (4.177) considering all time-constants.

$$
\begin{equation*}
\omega_{-3 \mathrm{~dB}} \cong 1 / \tau_{\text {out }}=2 \pi \times 6.3 \mathrm{kHz} \tag{4.182}
\end{equation*}
$$

This is not surprising since the large load capacitance $C_{\mathrm{L}}=5 \mathrm{pF}$ ensures that the time-constant at the output node dominates. Looking at (4.176), the second most important time-constant is $\tau_{\text {gd } 1}$ whose value is almost 3 orders of magnitude smaller than $\tau_{\text {out }}$. Hence, its effect on the -3 dB frequency is negligible.

When one pole dominates, as in Example 4.14, we can reasonably model the amplifier frequency response over a wide frequency range using a dominant pole approximation,

$$
\begin{equation*}
A(s) \cong \frac{A_{v}}{1+\left(s / \omega_{-3 \mathrm{~dB}}\right)} \tag{4.183}
\end{equation*}
$$

When the cascode amplifier is part of a feedback loop, we shall see that the frequency band of operation is primarily at frequencies substantially larger than $\omega_{-3 \mathrm{~dB}}$. In this range, the ( $\mathrm{s} / \omega_{-3 \mathrm{~dB}}$ ) term will dominate in the denominator and using (4.178) and (4.181), the frequency response is approximated by

$$
\begin{equation*}
A(s) \cong \frac{A_{v}}{s / \omega_{-3 \mathrm{~dB}}} \cong-\frac{g_{m 1}}{s C_{L}} \tag{4.184}
\end{equation*}
$$

The approximations of (4.181) and (4.184) are quite good unless either the source impedance or source capacitance is very large.

The dominant pole estimated in (4.181) is due to the parallel combination of the load capacitance, $\mathrm{C}_{\mathrm{L}}$, and large output resistance, $R_{\text {out }} \approx\left(g_{m} r_{d s}^{2}\right) / 2$. A more accurate analysis would reveal two other poles:

- $\omega_{\text {in }}$ due to the parallel combination of $R_{s}$ and total capacitance at $v_{g 1}$, which includes a Miller capacitance
- $\omega_{\mathrm{s} 2}$ due to the parallel combination of $\mathrm{C}_{\mathrm{s} 2}$ and the impedance at $\mathrm{v}_{\mathrm{s} 2}$

Both depend, in no small measure, on the admittance looking up into the source of of $\mathrm{Q}_{2}, \mathrm{Y}_{\mathrm{in} 2}$, depicted in Fig. 4.25. This admittance can be found by making use of (3.51) where $R_{L}$ is replaced by $R_{L} \|$ ( $1 / s C_{L}$ ). Such a substitution results in

$$
\begin{align*}
Y_{\mathrm{in} 2} & =\frac{g_{\mathrm{m} 2}+g_{\mathrm{s} 2}+g_{\mathrm{ds} 2}}{1+\frac{g_{\mathrm{d} 2} R_{\mathrm{L}}}{1+s R_{\mathrm{L}} C_{\mathrm{L}}}} \\
& \cong g_{\mathrm{m} 2}\left(\frac{1+s R_{\mathrm{L}} C_{\mathrm{L}}}{1+s R_{\mathrm{L}} C_{\mathrm{L}}+g_{\mathrm{d} 2} R_{\mathrm{L}}}\right) \\
& \cong g_{m 2}\left(\frac{1+s R_{\mathrm{L}} C_{\mathrm{L}}}{g_{\mathrm{d} 2} R_{\mathrm{L}}+s R_{\mathrm{L}} C_{\mathrm{L}}}\right) \tag{4.185}
\end{align*}
$$

image_name:Fig. 4.25
description:
[
name: Q1, type: NMOS, ports: {S: GND, D: VS2, G: VG1}
name: Q2, type: NMOS, ports: {S: VS2, D: D2, G: GND}
name: RL, type: Resistor, value: RL, ports: {N1: D2, N2: GND}
name: CL, type: Capacitor, value: CL, ports: {Np: D2, Nn: GND}
name: CS2, type: Capacitor, value: CS2, ports: {Np: VS2, Nn: GND}
]
extrainfo:The circuit is a common-source amplifier with a load resistor RL and a load capacitor CL. The input is applied to the gate of Q1, and the output is taken across CL. The circuit is designed to operate at frequencies where the load capacitance significantly affects the impedance.

Fig. 4.25 A large load capacitance leads to a reduced impedance (increased admittance) looking into the source of $Q_{2}$. This, in turn, ameliorates the Miller effect at the input, and increases the frequency of the pole due to $\mathrm{C}_{\mathrm{s} 2}$.

At frequencies where $\omega \gg 1 /\left(r_{d s} C_{\mathrm{L}}\right)$, the terms in s dominate and $Y_{\mathrm{in} 2} \cong \mathrm{~g}_{\mathrm{m} 2}$. Intuitively, this is because at such frequencies the load capacitor effectively shorts the output to ground, and we therefore see only a small-signal resistance $1 / g_{m 2}$ looking into the source of $Q_{2}$, as illustrated in Fig. 4.25.

Since the high-frequency impedance at the node $v_{\mathrm{s} 2}$ has been reduced to $1 / g_{m 2}$, the gain from $v_{g 1}$ to $v_{s 2}$ at these frequencies is roughly just $-g_{m} / g_{m}=-1$. Hence, the effective Miller capacitance at the input is only $2 C_{g d l}$, resulting in an input pole of

$$
\begin{equation*}
\omega_{\mathrm{in}} \cong \frac{1}{R_{s}\left(C_{g s 1}+2 C_{g d 1}\right)} \tag{4.186}
\end{equation*}
$$

The approximate frequency of the pole due to the parallel combination of $\mathrm{C}_{\mathrm{s} 2}$ and the impedance at $\mathrm{v}_{\mathrm{s} 2}$ is then simply given by

$$
\begin{equation*}
\omega_{\mathrm{s} 2} \cong \frac{\mathrm{~g}_{\mathrm{m} 2}}{\mathrm{C}_{\mathrm{s} 2}} \tag{4.187}
\end{equation*}
$$

When the source resistance, $R_{S}$, is small (for example, when the cascode stage is driven by an opamp circuit), $\omega_{\mathrm{in}} \gg \omega_{\mathrm{s} 2}$ and the second pole of a cascode amplifier is approximately given by (4.187).

It is very easy to derive a upper bound on $\omega_{\mathrm{s} 2}$. From (4.167) we see that

$$
\begin{equation*}
\mathrm{C}_{\mathrm{s} 2}>\mathrm{C}_{\mathrm{gs} 2}=\frac{2}{3}(\mathrm{WL}) \mathrm{C}_{\mathrm{ox}} \tag{4.188}
\end{equation*}
$$

For a folded-cascode amplifier with $\mathrm{PMOS}_{2}$,

$$
\begin{equation*}
g_{m 2}=\mu_{\mathrm{p}} C_{o x}\left(\frac{W}{L}\right)_{2} V_{\text {eff2 }} \tag{4.189}
\end{equation*}
$$

For the NMOS telescopic-cascode amplifier replace $\mu_{n}$ for $\mu_{\mathrm{p}}$ in (4.189). Substituting (4.188) and (4.189) into (4.187) gives the approximate frequency of the second pole.

$$
\begin{equation*}
\omega_{\mathrm{s} 2}<\frac{\mu_{\mathrm{p}} \mathrm{C}_{\mathrm{ox}}(\mathrm{~W} / \mathrm{L})_{2} \mathrm{~V}_{\mathrm{eff} 2}}{(2 / 3)(\mathrm{WL})_{2} \mathrm{C}_{\mathrm{ox}}}=\frac{3 \mu_{\mathrm{p}} \mathrm{~V}_{\text {eff }}}{2 \mathrm{~L}_{2}^{2}} \tag{4.190}
\end{equation*}
$$

When enclosed in a feedback loop, we shall see that stability demands the unity gain frequency of an amplifier be restricted to less than the frequency of its second pole. Equation (4.190) shows that for cascode amplifiers with a dominant output pole, the second pole frequency is relatively independent of that actual design once $\mathrm{V}_{\text {eff2 }}$ is chosen which is usually determined by maximum voltage swing requirements. Hence, this equation is an upper-limit on the unity-gain frequency of any feedback amplifier that uses a cascode gain stage. Note the very strong dependance on the channel length, $L_{2}$. Finally, you may recognize (4.190) as nothing more than the intrinsic speed (unity-gain frequency) of the cascode-transistor, $\mathrm{Q}_{2}$.

$$
\begin{equation*}
\omega_{\mathrm{s} 2}<2 \pi \mathrm{f}_{\mathrm{T}, 2} \tag{4.191}
\end{equation*}
$$

Key Point: The unity-gain frequency of any feedback amplifier that uses a cascode gain stage with a dominant output pole is limited by the unity-gain frequency of the cascode transistor, $\mathrm{Q}_{2}$

### EXAMPLE 4.15

Estimate the upper-bound on the frequency of the second-pole of a folded-cascode amplifier with a large load capacitance for a $0.18 \mu \mathrm{~m}$ technology where a typical value of 0.25 V is chosen for $\mathrm{V}_{\text {eff } 2}$.

### Solution

Normally, a minimum length of a cascode transistor in an analog circuit might be $25 \%$ to $50 \%$ larger than the minimum length of transistors used in digital circuits. Therefore, assuming $\mathrm{L}_{2}=1.5 \cdot 0.18 \mu \mathrm{~m}=0.27 \mu \mathrm{~m}$, and using $\mu_{\mathrm{p}}=0.0082 \mathrm{~m}^{2} / \mathrm{Vs}$ and $\mathrm{V}_{\text {eff2 }}=0.25 \mathrm{~V}$ in (4.190) gives

$$
\omega_{\mathrm{p} 2}<42.2 \times 10^{9} \mathrm{rad}=2 \pi \cdot 6.7 \mathrm{GHz}
$$

In most practical opamp designs, the unity-gain frequency of a typical design might be limited to around onequarter the frequency of the upper-bound established by (4.190) due to the uncertainty and temperature dependence of the variables there, or in this case around 1.5 GHz . For a NMOS telescopic-cascode amplifier, the upperbound would be 2-4 times higher due to the higher mobility of electrons compared to holes.

## 4.4 SOURCE-FOLLOWER AMPLIFIER

The high-frequency analysis of source-follower amplifiers is somewhat involved. It will be shown that these types of amplifiers can have complex poles and thus a designer should be careful that the circuit does not exhibit too much overshoot and ringing. Also shown is a compensation circuit that will result in only real axis poles and therefore no overshoot and ringing.

We shall find the frequency response of the source follower for the common situation in integrated circuits where the source may be modeled by its Norton equivalent circuit and the load is purely capacitive as shown in Fig. 4.26. The small-signal model for this circuit, including the parasitic capacitances, is shown in Fig. 4.27.
image_name:Fig. 4.26
description:
[
name: Iin, type: CurrentSource, value: Iin, ports: {Np: GND, Nn: P2}
name: Rin, type: Resistor, value: Rin, ports: {N1: P2, N2: GND}
name: Cin, type: Capacitor, value: Cin, ports: {Np: P2, Nn: GND}
name: NMOS, type: NMOS, ports: {S: Vout, D: LOAD, G: P2}
name: Ibias, type: CurrentSource, value: Ibias, ports: {Np: Vout, Nn: GND}
name: CL, type: Capacitor, value: CL, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is a source follower configuration with a capacitive load and parasitic capacitances, modeled using its Norton equivalent circuit. The input current source, resistor, and capacitor are connected in parallel at node P2. The NMOS transistor acts as a buffer with its gate connected to node P2, its drain connected to the output node Vout, and its source grounded. The load capacitor CL and bias current source Ibias are connected at the output node Vout.

$\mathrm{V}_{\text {out }}$

Fig. 4.26 The configuration used to analyze the frequency response of the source follower.
image_name:Fig. 4.27
description:
[
name: i_in, type: CurrentSource, ports: {Np: GND, Nn: P}
name: R_in, type: Resistor, value: R_in, ports: {N1: P, N2: GND}
name: C_in, type: Capacitor, value: C_in, ports: {Np: P, Nn: GND}
name: C_gs1, type: Capacitor, value: C_gs1, ports: {Np: P, Nn: Vout}
name: C_gd1, type: Capacitor, value: C_gd1, ports: {Np: P, Nn: Vd1}
name: g_m1*v_gs1, type: VoltageControlledCurrentSource, ports: {Np: Vd1, Nn: Vout}
name: g_s1*v_s1, type: VoltageControlledCurrentSource, ports: {Np: Vout, Nn: Vd1}
name: r_ds1, type: Resistor, value: r_ds1, ports: {N1: Vd1, N2: GND}
name: r_ds2, type: Resistor, value: r_ds2, ports: {N1: Vout, N2: GND}
name: C_s, type: Capacitor, value: C_s, ports: {Np: Vout, Nn: GND}
]
extrainfo:This is a small-signal model for a source follower configuration. The input current source, input resistor, and input capacitor are connected in parallel to node P. The NMOS transistor is modeled with voltage-controlled current sources representing transconductance and source conductance. The output node Vout is connected to a load capacitor and two resistors representing the drain-source resistances.

Capacitor $\mathrm{C}_{\mathrm{s}}$ includes both the load capacitor, $\mathrm{C}_{\mathrm{L}}$, and the parasitic capacitor $\mathrm{C}_{\mathrm{sb} \mathbf{1}}$. Similar to what was done at low-frequencies, $r_{d s 1}, r_{\mathrm{ds} 2}$, and the voltage-controlled current source modelling the body-effect current-source can be modelled by a single resistor. This allows us to analyze the simplified small-signal model shown in Fig. 4.28 where again $R_{s 1}=r_{d s 1}\left\|r_{d s 2}\right\|\left(1 / g_{s}\right)$ and the input capacitance is given by $C_{i n}^{\prime}=C_{i n}+C_{g d 1}$.

Nodal analysis is possible, but it is very complicated for this example. The analysis will proceed in three steps. First, the gain from $v_{g 1}$ to $v_{\text {out }}$ will be found. Next, the admittance, $Y_{g}$, looking into the gate of $Q_{1}$, but not taking into account $C_{g d 1}$, will be found. This will be used to find the gain from $i_{i n}$ to $v_{g 1}$. Finally, the overall gain from $v_{\text {in }}$ to $v_{\text {out }}$ will be found and the results interpreted.

The nodal equation at $v_{\text {out }}$ is

$$
\begin{equation*}
v_{\text {out }}\left(s C_{s}+s C_{g s 1}+G_{s 1}\right)-v_{g 1} s C_{g s 1}-g_{m 1}\left(v_{g 1}-v_{\text {out }}\right)=0 \tag{4.192}
\end{equation*}
$$

Solving for $\mathrm{v}_{\text {out }} / \mathrm{v}_{\mathrm{g} \mathbf{l}}$, we have

$$
\begin{equation*}
\frac{v_{\text {out }}}{v_{g 1}}=\frac{s C_{g s 1}+g_{m 1}}{s\left(C_{g s 1}+C_{s}\right)+g_{m 1}+G_{s 1}} \tag{4.193}
\end{equation*}
$$

image_name:Fig. 4.28
description:
[
name: i_in, type: CurrentSource, value: i_in, ports: {Np: GND, Nn: Vg1}
name: R_in, type: Resistor, value: R_in, ports: {N1: Vg1, N2: GND}
name: "C_in", type: Capacitor, value: "C_in", ports: {Np: Vg1, Nn: GND}
name: C_gs1, type: Capacitor, value: C_gs1, ports: {Np: Vg1, Nn: Vout}
name: g_m1*v_gs1, type: VoltageControlledCurrentSource, ports: {Np: GND, Nn: Vout}
name: R_s1, type: Resistor, value: R_s1, ports: {N1: Vout, N2: GND}
name: C_s, type: Capacitor, value: C_s, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is a small-signal model for a source-follower configuration with a current source input and a voltage-controlled current source. It includes resistive and capacitive components connected to ground and output nodes. The circuit models the admittance at the gate of a transistor, excluding the current into C_gd1.

Fig. 4.28 A simplified equivalent small-signal model for the source-follower.

The next step is to calculate the admittance, $\mathrm{Y}_{\mathrm{g}}$, looking into the gate of $\mathrm{Q}_{1}$, but not taking into account the current going into $\mathrm{C}_{\mathrm{gd1}}$. The input current is given by

$$
\begin{equation*}
i_{g 1}=\left(v_{g 1}-v_{\text {out }}\right) s C_{g s 1} \tag{4.194}
\end{equation*}
$$

Using (4.193) to eliminate $\mathrm{V}_{\text {out }}$ in (4.194) and solving for $\mathrm{Y}_{\mathrm{g}}=\mathrm{i}_{\mathrm{g} 1} / \mathrm{v}_{\mathrm{g} 1}$, we have

$$
\begin{equation*}
Y_{g}=\frac{i_{g 1}}{v_{g 1}}=\frac{s C_{g 11}\left(s C_{s}+G_{s 1}\right)}{s\left(C_{g s 1}+C_{s}\right)+g_{m 1}+G_{s 1}} \tag{4.195}
\end{equation*}
$$

Also, an equation can be written relating the input current, $\mathrm{i}_{\text {in }}$, to the gate voltage, $\mathrm{v}_{\mathrm{g} 1}$, as

$$
\begin{equation*}
i_{i n}=v_{g 1}\left(s C_{i n}^{\prime}+G_{i n}+Y_{g}\right) \tag{4.196}
\end{equation*}
$$

Substituting (4.195) into (4.196) and rearranging gives

$$
\begin{equation*}
\frac{v_{g 1}}{i_{i n}}=\frac{s\left(C_{g s 1}+C_{s}\right)+g_{m 1}+G_{s 1}}{a+s b+s^{2} c} \tag{4.197}
\end{equation*}
$$

where

$$
\begin{align*}
& \mathrm{a}=\mathrm{G}_{\mathrm{in}}\left(\mathrm{~g}_{\mathrm{m} 1}+\mathrm{G}_{\mathrm{s} 1}\right) \\
& \mathrm{b}=\mathrm{G}_{\mathrm{in}}\left(\mathrm{C}_{\mathrm{gs} 1}+\mathrm{C}_{\mathrm{s}}\right)+\mathrm{C}_{\mathrm{in}}^{\prime}\left(\mathrm{g}_{\mathrm{m} 1}+\mathrm{G}_{\mathrm{s} 1}\right)+\mathrm{C}_{\mathrm{gs} 1} \mathrm{G}_{\mathrm{s} 1}  \tag{4.198}\\
& \mathrm{c}=\mathrm{C}_{\mathrm{gs} 1} \mathrm{C}_{\mathrm{s}}+\mathrm{C}_{\mathrm{in}}\left(\mathrm{C}_{\mathrm{gs} 1}+\mathrm{C}_{\mathrm{s}}\right)
\end{align*}
$$

Using (4.193) and (4.197), we then have

$$
\begin{equation*}
A(s)=\frac{v_{\text {out }}}{i_{\text {in }}}=\frac{s C_{g s 1}+g_{m 1}}{a+s b+s^{2} c} \tag{4.199}
\end{equation*}
$$

Thus, we see that the transfer-function is second-order. Specifically, it has two poles (roots of the denominator) which may be either real or complex-conjugate. If they are complex-conjugate, then the step response of the circuit will exhibit over-shoot and possibly ringing, as described in Section 4.1.5. This potential problem is a disadvantage when using source-followers.

To determine if the transfer function will exhibit ringing, (4.199) can be written in the form

$$
\begin{equation*}
\mathrm{A}(\mathrm{~s})=\mathrm{A}(0) \frac{\mathrm{N}(\mathrm{~s})}{1+\frac{\mathrm{s}}{\omega_{0} \mathrm{Q}}+\frac{\mathrm{s}^{2}}{\omega_{0}^{2}}} \tag{4.200}
\end{equation*}
$$

where $\omega_{0}$ and $Q$ can be found by equating the coefficients of (4.200) to the coefficients of (4.199). As in Section 4.1.3, parameter $\omega_{0}$ is the resonant frequency and parameter Q is the Q -factor. It is well known that if $\mathrm{Q}<\sqrt{1 / 2} \approx 0.707$, then the magnitude of the transfer-function will have its maximum at dc and there will be no peaking (assuming the zero is at a very-high frequency and therefore has negligible effect). Furthermore, for $Q=\sqrt{1 / 2}$, the -3 dB frequency is equal to $\omega_{0}$. When the time-domain response is investigated, restrictions on the Q -factor can also be found to guarantee no overshoot for a step input. Specifically, for there to be no overshoot in the step-response, it is necessary that both poles be real which is equivalent to the requirement that $\mathrm{Q} \leq 0.5$. In the case where $\mathrm{Q}>0.5$, the percentage overshoot of the output voltage can be shown to be given by

$$
\begin{equation*}
\% \text { overshoot }=100 \mathrm{e}^{-\frac{\pi}{\sqrt{4 Q^{2}-1}}} \tag{4.201}
\end{equation*}
$$

For the source-follower, equating the coefficients of (4.200) to the coefficients of (4.199) and solving for $\omega_{0}$ and Q results in

$$
\begin{align*}
& \omega_{0}=\sqrt{\frac{G_{i n}\left(g_{m 1}+G_{s 1}\right)}{C_{g s 1} C_{s}+C_{i n}^{\prime}\left(C_{g s 1}+C_{s}\right)}}  \tag{4.202}\\
& Q=\frac{\sqrt{G_{i n}\left(g_{m 1}+G_{s 1}\right)\left[C_{g s 1} C_{s}+C_{\text {in }}^{\prime}\left(C_{g s 1}+C_{s}\right)\right]}}{G_{i n} C_{s}+C_{\text {in }}^{\prime}\left(g_{m 1}+G_{s 1}\right)+C_{g s 1} G_{s 1}} \tag{4.203}
\end{align*}
$$

If $Q$ is less than 0.5 , the poles will be real and distinct. Although this $Q$ equation is rather complex, it is interesting to note that if $C_{s}$ and/or $C_{\text {in }}^{\prime}$ becomes large (i.e. a large load and/or input capacitor), then $Q$ becomes small and there will be no overshoot (though the circuit will be slow). For example, one possibility is that the load is purely capacitive and very large so that $G_{s 1}$ « $g_{m 1}$ and $C_{s} / g_{m 1}$ » $R_{i n}\left(C_{g s 1}+C_{i n}{ }^{\prime}\right)$. In this case, it may be shown that $\mathrm{Q} \ll 0.5$ and, from (4.72), we have a dominant pole at

$$
\begin{equation*}
\omega_{p 1} \cong Q \omega_{0}=\frac{G_{i n}\left(g_{m 1}+G_{s 1}\right)}{G_{i n} C_{s}+C_{\text {in }}^{\prime}\left(g_{m 1}+G_{s 1}\right)+C_{g s 1} G_{s 1}} \cong \frac{g_{m 1}}{C_{s}} \tag{4.204}
\end{equation*}
$$

Hence, the bandwidth is determined mainly by the zero-value time constant corresponding to the load capacitance $C_{s}$.
If $Q$ is greater than 0.5 , the poles will be complex-conjugate and the circuit will exhibit overshoot. For example, when $C_{i n}^{\prime}$ and $G_{s 1}$ become small ${ }^{8}$ then the circuit will have a large $Q$ (i.e., large ringing) when $G_{i n}$ becomes small and $\mathrm{C}_{\mathrm{s}} \approx \mathrm{C}_{\mathrm{gs} 1}$. Fortunately, the parasitic capacitances and output impedances in practical microcircuits typically result in only moderate overshoot for worst-case conditions.

Finally, note also that the numerator zero of the transfer-function is on the negative real-axis at a frequency given by

$$
\begin{equation*}
-\omega_{\mathrm{z}}=-\frac{g_{m 1}}{C_{g s 1}} \tag{4.205}
\end{equation*}
$$

and is typically at a much higher frequency than $\omega_{0}$.

### EXAMPLE 4.16

Using the parameters in Example 3.4, and also assuming $\mathrm{R}_{\mathrm{in}}=18 \mathrm{k} \Omega, \mathrm{C}_{\mathrm{L}}=0.2 \mathrm{pF}$, and $\mathrm{C}_{\mathrm{in}}=10 \mathrm{fF}$, find $\omega_{0}$, Q and the frequency of the zero for the source-follower of Fig. 4.26.

### Solution

From Example 3.4 we know $g_{\mathrm{m} 1}=0.735 \mathrm{~mA} / \mathrm{V}, \mathrm{r}_{\mathrm{ds} 1}=25 \mathrm{k} \Omega, \mathrm{r}_{\mathrm{ds} 2}=25 \mathrm{k} \Omega$, and $\mathrm{g}_{\mathrm{s} 1}=0.1 \mathrm{~mA} / \mathrm{V}$. Moreover, we can estimate the parasitics as follows:

$$
\begin{align*}
\mathrm{C}_{\mathrm{gs} 1} & =\frac{2}{3} \mathrm{WLC}_{\mathrm{ox}}+\mathrm{WL}_{\mathrm{ov}} \mathrm{C}_{\mathrm{ox}} \\
& =\frac{2}{3}(2 \mu \mathrm{~m})(0.2 \mu \mathrm{~m})\left(8.5 \mathrm{fF} / \mu \mathrm{m}^{2}\right)+(2 \mu \mathrm{~m})(0.35 \mathrm{fF} / \mu \mathrm{m})  \tag{4.206}\\
& =3.0 \mathrm{fF}
\end{align*}
$$

8. $\mathrm{G}_{\mathrm{s} 1}$ becomes small when the transistor's source is connected to its body terminal which eliminates the body effect.

$$
\begin{gather*}
\mathrm{C}_{\mathrm{gd} 1}=\mathrm{WL}_{\mathrm{ov}} \mathrm{C}_{\mathrm{ox}}=(2 \mu \mathrm{~m})(0.35 \mathrm{fF} / \mu \mathrm{m})=0.7 \mathrm{fF}  \tag{4.207}\\
\mathrm{C}_{\mathrm{sb} 1}=(2 \mu \mathrm{~m})(0.5 \mathrm{fF} / \mu \mathrm{m})=1 \mathrm{fF} \tag{4.208}
\end{gather*}
$$

Thus, we have

$$
\begin{gather*}
\mathrm{C}_{\text {in }}^{\prime}=\mathrm{C}_{\mathrm{in}}+\mathrm{C}_{\mathrm{gd} 1}=10.7 \mathrm{fF}  \tag{4.209}\\
\mathrm{G}_{\mathrm{s} 1}=\mathrm{g}_{\mathrm{s} 1}+\mathrm{g}_{\mathrm{ds} 1}+\mathrm{g}_{\mathrm{d} 22}=0.18 \mathrm{~mA} / \mathrm{V}  \tag{4.210}\\
\mathrm{C}_{\mathrm{s}}=\mathrm{C}_{\mathrm{L}}+\mathrm{C}_{\mathrm{sb} 1} \cong 0.2 \mathrm{pF} \tag{4.211}
\end{gather*}
$$

and so we can find $\omega_{\circ}$ as

$$
\begin{align*}
& \omega_{0}=\sqrt{\frac{G_{i n}\left(g_{m 1}+G_{s 1}\right)}{C_{g s 1} C_{s}+C_{i n}^{\prime}\left(C_{g s 1}+C_{s}\right)}} \\
& =\left(4.27 \times 10^{9} \mathrm{rad} / \mathrm{s}=2 \pi \times 680 \mathrm{MHz}\right)  \tag{4.212}\\
& Q=\frac{\sqrt{G_{i n}\left(g_{m 1}+G_{s 1}\right)\left[C_{g s 1} C_{s}+C_{\text {in }}^{\prime}\left(C_{g s 1}+C_{s}\right)\right]}}{G_{i n} C_{s}+C_{\text {in }}^{\prime}\left(g_{m 1}+G_{s 1}\right)+C_{g s 1} G_{s 1}} \\
& =0.554 \tag{4.213}
\end{align*}
$$

This results in an overshoot for a step input given by

$$
\begin{equation*}
\% \text { overshoot }=100 \mathrm{e}^{-\frac{\pi}{\sqrt{4 Q^{2}-1}}}=0.13 \% \tag{4.214}
\end{equation*}
$$

The zero frequency is found using (4.205) to be 39 GHz and thus it can almost certainly be ignored.

When complex conjugate poles occur, they can be eliminated by adding a compensation network. To see this, note that (4.195) can be rewritten as

$$
\begin{equation*}
\mathrm{Y}_{\mathrm{g}}=\mathrm{sC}_{2}+\frac{1}{-\mathrm{R}_{1}-\frac{1}{\mathrm{sC}}} \tag{4.215}
\end{equation*}
$$

where

$$
\begin{align*}
& C_{1}=\frac{C_{g s 1}\left(C_{s} g_{m 1}-C_{g s 1} G_{s 1}\right)}{\left(g_{m 1}+G_{s 1}\right)\left(C_{g s 1}+C_{s}\right)} \cong \frac{g_{m 1} C_{g s 1} C_{s}}{\left(g_{m 1}+G_{s 1}\right)\left(C_{g s 1}+C_{s}\right)} \\
& R_{1}=\frac{\left(C_{g s 1}+C_{s}\right)^{2}}{C_{g s 1}\left(C_{s} g_{m 1}-C_{g s 1} G_{s 1}\right)} \cong \frac{\left(C_{g s 1}+C_{s}\right)^{2}}{C_{g s 1} C_{s} g_{m 1}}  \tag{4.216}\\
& C_{2}=\frac{C_{g s 1} C_{s}}{C_{g s 1}+C_{s}}
\end{align*}
$$

Fig. 4.29 A circuit having the same admittance as the input impedance looking into the gate of a source-follower (ignoring $)_{g d}$
image_name:Fig. 4.29
description:
[
name: C1, type: Capacitor, value: C1, ports: {Np: x, Nn: c1_r1}
name: C2, type: Capacitor, value: C2, ports: {Np: x, Nn: GND}
name: R1, type: Resistor, value: R1, ports: {N1: c1_r1, N2: GND}
]
extrainfo:The circuit is designed to have the same admittance as the input impedance looking into the gate of a source-follower. It includes a load represented by 'LOAD' and a conductance 'Yg'. The circuit is intended to address overshoot and ringing in source-follower circuits.

Key Point: Source follower circuits can exhibit large amounts of overshoot and ringing under certain conditions. When designing source-followers, the recommended procedure is to check to see if the poles are complex using either (4.203) or a SPICE transient analysis to look for overshoot. When the poles are complex, then increase the load and/or input capacitor or, alternatively, add the compensating network shown in Fig. 4.30.
and the approximation is due to the fact that typically $C_{s}>C_{g s 1}$ and $\mathrm{g}_{\mathrm{m} 1}>\mathrm{G}_{\mathrm{s} 1}$. This is the same admittance as the circuit shown in Fig. 4.29. Thus, the input admittance is same as a capacitor in parallel with a series combination of a negative capacitor and a negative resistor. If a third network consisting of a capacitor of size $C_{1}$ and a resistor of size $R_{1}$, in series, was connected to the gate of the sourcefollower as shown in Fig. 4.30, then the negative elements would be cancelled. The resulting input admittance would then simply be $\mathrm{C}_{2}$ as given in (4.216). In this case (4.197) becomes

$$
\begin{equation*}
\frac{v_{g 1}}{i_{i n}}=\frac{1}{G_{i n}+s\left(C_{i n}^{\prime}+\frac{C_{g s 1} C_{s}}{C_{g s 1}+C_{s}}\right)} \tag{4.217}
\end{equation*}
$$

and (4.199) becomes

$$
\begin{equation*}
A(s)=\frac{v_{\text {out }}}{i_{\text {in }}}=R_{\text {in }}\left(\frac{g_{m 1}}{g_{m 1}+G_{s 1}}\right) \frac{\left(1+s \frac{C_{\text {gs } 1}}{g_{m 1}}\right)}{\left(1+\frac{s}{p_{1}}\right)\left(1+\frac{s}{p_{2}}\right)} \tag{4.218}
\end{equation*}
$$

where

$$
\begin{equation*}
p_{1}=\frac{G_{i n}}{C_{\text {in }}^{\prime}+\frac{C_{g s 1} C_{L}}{C_{g s 1}+C_{L}}} \cong \frac{G_{i n}}{C_{\text {in }}^{\prime}+C_{g s 1}} \tag{4.219}
\end{equation*}
$$

image_name:Fig. 4.30
description:
[
name: Iin, type: CurrentSource, value: Iin, ports: {Np: GND, Nn: P}
name: Rin, type: Resistor, value: Rin, ports: {N1: P, N2: GND}
name: Cin, type: Capacitor, value: Cin, ports: {Np: P, Nn: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: P, Nn: r1_c1}
name: R1, type: Resistor, value: R1, ports: {N1: r1_c1, N2: GND}
name: Ibias, type: CurrentSource, value: Ibias, ports: {Np: Vout, Nn: GND}
name: M1, type: NMOS, ports: {S: Vout, D: Load, G: P}
name: CL, type: Capacitor, value: CL, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit diagram represents a source-follower configuration with a compensation network (C1 and R1) added to compensate for the negative components of the admittance looking into the gate of the source-follower.

Fig. 4.30 Adding a compensation network ( $C_{1}$ and $R_{1}$ ) to compensate for the negative components of the admittance looking into the gate of the source-follower.

$$
\begin{equation*}
p_{2}=\frac{g_{m 1}+G_{s 1}}{C_{g s}+C_{\mathrm{L}}} \cong \frac{g_{m 1}+G_{s 1}}{C_{\mathrm{L}}} \tag{4.220}
\end{equation*}
$$

The approximation is accurate when $\mathrm{C}_{\mathrm{s}}$ » $\mathrm{C}_{\mathrm{gs}}$. Irrespective of the approximation, the poles are now guaranteed real and no overshoot will occur.

### EXAMPLE 4.17

Using the same parameters as in Example 4.16, find the compensation network and the resulting first and second poles of the source follower of Fig. 4.26.

### Solution

Using (4.216), we have

$$
\begin{equation*}
C_{1} \cong \frac{g_{m 1} C_{g s 1} C_{s}}{\left(g_{m 1}+G_{s 1}\right)\left(C_{g s 1}+C_{s}\right)}=2.37 \mathrm{fF} \tag{4.221}
\end{equation*}
$$

and

$$
\begin{equation*}
R_{1} \cong \frac{\left(C_{g s 1}+C_{s}\right)^{2}}{C_{g s 1} C_{s} g_{m 1}} \cong 93 k \Omega \tag{4.222}
\end{equation*}
$$

The capacitor is a small but reasonable value to be realized on chip. The resistor could be realized by a MOS transistor biased in the triode (i.e., linear) region. Assuming the compensation network is used, the poles of the transfer function would then become

$$
\begin{equation*}
\mathrm{p}_{1} \cong \frac{\mathrm{G}_{\mathrm{in}}}{\mathrm{C}_{\mathrm{gs} 1}+\mathrm{C}_{\mathrm{gd} 1}}=2 \pi \times 2.39 \mathrm{GHz} \tag{4.223}
\end{equation*}
$$

and

$$
\begin{equation*}
\mathrm{p}_{2}=\frac{\mathrm{g}_{\mathrm{m} 1}+\mathrm{G}_{\mathrm{s} 1}}{\mathrm{C}_{\mathrm{gs}}+\mathrm{C}_{\mathrm{L}}}=2 \pi \times 0.72 \mathrm{GHz} \tag{4.224}
\end{equation*}
$$

Finally, it should be mentioned here that if the source-follower buffer is intended to be used in an opamp (and thus feedback will be placed around the buffer), and if the resonant frequency of the source-follower is substantially greater than the unity-gain frequency of the amplifier, then the overshoot can be tolerated and no compensation network is necessary.

## 4.5 DIFFERENTIAL PAIR

### 4.5.1 High-Frequency T Model

Similar to low-frequency analysis, there exists a Tmodel for high-frequency modelling that sometimes results in simpler analyses and greater insight, especially when the gain is not large. Consider the small-signal T model for a MOSFET shown in Fig. 4.31. The T model significantly simplifies the analysis of differential-pair-based amplifiers especially when the transistor output resistors can be ignored.

Fig. 4.31 A high-frequency T model for a MOSFET in the active region with the
image_name:Fig. 4.31
description:
[
name: Cgd, type: Capacitor, value: Cgd, ports: {Np: Vd, Nn: Vg}
name: Cgs, type: Capacitor, value: Cgs, ports: {Np: Vg, Nn: Vs}
name: Csb, type: Capacitor, value: Csb, ports: {Np: Vs, Nn: GND}
name: r_s, type: Resistor, value: 1/g_m, ports: {N1: Vg, N2: Vs}
name: r_ds, type: Resistor, value: r_ds, ports: {N1: Vd, N2: Vs}
name: g_m*v_gs, type: VoltageControlledCurrentSource, ports: {Np: Vd, Nn: Vg}
name: g_s*v_s, type: VoltageControlledCurrentSource, ports: {Np: Vs, Nn: Vd}
name: C_db, type: Capacitor, value: C_db, ports: {Np: Vd, Nn: GND}
]
extrainfo:This is a high-frequency T model for a MOSFET in the active region, simplifying the analysis by ignoring the transistor drain-source resistances.

### 4.5.2 Symmetric Differential Amplifier

A symmetric differential amplifier with resistive loads is shown in Fig. 4.32. A small-signal model of this amplifier using the T-model is shown in Fig. 4.33. Here we have ignored both the transistor drain-source resistances in order to simplify the circuit.

Key Point: The analysis of a symmetric differential pair may be simplified to that of the half-circuit, which is simply a common-source amplifier.

Assuming that the transistors are matched, then the circuit is perfectly symmetric. If one also assumes that $v_{\text {in }}^{-}=-v_{\text {in }}^{+}$, then based on the symmetry, the node voltage $\mathrm{v}_{\mathrm{s}}$ will never change similar to if it was connected to a small-signal ground. Indeed, if the node $\mathrm{v}_{\mathrm{s}}$ was connected to a small-signal ground, then circuit will operate identically. This allows one to ignore $\mathrm{C}_{\mathrm{sb} 1}$ and $\mathrm{C}_{\mathrm{sb} 2}$ (not included in Fig. 4.33) and simplify the analysis to that of the half-circuit which is identical to the common-source amplifier studied previously. Given this equivalence, and

Fig. 4.32 A symmetric MOS differential amplifier.
image_name:Fig. 4.32
description:
[
name: Q1, type: NMOS, ports: {S: P, D: Vout-, G: g1}
name: Q2, type: NMOS, ports: {S: P, D: Vout+, G: g2}
name: RD, type: Resistor, value: RD, ports: {N1: Vout-, N2: LOAD1}
name: RD, type: Resistor, value: RD, ports: {N1: Vout+, N2: LOAD2}
name: RS, type: Resistor, value: RS, ports: {N1: Vin+, N2: g1}
name: RS, type: Resistor, value: RS, ports: {N1: Vin-, N2: g2}
name: Ibias, type: CurrentSource, value: Ibias, ports: {Np: P, Nn: GND}
]
extrainfo:The circuit is a symmetric MOS differential amplifier with two NMOS transistors Q1 and Q2. The circuit uses a current source Ibias to provide biasing, and resistors RD as loads for each transistor. The input is differential with nodes Vin+ and Vin-. The outputs are taken from Vout+ and Vout-.

image_name:Fig. 4.33
description:
[
name: Cdb1, type: Capacitor, value: Cdb1, ports: {Np: Vout-, Nn: GND}
name: Cgd1, type: Capacitor, value: Cgd1, ports: {Np: Vout-, Nn: p1}
name: Cgs1, type: Capacitor, value: Cgs1, ports: {Np: p1, Nn: Vs}
name: Cgs2, type: Capacitor, value: Cgs2, ports: {Np: p2, Nn: Vs}
name: Cgd2, type: Capacitor, value: Cgd2, ports: {Np: Vout+, Nn: p2}
name: Cdb2, type: Capacitor, value: Cdb2, ports: {Np: Vout+, Nn: GND}
name: RD1, type: Resistor, value: RD, ports: {N1: Vout-, N2: GND}
name: RD2, type: Resistor, value: RD, ports: {N1: Vout+, N2: GND}
name: RS1, type: Resistor, value: RS, ports: {N1: Vin+, N2: p1}
name: RS2, type: Resistor, value: RS, ports: {N1: Vin-, N2: p2}
name: rs1, type: Resistor, value: rs1, ports: {N1: p1, N2: Vs}
name: rs2, type: Resistor, value: rs2, ports: {N1: p2, N2: Vs}
name: P1, type: VoltageControlledCurrentSource, ports: {N1: Vout-, N2: p1}
name: P2, type: VoltageControlledCurrentSource, ports: {N1: Vout+, N2: p2}
]
extrainfo:The circuit is a symmetric differential amplifier with two voltage-controlled current sources P1 and P2. It includes capacitors Cdb1, Cgd1, Cgs1, Cgs2, Cgd2, and Cdb2, and resistors RD, RS, rs1, and rs2. The inputs are differential at nodes Vin+ and Vin-, and the outputs are at nodes Vout+ and Vout-. The circuit is grounded at multiple points.

assuming the time constant associated with $\mathrm{C}_{\mathrm{db}}$ is negligible, one can immediately estimate the amplifier bandwidth.

$$
\begin{equation*}
\omega_{-3 \mathrm{~dB}} \cong \frac{1}{R_{s}\left[C_{g s 1}+C_{g d 1}\left(1+g_{m 1} R_{2}\right)\right]} \tag{4.225}
\end{equation*}
$$

### 4.5.3 Single-Ended Differential Amplifier

Consider next the frequency response of the single-ended output differential amplifier shown in Fig. 4.34. Before we analyze this amplifier for its frequency response, note that this configuration can be considered a two-stage amplifier comprising an source follower followed by a common-gate stage. The small-signal model for this amplifier is shown in Fig. $4.34(b)$. Note both the similarities and the differences of the circuits shown in Fig. 4.33 and Fig. $4.34(b)$. The differences, though they appear minor result in a significantly larger bandwidth (and approximately half the gain).

Before starting the analysis, note that between the gate of $Q_{1}$ and ground are two similar networks, namely $r_{s 1}$ in parallel with $C_{g s 1}$, and $r_{s 2}$ in parallel with $C_{g s 2}$. If we assume the bias current $I_{\text {bias }}$ is split equally between $Q_{1}$ and $Q_{2}$, we may simplify the circuit into the equivalent small-signal model shown in Fig. 4.35. This simplification assumes the transistor parameters are matched which allows one to drop the subscripts. Next notice that the left-most dependant current source is proportional to the voltage across it; this makes it equivalent to a negative resistor (given the direction of the current source) of size $-2 / \mathrm{g}_{\mathrm{m}}$. We can simplify the circuit even more by noting that the negative resistance $-2 / \mathrm{g}_{\mathrm{m}}$ perfectly cancels out the parallel resistance $2 \mathrm{r}_{\mathrm{s}}=2 / \mathrm{g}_{\mathrm{m}}$. The final simplified circuit is now shown in Fig. 4.36. The transfer function is now easily found almost by inspection to be

$$
\begin{equation*}
H(s)=\frac{-\frac{g_{m}}{2} R_{D}}{\left(1+s R_{s}\left(\frac{C_{g \mathrm{~s}}}{2}+C_{g d 1}\right)\right)\left(1+s C_{g d 2} R_{D}\right)} \tag{4.226}
\end{equation*}
$$

image_name:(a)
description:
[
name: Q1, type: NMOS, ports: {S: P, D: LOAD1, G: g1}
name: Q2, type: NMOS, ports: {S: P, D: Vout, G: GND}
name: RD, type: Resistor, value: RD, ports: {N1: Vout, N2: LOAD2}
name: Ibias, type: CurrentSource, value: Ibias, ports: {Np: P, Nn: LOAD3}
]
extrainfo:The circuit is a differential pair with single-ended output. It includes two NMOS transistors Q1 and Q2, a bias current source Ibias, and various capacitors and resistors. The input voltage is applied to the gate of Q1, and the output is taken from the drain of Q2. The circuit has a feedback mechanism through capacitors and voltage-controlled current sources to improve stability and performance.
image_name:(b)
description:This is a differential pair with a single-ended output, featuring two NMOS transistors, Q1 and Q2. The circuit includes resistors RS and RD, capacitors Cgdl, Cgs1, and Cgd2, and current sources Ibias, gm1Vgs1, and gm2Vgs2. The output is taken from the drain of Q2, and the circuit is biased with a current source Ibias. The circuit is designed to amplify small signals with a single-ended output.

Fig. 4.34 A differential pair with single-ended output: (a) complete circuit; (b) small-signal equivalent.

The first pole frequency due to the time constant at the gate of $Q_{1}$ is given by

$$
\begin{equation*}
\omega_{\mathrm{p} 1}=\frac{1}{\mathrm{R}_{\mathrm{s}}\left(\frac{\mathrm{C}_{\mathrm{gs}}}{2}+\mathrm{C}_{\mathrm{gd} 1}\right)} \tag{4.227}
\end{equation*}
$$

Note that there is no Miller-multiplication term (i.e., $1+A_{0}$ ) multiplying the capacitance $C_{\text {gdl }}$. For this reason, the compound stage is must faster than a common-source stage, although it has similar gain.

### 4.5.4 Differential Pair with Active Load

We next consider the high-frequency analysis of a MOS differential pair with an active current-mirror load. Described first in Section 3.8 and shown in Fig. 3.19, this stage is often used as the input to a classic two-stage
image_name:Fig. 4.35
description:
[
name: Rs, type: Resistor, value: Rs, ports: {N1: Vin, N2: Vgs}
name: 2rs, type: Resistor, value: 2rs, ports: {N1: Vgs, N2: GND}
name: Cgs/2, type: Capacitor, value: Cgs/2, ports: {Np: Vgs, Nn: GND}
name: Cgd1, type: Capacitor, value: Cgd1, ports: {Np: Vg1, Nn: GND}
name: gmVg1/2, type: VoltageControlledCurrentSource, ports: {Np: GND, Nn: Vg1}
name: gmVg1/2, type: VoltageControlledCurrentSource, ports: {Np: GND, Nn: Vout}
name: Cgd2, type: Capacitor, value: Cgd2, ports: {Np: Vout, Nn: GND}
name: RD, type: Resistor, value: RD, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit is a simplified small-signal model of a differential-input amplifier with an active load. It includes resistors, capacitors, and voltage-controlled current sources to model the behavior of the amplifier at high frequencies.

Fig. 4.35 A simplified and equivalent small-signal model of the amplifier of Fig. 4.34.
image_name:Fig. 4.36
description:
[
name: Rs, type: Resistor, value: Rs, ports: {N1: Vin, N2: Vg1}
name: Cgs, type: Capacitor, value: Cgs/2, ports: {Np: Vg1, Nn: GND}
name: Cgd1, type: Capacitor, value: Cgd1, ports: {Np: Vg1, Nn: GND}
name: g_m*Vg1/2, type: VoltageSource, value: g_m*Vg1/2, ports: {Np: Vout, Nn: GND}
name: Cgd2, type: Capacitor, value: Cgd2, ports: {Np: Vout, Nn: GND}
name: Rd, type: Resistor, value: Rd, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit represents a further simplified small-signal model of a differential-input amplifier. It includes resistors, capacitors, and a voltage-controlled current source to model the amplifier's behavior at high frequencies. The model is designed to analyze the amplifier's response, especially when driving a significant capacitive load.

Fig. 4.36 A further simplified small-signal model of the amplifier of Fig. 4.34.
image_name:Fig. 4.37
description:
[
name: g_m1*V_in, type: VoltageControlledCurrentSource, value: g_m1V_in, ports: {Np: Vout, Nn: GND}
name: r_out, type: Resistor, value: r_out, ports: {N1: Vout, N2: GND}
name: C_L, type: Capacitor, value: C_L, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is a small-signal model of a differential-input amplifier driving a capacitive load. It includes a voltage-controlled current source, a resistor, and a capacitor, modeling the amplifier's behavior at high frequencies.

Fig. 4.37 A small-signal model for the differential-input amplifier.
operational amplifier circuit. In that case, it drives a significant capacitive load, $\mathrm{C}_{\mathrm{L}}$. Assuming that load is dominant, we can easily modify the low-frequency small-signal analysis of this circuit performed in Section 3.8 by substituting $r_{\text {out }}$ with $z_{\text {out }}$,

$$
\begin{equation*}
A_{v}=\frac{v_{\text {out }}}{v_{\text {in }}}=g_{m 1} z_{\text {out }} \tag{4.228}
\end{equation*}
$$

where $Z_{\text {out }}=r_{\text {out }} \| 1 /\left(s \mathrm{C}_{\mathrm{L}}\right)$. Thus, for this differential stage, the very simple model shown in Fig. 4.37 is commonly used. This model implicitly assumes that only the capacitance at the output node is significant and the parasitic capacitances at the node at the sources of $Q_{1,2}$ and the node at the gates of $Q_{3,4}$ may be ignored. This assumption is usually justified, because the small-signal resistance at the output node, $r_{\text {out }}$, is much larger than the small-signal resistances at the other nodes which are generally $\approx 1 / \mathrm{g}_{\mathrm{m}}$. Also, the capacitance at the output node, $\mathrm{C}_{\mathrm{L}}$, is usually larger than the parasitic capacitances at the other nodes. Hence, the time-constant associated with the other capacitances will be much smaller than the time-constant associated with $C_{\llcorner }$and the -3 dB bandwidth is well approximated by

$$
\begin{equation*}
\omega_{-3 \mathrm{~dB}} \cong \frac{1}{r_{\text {out }} C_{\mathrm{L}}}=\frac{1}{\left(r_{\mathrm{ds} 2} \| r_{\mathrm{ds} 4}\right) C_{\mathrm{L}}} \tag{4.229}
\end{equation*}
$$

However, when high-frequency effects are important (which may be the case when compensating an opamp to guarantee stability), then this assumption may not be justified.

## 4.6 KEY POINTS

- The transfer functions in analog circuits throughout this text: a) are rational with $m \leq n$ b) have real-valued coefficients, $a_{i}$ and $b_{i} c$ ) have poles and zeros that are either real or appear in complex-conjugate pairs. Furthermore, if the system is stable, $d$ ) all denominator coefficients $b_{i}>0$ e) the real part of all poles will be negative. [p. 145]
- When a linear circuit is excited with a sinusoid, the output will be a sinusoid at the same frequency. Its magnitude will equal to the input magnitude multiplied by the magnitude response $\mathrm{IH}\left(\omega_{\text {in }}\right) \mid$. The phase difference between the output and input sinusoids will equal the phase response $\angle \mathrm{H}\left(\omega_{\text {in }}\right)$. Magnitude responses are often expressed in units of decibels, $20 \log _{10} 1 \mathrm{H}(\omega) \mid \mathrm{dB}$. [p. 146]
- For a first-order lowpass transfer function with dc gain $\mathrm{A}_{0} \gg>1$, the unity gain frequency is $\omega_{\mathrm{ta}} \approx \mathrm{A}_{0} \omega_{-3 \mathrm{~dB}}$ and $\angle A\left(\omega_{\text {ta }}\right) \approx 90^{\circ}$. [p. 154]
- Transfer functions with only real-valued poles and numerator order zero have monotonically decreasing magnitude and phase response plots with each pole contributing an additional $-20 \mathrm{~dB} /$ decade slope in the magnitude response, and an additional $-90^{\circ}$ phase shift. [p. 157]
- When a circuit has one or more capacitors with relatively very large value, one may consider those capacitors short-circuited to see how the circuit behaves at higher frequencies. Similarly, when one or more capacitors have relatively very small value, the circuit may be considered with those capacitors open-circuited to understand its operation at lower frequencies. [p. 161]
- The frequency-response of the common-source amplifier has 2 poles and 1 zero. The complexity of the analysis illustrates the importance of making approximations and simplifications in the high-frequency analysis of analog circuits. [p. 169]
- When a capacitor connects the input and output of a high-gain inverting amplifier, it appears much larger at the input than it really is. This Miller effect is often responsible for the dominant pole of such amplifiers and, hence, is useful for obtaining a quick estimate of bandwidth. [p. 172]
- The method of zero-value time-constants estimates the dominant pole and, hence, bandwidth of complex circuits by analyzing several simpler circuits at dc. [p. 173]
- All small-signal capacitances in the common-gate amplifier are (small-signal) grounded. Hence there is no Miller effect and it can provide high-frequency performance superior to that of the common-source amplifier, although with much lower input resistance. [p. 181]
- The cascode gain stage uses a common-gate transistor $Q_{2}$ to reduce the $V_{D S}$ variations on a common-source transistor $Q_{1}$. The result is high output resistance providing potentially high gain, a reduced Miller effect, and reduced short-channel effects. However, the available output voltage swing is reduced. [p. 182]
- The unity-gain frequency of any feedback amplifier that uses a cascode gain stage with a dominant output pole is limited by the unity-gain frequency of the cascode transistor, $\mathrm{Q}_{2}$. [p. 187]
- Source follower circuits can exhibit large amounts of overshoot and ringing under certain conditions. When designing source-followers, the recommended procedure is to check to see if the poles are complex using either (4.203) or a SPICE transient analysis to look for overshoot. When the poles are complex, then increase the load and/or input capacitor or, alternatively, add the compensating network shown in Fig. 4.30. [p. 192]
- The analysis of a symmetric differential pair may be simplified to that of the half-circuit, which is simply a com-mon-source amplifier. [p. 194]
