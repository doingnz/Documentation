---
layout: Hardware
title: Light-Emitting Diodes
---

LEDs are a type of diode that emit photons (light) as electrons flow through the P-N junction. These are awesome! LEDs are everywhere around us; they're used as lights, indicators, and even display screens. 

These bar graph displays use LEDs to indicate a battery charge or an operating value:

![Photo of two components each made from several different-colored LEDs. One component is simply several LEDs next to each other. The other has the LEDs grouped to look like a battery where the number of LEDs illuminated indicates the level of charge in the battery.](/Hardware/Tutorials/Electronics/Part6/Light_Related_Diodes/LED_Graph_Displays.jpg)

Many modern [displays](https://en.wikipedia.org/wiki/LED_display) also use LEDs to power their pixels, with each pixel containing three diodes; red, green, and blue. With each color (R, G, B) brightness controlled individually to create nearly any color.

## Overview

LEDs come in a variety of packages and combinations. Many packages have an arrangement of multiple LEDs in one, such as bar graphs and _7 segment_ displays that are often used to show levels or digit characters.

<!-- MarkT: commented out, this is a broken link 
![](/Hardware/Circuits/Components/LEDs/SomeLEDs.jpg)
-->

Regardless of what they look like, they're all basically the same to use. There are only two practical circuit concerns: making sure the _polarity_ is correct and limiting the current through them so they don't burn out.

The circuit symbol for an LED is a diode with arrows coming out of it, signifying the photon emission:

![LED symbol which is a diode with two arrows coming out, indicating photon emission.](/Hardware/Tutorials/Electronics/Part6/Support_Files/LED.svg)

### Physics

As electrons move into the holes in the P-Type lattice from the N-Type, they move from a higher energy orbit/state, known as the _conductance band_, to a lower energy orbit/state. When that transition happens, they lose energy. However, as the [first law of thermodynamics](https://en.wikipedia.org/wiki/First_law_of_thermodynamics) states; energy cannot be destroyed or created, only converted; so that energy is released in the form of photons (light particles):

![Diagram of an electron moving from a higher-energy state to a lower-energy state and causing a photon to be released from the lattice.](/Hardware/Tutorials/Electronics/Part6/Support_Files/Photon_Emission.svg)

In silicon, the electron orbital drop is very small, so the light released is low energy and the photon escapes at a low frequency of vibration. Since the color of light depends on its frequency, the light emitted is in the infrared spectrum, which is just below the frequency energies of the visible light spectrum.

Most diodes are designed in such a way that the P-N junction is hidden inside its casing, so these emissions are not visible. LEDs, however, are constructed in such a way that light can escape through them, and the materials used also have a much higher electron orbital energy drop when they combine with the holes.

#### Polarity

Typical through-hole LEDs have a flat spot on the cathode side, and a longer anode leg, signifying how to wire them up with the correct polarity:

![Diagram of the internal and external components of an LED. The external case has a flat spot to indicate which of the two legs is the cathode.](/Hardware/Tutorials/Electronics/Part6/Support_Files/LED_Components.svg)

### LED Colors

Because LEDs have a higher electron orbital energy transition than most diodes, the photons released are at higher energy/frequency, usually in the visible light spectrum (note that the energy/frequency is higher to the left, and lower to the right in the following image):

![Diagram of the visible light spectrum and the colors associated with different frequency.](/Hardware/Tutorials/Electronics/Part6/Support_Files/Linear_visible_spectrum.svg)

What's interesting about this, is that in order to change the color of light emitted, differing voltage drops (`V`<sub>`f`</sub>) are needed. The voltage drop therefore generally increases with the light frequency:

| Color  | Typical `V`<sub>`f`</sub> (Voltage drop)| Typical `I`<sub>`fmax`</sub> (max. current) |
|--------|---------------|------------------|
| Red    | 1.8V          | 15mA - 20mA      |
| Yellow | 2.0V          | 15mA             |
| Green  | 2.1V          | 20ma - 30mA      |
| Blue   | 2.7V - 3.6 V  | 20mA             |
| White  | 1.9V - 2.4V   | 30mA             |

White LEDs are usually a blue LED with a coating that turns the light white, however, some higher-end white LEDs actually have red, green, and blue LEDs in them which light in unison to create white.

Powering blue LEDs can be tricky on `3.3V` because many of them have more than a `3.3V`<sub>`f`</sub>. These LEDs need to be driven by a special circuit that increases the voltage if there is only `3.3V` available, as in the case with the digital output on Meadow and Netduino. However, it's much easier just to use blue LEDs with a smaller voltage drop. There are many that have as low as `2.65V`<sub>`f`</sub>. So if you're using `3.3V` to power your LEDs, make sure that you check the voltage drop on them when purchasing.

#### Red, Green, Blue (RGB) LEDs

RGB LEDs are available that have all three color components in a single package. By varying the amount of current to each leg, nearly any hue in the rainbow can be created.

Through-hole RGB LEDs will have a "common" leg that's longer than the rest, which could be anode or cathode, depending on if they're _common anode_ or _common cathode_:

![Photo of an RGB LED showing one leg longer than the rest.](/Hardware/Tutorials/Electronics/Part6/Support_Files/RGB_LED_Photo.jpg)

## Using LEDs in Circuits

Single LED circuits are typically fairly simple, requiring only a DC power source and a resistor to restrict current flow:

![Circuit diagram of the positive terminal of a voltage source connected to a resistor, then to an LED, and finally to the negative terminal of the source.](/Hardware/Tutorials/Electronics/Part6/Support_Files/LED_Circuit_Simplified.svg)

RGB LEDs are only slightly more complex. They come in two flavors, depending on whether they're common cathode or common anode:

![Diagram of the two types of RGB LEDs showing how each type would be connected to a voltage source.](/Hardware/Tutorials/Electronics/Part6/Support_Files/RGB_LED_Wiring.svg)

### Controlling Current

If you plug in an LED to a `3.3V` voltage source without reducing the voltage (and current), the LED is going to be very bright and then it's going to burn out.

#### Non-Ohmic Devices

This failure illuminates an interesting behavior of P-N junctions that warrants further explanation.

LEDs (actually, all P-N junctions) are referred to as _non-ohmic_ devices. Non-ohmic is a bit of a misnomer, because it implies that that they don't abide by Ohm's law; and this is a common source of confusion. 

To understand what this really means, we need to revisit Ohm's law. Ohm's law states that the amount of current than can pass through a device is a proportional function of how much force (voltage) is pushing against resistance:

```
Current = Force / Resistance
I = V / R
```

This means that as we increase the voltage (amount of force), as long as the resistance stays the same, the amount of current allowed to flow is proportional:

![Graph of voltage on the x-axis against current on the y-axis. The relationship is a 45º line beginning at the origin and moving up and to the right.](/Hardware/Tutorials/Electronics/Part6/Support_Files/Ohms_Law_Behavior_Graph.svg)

However, recall that with a P-N junction, as the voltage increases, the resistance actually goes down, which means that more current is allowed to flow. Recall the same scenario with a P-N junction looks like this:

![Graph of voltage on the x-axis against current on the y-axis for a P-N junction. The current remains near zero initially as voltage increases, then rises rapidly over a very small increase in voltage.](/Hardware/Tutorials/Electronics/Part6/Support_Files/Diode_Forward_Behavior.svg)

Once the voltage requirement has been met to overcome the junction potential, further increase in voltage greatly reduces the resistance of the diode, and therefore, the amount of current that the diode will conduct rises rapidly. The trick with LEDs then is to supply just enough voltage to light them up.

#### Options for Limiting Current

There are two common ways to control the voltage, either with a resistor or by driving it with a _PWM_ signal.

Using a resistor is the simplest way, but has the limitation of setting it at a fixed brightness when `ON`. A PWM signal is also reasonably simple, but is usually generated inside a microcontroller and controlled by software, rather than generated by an external circuit. The advantage of a PWM signal is that you have dynamic control of the voltage, allowing you to gently "pulse" the LED on and off.

#### Limiting Current with a Ballast Resistor

A resistor that's used to limit runaway current is sometimes called a _ballast_ resistor.

To calculate the resistance needed to reduce the voltage, we start with Ohm's law, solved for resistance:

```
R = V / I
ohms = volts / amps
```

However, because P-N junctions have a voltage-drop (`V`<sub>`f`</sub>), in which they "push back," that does something interesting to our calculation.

This means that the overall voltage available to the LED is actually reduced by that `V`<sub>`f`</sub>. Therefore to calculate the resistance needed, we need to account for the voltage drop by subtracting it from the voltage source:

```
R = (Vs - Fv) / I
```

![Circuit diagram of the positive terminal of a voltage source connected to a resistor, then to an LED, and finally to the negative terminal of the source.](/Hardware/Tutorials/Electronics/Part6/Support_Files/Single_LED_Circuit.svg)

##### Example

For example, let's say that we have a red LED that has a maximum current rating of `20mA`, and a `V`<sub>`f`</sub> of `1.8V`, and we're driving it from a `3.3V` voltage source. Solving for `R` then:

```
R = (3.3V - 1.8V) / 0.020A = 75Ω
```

The circuit would need at least a `75Ω` resistor to safely drive the LED.

However, in practice, we typically use a much larger resistor value because at the maximum current, LEDs tend to be far too bright, and therefore need to be dimmed. I typically double the required resistor value and then tune from there.  In fact, most of the time when throwing together quick circuits, I just grab a `330Ω` resistor and call it good!

### LEDs in Parallel

It's technically possible to use a single resistor with LEDs in parallel:

![Circuit diagram of the positive terminal of a voltage source connected to a resistor, then to three LEDs wired in parallel, and finally to the negative terminal of the source.](/Hardware/Tutorials/Electronics/Part6/Support_Files/LED_Parallel_Circuit.svg)

However, in practice, it's nearly impossible, because the voltage drop of LEDs are almost never perfectly balanced, which causes only one of them to conduct, pass too much current and fail, thus starting a cascade of failing LEDs.

Instead, the best practice is to use a resistor for each LED:

![Circuit diagram of the positive terminal of a voltage source connected to three sub-circuits wired in parallel and then to the negative terminal of the source. Each sub-circuit consists of a resistor and an LED connected in series.](/Hardware/Tutorials/Electronics/Part6/Support_Files/LED_Parallel_Circuit_Practical.svg)

In this case, each resistor is calculated as individual LED circuits.

If you need to calculate the total current draw, simply add the current from each LED up, as per [Kirchhoff's Current Law](/Hardware/Tutorials/Electronics/Part5/Kirchhoffs_Current_Law/).

#### Understanding the Failure

To understand the failure of parallel LEDs with a single resistor, imagine the circuit as a deep river gorge that has  dam blocking the flow of water. The dam is divided into three segments and each segment is a different height. The segments of the dam represent the LEDs. The varying segment heights indicate that each LED has a little different voltage height due slight variations during manufacture:

![Illustration of the front view of a dam with three segments of different heights.](/Hardware/Tutorials/Electronics/Part6/Support_Files/Dam_w_Varying_Heights.svg)

When the river "turns on," behind the dam, the river will rise until it reaches the top of the shortest segment, and when it does, it'll start to flow over that segment:

![Illustration of the front view of a three-segment dam with water flowing over the shortest segment.](/Hardware/Tutorials/Electronics/Part6/Support_Files/Dam_w_Single_LED.svg)

However, as soon as that segment starts to let water flow, imagine that the height of that segment of the dam actually gets lower, which means _more_ current is allowed to flow, current that was intended to spill over the other dams.

![Illustration of the front view of a three-segment dam where the shortest segment of the dam has lowered thus letting the water flow through that segment almost unimpeded.](/Hardware/Tutorials/Electronics/Part6/Support_Files/Dam_w_Avalanche_Breakdown.svg)

Finally, with ALL the current that was intended to be distributed across three dams flowing through that segment, the segment will fail and for a brief moment, let a lot of current through, before the infrastructure completely gives out (diode breaks), and closes off that river:

![Illustration of the front view of a three-segment dam where the shortest segment of the dam has completely collapsed and the rubble has entirely blocked the water from flowing through that area.](/Hardware/Tutorials/Electronics/Part6/Support_Files/Dam_w_Diode_Failure.svg)

Then the process repeats itself for the remaining segments of the dam.

### LEDs in Series

LEDs can be placed in series, as in the following configuration:

![Circuit diagram of the positive terminal of a voltage source connected first to a resistor, then to three LEDs all wired in series, and finally to the negative terminal of the source.](/Hardware/Tutorials/Electronics/Part6/Support_Files/LED_Series_Circuit.svg)

However, there are two important considerations in this particular configuration.

First, since the [current for all the components in series is the same](/Hardware/Tutorials/Electronics/Part4/Series_Resistance/#common-current-different-voltage), all the LEDs have to be rated for the same current; you _can_ mix colors and get the same amount of brightness from each one, but they have to have the same current rating.

Secondly, the `V`<sub>`f`</sub> of each LED is additive; which requires a voltage source with a high enough voltage to overcome the sum of the voltage drops, with enough leftover voltage to still drive current. A general guide is to use a voltage source that is about `1.5x` the sum of the voltage drops.

#### Resistor Calculation

Calculating the resistance needed is the same as a single LED, except that you must remove all the voltage drops from the voltage source, and the current (`I`) must be the same:

```
R = (Vs - (Vf1 + Vfn...)) / I
```

#### Sample Circuit

Consider the following series LED circuit:

![Circuit diagram of the positive terminal of a voltage source connected to a resistor and two LEDs all wired in series, then to the negative terminal of the source.](/Hardware/Tutorials/Electronics/Part6/Support_Files/LED_Series_Circuit_Example.svg)

The first thing to consider here is the voltage requirement; the circuit contains two LEDs, one green LED with a `V`<sub>`f`</sub> of `2V`, and a blue LED with a `V`<sub>`f`</sub> of `3V`, for a total of `5V` voltage drop. That means that we'll likely need at least somewhere near `7.5V` to power the LEDs; something that would be impossible to power directly from a `3.3V` output from a Meadow or Netduino board. In this case, we'd need to power from an external power supply and switch via a transistor (which we'll cover in the next chapter). Instead it would probably be simpler just to wire them in parallel.

However, if we did have an adequate voltage source, the resistance needed is easy to solve for:

```
Given:
R = (Vs - (Vf1 + Vfn...)) / I

Therefore:
R = (9V - (2V + 3V)) / .020A
R = 200Ω
```

In this case, we'd need at least `200Ω` resistor to keep them within their current limits.

### Online LED Resistance Calculator

While [iCircuit](http://icircuitapp.com/) is my go-to tool for circuit simulation and calculation, for one-off LED resistor calculations, there's a fantastic [LED resistor calculator at OhmsLawCalculator.com](http://www.ohmslawcalculator.com/led-resistor-calculator).

### Reducing Current with a PWM Signal

In order to "pulse" an LED, that is; gradually dim it on or off, you'd either need a complicated circuit or use a Pulse-Width-Modulation (PWM) signal:

![Illustration of a PWM 50% Duty Cycle. The voltage is a square wave alternating equally between 0 and 3.3 volts with an average of 1.6 volts.](/Hardware/Tutorials/Electronics/Part6/Support_Files/PWM_50p_DutyCycle.svg)

PWM is a way of controlling voltage digitally to emulate an analog signal. Instead of either being at `HIGH` or `LOW` such as `3.3V` or `0V`, it can actually have an intermediate value such as `1.6V`; by rapidly turning it off and on. Because of the inertia of electrons and the latency of the P-N junction change, the LED actually "sees" a voltage that is an average of the `ON`/`OFF` value:

A PWM signal generated by Meadow is a _square_ wave and the two key parameters available to control it are the _frequency_ and the _duty cycle_.

In the above diagram, the time where the signal is high is the same as the time where the signal is low. The percentage of time the signal is on (`HIGH`) is called the duty cycle. In the above illustration the signal is high 50% of each cycle and therefore the duty cycle is 50%. Consequently, the average voltage of the signal is 50% of `3.3V`, or `1.6V`.

To lower the voltage, we typically reduce the duty cycle (amount of time `ON`):

![Illustration of a PWM 25% Duty Cycle. The voltage is a square wave alternating between 0 and 3.3 volts. The signal is high 25% of the time which yields an average of 0.8 volts.](/Hardware/Tutorials/Electronics/Part6/Support_Files/PWM_25p_DutyCycle.svg)

#### Frequency and Flicker

Because a PWM signal is actually a pulse, at lower frequencies it can cause a noticeable flicker. Humans start to perceive a flicker at around `60Hz` (60 cycles per second) or lower, so it's best to make sure the frequency is above that. Fortunately, this isn't typically an issue, since modern microcontrollers (like the ones that power Meadow and Netduino) are capable of driving PWM signals at many thousands of hertz (Hz).

Incidentally, pigeons notice flicker around `100hz`, so if you're designing circuits for pigeons, you'll need to make sure that your PWM frequency is `100Hz` or higher. 🤣

