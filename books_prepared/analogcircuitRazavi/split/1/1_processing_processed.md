# Introduction to Microelectronics

Over the past five decades, microelectronics has revolutionized our lives. While beyond the realm of possibility a few decades ago, cellphones, digital cameras, laptop computers, and many other electronic products have now become an integral part of our daily affairs.

Learning microelectronics can be fun. As we learn how each device operates, how devices comprise circuits that perform interesting and useful functions, and how circuits form sophisticated systems, we begin to see the beauty of microelectronics and appreciate the reasons for its explosive growth.

This chapter gives an overview of microelectronics so as to provide a context for the material presented in this book. We introduce examples of microelectronic systems and identify important circuit "functions" that they employ. We also provide a review of basic circuit theory to refresh the reader's memory.

## 1.1 ELECTRONICS VERSUS MICROELECTRONICS

The general area of electronics began about a century ago and proved instrumental in the radio and radar communications used during the two world wars. Early systems incorporated "vacuum tubes," amplifying devices that operated with the flow of electrons between plates in a vacuum chamber. However, the finite lifetime and the large size of vacuum tubes motivated researchers to seek an electronic device with better properties.

The first transistor was invented in the 1940s and rapidly displaced vacuum tubes. It exhibited a very long (in principle, infinite) lifetime and occupied a much smaller volume (e.g., less than $1 \mathrm{~cm}^{3}$ in packaged form) than vacuum tubes did.

But it was not until 1960s that the field of microelectronics, i.e., the science of integrating many transistors on one chip, began. Early "integrated circuits" (ICs) contained only a handful of devices, but advances in the technology soon made it possible to dramatically increase the complexity of "microchips."

Example
1.1

Today's microprocessors contain about 100 million transistors in a chip area of approximately $3 \mathrm{~cm} \times 3 \mathrm{~cm}$. (The chip is a few hundred microns thick.) Suppose integrated circuits were not invented and we attempted to build a processor using 100 million "discrete" transistors. If each device occupies a volume of $3 \mathrm{~mm} \times 3 \mathrm{~mm} \times 3 \mathrm{~mm}$, determine the minimum volume for the processor. What other issues would arise in such an implementation?

Solution The minimum volume is given by $27 \mathrm{~mm}^{3} \times 10^{8}$, i.e., a cube 1.4 m on each side! Of course, the wires connecting the transistors would increase the volume substantially.

In addition to occupying a large volume, this discrete processor would be extremely slow; the signals would need to travel on wires as long as 1.4 m ! Furthermore, if each discrete transistor costs 1 cent and weighs 1 g , each processor unit would be priced at one million dollars and weigh 100 tons!

Exercise How much power would such a system consume if each transistor dissipates $10 \mu \mathrm{~W}$ ?

This book deals mostly with microelectronics while providing sufficient foundation for general (perhaps discrete) electronic systems as well.

## 1.2 EXAMPLES OF ELECTRONIC SYSTEMS

At this point, we introduce two examples of microelectronic systems and identify some of the important building blocks that we should study in basic electronics.

### 1.2.1 Cellular Telephone

Cellular telephones were developed in the 1980s and rapidly became popular in the 1990s. Today's cellphones contain a great deal of sophisticated analog and digital electronics that lie well beyond the scope of this book. But our objective here is to see how the concepts described in this book prove relevant to the operation of a cellphone.

Suppose you are speaking with a friend on your cellphone. Your voice is converted to an electric signal by a microphone and, after some processing, transmitted by the antenna. The signal produced by your antenna is picked up by your friend's receiver and, after some processing, applied to the speaker [Fig. 1.1(a)]. What goes on in these black boxes? Why are they needed?
image_name:Figure 1.1 (a)
description:The block diagram in Figure 1.1(a) represents a simplified view of a cellphone's operation during a call, illustrating both the transmission (TX) and reception (RX) paths.

1. **Main Components:**
- **Microphone:** Converts the speaker's voice into an electrical signal.
- **Transmitter (TX) Block:** This is an unspecified processing block (indicated by a question mark) that processes the electrical signal from the microphone before sending it to the antenna.
- **Antenna (TX):** Transmits the processed electrical signal as electromagnetic waves.
- **Antenna (RX):** Receives electromagnetic waves from the other end and converts them back to an electrical signal.
- **Receiver (RX) Block:** Another unspecified processing block that processes the received electrical signal before sending it to the speaker.
- **Speaker:** Converts the processed electrical signal back into sound.

2. **Flow of Information or Control:**
- The flow begins at the microphone, where the voice is converted to an electrical signal. This signal is then processed by the transmitter block.
- The processed signal is sent to the TX antenna, which transmits it as electromagnetic waves.
- These electromagnetic waves are received by the RX antenna of the receiving cellphone.
- The RX antenna converts the electromagnetic waves back into an electrical signal, which is then processed by the receiver block.
- Finally, the processed signal is sent to the speaker, converting it back into audible sound.

3. **Labels, Annotations, and Key Indicators:**
- The diagram includes labels for the microphone, speaker, transmitter, receiver, and antennas, clearly indicating the path of signal flow from the microphone to the speaker.
- The question marks in the transmitter and receiver blocks suggest unspecified processing, which typically involves modulation, amplification, filtering, and demodulation.

4. **Overall System Function:**
- The primary function of this system is to facilitate voice communication between two parties using cellphones. The arrangement of components ensures that voice signals are efficiently converted to and from electromagnetic waves, allowing for wireless communication over distances.
image_name:Figure 1.1 (b)
description:The diagram titled "Figure 1.1 (b)" presents a simplified representation of the transmit and receive paths in a cellphone communication system. This version omits the detailed processing blocks seen in more complex systems, focusing instead on the fundamental components necessary for basic operation.

1. **Main Components:**
- **Microphone:** This component captures the user's voice and converts it into an electrical signal. It is the starting point of the transmission path.
- **Antenna (Transmitter):** The antenna is responsible for converting the electrical signal from the microphone into electromagnetic waves, which are then transmitted through the air.
- **Antenna (Receiver):** This antenna receives electromagnetic waves from the transmitting antenna. It converts the electromagnetic waves back into an electrical signal.
- **Speaker:** The speaker takes the electrical signal from the receiving antenna and converts it back into sound, allowing the listener to hear the transmitted voice.

2. **Flow of Information or Control:**
- The flow begins at the microphone, where the voice is converted to an electrical signal. This signal is sent to the transmitting antenna, which radiates it as electromagnetic waves.
- These waves travel through the air to the receiving antenna, which captures them and converts them back into an electrical signal.
- The signal is then directed to the speaker, which converts it into sound.

3. **Labels, Annotations, and Key Indicators:**
- The diagram uses arrows to indicate the direction of signal flow, moving from the microphone to the transmitting antenna, through the air to the receiving antenna, and finally to the speaker.
- The absence of any processing blocks between these components highlights the simplicity of the system, focusing purely on the conversion and transmission of signals.

4. **Overall System Function:**
- The primary function of this simplified system is to transmit voice from one point to another using electromagnetic waves. By illustrating only the essential components (microphone, antennas, and speaker), the diagram emphasizes the basic process of voice capture, transmission, reception, and playback without detailing the complex processing that typically occurs in a cellphone.

Figure 1.1 (a) Simplified view of a cellphone, (b) further simplification of transmit and receive paths.

Let us attempt to omit the black boxes and construct the simple system shown in Fig. 1.1(b). How well does this system work? We make two observations. First, our voice contains frequencies from 20 Hz to 20 kHz (called the "voice band"). Second, for an antenna to operate efficiently, i.e., to convert most of the electrical signal to electromagnetic radiation, its dimension must be a significant fraction (e.g., $25 \%$ ) of the wavelength. Unfortunately, a frequency range of 20 Hz to 20 kHz translates to a wavelength ${ }^{1}$ of $1.5 \times 10^{7}$ m to $1.5 \times 10^{4} \mathrm{~m}$, requiring gigantic antennas for each cellphone. Conversely, to obtain a reasonable antenna length, e.g., 5 cm , the wavelength must be around 20 cm and the frequency around 1.5 GHz .

How do we "convert" the voice band to a gigahertz center frequency? One possible approach is to multiply the voice signal, $x(t)$, by a sinusoid, $A \cos \left(2 \pi f_{c} t\right)$ [Fig. 1.2(a)]. Since multiplication in the time domain corresponds to convolution in the frequency domain, and since the spectrum of the sinusoid consists of two impulses at $\pm f_{c}$, the voice spectrum is simply shifted (translated) to $\pm f_{c}$ [Fig. 1.2(b)]. Thus, if $f_{c}=1 \mathrm{GHz}$, the output occupies a bandwidth of 40 kHz centered at 1 GHz . This operation is an example of "amplitude modulation." ${ }^{2}$
image_name:(a)
description:The diagram labeled "(a)" illustrates the process of amplitude modulation by showing the multiplication of a voice signal with a sinusoidal carrier signal.

1. **Main Components:**
- **Voice Signal, $x(t)$:** This is the input signal, a time-domain waveform representing the original audio or voice data.
- **Sinusoidal Carrier, $A \cos(2\pi f_{c} t)$:** A cosine wave with amplitude $A$ and frequency $f_c$ that acts as the carrier signal.
- **Output Waveform:** The result of multiplying the voice signal by the sinusoidal carrier, depicted as a modulated waveform.

2. **Flow of Information:**
- The voice signal $x(t)$ and the sinusoidal carrier $A \cos(2\pi f_{c} t)$ are inputs to a multiplier block.
- These signals are multiplied together, resulting in the output waveform, which is the amplitude-modulated signal.

3. **Labels and Annotations:**
- The voice signal is labeled as $x(t)$, and the carrier signal is labeled as $A \cos(2\pi f_{c} t)$.
- The output waveform is shown as a modulated signal, indicating the effect of the multiplication process.

4. **Overall System Function:**
- The primary function of this system is to perform amplitude modulation, where the voice signal is modulated by the carrier frequency. This process shifts the frequency spectrum of the voice signal to be centered around the carrier frequency $f_c$, allowing it to be transmitted over radio frequencies. The resulting output waveform has the same frequency content as the original voice signal but is now centered at the carrier frequency, ready for transmission.
image_name:(b)
description:The graph labeled as (b) illustrates the frequency domain representation of amplitude modulation. It consists of three main parts:

1. **Voice Spectrum (X(f))**:
- **Type**: Frequency spectrum graph.
- **Axes**: The horizontal axis represents frequency (f) in hertz, ranging from -20 kHz to +20 kHz. The vertical axis represents amplitude, but no specific units are provided.
- **Behavior**: The voice spectrum is centered around 0 Hz, showing a bandwidth of 40 kHz. It has a symmetrical shape about the vertical axis, indicating the baseband frequency components of the voice signal.

2. **Spectrum of Cosine**:
- **Type**: Impulse spectrum.
- **Axes**: The horizontal axis represents frequency (f) in hertz, with impulses at -f_c and +f_c.
- **Key Features**: Two impulses are present at the carrier frequencies -f_c and +f_c, where f_c is the carrier frequency.

3. **Output Spectrum**:
- **Type**: Frequency spectrum graph.
- **Axes**: The horizontal axis represents frequency (f) in hertz, with marked points at -f_c, 0, and +f_c. The vertical axis represents amplitude.
- **Behavior**: The output spectrum shows two shifted versions of the original voice spectrum, centered at -f_c and +f_c, as a result of the modulation process. This indicates that the voice signal has been translated in frequency by the carrier frequency, creating sidebands around the carrier frequencies.

**Overall Description**:
The graph demonstrates how multiplying a voice signal by a sinusoidal carrier in the time domain results in the convolution of their spectra in the frequency domain. The voice spectrum, originally centered around 0 Hz, is shifted to new frequencies centered at -f_c and +f_c, corresponding to the carrier frequency. This operation effectively translates the voice signal to a higher frequency band, a key aspect of amplitude modulation.

Figure 1.2 (a) Multiplication of a voice signal by a sinusoid, (b) equivalent operation in the frequency domain.

We therefore postulate that the black box in the transmitter of Fig. 1.1(a) contains a multiplier, ${ }^{3}$ as depicted in Fig. 1.3(a). But two other issues arise. First, the cellphone must deliver a relatively large voltage swing (e.g., $20 \mathrm{~V}_{p p}$ ) to the antenna so that the radiated power can reach across distances of several kilometers, thereby requiring a "power amplifier" between the multiplier and the antenna. Second, the sinusoid, $A \cos 2 \pi f_{c} t$, must be produced by an "oscillator." We thus arrive at the transmitter architecture shown in Fig. 1.3(b).

[^0]image_name:(a)
description:The block diagram labeled as Fig. 1.3(a) represents a simple transmitter system used in communication devices like cellphones. This system consists of the following main components:

1. **Data Source (D):** This block represents the input data signal that needs to be transmitted. It is typically a low-frequency signal that contains the information to be sent.

2. **Multiplier (Mixer):** The data signal from the data source is fed into a multiplier. The multiplier's function is to combine the input data signal with a high-frequency carrier signal. This process is known as modulation.

3. **Carrier Signal:** The carrier signal is represented by the notation \( A \cos(2\pi f_c t) \), where \( A \) is the amplitude, and \( f_c \) is the carrier frequency. This sinusoidal signal is necessary for transmitting the data over long distances.

4. **Antenna:** After modulation, the combined signal is sent to the antenna. The antenna's role is to radiate the modulated signal into space as electromagnetic waves.

**Flow of Information:**
- The data signal from the data source is input into the multiplier.
- Simultaneously, the carrier signal \( A \cos(2\pi f_c t) \) is also input into the multiplier.
- The multiplier outputs a modulated signal, which is a combination of the data signal and the carrier signal.
- This modulated signal is then sent to the antenna, which transmits it as radio waves.

**Overall System Function:**
The primary function of this simple transmitter is to modulate a data signal with a high-frequency carrier signal and transmit it via an antenna. This allows the data to be sent over long distances, which is essential for communication systems such as cellphones. The simple architecture involves basic modulation and transmission without additional amplification or filtering stages.
image_name:(b)
description:The transmitter architecture shown in Fig. 1.3(b) is a more complete representation of a cellphone transmitter system. It consists of the following main components:

1. **Data Source (D):** This is the initial block where the input signal originates. It represents the digital or analog data intended for transmission.

2. **Mixer (Multiplier):** The data signal is fed into a mixer, which is responsible for combining the input signal with a carrier signal. The carrier signal is a sinusoidal waveform generated by the oscillator.

3. **Oscillator:** This component produces a sinusoidal signal, denoted as \( A \cos(2\pi f_c t) \), which serves as the carrier frequency for modulation. The oscillator is connected to the mixer and provides the necessary frequency to shift the data signal to the desired transmission frequency.

4. **Power Amplifier:** After modulation, the signal is passed through a power amplifier. The role of the power amplifier is to increase the amplitude of the signal, allowing it to be transmitted over long distances. This is crucial for ensuring that the signal can reach the intended receiver with sufficient strength.

5. **Antenna:** The amplified signal is then sent to the antenna, which radiates the electromagnetic waves into the air for transmission.

**Flow of Information:**
- The data signal from the source is first mixed with the carrier signal from the oscillator in the mixer block. This process modulates the data onto the carrier frequency.
- The modulated signal is then amplified by the power amplifier to achieve the required transmission power level.
- Finally, the amplified signal is transmitted through the antenna.

**Overall System Function:**
The primary function of this transmitter architecture is to modulate a data signal onto a higher frequency carrier, amplify it, and transmit it via an antenna. This ensures that the signal can travel over long distances to reach a receiver, which will demodulate and process the signal for the end-user. The inclusion of the oscillator and power amplifier makes this system capable of handling the requirements of real-world wireless communication, such as that used in cellphones.

Figure 1.3 (a) Simple transmitter, (b) more complete transmitter.

Let us now turn our attention to the receive path of the cellphone, beginning with the simple realization illustrated in Fig. 1.1(b). Unfortunately, this topology fails to operate with the principle of modulation: if the signal received by the antenna resides around a gigahertz center frequency, the audio speaker cannot produce meaningful information. In other words, a means of translating the spectrum back to zero center frequency is necessary. For example, as depicted in Fig. 1.4(a), multiplication by a sinusoid, $A \cos \left(2 \pi f_{c} t\right)$, translates the spectrum to left and right by $f_{c}$, restoring the original voice band. The newly-generated components at $\pm 2 f_{c}$ can be removed by a low-pass filter. We thus arrive at the receiver topology shown in Fig. 1.4(b).
image_name:(a)
description:The diagram labeled as (a) illustrates the translation of a modulated signal to a zero-center frequency, crucial for signal processing in communication systems. This is depicted through three distinct spectra: the Received Spectrum, the Spectrum of Cosine, and the Output Spectrum.

1. **Type of Graph and Function:**
- This is a frequency domain representation showing the spectral translation of signals.

2. **Axes Labels and Units:**
- The horizontal axis represents frequency \( f \), marked with significant points at \(-f_c\), \(0\), \(+f_c\), \(-2f_c\), and \(+2f_c\). There are no specific units marked, but frequency is typically measured in hertz (Hz).

3. **Overall Behavior and Trends:**
- The Received Spectrum shows two main lobes centered around \(-f_c\) and \(+f_c\). The Spectrum of Cosine is represented by two delta functions at \(-f_c\) and \(+f_c\), indicating the frequency components of the cosine wave used for mixing.
- The Output Spectrum results from the multiplication of the Received Spectrum with the Spectrum of Cosine, showing three sets of lobes centered at \(-2f_c\), \(0\), and \(+2f_c\). This indicates the translation of the spectrum to a zero-center frequency and the generation of additional components at \(\pm 2f_c\).

4. **Key Features and Technical Details:**
- The Received Spectrum is the initial modulated signal with its frequency components shifted by \(f_c\).
- The Spectrum of Cosine is used to mix with the Received Spectrum, effectively shifting the frequency components.
- The Output Spectrum shows that the original voice band is restored at zero frequency, while new components appear at \(\pm 2f_c\), which can be removed by a low-pass filter.

5. **Annotations and Specific Data Points:**
- The diagram uses dotted lines to indicate the center of each spectral component.
- The arrows in the Spectrum of Cosine highlight the points of frequency translation.

This diagram effectively demonstrates the process of frequency translation in signal processing, illustrating how a modulated signal can be shifted back to its original baseband frequency using a mixing technique with a cosine wave.
image_name:(b)
description:The system block diagram labeled (b) represents a simple receiver topology for processing a modulated signal received by an antenna. The primary components and their functions are as follows:

1. **Antenna**: This is the initial input point for the system, receiving the modulated radio frequency signals from the environment.

2. **Mixer**: The received signal from the antenna is fed into a mixer. The mixer combines the incoming signal with a sinusoidal signal generated by an oscillator. This process translates the frequency of the signal down, centering it at zero frequency, which is necessary for further processing.

3. **Oscillator**: This component generates a sinusoidal signal at a specified frequency. The frequency of this signal is used to mix with the incoming signal, effectively shifting its spectrum. This is a critical step for demodulating the signal.

4. **Low-Pass Filter**: After mixing, the signal is passed through a low-pass filter. The filter removes high-frequency components generated during mixing, specifically the components at twice the oscillator frequency (±2f_c), isolating the desired baseband signal.

5. **Speaker**: The filtered signal is finally sent to the speaker, which converts the electrical signal back into sound waves, allowing for audio output.

**Flow of Information**:
- The signal flow begins at the antenna, moves through the mixer where it is combined with the oscillator signal, and then passes through the low-pass filter. The output of the filter is sent directly to the speaker.

**Overall System Function**:
- The primary function of this receiver topology is to demodulate a received modulated signal and convert it into an audio signal that can be output through a speaker. The arrangement of components effectively translates the received spectrum to a baseband signal, filters out unwanted frequencies, and provides an audio output.
image_name:(c)
description:The system block diagram labeled (c) represents a more complete receiver topology designed to process and amplify weak signals received by an antenna.

1. **Main Components:**
- **Antenna:** Captures the incoming radio frequency signals.
- **Low-Noise Amplifier (LNA):** The first component after the antenna, which amplifies the weak received signals with minimal added noise, improving the signal-to-noise ratio.
- **Mixer:** Combines the amplified signal with a locally generated signal from an oscillator to translate the frequency of the incoming signal.
- **Oscillator:** Generates a sinusoidal signal used by the mixer to shift the frequency of the received signal.
- **Low-Pass Filter:** Removes unwanted high-frequency components generated during the mixing process, allowing only the desired baseband or low-frequency signal to pass through.
- **Amplifier:** Further amplifies the filtered signal to a level suitable for driving an audio speaker.
- **Speaker:** Converts the electrical signals back into sound for the user to hear.

2. **Flow of Information or Control:**
- The signal flow begins at the antenna, where the incoming radio frequency signals are captured and sent to the Low-Noise Amplifier.
- The amplified signal from the LNA is then fed into the mixer.
- Simultaneously, the oscillator provides a local frequency signal to the mixer.
- The mixer outputs a signal that is a combination of the input signal and the oscillator's frequency, effectively shifting the frequency of the input signal.
- This mixed signal is passed through the low-pass filter, which removes high-frequency noise and retains the baseband signal.
- The filtered signal is then amplified by the amplifier to a level sufficient for sound reproduction.
- Finally, the amplified signal drives the speaker, producing audible sound.

3. **Labels, Annotations, and Key Indicators:**
- The diagram labels each component clearly, indicating their function (e.g., "Low-Noise Amplifier," "Oscillator," "Low-Pass Filter," "Amplifier").
- The flow of the signal is indicated by arrows pointing from one block to the next, showing the direction of signal processing.

4. **Overall System Function:**
- The primary function of this receiver system is to capture weak radio frequency signals, amplify them, translate their frequency to a baseband signal, and finally convert them into audible sound. The arrangement of components ensures that the signal is amplified with minimal noise and filtered to remove unwanted frequencies, resulting in a clear audio output suitable for listening.

Figure 1.4 (a) Translation of modulated signal to zero center frequency, (b) simple receiver, (b) more complete receiver.

Our receiver design is still incomplete. The signal received by the antenna can be as low as a few tens of microvolts whereas the speaker may require swings of several tens
or hundreds of millivolts. That is, the receiver must provide a great deal of amplification ("gain") between the antenna and the speaker. Furthermore, since multipliers typically suffer from a high "noise" and hence corrupt the received signal, a "low-noise amplifier" must precede the multiplier. The overall architecture is depicted in Fig. 1.4(c).

Today's cellphones are much more sophisticated than the topologies developed above. For example, the voice signal in the transmitter and the receiver is applied to a digital signal processor (DSP) to improve the quality and efficiency of the communication. Nonetheless, our study reveals some of the fundamental building blocks of cellphones, e.g., amplifiers, oscillators, and filters, with the last two also utilizing amplification. We therefore devote a great deal of effort to the analysis and design of amplifiers.

Having seen the necessity of amplifiers, oscillators, and multipliers in both transmit and receive paths of a cellphone, the reader may wonder if "this is old stuff" and rather trivial compared to the state of the art. Interestingly, these building blocks still remain among the most challenging circuits in communication systems. This is because the design entails critical trade-offs between speed (gigahertz center frequencies), noise, power dissipation (i.e., battery lifetime), weight, cost (i.e., price of a cellphone), and many other parameters. In the competitive world of cellphone manufacturing, a given design is never "good enough" and the engineers are forced to further push the above trade-offs in each new generation of the product.

### 1.2.2 Digital Camera

Another consumer product that, by virtue of "going electronic," has dramatically changed our habits and routines is the digital camera. With traditional cameras, we received no immediate feedback on the quality of the picture that was taken, we were very careful in selecting and shooting scenes to avoid wasting frames, we needed to carry bulky rolls of film, and we would obtain the final result only in printed form. With digital cameras, on the other hand, we have resolved these issues and enjoy many other features that only electronic processing can provide, e.g., transmission of pictures through cellphones or ability to retouch or alter pictures by computers. In this section, we study the operation of the digital camera.

The "front end" of the camera must convert light to electricity, a task performed by an array (matrix) of "pixels." ${ }^{4}$ Each pixel consists of an electronic device (a "photodiode") that produces a current proportional to the intensity of the light that it receives. As illustrated in Fig. 1.5(a), this current flows through a capacitance, $C_{L}$, for a certain period of time, thereby developing a proportional voltage across it. Each pixel thus provides a voltage proportional to the "local" light density.

Now consider a camera with, say, 6.25 million pixels arranged in a $2500 \times 2500$ array [Fig. 1.5(b)]. How is the output voltage of each pixel sensed and processed? If each pixel contains its own electronic circuitry, the overall array occupies a very large area, raising the cost and the power dissipation considerably. We must therefore "time-share" the signal processing circuits among pixels. To this end, we follow the circuit of Fig. 1.5(a) with a simple, compact amplifier and a switch (within the pixel) [Fig. 1.5(c)]. Now, we connect a wire to the outputs of all 2500 pixels in a "column," turn on only one switch at a time, and apply the corresponding voltage to the "signal processing" block outside the column.
image_name:(a)
description:
[
name: D1, type: Diode, ports: {Na: Vout, Nc: GND}
name: CL, type: Capacitor, value: CL, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is a photodiode setup where a diode D1 is connected between Vout and GND. The capacitor CL is connected in parallel to the diode to stabilize the output voltage Vout when the photodiode is exposed to light.

(a)
image_name:(b)
description:The system block diagram labeled as "(b)" represents an array of pixels in a digital camera, specifically illustrating a 2500 by 2500 grid. This grid is part of the camera's sensor array, where each pixel is designed to capture light and convert it into an electrical signal.

**Main Components:**
- **Photodiodes:** Each pixel in the array contains a photodiode, which is responsible for converting incoming light into an electrical signal. The diagram shows several photodiodes arranged in a grid pattern, symbolized by the diode symbols at the corners and repeated across the array.
- **Columns and Rows:** The array is organized into 2500 columns and 2500 rows, indicating a total of 6,250,000 pixels.

**Flow of Information or Control:**
- **Light Capture:** Incoming light, represented by wavy arrows, strikes the photodiodes. Each photodiode generates a voltage corresponding to the intensity of the light it receives.
- **Signal Processing:** Although not explicitly shown in this part of the diagram, each column of photodiodes would typically be connected to a signal processing block that reads the electrical signals and processes them into digital data.

**Labels, Annotations, and Key Indicators:**
- The diagram is labeled with "2500 Columns" and "2500 Rows," clearly indicating the size and structure of the pixel array.

**Overall System Function:**
- The primary function of this pixel array is to capture an image by converting light into electrical signals, which are then processed to form a digital representation of the scene. Each column's signals are handled by dedicated signal processing blocks, allowing for efficient and parallel processing of the image data. This setup is typical in digital cameras, where high-resolution image capture is required.

(b)
image_name:Amplifier
description:
[
name: A1, type: OpAmp, value: A1, ports: {In: In(A1), OutP: Out(A1), OutN: GND}
name: A2, type: OpAmp, value: A2, ports: {In: In(A2), OutP: Out(A2), OutN: GND}
name: A3, type: OpAmp, value: A3, ports: {In: In(A3), OutP: Out(A3), OutN: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: In(A1), Nn: GND}
name: C2, type: Capacitor, value: C2, ports: {Np: In(A2), Nn: GND}
name: C3, type: Capacitor, value: C3, ports: {Np: In(A3), Nn: GND}
name: D1, type: Diode, ports: {Na: In(A1), Nc: GND}
name: D2, type: Diode, ports: {Na: In(A2), Nc: GND}
name: D3, type: Diode, ports: {Na: In(A3), Nc: GND}
name: SW1, type: Switch, ports: {N1: Out(A1), N2: X1}
name: SW2, type: Switch, ports: {N1: Out(A2), N2: X1}
name: SW3, type: Switch, ports: {N1: Out(A3), N2: X1}
]
extrainfo:This is an amplifier circuit with multiple stages, each consisting of a diode, capacitor, op-amp, and switch. The output of each op-amp is connected through a switch to a common node X1, which leads to a signal processing block. The diodes and capacitors are used for input signal conditioning and stabilization.

(c)

Figure 1.5 (a) Operation of a photodiode, (b) array of pixels in a digital camera, (c) one column of the array.

The overall array consists of 2500 of such columns, with each column employing a dedicated signal processing block.

Example A digital camera is focused on a chess board. Sketch the voltage produced by one column 1.2 as a function of time.

Solution The pixels in each column receive light only from the white squares [Fig. 1.6(a)]. Thus, the column voltage alternates between a maximum for such pixels and zero for those receiving no light. The resulting waveform is shown in Fig. 1.6(b).
image_name:(a)
description:The image named "(a)" depicts a standard chess board pattern, consisting of an 8x8 grid of alternating black and white squares. Each square is of equal size, forming a checkerboard pattern. The chess board is framed by a thin black border, emphasizing the grid structure. This pattern is typically used in chess games, where each square alternates in color to help distinguish the positions occupied by chess pieces. In the context of the digital camera example, this image is used to illustrate how a camera sensor column would receive light from the white squares, producing a voltage waveform that alternates between a maximum value for the white squares and zero for the black squares, as these receive no light. This pattern is crucial for understanding the concept of light detection and signal processing in digital imaging systems.

(a)
image_name:(a)
description:The image depicts a schematic diagram representing a portion of a digital camera sensor's column signal processing. It illustrates how light detection from a chessboard pattern is converted into an electrical signal.

1. **Identification of Components and Structure:**
- **Diodes (D1, D2):** These are likely photodiodes that convert light into electrical current. Each diode is connected to ground (GND), indicating it is part of a light detection circuit.
- **Capacitors (C1, C2):** These are connected in parallel with the diodes, serving to store charge generated by the photodiodes.
- **Operational Amplifiers (A1, A2):** These amplifiers are used to increase the signal strength of the current generated by the diodes. The input to each amplifier is labeled (In(A1), In(A2)), and the output is labeled (Out(A1), Out(A2)).
- **Switches (SW1, SW2):** These switches control the flow of the amplified signal to the load. They are connected between the amplifier outputs and the load.
- **Load:** This is where the processed signal is directed. It is labeled as "LOAD" and connected to a node labeled "V_column," indicating the voltage signal corresponding to a column in the camera sensor.

2. **Connections and Interactions:**
- Each photodiode is connected to a capacitor, forming a basic light detection and storage circuit.
- The output from each photodiode-capacitor pair feeds into an operational amplifier, which boosts the signal.
- The amplified signal is then directed through a switch to the load, where it contributes to the overall column voltage (V_column).

3. **Labels, Annotations, and Key Features:**
- The diagram includes annotations for each component, such as D1, C1, A1, SW1, etc., to identify their function.
- The outputs of the amplifiers are labeled to indicate their role in producing the column voltage signal.
- The presence of multiple identical circuits (as indicated by the ellipsis) suggests a repetitive structure typical of a sensor array, where each circuit corresponds to a different column in the sensor grid.

This diagram effectively illustrates the process of converting light detected by a camera sensor into a digital signal, highlighting the role of each component in the signal processing chain.
image_name:(b)
description:
[
name: D1, type: Diode, ports: {Na: In(A1), Nc: GND}
name: D2, type: Diode, ports: {Na: In(A2), Nc: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: In(A1), Nn: GND}
name: C2, type: Capacitor, value: C2, ports: {Np: In(A2), Nn: GND}
name: A1, type: OpAmp, value: A1, ports: {InP: In(A1), InN: GND, Out: Out(A1)}
name: A2, type: OpAmp, value: A2, ports: {InP: In(A2), InN: GND, Out: Out(A2)}
name: SW1, type: Switch, ports: {N1: Out(A1), N2: LOAD}
name: SW2, type: Switch, ports: {N1: Out(A2), N2: LOAD}
name: LOAD, type: Other, ports: {N1: LOAD, N2: Vcolumn}
]
extrainfo:The circuit is a part of a signal processing system involving diodes, capacitors, op-amps, and switches. It processes input signals and switches them to a common load, possibly for multiplexing purposes. The diodes and capacitors are likely for rectification and filtering, while the op-amps amplify the signals. The switches control which amplified signal is sent to the load.

(b)
image_name:(b)
description:The graph shown is a time-domain waveform representing the voltage across a column, labeled as \( V_{\text{column}} \), against time, \( t \). The waveform is a square wave, characterized by a repetitive pattern of high and low voltage levels over time.

1. **Type of Graph and Function:**
- The graph is a time-domain waveform displaying a square wave pattern.

2. **Axes Labels and Units:**
- The vertical axis represents voltage, labeled as \( V_{\text{column}} \).
- The horizontal axis represents time, labeled as \( t \).
- Specific units are not provided, but the waveform suggests a binary-like signal switching between two discrete voltage levels.

3. **Overall Behavior and Trends:**
- The waveform exhibits a periodic square wave pattern, alternating between high and low states.
- The waveform maintains a consistent shape and period, indicating a stable and regular switching behavior.

4. **Key Features and Technical Details:**
- The waveform has sharp transitions between the high and low states, characteristic of digital signals or pulse waveforms.
- Each cycle consists of a high state followed by a low state, with equal durations for both states, suggesting a 50% duty cycle.
- The waveform implies a repetitive process, possibly indicative of a scanning or multiplexing operation in the context of signal processing.

5. **Annotations and Specific Data Points:**
- No specific numerical values or annotations are provided on the graph.
- The graph visually emphasizes the regularity and consistency of the waveform pattern, important for understanding the operation of the signal processing system described.

(c)

Figure 1.6 (a) Chess board captured by a digital camera, (b) voltage waveform of one column.

Exercise Plot the voltage if the first and second squares in each row have the same color.

What does each signal processing block do? Since the voltage produced by each pixel is an analog signal and can assume all values within a range, we must first "digitize" it by means of an "analog-to-digital converter" (ADC). A 6.25 megapixel array must thus incorporate 2500 ADCs. Since ADCs are relatively complex circuits, we may time-share one ADC between every two columns (Fig. 1.7), but requiring that the ADC operate twice as fast (why?). In the extreme case, we may employ a single, very fast ADC for all 2500 columns. In practice, the optimum choice lies between these two extremes.
image_name:Figure 1.7
description:
[
name: D1, type: Diode, ports: {Na: In(A1), Nc: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: In(A1), Nn: GND}
name: A1, type: OpAmp, value: A1, ports: {InP: In(A1), InN: GND, OutP: Out(A1), OutN: GND}
name: SW1, type: Switch, ports: {N1: Out(A1), N2: X1}
name: D2, type: Diode, ports: {Na: In(A2), Nc: GND}
name: C2, type: Capacitor, value: C2, ports: {Np: In(A2), Nn: GND}
name: A2, type: OpAmp, value: A2, ports: {InP: In(A2), InN: GND, OutP: Out(A2), OutN: GND}
name: SW2, type: Switch, ports: {N1: Out(A2), N2: X1}
name: D3, type: Diode, ports: {Na: In(A3), Nc: GND}
name: C3, type: Capacitor, value: C3, ports: {Np: In(A3), Nn: GND}
name: A3, type: OpAmp, value: A3, ports: {InP: In(A3), InN: GND, OutP: Out(A3), OutN: GND}
name: SW3, type: Switch, ports: {N1: Out(A3), N2: X2}
name: D4, type: Diode, ports: {Na: In(A4), Nc: GND}
name: C4, type: Capacitor, value: C4, ports: {Np: In(A4), Nn: GND}
name: A4, type: OpAmp, value: A4, ports: {InP: In(A4), InN: GND, OutP: Out(A4), OutN: GND}
name: SW4, type: Switch, ports: {N1: Out(A4), N2: X2}
]
extrainfo:The circuit diagram shows a configuration where each OpAmp (A1 to A4) is connected to a diode and capacitor, forming a basic signal processing unit. These units are connected to switches (SW1 to SW4) that direct the processed signals to nodes X1 and X2. The signals from X1 and X2 are then fed into an ADC, which digitizes the analog signals. This setup allows sharing one ADC between two columns of a pixel array, optimizing the use of ADCs by time-sharing.

Figure 1.7 Sharing one ADC between two columns of a pixel array.

Once in the digital domain, the "video" signal collected by the camera can be manipulated extensively. For example, to "zoom in," the digital signal processor (DSP) simply considers only a section of the array, discarding the information from the remaining pixels. Also, to reduce the required memory size, the processor "compresses" the video signal.

The digital camera exemplifies the extensive use of both analog and digital microelectronics. The analog functions include amplification, switching operations, and analog-todigital conversion, and the digital functions consist of subsequent signal processing and storage.

### 1.2.3 Analog Versus Digital

Amplifiers and ADCs are examples of analog functions, circuits that must process each point on a waveform (e.g., a voice signal) with great care to avoid effects such as noise and "distortion." By contrast, digital circuits deal with binary levels (ONEs and ZEROs) and, evidently, contain no analog functions. The reader may then say, "I have no intention of working for a cellphone or camera manufacturer and, therefore, need not learn about analog circuits." In fact, with digital communications, digital signal processors, and every other function becoming digital, is there any future for analog design?

Well, some of the assumptions in the above statements are incorrect. First, not every function can be realized digitally. The architectures of Figs. 1.3 and 1.4 must employ lownoise and low-power amplifiers, oscillators, and multipliers regardless of whether the actual communication is in analog or digital form. For example, a $20-\mu \mathrm{V}$ signal (analog or digital)
received by the antenna cannot be directly applied to a digital gate. Similarly, the video signal collectively captured by the pixels in a digital camera must be processed with low noise and distortion before it appears in the digital domain.

Second, digital circuits require analog expertise as the speed increases. Figure 1.8 exemplifies this point by illustrating two binary data waveforms, one at $100 \mathrm{Mb} / \mathrm{s}$ and another at $1 \mathrm{~Gb} / \mathrm{s}$. The finite risetime and falltime of the latter raises many issues in the operation of gates, flipflops, and other digital circuits, necessitating great attention to each point on the waveform.
image_name:Figure 1.8
description:Figure 1.8 illustrates two time-domain waveforms representing binary data signals at different data rates. The graph is divided into two sections, each depicting a waveform labeled as \( x_1(t) \) and \( x_2(t) \).

1. **Type of Graph and Function:**
- The graph shows time-domain waveforms of binary data signals.

2. **Axes Labels and Units:**
- The horizontal axis is labeled \( t \), representing time.
- The vertical axes are not explicitly labeled with units, but they represent signal amplitude or voltage levels.
- Time intervals are marked in nanoseconds (ns).

3. **Overall Behavior and Trends:**
- **\( x_1(t) \):** This waveform is a square wave with a clear, rectangular shape, having a high level for 10 nanoseconds and then returning to a low level, indicating a 100 Mb/s data rate.
- **\( x_2(t) \):** This waveform is more rounded, with a noticeable rise and fall time, and a pulse width of 1 nanosecond, indicating a 1 Gb/s data rate. The waveform shows smoother transitions compared to \( x_1(t) \), reflecting higher frequency components and potential issues with finite rise and fall times.

4. **Key Features and Technical Details:**
- **\( x_1(t) \):** The key feature is the sharp transition between high and low states, characteristic of lower frequency signals.
- **\( x_2(t) \):** The waveform has more gradual transitions, indicative of the finite rise and fall times that become significant at higher frequencies. This can affect the performance of digital circuits by introducing timing uncertainties.

5. **Annotations and Specific Data Points:**
- The 10 ns width for \( x_1(t) \) and 1 ns width for \( x_2(t) \) are annotated on the graph, highlighting the difference in data rates and the resulting waveform characteristics.

Overall, this figure highlights the challenges in digital circuit design as data rates increase, emphasizing the need for careful consideration of waveform shapes and transition times.

Figure 1.8 Data waveforms at $100 \mathrm{Mb} / \mathrm{s}$ and $1 \mathrm{~Gb} / \mathrm{s}$.

## 1.3 BASIC CONCEPTS*

Analysis of microelectronic circuits draws upon many concepts that are taught in basic courses on signals and systems and circuit theory. This section provides a brief review of these concepts so as to refresh the reader's memory and establish the terminology used throughout this book. The reader may first glance through this section to determine which topics need a review or simply return to this material as it becomes necessary later.

### 1.3.1 Analog and Digital Signals

An electric signal is a waveform that carries information. Signals that occur in nature can assume all values in a given range. Called "analog," such signals include voice, video, seismic, and music waveforms. Shown in Fig. 1.9(a), an analog voltage
image_name:(a)
description:The graph labeled as Figure 1.9(a) depicts an analog signal waveform, represented as a time-domain waveform. The horizontal axis is labeled as 't', indicating time, while the vertical axis is labeled as 'V(t)', representing voltage. The scale appears to be linear for both axes.

The waveform exhibits a continuous and smooth oscillatory pattern, characteristic of analog signals. It includes several peaks and valleys, with varying amplitudes and frequencies. The waveform starts with a negative peak, followed by a series of oscillations that gradually increase in amplitude, reaching a significant positive peak before decreasing again.

Key features of this waveform include multiple maxima and minima, indicating points of highest and lowest voltage values over time. There are also inflection points where the curvature of the waveform changes, contributing to the overall smoothness of the curve. The signal does not appear to have a fixed period, suggesting it may represent a complex or non-repetitive signal.

This graph provides a visual representation of how analog signals can vary continuously over time, capturing the essence of natural signals such as voice or music.
image_name:(b)
description:The graph labeled as "(b)" is a time-domain waveform illustrating the effect of noise on an analog signal. The x-axis represents time \( t \), while the y-axis represents the voltage \( V(t) + \text{Noise} \). Both axes appear to have linear scales, though specific units and numerical values are not provided.

**Overall Behavior and Trends:**
The waveform shows a highly erratic and jagged pattern, indicative of significant noise interference. Unlike a smooth analog signal, this waveform exhibits rapid fluctuations and irregular oscillations around the zero voltage line, suggesting a high level of distortion.

**Key Features and Technical Details:**
- The waveform does not maintain a consistent pattern, with frequent peaks and valleys occurring in quick succession.
- There are no apparent periodic patterns, implying that the noise is random and does not follow a regular cycle.
- The amplitude of fluctuations varies, with some peaks reaching higher voltages than others, but specific values are not marked.

**Annotations and Specific Data Points:**
- There are no specific annotations or markers on the graph to indicate key data points or reference lines.
- The graph is primarily qualitative, demonstrating the concept of noise rather than providing precise measurements.

This representation effectively conveys the disruptive impact of noise on an analog signal, making it difficult to discern the original waveform's characteristics.

Figure 1.9 (a) Analog signal, (b) effect of noise on analog signal.

[^1]waveform swings through a "continuum" of values and provides information at each instant of time.

While occurring all around us, analog signals are difficult to "process" due to sensitivities to such circuit imperfections as "noise" and "distortion." ${ }^{5}$ As an example, Figure 1.9(b) illustrates the effect of noise. Furthermore, analog signals are difficult to "store" because they require "analog memories" (e.g., capacitors).

By contrast, a digital signal assumes only a finite number of values at only certain points in time. Depicted in Fig. 1.10(a) is a "binary" waveform, which remains at only one of two levels for each period, $T$. So long as the two voltages corresponding to ONEs and ZEROs differ sufficiently, logical circuits sensing such a signal process it correctly-even if noise or distortion create some corruption [Fig. 1.10(b)]. We therefore consider digital signals more "robust" than their analog counterparts. The storage of binary signals (in a digital memory) is also much simpler.
image_name:(a)
description:1. **Type of Graph and Function:** The graph in Fig. 1.10(a) is a time-domain waveform representing a digital signal. It is a binary waveform, which means it alternates between two distinct voltage levels.

2. **Axes Labels and Units:** The horizontal axis is labeled as \( t \), representing time, while the vertical axis is labeled as \( V(t) \), representing voltage. The time axis is linear, and the waveform is periodic with a period denoted by \( T \).

3. **Overall Behavior and Trends:** The waveform exhibits a square wave pattern, alternating between two voltage levels labeled "ONE" and "ZERO." The signal remains at each level for one period \( T \) before switching to the other level, creating a rectangular shape. The waveform is consistent and periodic, indicating a stable digital signal.

4. **Key Features and Technical Details:** The key feature of this waveform is its binary nature, with distinct and stable voltage levels for "ONE" and "ZERO." The transitions between these levels are sharp and instantaneous, typical of digital signals. There are no intermediate levels or gradual changes, highlighting the robustness of the digital format.

5. **Annotations and Specific Data Points:** The graph includes annotations for "ONE" and "ZERO" levels, indicating the high and low voltage states, respectively. The period \( T \) is marked on the time axis, showing the duration for which each voltage level is maintained before switching.
image_name:(b)
description:The graph labeled "(b)" is a time-domain waveform depicting a digital signal affected by noise. The horizontal axis represents time \( t \), while the vertical axis represents voltage \( V(t) + \text{Noise} \). The waveform illustrates how noise can impact a digital signal, which ideally alternates between two distinct voltage levels representing binary ONEs and ZEROs.

1. **Type of Graph and Function:**
- This is a time-domain waveform showing the effect of noise on a digital signal.

2. **Axes Labels and Units:**
- The horizontal axis is labeled \( t \) for time, without specific units marked.
- The vertical axis is labeled \( V(t) + \text{Noise} \), indicating voltage with noise.

3. **Overall Behavior and Trends:**
- The waveform shows a noisy signal that fluctuates around a central level. The noise causes rapid, irregular oscillations around the ideal binary levels.
- Despite the noise, the underlying binary structure is still discernible, with the signal attempting to maintain periods of high (ONE) and low (ZERO) voltage levels.

4. **Key Features and Technical Details:**
- The noise introduces significant variability, causing the signal to deviate from its ideal square shape.
- There are no specific numerical values or scales provided, but the graph suggests that the noise might cause momentary misinterpretations of the signal’s intended binary state.

5. **Annotations and Specific Data Points:**
- There are no specific annotations or markers on this graph. However, the effect of noise is visually evident as it distorts the clean transitions between binary states.

Figure 1.10 (a) Digital signal, (b) effect of noise on digital signal.

The foregoing observations favor processing of signals in the digital domain, suggesting that inherently analog information must be converted to digital form as early as possible. Indeed, complex microelectronic systems such as digital cameras, camcorders, and compact disk (CD) recorders perform some analog processing, "analog-to-digital conversion," and digital processing (Fig. 1.11), with the first two functions playing a critical role in the quality of the signal.
image_name:Figure 1.11
description:The system block diagram in Figure 1.11 illustrates the process of signal handling in a typical microelectronic system, emphasizing the conversion and processing of analog signals into digital form. The diagram consists of three main components arranged sequentially:

1. **Analog Signal**: This is the input to the system, representing inherently analog information that needs to be processed. It serves as the starting point for the signal processing sequence.

2. **Analog Processing**: The first block in the sequence is responsible for initial processing of the analog signal. This may involve amplification, filtering, or other modifications to prepare the signal for conversion. The goal is to optimize the signal quality before it undergoes digitization.

3. **Analog-to-Digital Conversion**: This block converts the processed analog signal into a digital format. It is a critical step that allows the inherently analog information to be handled by digital systems. The conversion involves sampling the analog signal and quantizing it into discrete digital values.

4. **Digital Processing and Storage**: The final block in the sequence handles the digital signal. This stage involves further processing, manipulation, and storage of the digital data. It allows for complex operations and long-term retention of information in a digital format.

**Flow of Information**: The signal flows from left to right, starting as an analog signal, undergoing analog processing, then being converted to digital form, and finally processed and stored digitally. Each block is connected sequentially, indicating a linear flow of information without feedback loops.

**Overall System Function**: The primary function of this system is to efficiently convert and process analog signals into a digital format suitable for storage and further digital processing. This arrangement ensures that analog information is handled with high fidelity and is ready for complex digital manipulation and storage.

Figure 1.11 Signal processing in a typical system.

It is worth noting that many digital binary signals must be viewed and processed as analog waveforms. Consider, for example, the information stored on a hard disk in a computer. Upon retrieval, the "digital" data appears as a distorted waveform with only a few millivolts of amplitude (Fig. 1.12). Such a small separation between ONEs and ZEROs proves inadequate if this signal is to drive a logical gate, demanding a great deal of amplification and other analog processing before the data reaches a robust digital form.

[^2]image_name:Figure 1.12
description:The image depicts a schematic representation of a signal being retrieved from a hard disk. The hard disk is illustrated as a circular disk with a central hole, representing the typical structure of a hard disk drive. Above the disk, a read/write head is shown, positioned close to the surface of the disk, indicating the point where data is read.

To the right of the hard disk, a waveform is depicted. This waveform represents the analog signal picked up from the hard disk. The waveform is irregular and jagged, signifying distortion and noise that typically accompany the raw data read from the disk. The amplitude of this waveform is indicated to be approximately 3 millivolts, showing the small signal level that is retrieved.

The horizontal axis of the waveform is labeled with 't', representing time, which indicates that the waveform is a time-domain representation of the signal. The vertical double-headed arrow next to the waveform denotes the amplitude measurement of approximately 3 millivolts. This illustrates the challenge of processing such low-amplitude signals, necessitating amplification and further analog processing to convert the data into a usable digital form.

Figure 1.12 Signal picked up from a hard disk in a computer.

### 1.3.2 Analog Circuits

Today's microelectronic systems incorporate many analog functions. As exemplified by the cellphone and the digital camera studied above, analog circuits often limit the performance of the overall system.

The most commonly-used analog function is amplification. The signal received by a cellphone or picked up by a microphone proves too small to be processed further. An amplifier is therefore necessary to raise the signal swing to acceptable levels.

The performance of an amplifier is characterized by a number of parameters, e.g., gain, speed, and power dissipation. We study these aspects of amplification in great detail later in this book, but it is instructive to briefly review some of these concepts here.

A voltage amplifier produces an output swing greater than the input swing. The voltage gain, $A_{v}$, is defined as

$$
\begin{equation*}
A_{v}=\frac{v_{\text {out }}}{v_{\text {in }}} \tag{1.1}
\end{equation*}
$$

In some cases, we prefer to express the gain in decibels ( dB ):

$$
\begin{equation*}
\left.A_{v}\right|_{d B}=20 \log \frac{v_{\text {out }}}{v_{\text {in }}} \tag{1.2}
\end{equation*}
$$

For example, a voltage gain of 10 translates to 20 dB . The gain of typical amplifiers falls in the range of $10^{1}$ to $10^{5}$.

Example A cellphone receives a signal level of $20 \mu \mathrm{~V}$, but it must deliver a swing of 50 mV to the 1.3 speaker that reproduces the voice. Calculate the required voltage gain in decibels.

Solution We have

$$
\begin{align*}
A_{v} & =20 \log \frac{50 \mathrm{mV}}{20 \mu \mathrm{~V}}  \tag{1.3}\\
& \approx 68 \mathrm{~dB} . \tag{1.4}
\end{align*}
$$

Exercise What is the output swing if the gain is 50 dB ?

In order to operate properly and provide gain, an amplifier must draw power from a voltage source, e.g., a battery or a charger. Called the "power supply," this source is typically denoted by $V_{C C}$ or $V_{D D}$ [Fig. 1.13(a)]. In complex circuits, we may simplify the notation to that shown in Fig. 1.13(b), where the "ground" terminal signifies a reference point with zero potential. If the amplifier is simply denoted by a triangle, we may even omit the supply terminals [Fig. 1.13(c)], with the understanding that they are present. Typical amplifiers operate with supply voltages in the range of 1 V to 10 V .
image_name:(a)
description:
[
name: A1, type: OpAmp, value: A1, ports: {InP: Vin, InN: GND, OutP: Vout, OutN: , Vdd: VCC, -Vdd: GND}
name: VCC, type: VoltageSource, value: VCC, ports: {Np: VCC, Nn: GND}
]
extrainfo:The circuit diagram (a) shows an amplifier configuration with an operational amplifier A1 powered by a voltage source VCC. The input is labeled as Vin and the output as Vout. The circuit is grounded at GND.
image_name:(b)
description:
[
name: A1, type: OpAmp, value: A1, ports: {InP: Vin, InN: GND, OutP: Vout, OutN: , Vdd: VCC, -Vdd: GND}
name: VCC, type: VoltageSource, value: VCC, ports: {Np: VCC, Nn: GND}
]
extrainfo:The circuit diagram (b) shows a simplified amplifier with a power supply VCC and a ground connection. The amplifier is connected to an input Vin and produces an output Vout.
image_name:(c)
description:
[
name: A1, type: OpAmp, value: A1, ports: {InP: Vin, InN: , OutP: Vout, OutN:}
]
extrainfo:The diagram (c) shows a simplified amplifier circuit with an operational amplifier (A1) having an input at Vin and an output at Vout. The power supply connections are omitted for simplicity.

Figure 1.13 (a) General amplifier symbol along with its power supply, (b) simplified diagram of (a), (b) amplifier with supply rails omitted.

What limits the speed of amplifiers? We expect that various capacitances in the circuit begin to manifest themselves at high frequencies, thereby lowering the gain. In other words, as depicted in Fig. 1.14, the gain rolls off at sufficiently high frequencies, limiting the (usable) "bandwidth" of the circuit. Amplifiers (and other analog circuits) suffer from trade-offs between gain, speed and power dissipation. Today's microelectronic amplifiers achieve bandwidths as large as tens of gigahertz.
image_name:Figure 1.14
description:The graph in Figure 1.14 is a Bode plot illustrating the frequency response of an amplifier. The x-axis represents frequency, likely in hertz (Hz), and the y-axis represents amplifier gain, usually in decibels (dB). The plot uses a logarithmic scale for the frequency axis, which is typical for Bode plots.

Initially, the graph shows a flat region where the amplifier gain remains constant over a range of low to mid-range frequencies. This indicates that the amplifier maintains a consistent gain within this bandwidth. As the frequency increases, the plot exhibits a downward slope, indicating a roll-off in gain at higher frequencies. This roll-off is marked as the 'High-Frequency Roll-off,' signifying the point at which the gain begins to decrease significantly.

The roll-off is a critical feature of the amplifier's performance, as it defines the upper limit of the amplifier's bandwidth. This behavior is typical due to the inherent capacitances in the circuit, which become more pronounced at high frequencies, leading to reduced gain.

No specific numerical values or annotations are provided in the graph, such as the -3 dB point, which would commonly define the bandwidth limit. However, the general trend clearly demonstrates the trade-off between gain and frequency response, a fundamental characteristic in amplifier design.

Figure 1.14 Roll-off of an amplifier's gain at high frequencies.
What other analog functions are frequently used? A critical operation is "filtering." For example, an electrocardiograph measuring a patient's heart activities also picks up the $60-\mathrm{Hz}$ ( or $50-\mathrm{Hz}$ ) electrical line voltage because the patient's body acts as an antenna. Thus, a filter must suppress this "interferer" to allow meaningful measurement of the heart.

### 1.3.3 Digital Circuits

More than $80 \%$ of the microelectronics industry deals with digital circuits. Examples include microprocessors, static and dynamic memories, and digital signal processors. Recall from basic logic design that gates form "combinational" circuits, and latches and flipflops constitute "sequential" machines. The complexity, speed, and power dissipation of these building blocks play a central role in the overall system performance.

In digital microelectronics, we study the design of the internal circuits of gates, flipflops, and other components. For example, we construct a circuit using devices such as transistors to realize the NOT and NOR functions shown in Fig. 1.15. Based on these implementations, we then determine various properties of each circuit. For example, what limits the speed
image_name:Figure 1.15 NOT Gate
description:
[
name: NOT Gate, type: Inverter, ports: {In: A, Out: Y}
name: NOR Gate, type: Other, ports: {N1: A, N2: B, N3: Y}
]
extrainfo:The diagram shows a NOT gate and a NOR gate. The NOT gate inverts input A to produce output Y. The NOR gate outputs Y as the NOR of inputs A and B.
image_name:Figure 1.15 NOR Gate
description:
[
name: NOT Gate, type: Inverter, ports: {In: A, Out: Y}
name: NOR Gate, type: Other, ports: {N1: A, N2: B, N3: Y}
]
extrainfo:The diagram shows a NOT gate and a NOR gate. The NOT gate inverts the input A to produce the output Y. The NOR gate outputs the NOR of inputs A and B, resulting in Y.

Figure 1.15 NOT and NOR gates.
of a gate? How much power does a gate consume while running at a certain speed? How robustly does a gate operate in the presence of nonidealities such as noise (Fig. 1.16)?
image_name:Figure 1.16
description:The graph in Figure 1.16 illustrates the response of a logic gate to a noisy input. The diagram consists of two main components: a waveform on the left and a logic gate symbol on the right.

1. **Type of Graph and Function:**
- The graph is a time-domain waveform representing a noisy input signal. It is not a traditional function graph but rather a representation of signal behavior in time.

2. **Axes Labels and Units:**
- The axes are not explicitly labeled in the image. However, it can be inferred that the horizontal axis represents time, and the vertical axis represents voltage or signal amplitude.

3. **Overall Behavior and Trends:**
- The waveform exhibits irregular fluctuations, characteristic of noise. There are sharp peaks and valleys, indicating rapid changes in the signal amplitude over time.
- The signal does not follow a regular pattern, showing a high level of randomness typical of noisy signals.

4. **Key Features and Technical Details:**
- The waveform shows variability in amplitude, with no clear periodicity or consistent trend.
- The logic gate symbol next to the waveform is a NOT gate, which suggests that the circuit is designed to invert the noisy input signal.

5. **Annotations and Specific Data Points:**
- There are no specific numerical annotations or markers on the waveform.
- The presence of the NOT gate symbol indicates the intended operation of the circuit, which is to provide an inverted output in response to the noisy input.

Overall, this diagram illustrates how a NOT gate processes a noisy input signal, highlighting the gate's role in inverting the signal despite the presence of noise.
image_name:Figure 1.15
description:
[
name: Inv, type: Inverter, ports: {In: Vin, Out: Vout}
]
extrainfo:The diagram shows a NOT gate (Inverter) with input 'Vin' and output 'Vout'. It inverts the input signal.

Figure 1.16 Response of a gate to a noisy input.

Example Consider the circuit shown in Fig. 1.17, where switch $S_{1}$ is controlled by the digital input.
1.4 That is, if $A$ is high, $S_{1}$ is on and vice versa. Prove that the circuit provides the NOT function.

Figure 1.17
image_name:Figure 1.17
description:
[
name: RL, type: Resistor, ports: {N1: VDD, N2: Vout}
name: S1, type: Switch, ports: {N1: Vout, N2: GND}
name: VDD, type: VoltageSource, ports: {Np: VDD, Nn: GND}
]
extrainfo:The circuit is a NOT gate implementation using a switch and resistor. When the input A is high, the switch S1 is closed, forcing Vout to GND. When A is low, S1 is open, and Vout is pulled high to VDD through RL.

Solution If $A$ is high, $S_{1}$ is on, forcing $V_{\text {out }}$ to zero. On the other hand, if $A$ is low, $S_{1}$ remains off, drawing no current from $R_{L}$. As a result, the voltage drop across $R_{L}$ is zero and hence $V_{\text {out }}=V_{D D}$; i.e., the output is high. We thus observe that, for both logical states at the input, the output assumes the opposite state.

Exercise Determine the logical function if $S_{1}$ and $R_{L}$ are swapped and $V_{\text {out }}$ is sensed across $R_{L}$.

The above example indicates that switches can perform logical operations. In fact, early digital circuits did employ mechanical switches (relays), but suffered from a very limited speed (a few kilohertz). It was only after "transistors" were invented and their ability to act as switches was recognized that digital circuits consisting of millions of gates and operating at high speeds (several gigahertz) became possible.

### 1.3.4 Basic Circuit Theorems

Of the numerous analysis techniques taught in circuit theory courses, some prove particularly important to our study of microelectronics. This section provides a review of such concepts.

Kirchoff's Laws The Kirchoff Current Law (KCL) states that the sum of all currents flowing into a node is zero (Fig. 1.18):

$$
\begin{equation*}
\sum_{j} I_{j}=0 \tag{1.5}
\end{equation*}
$$

KCL in fact results from conservation of charge: a nonzero sum would mean that either some of the charge flowing into node $X$ vanishes or this node produces charge.
image_name:Figure 1.18
description:
[

]
extrainfo:The diagram illustrates Kirchoff's Current Law (KCL), which states that the sum of currents flowing into a node is zero. The node is labeled as X1, and multiple currents (I1, I2, ..., In, Ij) are shown converging at this node.

Figure 1.18 Illustration of KCL.
The Kirchoff Voltage Law (KVL) states that the sum of voltage drops around any closed loop in a circuit is zero [Fig. 1.19(a)]:
image_name:Figure 1.19 (a)
description:
[
name: R5, type: Resistor, value: R5, ports: {N1: X1, N2: LOAD}
name: R6, type: Resistor, value: R6, ports: {N1: X4, N2: LOAD}
name: R7, type: Resistor, value: R7, ports: {N1: X3, N2: LOAD}
name: R8, type: Resistor, value: R8, ports: {N1: X3, N2: LOAD}
name: V1, type: VoltageSource, value: V1, ports: {Np: 1, Nn: X4}
name: V2, type: VoltageSource, value: V2, ports: {Np: 2, Nn: X2}
name: V3, type: VoltageSource, value: V3, ports: {Np: 3, Nn: X3}
name: V4, type: VoltageSource, value: V4, ports: {Np: 4, Nn: X4}
]
extrainfo:The circuit diagram illustrates a network of resistors and voltage sources connected at nodes X1, X2, X3, and X4 with LOAD connections. The voltage sources V1, V2, V3, and V4 are placed between these nodes, forming a loop that can be analyzed using Kirchoff's Voltage Law (KVL). Each resistor is connected to a LOAD, indicating a possible external connection or measurement point.

(a)
image_name:(a)
description:
[
name: R5, type: Resistor, value: R5, ports: {N1: X1, N2: LOAD}
name: R6, type: Resistor, value: R6, ports: {N1: X5, N2: LOAD}
name: R7, type: Resistor, value: R7, ports: {N1: X4, N2: LOAD}
name: R8, type: Resistor, value: R8, ports: {N1: X4, N2: LOAD}
name: R9, type: Resistor, value: R9, ports: {N1: X2, N2: LOAD}
name: V1, type: VoltageSource, value: V1, ports: {Np: X1, Nn: X5}
name: V2, type: VoltageSource, value: V2, ports: {Np: X2, Nn: X3}
name: V3, type: VoltageSource, value: V3, ports: {Np: X3, Nn: X5}
name: V4, type: VoltageSource, value: V4, ports: {Np: X5, Nn: X4}
]
extrainfo:The circuit forms a loop with voltage sources V1, V2, V3, and V4 connected at nodes X1, X2, X3, X4, and X5. Each resistor is connected to a LOAD, indicating external connections or measurement points. The loop can be analyzed using Kirchoff's Voltage Law (KVL), with the sum of voltages around the loop equating to zero: V1 + V2 + V3 + V4 = 0.

(b)

Figure 1.19 (a) Illustration of KVL, (b) slightly different view of the circuit.

$$
\begin{equation*}
\sum_{j} V_{j}=0 \tag{1.6}
\end{equation*}
$$

where $V_{j}$ denotes the voltage drop across element number $j$. KVL arises from the conservation of the "electromotive force." In the example illustrated in Fig. 1.19(a), we may sum the voltages in the loop to zero: $V_{1}+V_{2}+V_{3}+V_{4}=0$. Alternatively, adopting the modified view shown in Fig. 1.19(b), we can say $V_{1}$ is equal to the sum of the voltages across elements 2, 3, and 4: $V_{1}=V_{2}+V_{3}+V_{4}$. Note that the polarities assigned to $V_{2}$, $V_{3}$, and $V_{4}$ in Fig. 1.19(b) are different from those in Fig. 1.19(a).

In solving circuits, we may not know a priori the correct polarities of the currents and voltages. Nonetheless, we can simply assign arbitrary polarities, write KCLs and KVLs, and solve the equations to obtain the actual polarities and values. dependent current source $i_{1}$ is equal to a constant, $g_{m},{ }^{6}$ multiplied by the voltage drop across $r_{\pi}$. Determine the voltage gain of the amplifier, $v_{\text {out }} / v_{\text {in }}$.
${ }^{6}$ What is the dimension of $g_{m}$ ?

Figure 1.20
image_name:Figure 1.20
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: rπ, type: Resistor, value: rπ, ports: {N1: Vin, N2: Vπ}
name: gmvπ, type: VoltageControlledCurrentSource, value: gmvπ, ports: {Np: Vout, Nn: Vπ}
name: RL, type: Resistor, value: RL, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit is a basic amplifier with a voltage gain determined by the transconductance (gm) and the load resistor (RL). The current source is controlled by the voltage across rπ, and the output voltage is taken across RL.

Solution We must compute $V_{\text {out }}$ in terms of $v_{\text {in }}$, i.e., we must eliminate $v_{\pi}$ from the equations. Writing a KVL in the "input loop," we have

$$
\begin{equation*}
v_{i n}=v_{\pi}, \tag{1.7}
\end{equation*}
$$

and hence $g_{m} v_{\pi}=g_{m} v_{i n}$. A KCL at the output node yields

$$
\begin{equation*}
g_{m} v_{\pi}+\frac{v_{\text {out }}}{R_{L}}=0 . \tag{1.8}
\end{equation*}
$$

It follows that

$$
\begin{equation*}
\frac{v_{\text {out }}}{v_{\text {in }}}=-g_{m} R_{L} \tag{1.9}
\end{equation*}
$$

Note that the circuit amplifies the input if $g_{m} R_{L}>1$. Unimportant in most cases, the negative sign simply means the circuit "inverts" the signal.

Exercise Repeat the above example if $r_{\pi} \rightarrow \infty$.

Example
1.6

Figure 1.21 shows another amplifier topology. Compute the gain.
image_name:Figure 1.21
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: rπ, type: Resistor, value: rπ, ports: {N1: Vin, N2: GND}
name: gmvπ, type: VoltageControlledCurrentSource, ports: {Np: Vout, Nn: GND}
name: RL, type: Resistor, value: RL, ports: {N1: Vout, N2: GND}
name: Vout, type: VoltageSource, value: Vout, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is a basic amplifier topology with a voltage-controlled current source. It uses a resistor rπ and a load resistor RL to determine the gain. The input voltage Vin is applied across rπ and the controlled current source, gm*vπ, produces an output voltage Vout across RL. The amplifier does not invert the signal.

Figure 1.21
Solution Noting that $r_{\pi}$ in fact appears in parallel with $v_{i n}$, we write a KVL across these two components:

$$
\begin{equation*}
v_{i n}=-v_{\pi} \tag{1.10}
\end{equation*}
$$

The KCL at the output node is similar to (1.8). Thus,

$$
\begin{equation*}
\frac{v_{\text {out }}}{v_{\text {in }}}=g_{m} R_{L} \tag{1.11}
\end{equation*}
$$

Interestingly, this type of amplifier does not invert the signal.
Exercise Repeat the above example if $r_{\pi} \rightarrow \infty$.

Example 1.7

A third amplifier topology is shown in Fig. 1.22. Determine the voltage gain.
image_name:Figure 1.22
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: rπ, type: Resistor, value: rπ, ports: {N1: Vin, N2: Vout}
name: gmvπ, type: VoltageControlledCurrentSource, ports: {Np: Vout, Nn: GND}
name: RE, type: Resistor, value: RE, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit is a basic amplifier topology with a voltage source Vin, a resistor rπ, a voltage-controlled current source gmvπ, and a resistor RE. It demonstrates a non-inverting amplifier configuration.

Figure 1.22
Solution We first write a KVL around the loop consisting of $v_{i n}, r_{\pi}$, and $R_{E}$ :

$$
\begin{equation*}
v_{\text {in }}=v_{\pi}+v_{\text {out }} . \tag{1.12}
\end{equation*}
$$

That is, $v_{\pi}=v_{\text {in }}-v_{\text {out }}$. Next, noting that the currents $v_{\pi} / r_{\pi}$ and $g_{m} v_{\pi}$ flow into the output node, and the current $v_{\text {out }} / R_{E}$ flows out of it, we write a KCL:

$$
\begin{equation*}
\frac{v_{\pi}}{r_{\pi}}+g_{m} v_{\pi}=\frac{v_{\text {out }}}{R_{E}} \tag{1.13}
\end{equation*}
$$

Substituting $v_{\text {in }}-v_{\text {out }}$ for $v_{\pi}$ gives

$$
\begin{equation*}
v_{\text {in }}\left(\frac{1}{r_{\pi}}+g_{m}\right)=v_{\text {out }}\left(\frac{1}{R_{E}}+\frac{1}{r_{\pi}}+g_{m}\right), \tag{1.14}
\end{equation*}
$$

and hence

$$
\begin{align*}
\frac{v_{\text {out }}}{v_{\text {in }}} & =\frac{\frac{1}{r_{\pi}}+g_{m}}{\frac{1}{R_{E}}+\frac{1}{r_{\pi}}+g_{m}}  \tag{1.15}\\
& =\frac{\left(1+g_{m} r_{\pi}\right) R_{E}}{r_{\pi}+\left(1+g_{m} r_{\pi}\right) R_{E}} \tag{1.16}
\end{align*}
$$

Note that the voltage gain always remains below unity. Would such an amplifier prove useful at all? In fact, this topology exhibits some important properties that make it a versatile building block.

Exercise Repeat the above example if $r_{\pi} \rightarrow \infty$.

The foregoing three examples relate to three amplifier topologies that are studied extensively in Chapter 5.

Thevenin and Norton Equivalents While Kirchoff's laws can always be utilized to solve any circuit, the Thevenin and Norton theorems can both simplify the algebra and, more importantly, provide additional insight into the operation of a circuit.

Thevenin's theorem states that a (linear) one-port network can be replaced with an equivalent circuit consisting of one voltage source in series with one impedance. Illustrated in Fig. 1.23(a), the term "port" refers to any two nodes whose voltage difference is of interest. The equivalent voltage, $v_{\text {Thev }}$, is obtained by leaving the port open and computing the voltage created by the actual circuit at this port. The equivalent impedance, $Z_{\text {Thev }}$, is
image_name:(a)
description:
[
name: V1, type: VoltageSource, value: V1, ports: {Np: Vi, Nn: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: Vi, Nn: X1}
name: R1, type: Resistor, value: R1, ports: {N1: X1, N2: LOAD}
name: L1, type: Inductor, value: L1, ports: {N1: X1, N2: LOAD}
name: X1, type: CurrentSource, ports: {Np: X1, Nn: GND}
name: ZThev, type: Resistor, value: ZThev, ports: {N1: Port, N2: VThev}
name: VThev, type: VoltageSource, value: VThev, ports: {Np: VThev, Nn: Port}
]
extrainfo:The circuit diagram (a) represents a Thevenin equivalent circuit with a voltage source V1, a capacitor C1, a resistor R1, an inductor L1, and a current source X1. Thevenin equivalent voltage VThev and impedance ZThev are shown in the equivalent circuit. The circuit is used to compute the equivalent impedance and voltage seen at the port.
image_name:(b)
description:
[
name: V1, type: VoltageSource, value: V1, ports: {Np: GND, Nn: C1}
name: C1, type: Capacitor, value: C1, ports: {Np: GND, Nn: X1}
name: R1, type: Resistor, value: R1, ports: {N1: X1, N2: LOAD}
name: L1, type: Inductor, value: L1, ports: {N1: LOAD, N2: X1}
name: Load, type: CurrentSource, ports: {Np: X1, Nn: LOAD}
name: ZThev, type: Resistor, value: ZThev, ports: {N1: X1, N2: VX}
name: VThev, type: VoltageSource, value: VThev, ports: {Np: VX, Nn: ZThev}
]
extrainfo:The circuit diagram (b) illustrates the computation of equivalent impedance using Thevenin's theorem. The circuit consists of a voltage source V1, a capacitor C1, a resistor R1, an inductor L1, and a current source Load. Thevenin's equivalent circuit is represented by VThev and ZThev. The nodes are labeled GND, X1, LOAD, and VX.

Figure 1.23 (a) Thevenin equivalent circuit, (b) computation of equivalent impedance.
determined by setting all independent voltage and current sources in the circuit to zero and calculating the impedance between the two nodes. We also call $Z_{\text {Thev }}$ the impedance "seen" when "looking" into the output port [Fig. 1.23(b)]. The impedance is computed by applying a voltage source across the port and obtaining the resulting current. A few examples illustrate these principles.

Suppose the input voltage source and the amplifier shown in Fig. 1.20 are placed in a box and only the output port is of interest [Fig. 1.24(a)]. Determine the Thevenin equivalent of the circuit.

Solution

We must compute the open-circuit output voltage and the impedance seen when looking into the output port. The Thevenin voltage is obtained from Fig. 1.24(a) and Eq. (1.9):

$$
\begin{align*}
v_{\text {Thev }} & =v_{\text {out }}  \tag{1.17}\\
& =-g_{m} R_{L} v_{\text {in }} . \tag{1.18}
\end{align*}
$$

To calculate $Z_{\text {Thev }}$, we set $v_{\text {in }}$ to zero, apply a voltage source, $v_{X}$, across the output port, and determine the current drawn from the voltage source, $i_{X}$. As shown in Fig. 1.24(b), setting $v_{\text {in }}$ to zero means replacing it with a short circuit. Also, note that the current source $g_{m} v_{\pi}$ remains in the circuit because it depends on the voltage across $r_{\pi}$, whose value is not known a priori.
image_name:(a)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: rπ, type: Resistor, value: rπ, ports: {N1: Vin, N2: GND}
name: i1, type: CurrentSource, value: gmvπ, ports: {Np: GND, Nn: Vout}
name: RL, type: Resistor, value: RL, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit represents a small-signal model with a voltage source Vin, a resistor rπ, a dependent current source gmvπ, and a load resistor RL. The current source is dependent on the voltage across rπ.

(a)
image_name:(b)
description:
[
name: r_π, type: Resistor, value: r_π, ports: {N1: Vπ, N2: GND}
name: g_m v_π, type: CurrentControlledCurrentSource, value: g_m v_π, ports: {Np: GND, Nn: Vx}
name: R_L, type: Resistor, value: R_L, ports: {N1: Vx, N2: GND}
name: v_x, type: VoltageSource, value: v_x, ports: {Np: Vx, Nn: GND}
]
extrainfo:The circuit is a small-signal model representing a voltage source v_x, a resistor r_π, a dependent current source g_m v_π, and a load resistor R_L. The dependent current source is controlled by the voltage across r_π. Since both terminals of r_π are tied to ground, v_π = 0, and the circuit reduces to a simple load resistor R_L and voltage source v_x.

(b)
image_name:Figure 1.24(c)
description:
[
name: RL, type: Resistor, value: RL, ports: {N1: X, N2: Vout}
name: Vin, type: VoltageSource, value: Vin, ports: {Np: X, Nn: GND}
]
extrainfo:The circuit represents the Thevenin equivalent of a voltage source and amplifier. The dependent current source gmRLVin is not explicitly shown as a separate device but is part of the voltage source model. The circuit reduces to a resistor RL connected to a voltage source Vin, with the output voltage Vout across RL.

(c)

Figure 1.24
How do we solve the circuit of Fig. 1.24(b)? We must again eliminate $v_{\pi}$. Fortunately, since both terminals of $r_{\pi}$ are tied to ground, $v_{\pi}=0$ and $g_{m} v_{\pi}=0$. The circuit thus reduces to $R_{L}$ and

$$
\begin{equation*}
i_{X}=\frac{v_{X}}{R_{L}} \tag{1.19}
\end{equation*}
$$

That is,

$$
\begin{equation*}
R_{\text {Thev }}=R_{L} \tag{1.20}
\end{equation*}
$$

Figure 1.24(c) depicts the Thevenin equivalent of the input voltage source and the amplifier. In this case, we call $R_{\text {Thev }}\left(=R_{L}\right)$ the "output impedance" of the circuit.

Exercise $\quad$ Repeat the above example if $r_{\pi} \rightarrow \infty$.

With the Thevenin equivalent of a circuit available, we can readily analyze its behavior in the presence of a subsequent stage or "load."

Example
1.9

The amplifier of Fig. 1.20 must drive a speaker having an impedance of $R_{s p}$. Determine the voltage delivered to the speaker.

Solution Shown in Fig. 1.25(a) is the overall circuit arrangement that we must solve. Replacing the section in the dashed box with its Thevenin equivalent from Fig. 1.24(c), we greatly simplify the circuit [Fig. 1.25(b)], and write

$$
\begin{align*}
v_{\text {out }} & =-g_{m} R_{L} v_{\text {in }} \frac{R_{s p}}{R_{s p}+R_{L}}  \tag{1.21}\\
& =-g_{m} v_{\text {in }}\left(R_{L} \| R_{s p}\right) . \tag{1.22}
\end{align*}
$$

image_name:(a)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: rπ, type: Resistor, value: rπ, ports: {N1: Vin, N2: GND}
name: gmvπ, type: VoltageControlledCurrentSource, value: gmvπ, ports: {Np: Vout, Nn: GND}
name: RL, type: Resistor, value: RL, ports: {N1: Vout, N2: GND}
name: Rsp, type: Resistor, value: Rsp, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit is a simplified model using Thevenin's theorem to determine the output voltage across the speaker. It includes a voltage source, resistors, and a voltage-controlled current source.
image_name:(b)
description:
[
name: vin, type: VoltageSource, value: vin, ports: {Np: X, Nn: GND}
name: RL, type: Resistor, value: RL, ports: {N1: X, N2: Vout}
name: Rsp, type: Resistor, value: Rsp, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit in Figure 1.25(b) shows a simplified Thevenin equivalent with a voltage source 'vin', resistors 'RL' and 'Rsp', and an output voltage 'Vout'. The circuit is grounded at one node.

Figure 1.25

Exercise Repeat the above example if $r_{\pi} \rightarrow \infty$.

Example Determine the Thevenin equivalent of the circuit shown in Fig. 1.22 if the output port is 1.10 of interest.

Solution The open-circuit output voltage is simply obtained from (1.16):

$$
\begin{equation*}
v_{\text {Thev }}=\frac{\left(1+g_{m} r_{\pi}\right) R_{L}}{r_{\pi}+\left(1+g_{m} r_{\pi}\right) R_{L}} v_{i n} \tag{1.23}
\end{equation*}
$$

To calculate the Thevenin impedance, we set $v_{i n}$ to zero and apply a voltage source across the output port as depicted in Fig. 1.26. To eliminate $v_{\pi}$, we recognize that the two terminals of $r_{\pi}$ are tied to those of $v_{X}$ and hence

$$
\begin{equation*}
v_{\pi}=-v_{X} . \tag{1.24}
\end{equation*}
$$

image_name:Figure 1.26
description:
[
name: rπ, type: Resistor, value: rπ, ports: {N1: GND, N2: Vx}
name: gmvπ, type: CurrentSource, value: gmvπ, ports: {Np: GND, Nn: Vx}
name: RL, type: Resistor, value: RL, ports: {N1: Vx, N2: GND}
name: vX, type: VoltageSource, value: vX, ports: {Np: Vx, Nn: GND}
]
extrainfo:The circuit represents a small-signal model with a dependent current source and resistive elements. The current source gmvπ is controlled by the voltage across rπ. Thevenin's theorem is applied to find the equivalent impedance.

Figure 1.26
We now write a KCL at the output node. The currents $v_{\pi} / r_{\pi}, g_{m} v_{\pi}$, and $i_{X}$ flow into this node and the current $v_{X} / R_{L}$ flows out of it. Consequently,

$$
\begin{equation*}
\frac{v_{\pi}}{r_{\pi}}+g_{m} v_{\pi}+i_{X}=\frac{v_{X}}{R_{L}} \tag{1.25}
\end{equation*}
$$

or

$$
\begin{equation*}
\left(\frac{1}{r_{\pi}}+g_{m}\right)\left(-v_{X}\right)+i_{X}=\frac{v_{X}}{R_{L}} . \tag{1.26}
\end{equation*}
$$

That is,

$$
\begin{align*}
R_{\text {Thev }} & =\frac{v_{X}}{i_{X}}  \tag{1.27}\\
& =\frac{r_{\pi} R_{L}}{r_{\pi}+\left(1+g_{m} r_{\pi}\right) R_{L}} \tag{1.28}
\end{align*}
$$

Exercise What happens if $R_{L}=\infty$ ?

Norton's theorem states that a (linear) one-port network can be represented by one current source in parallel with one impedance (Fig. 1.27). The equivalent current, $i_{\text {Nor }}$, is obtained by shorting the port of interest and computing the current that flows through it. The equivalent impedance, $Z_{\mathrm{Nor}}$, is determined by setting all independent voltage and current sources in the circuit to zero and calculating the impedance seen at the port. Of course, $Z_{\text {Nor }}=Z_{\text {Thev }}$.
image_name:Figure 1.27 Norton's theorem
description:
[
name: V1, type: VoltageSource, value: V1, ports: {Np: Vi, Nn: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: Vi, Nn: X1}
name: R1, type: Resistor, value: R1, ports: {N1: X1, N2: Port_j}
name: L1, type: Inductor, value: L1, ports: {N1: X1, N2: Port_j}
name: I1, type: CurrentSource, value: I1, ports: {Np: X1, Nn: GND}
name: Z_Nor, type: Resistor, value: Z_Nor, ports: {N1: Port_j, N2: GND}
name: i_Nor, type: CurrentSource, value: i_Nor, ports: {Np: Port_j, Nn: GND}
]
extrainfo:The circuit represents a Norton equivalent with a current source i_Nor in parallel with an impedance Z_Nor. The original circuit consists of a voltage source V1, capacitor C1, resistor R1, inductor L1, and current source I1 connected to a load at Port_j.

Figure 1.27 Norton's theorem.

Example
1.11

Solution As depicted in Fig. 1.28(a), we short the output port and seek the value of $i_{\text {Nor }}$. Since the voltage across $R_{L}$ is now forced to zero, this resistor carries no current.
image_name:(a)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: rπ, type: Resistor, value: rπ, ports: {N1: Vin, N2: X1}
name: i1, type: CurrentControlledCurrentSource, ports: {Np: X1, Nn: GND}
name: RL, type: Resistor, value: RL, ports: {N1: X1, N2: GND}
]
extrainfo:The circuit illustrates a Norton equivalent circuit with a current source i_Nor in parallel with the impedance Z_Nor. The diagram shows the transformation of a voltage source with a resistor into its Norton equivalent, indicating the analysis for determining the Norton current i_Nor through a short circuit.

(a)

Determine the Norton equivalent of the circuit shown in Fig. 1.20 if the output port is of interest.
image_name:(b)
description:
[
name: gm*vin, type: VoltageControlledCurrentSource, ports: {Np: X1, Nn: GND}
name: RL, type: Resistor, value: RL, ports: {N1: X1, N2: GND}
]
extrainfo:The circuit represents a Norton equivalent with a current source gm*vin in parallel with a resistor RL, connected between node X1 and ground (GND). The Norton current i_Nor is given by -gm*vin.

Figure 1.28

A KCL at the output node thus yields

$$
\begin{align*}
i_{\text {Nor }} & =-g_{m} v_{\pi}  \tag{1.29}\\
& =-g_{m} v_{i n} \tag{1.30}
\end{align*}
$$

Also, from Example $1.8, R_{\text {Nor }}\left(=R_{\text {Thev }}\right)=R_{L}$. The Norton equivalent therefore emerges as shown in Fig. 1.28(b). To check the validity of this model, we observe that the flow of $i_{\text {Nor }}$ through $R_{L}$ produces a voltage of $-g_{m} R_{L} v_{i n}$, the same as the output voltage of the original circuit.

Exercise Repeat the above example if a resistor of value $R_{1}$ is added between the top terminal of $v_{\text {in }}$ and the output node.

Example Determine the Norton equivalent of the circuit shown in Fig. 1.22 if the output port is 1.12 interest.

Solution Shorting the output port as illustrated in Fig. 1.29(a), we note that $R_{L}$ carries no current. Thus,
image_name:(a)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: rπ, type: Resistor, value: rπ, ports: {N1: Vin, N2: X1}
name: i1, type: CurrentSource, ports: {Np: X1, Nn: GND}
name: gmvπ, type: VoltageControlledCurrentSource, ports: {Np: X1, Nn: GND}
name: RL, type: Resistor, value: RL, ports: {N1: X1, N2: GND}
]
extrainfo:The circuit is a Norton equivalent with a voltage source Vin, a resistor rπ, a current source i1, a voltage-controlled current source gmvπ, and a load resistor RL. The node X1 is the main connection point for the controlled sources and the load.

(a)
image_name:Figure 1.29(b)
description:
[
name: Current Source, type: CurrentSource, ports: {Np: X1, Nn: GND}
name: gmvπ, type: VoltageControlledCurrentSource, ports: {Np: X1, Nn: GND}
name: RL, type: Resistor, value: RL, ports: {N1: X1, N2: GND}
]
extrainfo:The circuit is a Norton equivalent with a voltage source Vin, a resistor rπ, a current source i1, a voltage-controlled current source gmvπ, and a load resistor RL. The node X1 is the main connection point for the controlled sources and the load.

(b)

Figure 1.29

$$
\begin{equation*}
i_{\text {Nor }}=\frac{v_{\pi}}{r_{\pi}}+g_{m} v_{\pi} . \tag{1.31}
\end{equation*}
$$

Also, $v_{i n}=v_{\pi}$ (why?), yielding

$$
\begin{equation*}
i_{\text {Nor }}=\left(\frac{1}{r_{\pi}}+g_{m}\right) v_{i n} \tag{1.32}
\end{equation*}
$$

With the aid of $R_{\text {Thev }}$ found in Example 1.10, we construct the Norton equivalent depicted in Fig. 1.29(b).

Exercise What happens if $r_{\pi}=\infty$ ?

## 1.4 CHAPTER SUMMARY

- Electronic functions appear in many devices, including cellphones, digital cameras, laptop computers, etc.
- Amplification is an essential operation in many analog and digital systems.
- Analog circuits process signals that can assume various values at any time. By contrast, digital circuits deal with signals having only two levels and switching between these values at known points in time.
- Despite the "digital revolution," analog circuits find wide application in most of today's electronic systems.
- The voltage gain of an amplifier is defined as $v_{\text {out }} / v_{\text {in }}$ and sometimes expressed in decibels $(\mathrm{dB})$ as $20 \log \left(v_{\text {out }} / v_{\text {in }}\right)$.
- Kirchoff's current law (KCL) states that the sum of all currents flowing into any node is zero. Kirchoff's voltage law (KVL) states that the sum of all voltages around any loop is zero.
- Norton's theorem allows simplifying a one-port circuit to a current source in parallel with an impedance. Similarly, Thevenin's theorem reduces a one-port circuit to a voltage source in series with an impedance.
image_name:2
description:The image labeled "2" appears to be a microchip or integrated circuit layout. The central portion of the image shows a detailed view of a semiconductor die, which includes several key components and structures.

1. **Identification of Components and Structure:**
- The layout includes a central octagonal or circular structure, possibly an inductor or a looped trace, which is commonly used in RF circuits or for creating inductive components on a chip.
- Surrounding this central structure are various rectangular and polygonal shapes, which could represent different layers of metal interconnects or semiconductor regions.
- The background grid pattern suggests the presence of a substrate or base layer on which these components are fabricated.

2. **Connections and Interactions:**
- The central looped structure is connected to other parts of the circuit through thin traces, indicating electrical connectivity. These traces are likely part of the interconnect layers that route signals or power across the chip.
- There are no visible external connections (such as bond pads) in this zoomed-in section, but the layout indicates internal connectivity that would be part of a larger circuit.

3. **Labels, Annotations, and Key Features:**
- The image does not include any textual labels or annotations directly on the chip layout, but the context suggests this is a detailed view of a specific component or section of an integrated circuit.
- The number "2" is prominently displayed on a blue background to the right of the image, likely serving as an identifier for this particular image or section within a larger set of diagrams.

This microchip layout is likely part of a more extensive design, possibly involving RF or analog circuitry, where the central looped structure plays a critical role in the circuit's functionality.
