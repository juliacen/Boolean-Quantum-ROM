# Boolean Quantum ROM

This repository contains a Jupyter notebook that constructs a **Boolean Quantum Read-Only Memory (ROM)** using Qiskit. The circuit implements an arbitrary Boolean function \( f : \mathbb{F}_2^n \to \mathbb{F}_2 \), mapping input bitstrings to a single output bit, within a reversible quantum framework.

## Overview

In quantum algorithms, it’s often necessary to embed classical data into quantum circuits in a reversible way. A Boolean quantum ROM circuit performs the transformation:

\[
|x\rangle_n|0\rangle \mapsto |x\rangle_n|f(x)\rangle
\]

This notebook provides a generic template to convert any classical Boolean function \( f \), defined over \( n \)-bit inputs, into a quantum circuit using standard gate-level techniques.

## Contents

### Boolean Function Specification
The user provides a Boolean function as a Python dictionary:

```python
f = {
    "000": 1,
    "001": 0,
    ...
}
```

### Circuit Construction
For each input \( x \) where \( f(x) = 1 \), the following is performed:

1. Apply **X gates** to invert input bits where \( x_i = 0 \)
2. Apply a **multi-controlled X (MCX)** gate targeting the output qubit
3. Undo the **X gates** to restore the input

This effectively flips the output qubit if and only if the input matches an \( x \) such that \( f(x) = 1 \).

### Example
For \( n = 3 \), the notebook builds a circuit that implements a function \( f: \{0,1\}^3 \rightarrow \{0,1\} \) and visualizes it using Qiskit's `draw` function.

### Resource Considerations
- Uses `mcx` gates (multi-controlled Toffoli)
- Scales with the number of \( f(x) = 1 \) entries
- No ancilla required for small functions (Qiskit supports ancilla-free `mcx` up to ~5 controls)
