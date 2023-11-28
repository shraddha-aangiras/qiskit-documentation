---
title: ConstrainedReschedule
description: API reference for qiskit.transpiler.passes.ConstrainedReschedule
in_page_toc_min_heading_level: 1
python_api_type: class
python_api_name: qiskit.transpiler.passes.ConstrainedReschedule
---

# ConstrainedReschedule

<span id="qiskit.transpiler.passes.ConstrainedReschedule" />

`qiskit.transpiler.passes.ConstrainedReschedule(*args, **kwargs)`

Bases: [`AnalysisPass`](qiskit.transpiler.AnalysisPass "qiskit.transpiler.basepasses.AnalysisPass")

Rescheduler pass that updates node start times to conform to the hardware alignments.

This pass shifts DAG node start times previously scheduled with one of the scheduling passes, e.g. [`ASAPScheduleAnalysis`](qiskit.transpiler.passes.ASAPScheduleAnalysis "qiskit.transpiler.passes.ASAPScheduleAnalysis") or [`ALAPScheduleAnalysis`](qiskit.transpiler.passes.ALAPScheduleAnalysis "qiskit.transpiler.passes.ALAPScheduleAnalysis"), so that every instruction start time satisfies alignment constraints.

## Examples

We assume executing the following circuit on a backend with 16 dt of acquire alignment.

```python
     ┌───┐┌────────────────┐┌─┐
q_0: ┤ X ├┤ Delay(100[dt]) ├┤M├
     └───┘└────────────────┘└╥┘
c: 1/════════════════════════╩═
                             0
```

Note that delay of 100 dt induces a misalignment of 4 dt at the measurement. This pass appends an extra 12 dt time shift to the input circuit.

```python
     ┌───┐┌────────────────┐┌─┐
q_0: ┤ X ├┤ Delay(112[dt]) ├┤M├
     └───┘└────────────────┘└╥┘
c: 1/════════════════════════╩═
                             0
```

## Notes

Your backend may execute circuits violating these alignment constraints. However, you may obtain erroneous measurement result because of the untracked phase originating in the instruction misalignment.

Create new rescheduler pass.

The alignment values depend on the control electronics of your quantum processor.

**Parameters**

*   **acquire\_alignment** – Integer number representing the minimum time resolution to trigger acquisition instruction in units of `dt`.
*   **pulse\_alignment** – Integer number representing the minimum time resolution to trigger gate instruction in units of `dt`.

## Attributes

<span id="qiskit.transpiler.passes.ConstrainedReschedule.is_analysis_pass" />

### is\_analysis\_pass

Check if the pass is an analysis pass.

If the pass is an AnalysisPass, that means that the pass can analyze the DAG and write the results of that analysis in the property set. Modifications on the DAG are not allowed by this kind of pass.

<span id="qiskit.transpiler.passes.ConstrainedReschedule.is_transformation_pass" />

### is\_transformation\_pass

Check if the pass is a transformation pass.

If the pass is a TransformationPass, that means that the pass can manipulate the DAG, but cannot modify the property set (but it can be read).

## Methods

### name

<span id="qiskit.transpiler.passes.ConstrainedReschedule.name" />

`name()`

Return the name of the pass.

### run

<span id="qiskit.transpiler.passes.ConstrainedReschedule.run" />

`run(dag)`

Run rescheduler.

This pass should perform rescheduling to satisfy:

> *   All DAGOpNode nodes (except for compiler directives) are placed at start time satisfying hardware alignment constraints.
> *   The end time of a node does not overlap with the start time of successor nodes.

Assumptions:

> *   Topological order and absolute time order of DAGOpNode are consistent.
> *   All bits in either qargs or cargs associated with node synchronously start.
> *   Start time of qargs and cargs may different due to I/O latency.

Based on the configurations above, the rescheduler pass takes the following strategy:

1.  **The nodes are processed in the topological order, from the beginning of**

    the circuit (i.e. from left to right). For every node (including compiler directives), the function `_push_node_back` performs steps 2 and 3.

2.  **If the start time of the node violates the alignment constraint,**

    the start time is increased to satisfy the constraint.

3.  **Each immediate successor whose start\_time overlaps the node’s end\_time is**

    pushed backwards (towards the end of the wire). Note that at this point the shifted successor does not need to satisfy the constraints, but this will be taken care of when that successor node itself is processed.

4.  **After every node is processed, all misalignment constraints will be resolved,**

    and there will be no overlap between the nodes.

**Parameters**

**dag** ([*DAGCircuit*](qiskit.dagcircuit.DAGCircuit "qiskit.dagcircuit.dagcircuit.DAGCircuit")) – DAG circuit to be rescheduled with constraints.

**Raises**

[**TranspilerError**](transpiler#qiskit.transpiler.TranspilerError "qiskit.transpiler.TranspilerError") – If circuit is not scheduled.
