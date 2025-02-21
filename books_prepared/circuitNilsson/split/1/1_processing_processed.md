# 1. Circuit Variables
CHAPTER

CHAPTER CONTENTS

```
Electrical Engineering: An Overview p. }
The International System of Units p. 8
Circuit Analysis: An Overview p. }1
Voltage and Current p. 11
The Ideal Basic Circuit Element p. 12
Power and Energy p. }1
```


CHAPTER OBJECTIVES

1 Understand and be able to use SI units and the standard prefixes for powers of 10.
2 Know and be able to use the definitions of voltage and current.
3 Know and be able to use the definitions of power and energy.
4 Be able to use the passive sign convention to calculate the power for an ideal basic circuit element given its voltage and current.



Electrical engineering is an exciting and challenging profession for anyone who has a genuine interest in, and aptitude for, applied science and mathematics. Over the past century and a half, electrical engineers have played a dominant role in the development of systems that have changed the way people live and work. Satellite communication links, telephones, digital computers, televisions, diagnostic and surgical medical equipment, assembly-line robots, and electrical power tools are representative components of systems that define a modern technological society. As an electrical engineer, you can participate in this ongoing technological revolution by improving and refining these existing systems and by discovering and developing new systems to meet the needs of our ever-changing society.

As you embark on the study of circuit analysis, you need to gain a feel for where this study fits into the hierarchy of topics that comprise an introduction to electrical engineering. Hence we begin by presenting an overview of electrical engineering, some ideas about an engineering point of view as it relates to circuit analysis, and a review of the international system of units.

We then describe generally what circuit analysis entails. Next, we introduce the concepts of voltage and current. We follow these concepts with discussion of an ideal basic element and the need for a polarity reference system. We conclude the chapter by describing how current and voltage relate to power and energy.

Practical Perspective

Balancing Power

One of the most important skills you will develop is the ability to check your answers for the circuits you design and analyze using the tools developed in this text. A common method used to check for valid answers is to balance the power in the circuit. The linear circuits we study have no net power, so the sum of the power associated with each circuit component must be zero. If the total power for the circuit is zero, we say that the power balances, but if the total power is not zero, we need to find the errors in our calculation.

As an example, we will consider a very simple model for the distribution of electricity to a typical home, as shown
below. (Note that a more realistic model will be investigated in the Practical Perspective for Chapter 9.) The components labeled a and b represent the electrical source to the home. The components labeled c, $d$, and e represent the wires that carry the electrical current from the source to the devices in the home requiring electrical power. The components labeled f , g , and h represent lamps, televisions, hair dryers, refrigerators, and other devices that require power.

Once we have introduced the concepts of voltage, current, power, and energy, we will examine this circuit model in detail, and use a power balance to determine whether the results of analyzing this circuit are correct.
image_name:romakoma / Shutterstock
description:The image consists of two main parts. On the left side, there is a photograph of a well-lit, modern house under a twilight sky. The house features multiple gables, large windows, and decorative lighting that highlights its architectural details. The surrounding landscaping is neatly maintained, with shrubs and a manicured lawn.

On the right side, there is a simple block diagram representing an electrical circuit model. This diagram includes several labeled components and connections:

1. **Components and Structure:**
- The diagram consists of eight blocks labeled from 'a' to 'h'.
- Blocks 'c', 'd', and 'e' are identified as wires carrying electrical current from the source to various devices in the home.
- Blocks 'f', 'g', and 'h' represent devices like lamps, televisions, hair dryers, and refrigerators that require power.

2. **Connections and Interactions:**
- The blocks are connected by lines indicating the flow of electrical current.
- The connections form a network, suggesting a layout of an electrical circuit within a home.
- There are junctions where multiple connections meet, which might represent distribution points or nodes in the circuit.

3. **Labels, Annotations, and Key Features:**
- The blocks are clearly labeled with letters 'a' to 'h', which are crucial for identifying different parts of the circuit.
- The layout is straightforward, with lines connecting the blocks in a grid-like pattern, indicating a systematic approach to distributing electrical power throughout the home.

This image serves as a conceptual representation of how electrical power is distributed from the source to various devices within a home, using a simplified circuit diagram to illustrate the connections and flow of electricity.
image_name:Elena Elisseeva / Alamy
description:The diagram represents a simple electrical circuit model of a home. The wires labeled a, b, c, d, and e carry electrical current to various devices in the home. The components labeled f, g, and h represent different electrical devices such as lamps, televisions, hair dryers, and refrigerators. The circuit is a basic representation of how electricity is distributed to various appliances in a household.

romakoma / Shutterstock
image_name:Elena Elisseeva / Alamy
description:The image depicts a tall floor lamp positioned against a dark wall, standing on a wooden floor. The lamp features a slender, metallic stand with a circular base that provides stability. At the top, there is a lampshade with a warm, amber hue that emits a soft glow, illuminating the surrounding area. The lamp is plugged into a wall socket visible on the left side of the image, with a black power cord trailing from the base to the socket. This setup exemplifies a simple electrical circuit where the lamp is the electrical device being powered by the household electrical system via the socket.


Elena Elisseeva / Alamy
image_name:Figure 1.1
description:The diagram illustrates a telephone system that uses a combination of satellite and terrestrial communication methods to connect two telephones. The system is comprised of several key components:

1. **Telephones:** Two telephones are depicted at the bottom of the diagram. Each telephone is connected to a microphone, which converts sound signals into electrical signals.

2. **Wiring and Cables:** The electrical signals from the telephones travel through wires and cables to a switching center. The cables are labeled as 'Wire' and 'Cable' for the two telephones, indicating the physical medium used for signal transmission.

3. **Switching Centers:** These are intermediary stations that route the signals from the telephones to the appropriate destination. Each telephone is connected to its respective switching center, which facilitates the connection between the two telephones.

4. **Coaxial and Fiber-optic Cables:** Signals are transmitted from the switching centers through coaxial and fiber-optic cables to microwave stations. The coaxial cable is depicted on the left side, while the fiber-optic cable is on the right, illustrating different transmission mediums that can be used in the system.

5. **Microwave Stations:** These stations receive signals from the cables and transmit them wirelessly via microwave frequencies. Each microwave station is connected to an antenna.

6. **Transmission and Receiving Antennas:** The transmission antenna sends signals to a communications satellite, while the receiving antenna on the opposite side receives signals from the satellite.

7. **Communications Satellite:** Positioned in space, the satellite acts as a relay station, receiving signals from the transmission antenna and sending them to the receiving antenna.

8. **Signal Flow:** The flow of information starts at the telephone, where sound is converted to electrical signals. These signals travel through wires, switching centers, and cables to microwave stations. From there, signals are transmitted via antennas to the satellite, which relays them to the receiving antenna. The process is reversed on the receiving side, ultimately delivering the sound to the other telephone.

Overall, the system enables long-distance communication by converting sound to electrical signals, transmitting them through various media, and using satellites to bridge large distances, ensuring signals reach the intended recipient efficiently.


Figure 1.1 A A telephone system.

## 1.1 Electrical Engineering: An Overview

Electrical engineering is the profession concerned with systems that produce, transmit, and measure electric signals. Electrical engineering combines the physicist's models of natural phenomena with the mathematician's tools for manipulating those models to produce systems that meet practical needs. Electrical systems pervade our lives; they are found in homes, schools, workplaces, and transportation vehicles everywhere. We begin by presenting a few examples from each of the five major classifications of electrical systems:

- communication systems
- computer systems
- control systems
- power systems
- signal-processing systems

Then we describe how electrical engineers analyze and design such systems.
Communication systems are electrical systems that generate, transmit, and distribute information. Well-known examples include television equipment, such as cameras, transmitters, receivers, and VCRs; radio telescopes, used to explore the universe; satellite systems, which return images of other planets and our own; radar systems, used to coordinate plane flights; and telephone systems.

Figure 1.1 depicts the major components of a modern telephone system. Starting at the left of the figure, inside a telephone, a microphone turns sound waves into electric signals. These signals are carried to a switching center where they are combined with the signals from tens, hundreds, or thousands of other telephones. The combined signals leave the switching center; their form depends on the distance they must travel. In our example, they are sent through wires in underground coaxial cables to a microwave transmission station. Here, the signals are transformed into microwave frequencies and broadcast from a transmission antenna through air and space, via a communications satellite, to a receiving antenna. The microwave receiving station translates the microwave signals into a form suitable for further transmission, perhaps as pulses of light to be sent through fiber-optic cable. On arrival at the second switching center, the combined signals are separated, and each is routed to the appropriate telephone, where an earphone acts as a speaker to convert the received electric signals back into sound waves. At each stage of the process, electric circuits operate on the signals. Imagine the challenge involved in designing, building, and operating each circuit in a way that guarantees that all of the hundreds of thousands of simultaneous calls have high-quality connections.

Computer systems use electric signals to process information ranging from word processing to mathematical computations. Systems range in size and power from pocket calculators to personal computers to supercomputers that perform such complex tasks as processing weather data and modeling chemical interactions of complex organic molecules. These systems include networks of microcircuits, or integrated circuits-postage-stampsized assemblies of hundreds, thousands, or millions of electrical components that often operate at speeds and power levels close to fundamental physical limits, including the speed of light and the thermodynamic laws.

Control systems use electric signals to regulate processes. Examples include the control of temperatures, pressures, and flow rates in an oil refinery; the fuel-air mixture in a fuel-injected automobile engine; mechanisms such as the motors, doors, and lights in elevators; and the locks in the

Panama Canal. The autopilot and autolanding systems that help to fly and land airplanes are also familiar control systems.

Power systems generate and distribute electric power. Electric power, which is the foundation of our technology-based society, usually is generated in large quantities by nuclear, hydroelectric, and thermal (coal-, oil-, or gas-fired) generators. Power is distributed by a grid of conductors that crisscross the country. A major challenge in designing and operating such a system is to provide sufficient redundancy and control so that failure of any piece of equipment does not leave a city, state, or region completely without power.

Signal-processing systems act on electric signals that represent information. They transform the signals and the information contained in them into a more suitable form. There are many different ways to process the signals and their information. For example, image-processing systems gather massive quantities of data from orbiting weather satellites, reduce the amount of data to a manageable level, and transform the remaining data into a video image for the evening news broadcast. A computerized tomography (CT) scan is another example of an image-processing system. It takes signals generated by a special X-ray machine and transforms them into an image such as the one in Fig. 1.2. Although the original X-ray signals are of little use to a physician, once they are processed into a recognizable image the information they contain can be used in the diagnosis of disease and injury.

Considerable interaction takes place among the engineering disciplines involved in designing and operating these five classes of systems. Thus communications engineers use digital computers to control the flow of information. Computers contain control systems, and control systems contain computers. Power systems require extensive communications systems to coordinate safely and reliably the operation of components, which may be spread across a continent. A signal-processing system may involve a communications link, a computer, and a control system.

A good example of the interaction among systems is a commercial airplane, such as the one shown in Fig. 1.3. A sophisticated communications system enables the pilot and the air traffic controller to monitor the plane's location, permitting the air traffic controller to design a safe flight path for all of the nearby aircraft and enabling the pilot to keep the plane on its designated path. On the newest commercial airplanes, an onboard computer system is used for managing engine functions, implementing the navigation and flight control systems, and generating video information screens in the cockpit. A complex control system uses cockpit commands to adjust the position and speed of the airplane, producing the appropriate signals to the engines and the control surfaces (such as the wing flaps, ailerons, and rudder) to ensure the plane remains safely airborne and on the desired flight path. The plane must have its own power system to stay aloft and to provide and distribute the electric power needed to keep the cabin lights on, make the coffee, and show the movie. Signal-processing systems reduce the noise in air traffic communications and transform information about the plane's location into the more meaningful form of a video display in the cockpit. Engineering challenges abound in the design of each of these systems and their integration into a coherent whole. For example, these systems must operate in widely varying and unpredictable environmental conditions. Perhaps the most important engineering challenge is to guarantee that sufficient redundancy is incorporated in the designs to ensure that passengers arrive safely and on time at their desired destinations.

Although electrical engineers may be interested primarily in one area, they must also be knowledgeable in other areas that interact with this area of interest. This interaction is part of what makes electrical
image_name:Figure 1.2 ∆ACT scan of an adult head
description:The image labeled "Figure 1.2 ∆ACT scan of an adult head" appears to be a composite of brain imaging scans, likely from a CT (Computed Tomography) scan, showcasing different layers or slices of an adult human head. The image is divided into two rows, each containing multiple cross-sectional views of the brain.

1. **Identification of Components and Structure:**
- **Top Row:** Displays four images that appear to be color-coded, possibly indicating different levels of brain activity or tissue density. The images might be PET (Positron Emission Tomography) scans, showing areas of metabolic activity, with warmer colors (reds and yellows) indicating higher activity.
- **Bottom Row:** Shows three grayscale images, likely standard CT scans, providing detailed anatomical structure of the brain. These images highlight the brain's physical features, such as ventricles and various lobes.

2. **Connections and Interactions:**
- The images do not directly show connections as in a circuit diagram but rather illustrate the internal structure and activity within the brain. The different sections might be used to compare and contrast areas of interest, such as identifying abnormalities or assessing brain function.

3. **Labels, Annotations, and Key Features:**
- There are no explicit labels or annotations visible in the image itself, but the color variations and grayscale differences serve as visual indicators of different features or levels of activity. The top row's color-coded images might be annotated in accompanying documentation to specify regions of interest or concern. The bottom row's CT images provide structural details that could be used for medical analysis or diagnosis.

Overall, this composite image serves as a diagnostic tool, offering both functional and structural insights into the brain, useful for medical professionals in assessing neurological conditions.


Figure 1.2 $\triangle \mathrm{A} C \mathrm{~T}$ scan of an adult head.
image_name:Figure 1.3
description:The image labeled "Figure 1.3" depicts an airplane in flight, shown from a perspective that highlights both the exterior and a section of the cockpit. The airplane is illustrated with a classic passenger jet design, featuring a streamlined fuselage, multiple windows along the side, and two engines mounted under each wing.

1. **Identification of Components and Structure:**
- **Exterior:** The airplane has a sleek, aerodynamic design with a pointed nose and a smooth body. The wings are broad and equipped with jet engines.
- **Cockpit:** A magnified section of the cockpit is shown, focusing on the pilot’s controls and instruments.

2. **Connections and Interactions:**
- The cockpit image highlights the pilot’s control yoke, essential for maneuvering the aircraft. The control panel includes various instruments and displays that provide flight information.
- The image does not detail specific electrical connections or interactions but implies the use of standard avionics systems for flight control.

3. **Labels, Annotations, and Key Features:**
- A red arrow points from the airplane’s cockpit window to the enlarged cockpit view, indicating the specific area of interest.
- The cockpit display includes a screen with a target-like graphic, possibly representing a navigational or flight monitoring system.
- There are no explicit labels or annotations on the airplane exterior, but the design and color scheme suggest a commercial passenger aircraft.
image_name:An airplane
description:The image depicts an airplane in flight, viewed from an angle that highlights its fuselage, wings, and engines. The airplane has a sleek design with a metallic body, red and blue stripes running along the fuselage, and windows lining the side. The wings are equipped with jet engines, and the tail section is visible, showcasing a typical commercial airliner configuration.

In the foreground, there is an inset illustration of the airplane's cockpit. This section is highlighted with an arrow pointing to the cockpit area on the airplane, indicating a focus on this component. The cockpit illustration shows a control panel with various instruments and a yoke, which pilots use to steer the aircraft. The control panel includes a display screen showing a target-like symbol, knobs, buttons, and indicator lights, suggesting a modern avionics setup.

The image serves as a conceptual representation of an airplane, emphasizing both the exterior structure and the interior cockpit elements, potentially for educational or illustrative purposes in an engineering context.


Figure 1.3 $\triangle$ An airplane.
engineering a challenging and exciting profession. The emphasis in engineering is on making things work, so an engineer is free to acquire and use any technique, from any field, that helps to get the job done.

Circuit Theory

In a field as diverse as electrical engineering, you might well ask whether all of its branches have anything in common. The answer is yes-electric circuits. An electric circuit is a mathematical model that approximates the behavior of an actual electrical system. As such, it provides an important foundation for learning-in your later courses and as a practicing engineer-the details of how to design and operate systems such as those just described. The models, the mathematical techniques, and the language of circuit theory will form the intellectual framework for your future engineering endeavors.

Note that the term electric circuit is commonly used to refer to an actual electrical system as well as to the model that represents it. In this text, when we talk about an electric circuit, we always mean a model, unless otherwise stated. It is the modeling aspect of circuit theory that has broad applications across engineering disciplines.

Circuit theory is a special case of electromagnetic field theory: the study of static and moving electric charges. Although generalized field theory might seem to be an appropriate starting point for investigating electric signals, its application is not only cumbersome but also requires the use of advanced mathematics. Consequently, a course in electromagnetic field theory is not a prerequisite to understanding the material in this book. We do, however, assume that you have had an introductory physics course in which electrical and magnetic phenomena were discussed.

Three basic assumptions permit us to use circuit theory, rather than electromagnetic field theory, to study a physical system represented by an electric circuit. These assumptions are as follows:

1. Electrical effects happen instantaneously throughout a system. We can make this assumption because we know that electric signals travel at or near the speed of light. Thus, if the system is physically small, electric signals move through it so quickly that we can consider them to affect every point in the system simultaneously. A system that is small enough so that we can make this assumption is called a lumped-parameter system.
2. The net charge on every component in the system is always zero. Thus no component can collect a net excess of charge, although some components, as you will learn later, can hold equal but opposite separated charges.
3. There is no magnetic coupling between the components in a system. As we demonstrate later, magnetic coupling can occur within a component.
That's it; there are no other assumptions. Using circuit theory provides simple solutions (of sufficient accuracy) to problems that would become hopelessly complicated if we were to use electromagnetic field theory. These benefits are so great that engineers sometimes specifically design electrical systems to ensure that these assumptions are met. The importance of assumptions 2 and 3 becomes apparent after we introduce the basic circuit elements and the rules for analyzing interconnected elements.

However, we need to take a closer look at assumption 1. The question is, "How small does a physical system have to be to qualify as a lumpedparameter system?" We can get a quantitative handle on the question by noting that electric signals propagate by wave phenomena. If the wavelength of the signal is large compared to the physical dimensions of the
system, we have a lumped-parameter system. The wavelength $\lambda$ is the velocity divided by the repetition rate, or frequency, of the signal; that is, $\lambda=c / f$. The frequency $f$ is measured in hertz $(\mathrm{Hz})$. For example, power systems in the United States operate at 60 Hz . If we use the speed of light $\left(c=3 \times 10^{8} \mathrm{~m} / \mathrm{s}\right)$ as the velocity of propagation, the wavelength is $5 \times 10^{6} \mathrm{~m}$. If the power system of interest is physically smaller than this wavelength, we can represent it as a lumped-parameter system and use circuit theory to analyze its behavior. How do we define smaller? A good rule is the rule of $1 / 10$ th: If the dimension of the system is $1 / 10$ th (or smaller) of the dimension of the wavelength, you have a lumped-parameter system. Thus, as long as the physical dimension of the power system is less than $5 \times 10^{5} \mathrm{~m}$, we can treat it as a lumped-parameter system.

On the other hand, the propagation frequency of radio signals is on the order of $10^{9} \mathrm{~Hz}$. Thus the wavelength is 0.3 m . Using the rule of $1 / 10$ th, the relevant dimensions of a communication system that sends or receives radio signals must be less than 3 cm to qualify as a lumped-parameter system. Whenever any of the pertinent physical dimensions of a system under study approaches the wavelength of its signals, we must use electromagnetic field theory to analyze that system. Throughout this book we study circuits derived from lumped-parameter systems.

Problem Solving

As a practicing engineer, you will not be asked to solve problems that have already been solved. Whether you are trying to improve the performance of an existing system or creating a new system, you will be working on unsolved problems. As a student, however, you will devote much of your attention to the discussion of problems already solved. By reading about and discussing how these problems were solved in the past, and by solving related homework and exam problems on your own, you will begin to develop the skills to successfully attack the unsolved problems you'll face as a practicing engineer.

Some general problem-solving procedures are presented here. Many of them pertain to thinking about and organizing your solution strategy before proceeding with calculations.

1. Identify what's given and what's to be found. In problem solving, you need to know your destination before you can select a route for getting there. What is the problem asking you to solve or find? Sometimes the goal of the problem is obvious; other times you may need to paraphrase or make lists or tables of known and unknown information to see your objective.

The problem statement may contain extraneous information that you need to weed out before proceeding. On the other hand, it may offer incomplete information or more complexities than can be handled given the solution methods at your disposal. In that case, you'll need to make assumptions to fill in the missing information or simplify the problem context. Be prepared to circle back and reconsider supposedly extraneous information and/or your assumptions if your calculations get bogged down or produce an answer that doesn't seem to make sense.
2. Sketch a circuit diagram or other visual model. Translating a verbal problem description into a visual model is often a useful step in the solution process. If a circuit diagram is already provided, you may need to add information to it, such as labels, values, or reference directions. You may also want to redraw the circuit in a simpler, but equivalent, form. Later in this text you will learn the methods for developing such simplified equivalent circuits.
3. Think of several solution methods and decide on a way of choosing among them. This course will help you build a collection of analytical tools, several of which may work on a given problem. But one method may produce fewer equations to be solved than another, or it may require only algebra instead of calculus to reach a solution. Such efficiencies, if you can anticipate them, can streamline your calculations considerably. Having an alternative method in mind also gives you a path to pursue if your first solution attempt bogs down.
4. Calculate a solution. Your planning up to this point should have helped you identify a good analytical method and the correct equations for the problem. Now comes the solution of those equations. Paper-and-pencil, calculator, and computer methods are all available for performing the actual calculations of circuit analysis. Efficiency and your instructor's preferences will dictate which tools you should use.
5. Use your creativity. If you suspect that your answer is off base or if the calculations seem to go on and on without moving you toward a solution, you should pause and consider alternatives. You may need to revisit your assumptions or select a different solution method. Or, you may need to take a less-conventional problem-solving approach, such as working backward from a solution. This text provides answers to all of the Assessment Problems and many of the Chapter Problems so that you may work backward when you get stuck. In the real world, you won't be given answers in advance, but you may have a desired problem outcome in mind from which you can work backward. Other creative approaches include allowing yourself to see parallels with other types of problems you've successfully solved, following your intuition or hunches about how to proceed, and simply setting the problem aside temporarily and coming back to it later.
6. Test your solution. Ask yourself whether the solution you've obtained makes sense. Does the magnitude of the answer seem reasonable? Is the solution physically realizable? You may want to go further and rework the problem via an alternative method. Doing so will not only test the validity of your original answer, but will also help you develop your intuition about the most efficient solution methods for various kinds of problems. In the real world, safetycritical designs are always checked by several independent means. Getting into the habit of checking your answers will benefit you as a student and as a practicing engineer.

These problem-solving steps cannot be used as a recipe to solve every problem in this or any other course. You may need to skip, change the order of, or elaborate on certain steps to solve a particular problem. Use these steps as a guideline to develop a problem-solving style that works for you.

## 1.2 The International System of Units

Engineers compare theoretical results to experimental results and compare competing engineering designs using quantitative measures. Modern engineering is a multidisciplinary profession in which teams of engineers work together on projects, and they can communicate their results in a meaningful way only if they all use the same units of measure. The International System of Units (abbreviated SI) is used by all the major engineering societies and most engineers throughout the world; hence we use it in this book.

TABLE 1.1 The International System of Units (SI)

| Quantity | Basic Unit | Symbol |
| :--- | :--- | :--- |
| Length | meter | m |
| Mass | kilogram | kg |
| Time | second | s |
| Electric current | ampere | A |
| Thermodynamic temperature | degree kelvin | K |
| Amount of substance | mole | mol |
| Luminous intensity | candela | cd |

National Institute of Standards and Technology Special Publication 330, 2008 Edition, Natl. Inst. Stand. Technol. Spec. Pub. 330, 2008 Ed., 96 pages (March 2008)

The SI units are based on seven defined quantities:

- length
- mass
- time
- electric current
- thermodynamic temperature
- amount of substance
- luminous intensity

These quantities, along with the basic unit and symbol for each, are listed in Table 1.1. Although not strictly SI units, the familiar time units of minute ( 60 s ), hour ( 3600 s ), and so on are often used in engineering calculations. In addition, defined quantities are combined to form derived units. Some, such as force, energy, power, and electric charge, you already know through previous physics courses. Table 1.2 lists the derived units used in this book.

In many cases, the SI unit is either too small or too large to use conveniently. Standard prefixes corresponding to powers of 10 , as listed in Table 1.3, are then applied to the basic unit. All of these prefixes are correct, but engineers often use only the ones for powers divisible by 3 ; thus centi, deci, deka, and hecto are used rarely. Also, engineers often select the prefix that places the base number in the range between 1 and 1000. Suppose that a time calculation yields a result of $10^{-5} \mathrm{~s}$, that is, 0.00001 s . Most engineers would describe this quantity as $10 \mu \mathrm{~s}$, that is, $10^{-5}=10 \times 10^{-6} \mathrm{~s}$, rather than as 0.01 ms or $10,000,000 \mathrm{ps}$.

TABLE 1.2 Derived Units in SI

| Quantity | Unit Name (Symbol) | Formula |
| :--- | :--- | :--- |
| Frequency | hertz $(\mathrm{Hz})$ | $\mathrm{s}^{-1}$ |
| Force | newton $(\mathrm{N})$ | $\mathrm{kg} \cdot \mathrm{m} / \mathrm{s}^{2}$ |
| Energy or work | joule $(\mathrm{J})$ | $\mathrm{N} \cdot \mathrm{m}$ |
| Power | watt $(\mathrm{W})$ | $\mathrm{J} / \mathrm{s}$ |
| Electric charge | $\operatorname{coulomb}(\mathrm{C})$ | $\mathrm{A} \cdot \mathrm{s}$ |
| Electric potential | $\operatorname{volt}(\mathrm{V})$ | $\mathrm{J} / \mathrm{C}$ |
| Electric resistance | ohm $(\Omega)$ | $\mathrm{V} / \mathrm{A}$ |
| Electric conductance | $\operatorname{siemens}(\mathrm{S})$ | $\mathrm{A} / \mathrm{V}$ |
| Electric capacitance | farad $(\mathrm{F})$ | $\mathrm{C} / \mathrm{V}$ |
| Magnetic flux | weber $(\mathrm{Wb})$ | $\mathrm{V} \cdot \mathrm{s}$ |
| Inductance | henry $(\mathrm{H})$ | $\mathrm{Wb} / \mathrm{A}$ |

National Institute of Standards and Technology Special Publication 330, 2008 Edition, Natl. Inst. Stand. Technol. Spec. Pub. 330, 2008 Ed., 96 pages (March 2008)

TABLE 1.3 Standardized Prefixes to Signify Powers of 10

| Prefix | Symbol | Power |
| :--- | :--- | :--- |
| atto | a | $10^{-18}$ |
| femto | f | $10^{-15}$ |
| pico | p | $10^{-12}$ |
| nano | n | $10^{-9}$ |
| micro | $\mu$ | $10^{-6}$ |
| milli | m | $10^{-3}$ |
| centi | c | $10^{-2}$ |
| deci | d | $10^{-1}$ |
| deka | da | 10 |
| hecto | h | $10^{2}$ |
| kilo | k | $10^{3}$ |
| mega | M | $10^{6}$ |
| giga | G | $10^{9}$ |
| tera | T | $10^{12}$ |

National Institute of Standards and Technology Special Publication 330, 2008 Edition, Natl. Inst. Stand. Technol. Spec. Pub. 330, 2008 Ed., 96 pages (March 2008)

Example 1.1 illustrates a method for converting from one set of units to another and also uses power-of-ten prefixes.

#### Example 1.1 Using SI Units and Prefixes for Powers of 10

If a signal can travel in a cable at $80 \%$ of the speed of light, what length of cable, in inches, represents 1 ns ?

Therefore, a signal traveling at $80 \%$ of the speed of light will cover 9.45 inches of cable in 1 nanosecond.

#### Solution

First, note that $1 \mathrm{~ns}=10^{-9} \mathrm{~s}$. Also, recall that the speed of light $c=3 \times 10^{8} \mathrm{~m} / \mathrm{s}$. Then, $80 \%$ of the speed of light is $0.8 c=(0.8)\left(3 \times 10^{8}\right)=$ $2.4 \times 10^{8} \mathrm{~m} / \mathrm{s}$. Using a product of ratios, we can convert $80 \%$ of the speed of light from meters-persecond to inches-per-nanosecond. The result is the distance in inches traveled in 1 ns :

$$
\begin{aligned}
& \frac{2.4 \times 10^{8} \text { meters }}{1 \text { second }} \cdot \frac{1 \text { second }}{10^{9} \text { nanoseconds }} \cdot \frac{100 \text { centimeters }}{1 \text { meter }} \cdot \frac{1 \text { inch }}{2.54 \text { centimeters }} \\
& =\frac{\left(2.4 \times 10^{8}\right)(100)}{\left(10^{9}\right)(2.54)}=9.45 \text { inches } / \text { nanosecond }
\end{aligned}
$$

ASSESSMENT PROBLEMS

Objective 1-Understand and be able to use SI units and the standard prefixes for powers of 10
1.1 Assume a telephone signal travels through a cable at two-thirds the speed of light. How long does it take the signal to get from New York City to Miami if the distance is approximately 1100 miles?

Answer: 8.85 ms .
NOTE: Also try Chapter Problems 1.1, 1.3, and 1.5.
1.2 How many dollars per millisecond would the federal government have to collect to retire a deficit of $\$ 100$ billion in one year?
Answer: \$3.17/ms.

## 1.3 Circuit Analysis: An Overview

Before becoming involved in the details of circuit analysis, we need to take a broad look at engineering design, specifically the design of electric circuits. The purpose of this overview is to provide you with a perspective on where circuit analysis fits within the whole of circuit design. Even though this book focuses on circuit analysis, we try to provide opportunities for circuit design where appropriate.

All engineering designs begin with a need, as shown in Fig. 1.4. This need may come from the desire to improve on an existing design, or it may be something brand-new. A careful assessment of the need results in design specifications, which are measurable characteristics of a proposed design. Once a design is proposed, the design specifications allow us to assess whether or not the design actually meets the need.

A concept for the design comes next. The concept derives from a complete understanding of the design specifications coupled with an insight into
the need, which comes from education and experience. The concept may be realized as a sketch, as a written description, or in some other form. Often the next step is to translate the concept into a mathematical model. A commonly used mathematical model for electrical systems is a circuit model.

The elements that comprise the circuit model are called ideal circuit components. An ideal circuit component is a mathematical model of an actual electrical component, like a battery or a light bulb. It is important for the ideal circuit component used in a circuit model to represent the behavior of the actual electrical component to an acceptable degree of accuracy. The tools of circuit analysis, the focus of this book, are then applied to the circuit. Circuit analysis is based on mathematical techniques and is used to predict the behavior of the circuit model and its ideal circuit components. A comparison between the desired behavior, from the design specifications, and the predicted behavior, from circuit analysis, may lead to refinements in the circuit model and its ideal circuit elements. Once the desired and predicted behavior are in agreement, a physical prototype can be constructed.

The physical prototype is an actual electrical system, constructed from actual electrical components. Measurement techniques are used to determine the actual, quantitative behavior of the physical system. This actual behavior is compared with the desired behavior from the design specifications and the predicted behavior from circuit analysis. The comparisons may result in refinements to the physical prototype, the circuit model, or both. Eventually, this iterative process, in which models, components, and systems are continually refined, may produce a design that accurately matches the design specifications and thus meets the need.

From this description, it is clear that circuit analysis plays a very important role in the design process. Because circuit analysis is applied to circuit models, practicing engineers try to use mature circuit models so that the resulting designs will meet the design specifications in the first iteration. In this book, we use models that have been tested for between 20 and 100 years; you can assume that they are mature. The ability to model actual electrical systems with ideal circuit elements makes circuit theory extremely useful to engineers.

Saying that the interconnection of ideal circuit elements can be used to quantitatively predict the behavior of a system implies that we can describe the interconnection with mathematical equations. For the mathematical equations to be useful, we must write them in terms of measurable quantities. In the case of circuits, these quantities are voltage and current, which we discuss in Section 1.4. The study of circuit analysis involves understanding the behavior of each ideal circuit element in terms of its voltage and current and understanding the constraints imposed on the voltage and current as a result of interconnecting the ideal elements.

## 1.4 Voltage and Current

The concept of electric charge is the basis for describing all electrical phenomena. Let's review some important characteristics of electric charge.

- The charge is bipolar, meaning that electrical effects are described in terms of positive and negative charges.
- The electric charge exists in discrete quantities, which are integral multiples of the electronic charge, $1.6022 \times 10^{-19} \mathrm{C}$.
- Electrical effects are attributed to both the separation of charge and charges in motion.

In circuit theory, the separation of charge creates an electric force (voltage), and the motion of charge creates an electric fluid (current).
image_name:Figure 1.4 ∆A conceptual model for electrical engineering design
description:The system block diagram, titled "Figure 1.4 ∆A conceptual model for electrical engineering design," illustrates a structured process for designing electrical circuits. The diagram is organized into several key components and stages, each representing a step in the design and refinement of a circuit.

1. **Main Components:**
- **Need:** This is the initial stage where the requirement or problem is identified.
- **Design Specifications:** Derived from the need, these specifications guide the design process.
- **Concept:** This block represents the initial conceptual idea based on physical insight.
- **Circuit Model:** A theoretical model of the circuit is developed from the concept.
- **Physical Prototype:** A tangible version of the circuit model is created to test its functionality.
- **Circuit Which Meets Design Specifications:** The final product that satisfies the initial design specifications.

2. **Flow of Information or Control:**
- The process begins with identifying a "Need," which flows into "Design Specifications."
- From "Design Specifications," the flow splits into developing a "Concept" and a "Circuit Model."
- "Physical Insight" feeds into the "Concept" stage, enhancing the initial design.
- "Circuit Analysis" is performed on the "Circuit Model," leading to "Refinement Based on Analysis."
- The "Circuit Model" is then used to create a "Physical Prototype."
- "Laboratory Measurements" are conducted on the "Physical Prototype," resulting in "Refinement Based on Measurements."
- Feedback loops exist where the "Circuit Model" and "Physical Prototype" are refined based on analysis and measurements, respectively.
- The process culminates in a "Circuit Which Meets Design Specifications."

3. **Labels, Annotations, and Key Indicators:**
- Arrows indicate the flow of information and refinement processes, with feedback loops clearly marked.
- Labels such as "Physical Insight," "Circuit Analysis," "Refinement Based on Analysis," "Laboratory Measurements," and "Refinement Based on Measurements" provide clarity on the actions taken at each stage.

4. **Overall System Function:**
- The primary function of this system is to guide the development of an electrical circuit from an initial need to a final product that meets specified requirements. The process includes conceptualization, modeling, prototyping, and iterative refinement based on analysis and empirical measurements. This structured approach ensures that the final circuit is both functional and aligned with the initial design objectives.


Figure $1.4 \triangle \mathrm{~A}$ conceptual model for electrical engineering design.

Definition of voltage

Definition of current

The concepts of voltage and current are useful from an engineering point of view because they can be expressed quantitatively. Whenever positive and negative charges are separated, energy is expended. Voltage is the energy per unit charge created by the separation. We express this ratio in differential form as

$$
\begin{equation*}
v=\frac{d w}{d q} \tag{1.1}
\end{equation*}
$$

where
$v=$ the voltage in volts,
$w=$ the energy in joules,
$q=$ the charge in coulombs.
The electrical effects caused by charges in motion depend on the rate of charge flow. The rate of charge flow is known as the electric current, which is expressed as

$$
\begin{equation*}
i=\frac{d q}{d t} \tag{1.2}
\end{equation*}
$$

where
$i=$ the current in amperes,
$q=$ the charge in coulombs,
$t=$ the time in seconds.
Equations 1.1 and 1.2 are definitions for the magnitude of voltage and current, respectively. The bipolar nature of electric charge requires that we assign polarity references to these variables. We will do so in Section 1.5.

Although current is made up of discrete, moving electrons, we do not need to consider them individually because of the enormous number of them. Rather, we can think of electrons and their corresponding charge as one smoothly flowing entity. Thus, $i$ is treated as a continuous variable.

One advantage of using circuit models is that we can model a component strictly in terms of the voltage and current at its terminals. Thus two physically different components could have the same relationship between the terminal voltage and terminal current. If they do, for purposes of circuit analysis, they are identical. Once we know how a component behaves at its terminals, we can analyze its behavior in a circuit. However, when developing circuit models, we are interested in a component's internal behavior. We might want to know, for example, whether charge conduction is taking place because of free electrons moving through the crystal lattice structure of a metal or whether it is because of electrons moving within the covalent bonds of a semiconductor material. However, these concerns are beyond the realm of circuit theory. In this book we use circuit models that have already been developed; we do not discuss how component models are developed.

## 1.5 The Ideal Basic Circuit Element

An ideal basic circuit element has three attributes: (1) it has only two terminals, which are points of connection to other circuit components; (2) it is described mathematically in terms of current and/or voltage; and (3) it cannot be subdivided into other elements. We use the word ideal to imply
that a basic circuit element does not exist as a realizable physical component. However, as we discussed in Section 1.3, ideal elements can be connected in order to model actual devices and systems. We use the word basic to imply that the circuit element cannot be further reduced or subdivided into other elements. Thus the basic circuit elements form the building blocks for constructing circuit models, but they themselves cannot be modeled with any other type of element.

Figure 1.5 is a representation of an ideal basic circuit element. The box is blank because we are making no commitment at this time as to the type of circuit element it is. In Fig. 1.5, the voltage across the terminals of the box is denoted by $v$, and the current in the circuit element is denoted by $i$. The polarity reference for the voltage is indicated by the plus and minus signs, and the reference direction for the current is shown by the arrow placed alongside the current. The interpretation of these references given positive or negative numerical values of $v$ and $i$ is summarized in Table 1.4. Note that algebraically the notion of positive charge flowing in one direction is equivalent to the notion of negative charge flowing in the opposite direction.

The assignments of the reference polarity for voltage and the reference direction for current are entirely arbitrary. However, once you have assigned the references, you must write all subsequent equations to agree with the chosen references. The most widely used sign convention applied to these references is called the passive sign convention, which we use throughout this book. The passive sign convention can be stated as follows:

Whenever the reference direction for the current in an element is in the direction of the reference voltage drop across the element (as in Fig. 1.5), use a positive sign in any expression that relates the voltage to the current. Otherwise, use a negative sign.

We apply this sign convention in all the analyses that follow. Our purpose for introducing it even before we have introduced the different types of basic circuit elements is to impress on you the fact that the selection of polarity references along with the adoption of the passive sign convention is not a function of the basic elements nor the type of interconnections made with the basic elements. We present the application and interpretation of the passive sign convention in power calculations in Section 1.6.

Example 1.2 illustrates one use of the equation defining current.

TABLE 1.4 Interpretation of Reference Directions in Fig. 1.5

Positive Value

$v$ voltage drop from terminal 1 to terminal 2
or
voltage rise from terminal 2 to terminal 1
$i$ positive charge flowing from terminal 1 to terminal 2 or
negative charge flowing from terminal 2 to terminal 1

Negative Value
voltage rise from terminal 1 to terminal 2
or
voltage drop from terminal 2 to terminal 1
positive charge flowing from terminal 2 to terminal 1
or
negative charge flowing from terminal 1 to terminal 2

#### Example 1.2 Relating Current and Charge

No charge exists at the upper terminal of the element in Fig. 1.5 for $t<0$. At $t=0$, a 5 A current begins to flow into the upper terminal.
a) Derive the expression for the charge accumulating at the upper terminal of the element for $t>0$.
b) If the current is stopped after 10 seconds, how much charge has accumulated at the upper terminal?

#### Solution

a) From the definition of current given in Eq. 1.2, the expression for charge accumulation due to current flow is

$$
q(t)=\int_{0}^{t} i(x) d x
$$

Therefore,

$$
q(t)=\int_{0}^{t} 5 d x=\left.5 x\right|_{0} ^{t}=5 t-5(0)=5 t \mathrm{C} \quad \text { for } t>0
$$

b) The total charge that accumulates at the upper terminal in 10 seconds due to a 5 A current is $q(10)=5(10)=50 \mathrm{C}$.

ASSESSMENT PROBLEMS

Objective 2—Know and be able to use the definitions of voltage and current

1.3 The current at the terminals of the element in Fig. 1.5 is

$$
\begin{array}{ll}
i=0, & t<0 \\
i=20 e^{-5000 t} \mathrm{~A}, & t \geq 0
\end{array}
$$

Calculate the total charge (in microcoulombs) entering the element at its upper terminal.

Answer: $4000 \mu \mathrm{C}$.
NOTE: Also try Chapter Problem 1.8.
1.4 The expression for the charge entering the upper terminal of Fig. 1.5 is

$$
q=\frac{1}{\alpha^{2}}-\left(\frac{t}{\alpha}+\frac{1}{\alpha^{2}}\right) e^{-\alpha t} \mathrm{C}
$$

Find the maximum value of the current entering the terminal if $\alpha=0.03679 \mathrm{~s}^{-1}$.

Answer: 10 A .

## 1.6 Power and Energy

Power and energy calculations also are important in circuit analysis. One reason is that although voltage and current are useful variables in the analysis and design of electrically based systems, the useful output of the system often is nonelectrical, and this output is conveniently expressed in terms of power or energy. Another reason is that all practical devices have limitations on the amount of power that they can handle. In the design process, therefore, voltage and current calculations by themselves are not sufficient.

We now relate power and energy to voltage and current and at the same time use the power calculation to illustrate the passive sign convention. Recall from basic physics that power is the time rate of expending or
absorbing energy. (A water pump rated 75 kW can deliver more liters per second than one rated 7.5 kW .) Mathematically, energy per unit time is expressed in the form of a derivative, or

$$
\begin{equation*}
p=\frac{d w}{d t} \tag{1.3}
\end{equation*}
$$

where

$$
\begin{aligned}
p & =\text { the power in watts } \\
w & =\text { the energy in joules } \\
i & =\text { the time in seconds. }
\end{aligned}
$$

Thus 1 W is equivalent to $1 \mathrm{~J} / \mathrm{s}$.
The power associated with the flow of charge follows directly from the definition of voltage and current in Eqs. 1.1 and 1.2, or

$$
p=\frac{d w}{d t}=\left(\frac{d w}{d q}\right)\left(\frac{d q}{d t}\right)
$$

SO

$$
\begin{equation*}
p=v i \tag{1.4}
\end{equation*}
$$

where

$$
\begin{aligned}
p & =\text { the power in watts, } \\
v & =\text { the voltage in volts, } \\
i & =\text { the current in amperes. }
\end{aligned}
$$

Equation 1.4 shows that the power associated with a basic circuit element is simply the product of the current in the element and the voltage across the element. Therefore, power is a quantity associated with a pair of terminals, and we have to be able to tell from our calculation whether power is being delivered to the pair of terminals or extracted from it. This information comes from the correct application and interpretation of the passive sign convention.

If we use the passive sign convention, Eq. 1.4 is correct if the reference direction for the current is in the direction of the reference voltage drop across the terminals. Otherwise, Eq. 1.4 must be written with a minus sign. In other words, if the current reference is in the direction of a reference voltage rise across the terminals, the expression for the power is

$$
\begin{equation*}
p=-v i \tag{1.5}
\end{equation*}
$$

The algebraic sign of power is based on charge movement through voltage drops and rises. As positive charges move through a drop in voltage, they lose energy, and as they move through a rise in voltage, they gain energy. Figure 1.6 summarizes the relationship between the polarity references for voltage and current and the expression for power.
image_name:(a)
description:The system block diagram labeled "(a)" illustrates a basic electrical circuit component represented as a box with two terminals, labeled 1 and 2. The primary focus of this diagram is to illustrate the relationship between current, voltage, and power.

1. **Main Components:**
- The diagram consists of a single box representing an electrical component or system with two terminals.
- The terminals are labeled numerically as 1 and 2, indicating input and output connections.

2. **Flow of Information or Control:**
- The current (i) is shown entering the box at terminal 1 and exiting at terminal 2. The direction of the current is indicated by an arrow.
- The voltage (v) is applied across the terminals, with the positive side connected to terminal 1 and the negative side to terminal 2.
- The flow of current and the polarity of voltage are aligned, indicating that the current enters through the positive voltage terminal.

3. **Labels, Annotations, and Key Indicators:**
- The voltage is labeled with a plus (+) sign at terminal 1 and a minus (-) sign at terminal 2, indicating the polarity.
- The current is labeled with an arrow pointing from terminal 1 to terminal 2.
- The expression for power is given as \( p = vi \), which means that power is being delivered to the circuit inside the box since the product of voltage and current is positive.

4. **Overall System Function:**
- This configuration represents a scenario where power is being delivered to the component inside the box. The alignment of current direction and voltage polarity results in positive power, indicating energy is being supplied to the system. This is a typical representation of a load receiving power.
image_name:(b)
description:The diagram labeled (b) in Figure 1.6 represents a system where the direction of current (i) is flowing into the positive terminal of a two-terminal element, and the voltage (v) across the terminals is labeled with the positive sign on the same side as the current entry. This configuration indicates that the power expression for this setup is \( p = -vi \).

Main Components:
1. **Two-Terminal Element:**
- The diagram shows a block representing an electrical component with two terminals labeled 1 and 2. The component's function is not specified, but it could represent any generic two-terminal device like a resistor, capacitor, or battery.

Flow of Information or Control:
- **Current Flow (i):** The current is shown entering terminal 1 of the block and exiting terminal 2. The direction of the current is indicated by an arrow pointing towards the block.
- **Voltage (v):** The voltage across the terminals is indicated with a positive sign at terminal 1 (where the current enters) and a negative sign at terminal 2.

Labels, Annotations, and Key Indicators:
- The diagram is annotated with the expression \( p = -vi \), indicating the power is negative, meaning power is being extracted from the circuit inside the box.
- Terminals are labeled as 1 and 2 for reference.

Overall System Function:
- The primary function illustrated by this diagram is to demonstrate the relationship between current direction, voltage polarity, and power calculation in a two-terminal element. In this configuration, since the power \( p = -vi \), it implies that the circuit within the block is delivering power to an external circuit or load. This is a typical scenario for a power supply or energy source where the device is supplying power to the rest of the circuit.
image_name:(c)
description:The system block diagram labeled "(c)" illustrates a simple electrical circuit with a focus on the polarity of voltage and the direction of current flow, which affects the power calculation.

1. **Main Components:**
- The diagram consists of a rectangular block representing a circuit element with two terminals, labeled "1" and "2."
- Voltage and current are the primary elements depicted, with specific polarity and direction.

2. **Flow of Information or Control:**
- The voltage across the terminals is labeled with a negative sign at the top and a positive sign at the bottom, indicating a rise in voltage from terminal 2 to terminal 1.
- The current "i" is shown flowing into terminal 1 and out of terminal 2, represented by an arrow pointing from left to right.

3. **Labels, Annotations, and Key Indicators:**
- The voltage is denoted by "v" with polarity indicators showing a negative to positive rise.
- The current "i" is indicated with an arrow and labeled accordingly.
- The expression for power is given as \( p = -vi \), reflecting the relationship between the voltage polarity and current direction.

4. **Overall System Function:**
- This configuration highlights the scenario where power is being extracted from the circuit inside the box. The negative sign in the power expression \( p = -vi \) indicates that the direction of current and the polarity of voltage result in energy being drawn from the circuit element. This aligns with the rule that if the power is negative, energy is being extracted from the circuit.
image_name:(d)
description:The system block diagram labeled "(d)" illustrates the relationship between voltage polarity, current direction, and power expression in an electrical circuit. The diagram consists of a simple block representing a circuit element with two terminals labeled 1 and 2. The key components and their functions are as follows:

1. **Main Components:**
- **Circuit Element Block:** A grey box with two terminals labeled 1 and 2, representing a generic circuit component.

2. **Flow of Information or Control:**
- **Voltage (v):** The voltage across the terminals is indicated by the polarity signs. In this diagram, the positive sign is at terminal 2, and the negative sign is at terminal 1, meaning the voltage rises from terminal 1 to terminal 2.
- **Current (i):** The current direction is shown by an arrow pointing from terminal 1 to terminal 2. This indicates that the current flows into terminal 1 and out of terminal 2.

3. **Labels, Annotations, and Key Indicators:**
- **Polarity and Direction:** The voltage and current are labeled with their respective symbols (v and i), and the direction of current flow is indicated by an arrow.
- **Power Expression:** The expression for power in this configuration is given as \( p = vi \), suggesting that power is being delivered to the circuit element (since p is positive).

4. **Overall System Function:**
- The primary function of this diagram is to illustrate how the polarity of voltage and the direction of current affect the calculation of power in a circuit. In this specific configuration, with the voltage rising from terminal 1 to 2 and current flowing in the same direction, the power calculated is positive, indicating power delivery to the circuit element. This aligns with the rule that when both voltage rise and current flow are in the same direction, power is delivered to the component.


Figure 1.6 $\boldsymbol{\Delta}$ Polarity references and the expression for power.

We can now state the rule for interpreting the algebraic sign of power:

If the power is positive (that is, if $p>0$ ), power is being delivered to the circuit inside the box. If the power is negative (that is, if $p<0$ ), power is being extracted from the circuit inside the box.

For example, suppose that we have selected the polarity references shown in Fig. 1.6(b). Assume further that our calculations for the current and voltage yield the following numerical results:

$$
i=4 \mathrm{~A} \quad \text { and } \quad v=-10 \mathrm{~V}
$$

Then the power associated with the terminal pair 1,2 is

$$
p=-(-10)(4)=40 \mathrm{~W}
$$

Thus the circuit inside the box is absorbing 40 W .
To take this analysis one step further, assume that a colleague is solving the same problem but has chosen the reference polarities shown in Fig. 1.6(c). The resulting numerical values are

$$
i=-4 \mathrm{~A}, \quad v=10 \mathrm{~V}, \quad \text { and } \quad p=40 \mathrm{~W}
$$

Note that interpreting these results in terms of this reference system gives the same conclusions that we previously obtained-namely, that the circuit inside the box is absorbing 40 W . In fact, any of the reference systems in Fig. 1.6 yields this same result.

Example 1.3 illustrates the relationship between voltage, current, power, and energy for an ideal basic circuit element and the use of the passive sign convention.

#### Example 1.3 Relating Voltage, Current, Power, and Energy

Assume that the voltage at the terminals of the element in Fig. 1.5, whose current was defined in Assessment Problem 1.3, is

$$
\begin{array}{ll}
v=0 & t<0 \\
v=10 e^{-5000 t} \mathrm{kV}, & t \geq 0
\end{array}
$$

a) Calculate the power supplied to the element at 1 ms .
b) Calculate the total energy (in joules) delivered to the circuit element.

#### Solution

a) Since the current is entering the + terminal of the voltage drop defined for the element in Fig. 1.5, we use a " + " sign in the power equation.

$$
\begin{aligned}
& p=v i=\left(10,000 e^{-5000 t}\right)\left(20 e^{-5000 t}\right)=200,000 e^{-10,000 t} \mathrm{~W} \\
& \begin{aligned}
p(0.001) & =200,000 e^{-10,000 t(0.001)}=200,000 e^{-10} \\
& =200,000\left(45.4 \times 10^{-6}\right)=0.908 \mathrm{~W}
\end{aligned}
\end{aligned}
$$

b) From the definition of power given in Eq. 1.3, the expression for energy is

$$
w(t)=\int_{0}^{t} p(x) d x
$$

To find the total energy delivered, integrate the expresssion for power from zero to infinity. Therefore,

$$
\begin{aligned}
w_{\text {total }}= & \int_{0}^{\infty} 200,000 e^{-10,000 x} d x=\left.\frac{200,000 e^{-10,000 x}}{-10,000}\right|_{0} ^{\infty} \\
& =-20 e^{-\infty}-\left(-20 e^{-0}\right)=0+20=20 \mathrm{~J}
\end{aligned}
$$

Thus, the total energy supplied to the circuit element is 20 J .

ASSESSMENT PROBLEMS

Objective 3-Know and use the definitions of power and energy; Objective 4-Be able to use the passive sign convention
1.5 Assume that a 20 V voltage drop occurs across an element from terminal 2 to terminal 1 and that a current of 4 A enters terminal 2.
a) Specify the values of $v$ and $i$ for the polarity references shown in Fig. 1.6(a)-(d).
b) State whether the circuit inside the box is absorbing or delivering power.
c) How much power is the circuit absorbing?

Answer: (a) Circuit 1.6(a): $v=-20 \mathrm{~V}, i=-4 \mathrm{~A}$; circuit 1.6(b): $v=-20 \mathrm{~V}, i=4 \mathrm{~A}$; circuit 1.6(c): $v=20 \mathrm{~V}, i=-4 \mathrm{~A}$; circuit 1.6(d): $v=20 \mathrm{~V}, i=4 \mathrm{~A}$;
(b) absorbing;
(c) 80 W .
1.6 The voltage and current at the terminals of the circuit element in Fig 1.5 are zero for $t<0$. For $t \geq 0$, they are

$$
\begin{aligned}
v & =80,000 t e^{-500 t} \mathrm{~V}, & & t \geq 0 \\
i & =15 t e^{-500 t} \mathrm{~A}, & & t \geq 0 .
\end{aligned}
$$

a) Find the time when the power delivered to the circuit element is maximum.
b) Find the maximum value of power.
c) Find the total energy delivered to the circuit element.

Answer: (a) 2 ms ; (b) 649.6 mW ; (c) 2.4 mJ .
1.7 A high-voltage direct-current (dc) transmission line between Celilo, Oregon and Sylmar, California is operating at 800 kV and carrying 1800 A, as shown. Calculate the power (in megawatts) at the Oregon end of the line and state the direction of power flow.
image_name:high-voltage direct-current (dc) transmission line
description:The block diagram represents a high-voltage direct-current (dc) transmission line system, specifically between Celilo, Oregon, and Sylmar, California.

1. **Main Components:**
- **Celilo, Oregon:** This is the starting point of the transmission line. It is represented as a block on the left side of the diagram.
- **Sylmar, California:** This is the endpoint of the transmission line, shown as a block on the right side.
- **Transmission Line:** A line connecting the two blocks, indicating the path of power flow.

2. **Flow of Information or Control:**
- The diagram shows a current of 1.8 kA (1800 A) flowing from Celilo, Oregon, to Sylmar, California, as indicated by the arrow pointing to the right.
- The voltage across the transmission line is labeled as 800 kV, with the positive polarity on the Celilo side and the negative polarity on the Sylmar side. This indicates that power is being transmitted from Celilo to Sylmar.

3. **Labels, Annotations, and Key Indicators:**
- The current is labeled as 1.8 kA, and the voltage as 800 kV.
- The direction of the current is indicated by an arrow, showing the flow from Celilo to Sylmar.

4. **Overall System Function:**
- The primary function of this system is to transmit electrical power over a long distance from Celilo, Oregon, to Sylmar, California. The high voltage of 800 kV allows for efficient transmission with reduced losses over the long distance. The direction of power flow is clearly indicated from Celilo to Sylmar, suggesting a unidirectional power transmission system.


Answer: 1440 MW, Celilo to Sylmar

NOTE: Also try Chapter Problems 1.12, 1.19, and 1.24.

#Practical Perspective

Balancing Power

A model of the circuitry that distributes power to a typical home is shown in Fig. 1.7 with voltage polarities and current directions defined for all of the circuit components. The results of circuit analysis give the values for all of these voltages and currents, which are summarized in Table 1.4. To determine whether or not the values given are correct, calculate the power associated with each component. Use the passive sign convention in the power calculations, as shown below.

$$
\begin{array}{ll}
p_{a}=v_{a} i_{a}=(120)(-10)=-1200 \mathrm{~W} & p_{b}=-v_{b} i_{b}=-(120)(9)=-1080 \mathrm{~W} \\
p_{c}=v_{c} i_{c}=(10)(10)=100 \mathrm{~W} & p_{d}=-v_{d} i_{d}=-(10)(1)=-10 \mathrm{~W} \\
p_{e}=v_{e} i_{e}=(-10)(-9)=90 \mathrm{~W} & p_{f}=-v_{f} i_{f}=-(-100)(5)=500 \mathrm{~W} \\
p_{g}=v_{g} i_{g}=(120)(4)=480 \mathrm{~W} & p_{h}=v_{h} i_{h}=(-220)(-5)=1100 \mathrm{~W}
\end{array}
$$

The power calculations show that components $a, b$, and $d$ are supplying power, since the power values are negative, while components $c, e, f, g$, and h are absorbing power. Now check to see if the power balances by finding the total power supplied and the total power absorbed.

$$
\begin{aligned}
p_{\text {supplied }} & =p_{a}+p_{b}+p_{d}=-1200-1080-10=-2290 \mathrm{~W} \\
p_{\text {absorbed }} & =p_{c}+p_{e}+p_{f}+p_{g}+p_{h} \\
& =100+90+500+480+1100=2270 \mathrm{~W} \\
p_{\text {supplied }} & +p_{\text {absorbed }}=-2290+2270=-20 \mathrm{~W}
\end{aligned}
$$

Something is wrong-if the values for voltage and current in this circuit are correct, the total power should be zero! There is an error in the data and we can find it from the calculated powers if the error exists in the sign of a single component. Note that if we divide the total power by 2 , we get -10 W , which is the power calculated for component d. If the power for component d was +10 W , the total power would be 0 . Circuit analysis techniques from upcoming chapters can be used to show that the current through component d should be -1 A , not +1 A given in Table 1.4.

TABLE 1.4 Volatage and current values for the circuit in Fig. 1.7.

| Component | $v(\mathbf{V})$ | $\boldsymbol{i}(\mathbf{A})$ |
| :---: | ---: | ---: |
| a | 120 | -10 |
| b | 120 | 9 |
| c | 10 | 10 |
| d | 10 | 1 |
| e | -10 | -9 |
| f | -100 | 5 |
| g | 120 | 4 |
| h | -220 | -5 |

image_name:Figure 1.7
description:The circuit represents a power distribution model with multiple voltage sources and defined current directions. Each component has specific voltage and current values.


Figure 1.7 - Circuit model for power distribution in a home, with voltages and currents defined.

Note: Assess your understanding of the Practical Perspective by trying Chapter Problems 1.34 and 1.35.

## Summary

- The International System of Units (SI) enables engineers to communicate in a meaningful way about quantitative results. Table 1.1 summarizes the base SI units; Table 1.2 presents some useful derived SI units. (See pages 8 and 9.)
- Circuit analysis is based on the variables of voltage and current. (See page 11.)
- Voltage is the energy per unit charge created by charge separation and has the SI unit of volt ( $v=d w / d q)$. (See page 12.)
- Current is the rate of charge flow and has the SI unit of ampere $(i=d q / d t)$. (See page 12.)
- The ideal basic circuit element is a two-terminal component that cannot be subdivided; it can be described mathematically in terms of its terminal voltage and current. (See page 12.)
- The passive sign convention uses a positive sign in the expression that relates the voltage and current at the terminals of an element when the reference direction for the current through the element is in the direction of the reference voltage drop across the element. (See page 13.)
- Power is energy per unit of time and is equal to the product of the terminal voltage and current; it has the SI unit of watt $(p=d w / d t=v i)$. (See page 15.)
- The algebraic sign of power is interpreted as follows:
- If $p>0$, power is being delivered to the circuit or circuit component.
- If $p<0$, power is being extracted from the circuit or circuit component. (See page 16.)
