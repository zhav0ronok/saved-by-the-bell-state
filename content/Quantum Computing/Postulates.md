There are six postulates of quantum mechanics. These are taken from a handful of sources, but I have most heavily cited David McIntyre's textbook. 
### I.)
**The state of a system is described in its entirety (that is, everything that can possibly be known about it) is represented mathematically by a normalized ket $|\psi\rangle$.** 

Alternatively, the state of the system is described in its entirety by a wavefunction $\psi(\mathbf{r},t)$.

### II.)
**A physical observable is represented by an Hermitian operator $A$ which acts on a ket, and whose eigenvectors form a complete basis.**

### III.)
**The only possible measurement of an observable corresponding to the operator $A$ is one of its eigenvalues, $a_{n}$.**

### IV.) Probability Postulate
The probability of obtaining $a_{n}$ as the result of a measurement of $A$ on the system in the state $|\psi\rangle$ is
$$
\boxed{\mathcal{P}_{a_{n}}=|\langle a_{n} | \psi\rangle|^2}
$$

### V.) Projection Postulate
**After a measurement of $A$ yielding $a_{n}$, the quantum system, originally in state $|\psi\rangle$ is now in a new state $|\psi'\rangle$, which is the normalized projection of $|\psi\rangle$ onto** 
$$
\boxed{|\psi'\rangle = \frac{P_{n}|\psi\rangle}{\sqrt{ \langle \psi | P_{n}|\psi\rangle }}}
$$
Where, $P_{n}$ are projection operators. For more information on this, see section [[1.3 - Operators#1.3.3 - Projection Operators|1.3.3]]. 
### VI.) Time Evolution
**The time evolution of a quantum system is given by the Schrödinger equation:**
$$
\boxed{i\hbar \frac{d}{dt}|\psi(t)\rangle = H(t)|\psi(t)\rangle}
$$
**Where $H(t)$ is the Hamiltonian (total energy) operator.** 

In an intro quantum class, there are very few cases of this equation that can be dealt with:
1. Time independent Hamiltonian
2. Periodic Hamiltonian
3. Time-random Hamiltonian

***
#### Useful Resources
- https://web.stanford.edu/class/rad226a/Lectures/Lecture5-2019-Quantum-III.pdf
