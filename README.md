\# Quantum Palindrome Search using Grover's Algorithm



This repository contains a quantum computing implementation of Grover's Search Algorithm using Qiskit. The project utilizes a custom Quantum Oracle to identify palindrome binary strings (sequences that read the same forwards and backwards) within an unstructured search space.



\## Project Overview



Grover's Algorithm provides a quadratic speedup for unstructured search problems. This implementation adapts the algorithm to search for "palindromic" states among $2^n$ possible bitstrings.



For a bitstring of length $n$, the oracle identifies states where the outer bits match the inner bits symmetrically. The circuit consists of three main stages:



1\. \*\*Initialization:\*\* Creating an equal superposition of all possible states using Hadamard gates.

2\. \*\*Oracle (ZF):\*\* Marks the palindrome states by flipping their phase.

3\. \*\*Diffuser (ZOR):\*\* Amplifies the amplitude of the marked states (inversion about the mean).



\## Requirements



To run this simulation, you need Python installed with the following libraries:



\- `qiskit`

\- `qiskit-aer`

\- `numpy`

\- `matplotlib`

\- `ipython`



\## Implementation Details



\### The Oracle (ZF)

The Phase Oracle detects palindromes without prior knowledge of the solution. It relies on the property of CNOT gates where $Target = Control \\oplus Target$.



1\. \*\*Comparison:\*\* The algorithm applies CNOT gates between symmetric qubit pairs (e.g., qubit $i$ and qubit $n-1-i$). If the bits are identical, the XOR operation results in 0.

2\. \*\*Phase Kickback:\*\* The circuit inverts the results (0 to 1) and applies a Multi-Controlled Phase gate. This flips the phase of the state only if all symmetric pairs match.

3\. \*\*Uncomputation:\*\* The CNOT and X gates are applied in reverse to restore the auxiliary qubits to their original state, ensuring entanglement is not broken.



\### The Diffuser (ZOR)

The diffuser performs the standard reflection about the mean amplitude. It is implemented using:

\- Hadamard gates on all qubits.

\- X gates on all qubits.

\- A multi-controlled phase shift.

\- Reversal of X and Hadamard gates.



\### Optimal Iteration Calculation

The code automatically calculates the optimal number of Grover iterations to avoid over-rotation. It uses the exact formula:



$$k \\approx \\text{round}\\left( \\frac{\\pi}{4 \\theta} - \\frac{1}{2} \\right)$$



Where $\\theta = \\arcsin(\\sqrt{M/N})$, $N = 2^n$ is the total search space, and $M = 2^{\\lceil n/2 \\rceil}$ is the number of palindrome solutions.



\## Usage



1\. Download the repository files to your local machine.

2\. Open the script in a Jupyter Notebook environment or run it as a standard Python script.

3\. When prompted, enter the simulation parameters:

&nbsp;  - \*\*BitString Length:\*\* The number of qubits ($n$).

&nbsp;  - \*\*Shots:\*\* The number of simulation runs (e.g., 1024 or 8192).



\## Results



The program outputs the list of high-probability binary strings found and displays the measurement distribution via:

\- A pie chart showing the probability distribution of high-confidence palindrome states (filtered for noise).

\- A histogram detailing the raw measurement counts for all states.



Successful execution will show a high probability peak at palindrome states (e.g., `10001`, `01110`, `00000`).





