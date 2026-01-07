+++
title = 'Shockingly Common Sense'
date = 2026-01-05
draft = false
+++

When I was attending Texas Tech I worked at a particular orange big box home improvement store in the electrical department. There were two horror stories that I remember from this time: the first was the guy that needed an extension cord with two male ends; the second was the guy that kept burning up light switches by connecting the black and the white wire to each side.

The craziest part here is these ideas were just innate in me to never do, maybe it has something to do with genetics. My grandfather and uncle were both master electricians. Regardless of why I was beside myself when these two presented their problems to me.

So why are these things dangerous?

The danger in plain English: If you have two male ends on an extension cord and one is plugged in to the wall, what we would call the voltage source, the other end is electrified. It is just looking for something, possibly you, to close the circuit. The same is true for wiring up the switch with the black and white wires, when you flip the switch you close the circuit. Cue electrocution or fire.

If we take first principles thinking I'd present:
1. Conventional current flows from higher potential energy to lower potential energy.
2. A circuit must be closed between the two voltage potentials for current to flow.

The figure below shows a closed circuit with a battery (voltage source), a light bulb (load), and a switch that is turned on (closed).

![Closed circuit diagram showing a light switch and circuit with higher and lower potential energy](/circuit.jpg)

Current flows from the higher potential (positive side) to the lower potential (negative side) of the battery. In the diagram we can denote:
- The battery supplying the "push"(voltage)
- The resistance of the light bulb
- The resistance of the switch

If you turn the switch on (close the circuit), that switch looks schematically like a 0 ohm resistor. This allows current to flow to the light bulb. We can fill in with Ohm's law what is happening. If its a 60 W light bulb, and your battery is 120 V you have .5 A of current flowing through the circuit.

If you then turn the switch off (open the circuit), that switch looks schematically like a near infinite ohm resistor. Since there is not enough voltage to push through that resistance current cannot flow. Power will not be emitted as light.

Go back to those horror stories; the guy with the burned up light switches was basically connecting the battery positive and battery negative to the light switch, and then turning it on.

If the white and black wire are connected to the light switch instead of breaking a single side of the circuit there is no light bulb present to consume energy anymore from the voltage source's perspective. Without a bulb to slow it down, the electricity rushes through at maximum velocity, turning the wire itself into a heating element. Remember power is V (voltage) times I (current) so if current is almost infinity because resistance is almost 0 then power is really high!

![Switch miswired with hot and neutral](/switchmiswire.png)

In the other example from the store he wanted to make a two male sided extension cord. Once you plug in the cord to the wall that wire is just an open switch and if you pick up the cord to plug it in, and potentially touch the metal you become the light bulb, and also near 0 resistance but instead of heating up the wire, it heats up you.

![Electrocution danger from double male extension cord](/zap.png)

In house wiring (AC) it takes about 1/14 of an amp to stop the human heart.

So you can see now why both of these ideas are bad. Fire, death, sparks, etc. are all possibly horrible ends to an uninformed attempt at fixing a real world problem at home. This is why people are often afraid of electricity.

These two principles, current flowing from higher potential energy to lower potential energy, and requiring a closed circuit are key steps in understanding how electricity works. I hope it helped shed light on a few things. Until next time be safe, and don't wire your voltage source to itself with no load in between. Remember: A circuit needs a 'load' (a purpose, a struggle, a light bulb) to be useful. Energy without a burden to carry doesn't create light; it just burns out the wire.

P.S. What is it with Christmas stuff that causes people to take on electrical problems and potentially bring grave harm to themselves and, or their houses? Thanksgiving is all about grease fires, Christmas is about electrical fires. Sometimes I think that it is a damned miracle we've survived as a species for as long as we have, but man I love sparkly lights at Christmas and fried turkey! Remember that 0.07 A of current will kill you, and the breaker saves your house, not you.
