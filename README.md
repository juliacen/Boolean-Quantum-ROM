# Boolean Quantum ROM

This repository contains a Jupyter notebook that constructs a **Boolean Quantum Read-Only Memory (QROM)** using Qiskit. Specifically, we build a circuit that simulates any function that maps an arbitrary sized Boolean string to a 0 or 1. 

## Introduction

The idea of a QROM is to help us store classical inofrmation/data on quantum computer. The type of QROM built in this notebook is especially advantageous when the data is sparse, meaning that the function f is 1 for only a small fraction of possible inputs. In such cases, the QROM can be implemented with exponentially fewer quantum gates than encoding a full classical truth table. This makes it an efficient approach for representing large, mostly-zero classical datasets inside a quantum algorithm.

## Contents of Notebook

### 1) Boolean Function Definition
The user provides a Boolean function as a Python dictionary.

### 2) QROM Construction
For each Boolean string input where the output is 1, the following is performed:

1. Apply **X gates** to invert input bits where they are 0
2. Apply a **multi-controlled X (MCX)** gate targeting the output qubit
3. Undo the **X gates** to restore the input

This effectively flips the output qubit if and only if the input matches an x  such that f(x) = 1.

### 3) An Example
The notebook gives an example of a Boolean function as a dictionary for \( n = 3 \), but this can always be generalized for arbitrary \( n \).
