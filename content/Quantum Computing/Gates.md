---
title: Gates
---

If you are at all familiar with [logic gates](https://en.wikipedia.org/wiki/Logic_gate), then **quantum logic gates** (which I will just refer to here as "gates", or "quantum gates") will be intuitive for you.

A quantum gate is a **unitary transformation** on one or more qubit. If you have taken linear algebra, you are likely familiar with unitary matrices, and unsurprisingly, quantum gates correspond to exactly those. 


> [!NOTE] Unitary Matrix
> A matrix $U$ such that its inverse equals its conjugate transpose:
> $$U U^{\dagger} = U^{\dagger} U =1$$

Gates can also be drawn as elements of quantum circuits. An example is shown below:
![[DemoCircuit-1.png]]
*Figure 1: Hadamard gate (red) applied to the first qubit $q_0$ and CNOT gate (blue) applied between $q_0$ and $q_1$.*

Note: This is the output from running the demo circuit from the Qiskit documentation.[^1]

[^1]: Technical detail: if you are executing this code in nvim with LazyVim as I am, you will not be able to create images like this in the built-in terminal. See [[Technical Note]] for more information. 