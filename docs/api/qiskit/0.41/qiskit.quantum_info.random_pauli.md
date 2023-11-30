---
title: random_pauli
description: API reference for qiskit.quantum_info.random_pauli
in_page_toc_min_heading_level: 1
python_api_type: function
python_api_name: qiskit.quantum_info.random_pauli
---

# qiskit.quantum\_info.random\_pauli[¶](#qiskit-quantum-info-random-pauli "Permalink to this headline")

<span id="qiskit.quantum_info.random_pauli" />

`random_pauli(num_qubits, group_phase=False, seed=None)`

Return a random Pauli.

**Parameters**

*   **num\_qubits** (*int*) – the number of qubits.
*   **group\_phase** (*bool*) – Optional. If True generate random phase. Otherwise the phase will be set so that the Pauli coefficient is +1 (default: False).
*   **seed** (*int or np.random.Generator*) – Optional. Set a fixed seed or generator for RNG.

**Returns**

a random Pauli

**Return type**

[Pauli](qiskit.quantum_info.Pauli "qiskit.quantum_info.Pauli")
