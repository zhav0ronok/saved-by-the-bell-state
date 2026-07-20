---
title: The Transpiler
---
Qiskit gives the user the ability to execute their code on real quantum hardware, however, in order to do this, the input circuit (that is, the one you create) must undergo a series of transformations in order to be compatible with the target device's hardware. This process is known as **transpilation**.

To transpile with Qiskit, you must first import it:
```
from qiskit import transpile
```
