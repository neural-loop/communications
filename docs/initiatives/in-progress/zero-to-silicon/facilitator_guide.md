# Zero to Silicon
## Weekly Tasks — Facilitator Guide & Rubrics
**ONM Team Edition | Not for participant distribution**

*Scoring rubrics, model answers, facilitation notes, and common mistakes for each task.*

## Facilitation principles

The tasks are deliberately graduated. Tasks 1–3 require only understanding and Python — the barrier is low enough that anyone who attended the session can attempt them. Tasks 4–5 require following a structured format, which reduces the cognitive load of the HDL work. Task 6 is the only one that requires a working toolchain.

When reviewing in Discord: focus feedback on the "feeds into" connection. The most useful thing you can say to a participant is "your voltage trace shows X, which means your Python class should behave like Y" — connecting the artifact to the next task is more valuable than correcting minor errors in isolation.

Tasks are scored out of 100 for completeness and correctness. For async Discord review, a simpler pass/needs-revision approach is fine — the rubric is a guide for the team, not a grade for participants.

---

## Task 1 rubric — Sketch the neuron

### Part A — Anatomy (20 pts)

| Criterion | What we look for | Points |
| :--- | :--- | :--- |
| **All 6 labels present** | Dendrites, soma, axon, terminal, membrane, threshold location | **12 pts** |
| **Labels correctly placed** | Threshold on soma/axon hillock, not on dendrite | **5 pts** |
| **Diagram is readable** | Clear enough for someone else to follow | **3 pts** |

### Part B — Voltage trace (30 pts)

| Criterion | What we look for | Points |
| :--- | :--- | :--- |
| **All 5 features labelled** | Resting, integration, `V_th` dashed line, spike, reset | **20 pts** |
| **Two full cycles shown** | Both spikes visible with reset between them | **5 pts** |
| **Qualitative shape correct** | Integration ramp, sharp spike, abrupt reset | **5 pts** |

### Part C — Written questions (50 pts)

**Q1 model answer — the leak (15 pts)**  
Full marks: The leak is the passive decay of membrane potential back toward resting potential when no input is present. Biologically, ion channels in the membrane allow charge to leak out. Without a leak, the neuron would be a perfect integrator — it would accumulate all input forever, never forgetting old stimuli, and fire at rates determined entirely by total past input rather than recent activity. This makes it a poor model of real neurons, which are sensitive to recent input.

**Q2 model answers by property (15 pts)**  
*Sparsity:* most digital circuits are active all the time (clock-driven). A neuromorphic chip exploits sparsity by only doing work when a spike occurs — power consumption scales with activity rather than clock rate.  
*Event-driven signalling:* instead of sampling every cycle, the chip only processes when a spike arrives. This maps to interrupt-driven or asynchronous logic and is the basis of AER (Address Event Representation).  
*Coincidence detection:* the synapse only fires if two inputs arrive within a short time window. In hardware this is a logical AND with a time window — implemented as a register that holds the first spike and a comparator that checks whether the second arrives before the register clears.

**Q3 model answer — doubling current (20 pts)**  
Full marks: (a) Time between spikes decreases — the integration ramp is steeper, so threshold is crossed more quickly. (b) Spike height does not change — the LIF model has a fixed threshold and reset; the spike is a discrete event, not a graded signal. (c) The integration ramp becomes steeper — dV/dt is larger because `I_in` is larger, but the leak also increases as V rises, so the ramp curves slightly rather than being perfectly linear.

### Common mistakes to watch for
*   Drawing the spike as a smooth curve rather than a sharp event — the LIF spike is instantaneous in the discrete model
*   Placing the threshold label on the axon terminal rather than the axon hillock / soma
*   Q3: saying spike height increases with current — the threshold-and-reset mechanism means it does not

---

## Task 2 rubric — Code the neuron

### Part A — LIF class (50 pts)

| Criterion | What we look for | Points |
| :--- | :--- | :--- |
| **Correct update equation** | `dV = dt/tau * (-(V-V_reset) + I_in)`, **applied each step** | **20 pts** |
| **Threshold + reset logic** | `spike=1` and `V=V_reset` when `V >= V_th`, else `spike=0` | **15 pts** |
| **Interface matches spec** | `step()` returns `(V, spike)`; `reset_state()` works | **10 pts** |
| **State maintained between calls** | `V` persists across `step()` calls (instance variable) | **5 pts** |

**Model implementation**

```python
import numpy as np

class LIFNeuron:
    def __init__(self, tau, V_th, V_reset, dt=1.0):
        self.tau = tau
        self.V_th = V_th
        self.V_reset = V_reset
        self.dt = dt
        self.V = V_reset

    def step(self, I_in):
        dV = (self.dt / self.tau) * (-(self.V - self.V_reset) + I_in)
        self.V += dV
        
        if self.V >= self.V_th:
            spike = 1
            self.V = self.V_reset
        else:
            spike = 0
            
        return self.V, spike

    def reset_state(self):
        self.V = self.V_reset
```

Part B — Plot (30 pts)

| Criterion                       | What we look for                                     | Points     |
| :------------------------------ | :--------------------------------------------------- | :--------- |
| **Single-current plot correct** | V trace visible, threshold annotated, spikes present | **10 pts** |
| **Three-current comparison**    | All three traces on same axes, legend included       | **10 pts** |
| **Qualitative match to Task 1** | Plot shape matches voltage trace from Task 1 sketch  | **10 pts** |

Part C — Written questions (20 pts)

Q1 model answer — spike rate vs current
Spike rate does not increase linearly with current. At low currents the neuron
may not spike at all (sub-threshold). Above threshold, rate increases with
current but the relationship is nonlinear due to the leak term — as V rises
toward threshold, the leak current -(V - V_reset) partially cancels I_in,
slowing the ramp. This is the f-I curve of the LIF model.

Q2 model answer — removing the leak
Without the leak term, dV = dt/tau * I_in. The neuron becomes a perfect
integrator — V increases monotonically as long as I_in > 0 and never decays. It
would still fire, but it would remember all past input with no forgetting.
Biologically implausible: real neurons are sensitive to recent input, not total
past input.

Task 3 rubric — Map the logic

Part A — Mapping table (40 pts) — answer key

| Criterion                    | What we look for                                     | Points     |
| :--------------------------- | :--------------------------------------------------- | :--------- |
| **`V >= V_th`**              | Comparator                                           | **8 pts**  |
| **`V = V_reset` (on spike)** | Multiplexer (selects V\_reset when comparator fires) | **8 pts**  |
| **`return spike`**           | Register output / wire                               | **4 pts**  |
| **Store V between steps**    | D flip-flop / register (clocked storage)             | **8 pts**  |
| **Partial credit**           | Subtractor, adder described correctly                | **12 pts** |

Part B — Block diagram (30 pts)

| Criterion                         | What we look for                                                    | Points     |
| :-------------------------------- | :------------------------------------------------------------------ | :--------- |
| **All 5 component types present** | Subtractor, adder/accumulator, comparator, mux, register            | **15 pts** |
| **Data flow correct**             | `I_in` → adder → mux → register → `V`; comparator drives mux select | **10 pts** |
| **Clock and reset shown**         | Clock to register; reset forcing `V_RESET` through mux              | **5 pts**  |

Part C — Bit width (30 pts) — model answers

Q1 — bit width calculation
Range = -40 - (-70) = 30 mV. Resolution = 0.5 mV. Steps needed = 30 / 0.5 = 60.
bits = ceil(log2(60)) = 6 bits for the fractional part. However, signed
representation and fractional bits for the intermediate dV calculation require
~16 bits total. Full marks for any well-reasoned answer in the range of 8–16
bits with correct working.

Q2 — bit-shift approximation
dt/tau = 0.5/20 = 0.025. Closest power-of-2 approximations: 1/32 = 0.03125
(right-shift by 5), 1/64 = 0.015625 (right-shift by 6). Using 1/32 introduces an
error of (0.03125-0.025)/0.025 = 25%. The neuron will fire ~25% faster than the
Python model. This is the main source of discrepancy participants will observe
in Task 6.

Task 4 rubric — Write the spec

Part A — lif_chip_spec.md (70 pts)

| Criterion                         | What we look for                                                | Points     |
| :-------------------------------- | :-------------------------------------------------------------- | :--------- |
| **Module overview complete**      | Describes purpose, not just restates the title                  | **10 pts** |
| **Port table complete**           | All 5 required ports with correct direction, width, description | **20 pts** |
| **Internal registers listed**     | `V_mem` at minimum; initial value and width specified           | **15 pts** |
| **Behaviour pseudocode complete** | Reset, update, threshold, mux, spike all covered                | **25 pts** |

Part B — Self-review (30 pts)

| Criterion                           | What we look for                                  | Points    |
| :---------------------------------- | :------------------------------------------------ | :-------- |
| **Q1: all signals have widths**     | No signal left undefined                          | **8 pts** |
| **Q2: reset behaviour specified**   | `V` value on cycle after `rst` goes low is stated | **8 pts** |
| **Q3: I\_in+rst conflict handled**  | Specifies priority (`rst` wins, or both applied)  | **7 pts** |
| **Q4: implementability assessment** | Honest identification of any ambiguous section    | **7 pts** |

Common mistakes

  - Forgetting to specify signal widths for I_in — it must have a defined bit
    width
  - Behaviour section says "compare V to threshold" without specifying what
    happens next
  - Spike output described as persistent (stays high) rather than single-cycle

Task 5 rubric — Implement in Verilog

Part A — Implementation (60 pts)

| Criterion                        | What we look for                                     | Points     |
| :------------------------------- | :--------------------------------------------------- | :--------- |
| **Register declaration correct** | `V_mem` declared as `reg` with correct width         | **10 pts** |
| **Reset logic correct**          | `rst` sets `V_mem` to `V_RESET`, `spike` to 0        | **10 pts** |
| **LIF update implemented**       | `dV` computed and added to `V_mem` each cycle        | **20 pts** |
| **Threshold + reset logic**      | Spike asserted for 1 cycle; `V_mem` set to `V_RESET` | **15 pts** |
| **`V_out` assigned correctly**   | `V_out` reflects `V_mem` (continuous or registered)  | **5 pts**  |

Part B — Lint clean (20 pts)

| Criterion          | What we look for                             | Points             |
| :----------------- | :------------------------------------------- | :----------------- |
| **Zero warnings**  | `verilator --lint-only -Wall` passes cleanly | **20 pts**         |
| **Partial credit** | Each unresolved warning costs 5 pts          | **−5 per warning** |

Part C — Written questions (20 pts)

Q1 model answer — reg vs wire
A reg holds a value across clock edges — it is a storage element. A wire is a
combinational connection — its value is always driven by whatever is currently
connected to it. V_mem must be a reg because it needs to hold the membrane
potential between clock cycles. A wire cannot do this — it has no memory.

Q2 model answer — blocking vs non-blocking
With = (blocking), assignments execute in order within the always block — a
later assignment can see the result of an earlier one in the same time step.
This creates combinational behaviour inside a sequential block, which in
simulation produces race conditions: the order of statements in the source file
affects the result. With <= (non-blocking), all right-hand sides are evaluated
first, then all left-hand sides are updated simultaneously at the clock edge —
matching real flip-flop behaviour.

Task 6 rubric — Simulate and verify

Part A — Testbench (40 pts)

| Criterion                         | What we look for                                                      | Points     |
| :-------------------------------- | :-------------------------------------------------------------------- | :--------- |
| **Testbench compiles**            | `make` succeeds without errors                                        | **10 pts** |
| **Passing run achieved**          | `PASS` message with cycle number, OR documented `FAIL` with diagnosis | **20 pts** |
| **Terminal screenshot submitted** | Discord post includes screenshot                                      | **10 pts** |

Part B — Waveform (30 pts)

| Criterion                       | What we look for                                              | Points     |
| :------------------------------ | :------------------------------------------------------------ | :--------- |
| **Waveform screenshot correct** | All 5 signals visible: `clk`, `rst`, `I_in`, `V_out`, `spike` | **10 pts** |
| **ISI measured correctly**      | Correct clock cycle count between spikes                      | **10 pts** |
| **`V_out` shape described**     | Reset, ramp, and spike visible and correctly described        | **10 pts** |

Part C — HW vs Python comparison (30 pts)

| Criterion                    | What we look for                                   | Points     |
| :--------------------------- | :------------------------------------------------- | :--------- |
| **ISI comparison attempted** | Python simulation run with same parameters         | **10 pts** |
| **Error quantified**         | Percentage difference calculated and stated        | **10 pts** |
| **Root cause identified**    | Bit-shift approximation identified as likely cause | **5 pts**  |
| **Reflection quality**       | 150–200 words, all four bullet points addressed    | **5 pts**  |

Expected results (for facilitator reference)

With the default parameters (I_in=200, TAU_INV=5 i.e. right-shift-by-5) the
expected ISI is approximately 180–220 clock cycles. The Python model with
equivalent parameters will give ~240 timesteps. The ~25% discrepancy is expected
and is the correct answer to the root-cause question.

If a participant's hardware fires significantly faster or slower than this
range, the most likely causes are: (1) incorrect fixed-point encoding of V_RESET
or V_TH parameters, (2) V_out not resetting to V_RESET after spike, or (3) the
update equation applying dt/tau incorrectly.

Open Neuromorphic | Zero to Silicon | Facilitator Edition | Not for participant
distribution