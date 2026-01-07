+++
title = 'Beyond Not Dying'
date = 2026-01-07
draft = false
+++

In my last post I told you that current flows from higher potential to lower potential energy source (voltage, think positive and negative post in the battery). The statement of conventional current flowing this way is true, and yet to really start to understand what is even happening we need to talk about electron flow now. I know that my stories of death, house fires and holiday catastrophe are way more interesting. However, you really only need to know that stuff not to die. To really live (in the world of electronics) we turn to physics.

Lets just establish that the electrons move from negative to positive (because opposites attract). I made it to the third article before I brought up a boring theorem or law. I suppose I brought up Ohm's law, but that isn't that bad as the name sounds cool. The next principles we need to learn about electricity are the fundamentals in how you design a circuit.

**Kirchhoff's Current Law** - *The algebraic sum of currents in a network of conductors meeting at a point is zero.*

Cliff's translation - *All the current that flows in, must flow out.*

Cliff's translation of why - *Wire is a highway, not a parking lot. Electrons must keep moving. Electrons are matter, and they cannot occupy the same space as another electron. Because electrons repel each other, they cannot pile up in one spot; they force the traffic to keep moving.*

![Kirchhoff's Current Law diagram](/kcl.jpeg)

**Kirchhoff's Voltage Law** - *The directed sum of the potential differences (voltages) around any closed loop is zero.*

Cliff's translation - *A trip from Point A to Point B costs the same energy, regardless of the path.*

Cliff's translation of why - *The electrons lose the same energy. The electric field (the invisible landscape that voltage creates) is geometry that doesn't change based on your path. You've seen me use the word "potential" to describe voltage. That flow we talked about in the last post is always between a "potential difference", a higher point and lower point in a geometric field. In our case, if you view the electric field like a mountain, the height doesn't change just because you took a different trail up or down.*

![Kirchhoff's Voltage Law diagram](/kvl.jpeg)

So why did I just drag you through physics definitions and talk about "fields" and "matter"? Because these two laws are the secret decoder ring for the two most common circuit configurations you will ever see.

When you wire things together, the universe forces the circuit to find a balance. Depending on *how* you wire it, one variable gets locked down (the Constraint), forcing the other variable to change to compensate.

### 1. Series Circuits: The "Single Lane Highway"

In a series circuit, there is only one physical path for the electrons to travel.

- **Apply the Current Law (KCL):** Remember, "Wire is a highway, not a parking lot." Since there is only one road, traffic cannot turn off, and it cannot park. Every electron that leaves the battery must march through every single component to get home.

- **The Constraint:** **Current is locked.** It is identical everywhere in the loop.

- **The Consequence:** Since the flow is fixed, the *Energy* (Voltage) is what has to split. You "spend" a portion of your total voltage at every obstacle you hit, proportional to how hard it is to get through.

![Series circuit diagram](/series.png)

### 2. Parallel Circuits: The "Ski Slope"

In a parallel circuit, you have multiple paths (branches), but they all connect to the same two points, the same start and the same finish.

- **Apply the Voltage Law (KVL):** Remember, "The mountain doesn't change." Since every branch connects to the exact same top rail (High Potential) and bottom rail (Low Potential), the "vertical drop" is identical for everyone.

- **The Constraint:** **Voltage is locked.** It is identical across every branch.

- **The Consequence:** Since the electrical pressure is fixed, the *Traffic* (Current) is what has to split. The current divides itself up based on difficulty: massive flow goes down the easy paths (low resistance), and a trickle goes down the hard paths (high resistance).

![Parallel circuit diagram](/parallel.png)

### The Cliff's Notes Summary

If you ever get confused, just ask: **"What is the constraint?"**

- **Series:** The Path is the constraint → **Current** stays the same, **Voltage** splits.

- **Parallel:** The Geometry is the constraint → **Voltage** stays the same, **Current** splits.

In the next article I'll start talking about more complex pieces of electronics, and we'll talk about alternating current (AC) vs direct current (DC) and how it impacts these new components. Until then dwell in the essence of some new found physics in how it relates to electricity!
