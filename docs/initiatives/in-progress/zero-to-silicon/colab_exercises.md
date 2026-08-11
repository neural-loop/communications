**Zero to Silicon**

Weekly Take-Home Problem Sets

Participant Edition \| Open Neuromorphic \| Summer 2026

*Build one artifact per week. By the end, they chain into a complete
working system.*

**How the series works**

Each event is followed by a take-home task. Every task produces one
artifact --- something you build, write, or code. The artifact you
produce this week is the raw material for next week's session. By event
6, your six artifacts chain together into a complete pipeline: from a
hand-drawn neuron sketch all the way to a verified hardware simulation.

  -----------------------------------------------------------------------------
  **Event**   **Task name**         **Artifact you        **Feeds into**
                                    produce**             
  ----------- --------------------- --------------------- ---------------------
  **1**       **Sketch the neuron** Annotated diagram +   *Event 2 --- your
                                    voltage trace         Python spec*

  **2**       **Code the neuron**   lif_neuron.py + spike *Event 3 --- your
                                    plot                  gate mapping source*

  **3**       **Map the logic**     Mapping table + block *Event 4 --- your
                                    diagram               chip blueprint*

  **4**       **Write the spec**    lif_chip_spec.md      *Event 5 --- your
                                                          Verilog target*

  **5**       **Implement in        lif_neuron.v          *Event 6 --- design
              Verilog**             (lint-clean)          under test*

  **6**       **Simulate & verify** Passing testbench +   *Your portfolio
                                    waveform              capstone*
  -----------------------------------------------------------------------------

+-----------------------------------------------------------------------+
| **Task 1 --- Sketch the neuron**                                      |
|                                                                       |
| Event 1: Neuroscience Foundations \| No tools required                |
+-----------------------------------------------------------------------+

**Time estimate:** 60--90 minutes

**Tools needed:** Pencil and paper, or any drawing tool (Excalidraw,
iPad, Figma --- anything works)

**Submit to:** Discord #z2s-task-1 as an image or PDF

**Background**

In the session you learned that a neuron is a dynamical system --- it
integrates input, builds up membrane potential, and fires a discrete
spike when a threshold is crossed. Before you write any code, you are
going to draw that system. Drawing forces you to encode the concepts. If
you can label the diagram correctly, you understand the vocabulary that
every later session builds on.

**Part A --- The neuron anatomy (20 pts)**

Draw a single neuron. Your drawing does not need to be anatomically
perfect --- a clear schematic is better than a detailed illustration.
Label all of the following:

-   Dendrites --- where input arrives

-   Soma (cell body) --- where integration happens

-   Axon --- where the spike travels

-   Axon terminal / synapse --- where the signal passes to the next
    neuron

-   Membrane --- the boundary that maintains the electrical potential

-   Indicate (with an arrow or annotation) where threshold crossing
    occurs

**Part B --- The voltage trace (30 pts)**

Draw a graph with time on the x-axis and membrane potential V on the
y-axis. Your trace must show a complete LIF cycle. Label all of the
following on the graph:

-   Resting potential --- the baseline V before any input

-   Integration phase --- V rising as input current arrives

-   Threshold V_th --- mark it as a dashed horizontal line

-   Spike --- the moment V crosses threshold (draw a sharp upward
    deflection)

-   Reset --- V dropping back to resting potential after the spike

-   Show at least two full spike cycles

**Part C --- Written questions (50 pts)**

**Question 1 (15 pts)**

In your own words: what does the "leak" in Leaky Integrate-and-Fire
mean? What would happen to a neuron's firing behaviour if there were no
leak at all? Answer in 3--4 sentences.

**Question 2 (15 pts)**

The talk introduced the concept of the "neuromorphic bridge" --- how a
biological property maps to a hardware constraint. Choose one of the
following biological properties and describe, in 2--3 sentences, how you
expect it to appear in the digital chip we will build later in the
series:

-   Sparsity of spiking

-   Event-driven signalling

-   Coincidence detection at the synapse

**Question 3 (20 pts)**

Look at your voltage trace from Part B. If you doubled the input
current, describe what you would expect to happen to: (a) the time
between spikes, (b) the height of the spike, and (c) the shape of the
integration ramp. Answer in 4--5 sentences. You do not need to calculate
exact numbers --- we are looking for correct qualitative reasoning.

  -----------------------------------------------------------------------
  **What this feeds into**

  Your Part B voltage trace is your specification for the Python class in
  Task 2. When you write lif_neuron.py, its output should produce a plot
  that looks like the trace you drew here. If they don't match, something
  in your code is wrong --- and this drawing tells you what the correct
  behaviour looks like.
  -----------------------------------------------------------------------

+-----------------------------------------------------------------------+
| **Task 2 --- Code the neuron**                                        |
|                                                                       |
| Event 2: Prototyping an LIF Neuron in Python \| Python + NumPy only   |
+-----------------------------------------------------------------------+

**Time estimate:** 2--3 hours

**Tools needed:** Python 3, NumPy, Matplotlib. No snnTorch for the class
itself.

**Submit to:** GitHub repo /python-model/lif_neuron.py + one plot image
in Discord #z2s-task-2

**Background**

The session covered the LIF equations and showed them implemented in
snnTorch. Your task is to implement the neuron from scratch without that
library. Writing the equations yourself --- before using a framework ---
is the difference between understanding what snnTorch does and just
calling functions. Your implementation will be the reference model that
your hardware chip must later replicate.

**Part A --- The LIF class (50 pts)**

Write a Python class called LIFNeuron. It must implement the following
interface exactly, as later tasks depend on it:

> class LIFNeuron:
>
> def \_\_init\_\_(self, tau, V_th, V_reset, dt=1.0):
>
> \# tau : membrane time constant (ms)
>
> \# V_th : spike threshold (mV)
>
> \# V_reset : reset potential after spike (mV)
>
> \# dt : timestep (ms)
>
> pass
>
> def step(self, I_in):
>
> \# I_in : input current for this timestep
>
> \# Returns: (V, spike) where spike is 1 if fired, 0 otherwise
>
> pass
>
> def reset_state(self):
>
> \# Reset membrane potential to V_reset
>
> pass

The update rule your step() method must implement is the discrete-time
LIF equation:

> dV = dt/tau \* (-(V - V_reset) + I_in)
>
> V = V + dV
>
> if V \>= V_th:
>
> spike = 1
>
> V = V_reset
>
> else:
>
> spike = 0

**Part B --- Simulation and plot (30 pts)**

Instantiate your neuron with these parameters: tau=20, V_th=-55,
V_reset=-70, dt=0.5. Run two simulations:

1.  Constant input current I=2.0 for 500 timesteps. Plot V over time.
    Annotate the threshold line.

2.  Run the same simulation with I=1.0, I=2.0, and I=4.0. Plot all three
    V traces on the same axes. Add a legend.

Your plot should visually match the voltage trace you drew in Task 1. If
it does not, revisit your drawing or your code --- one of them is wrong.

**Part C --- Written questions (20 pts)**

**Question 1 (10 pts)**

Look at your three-current plot from Part B. Does spike rate increase
linearly with input current? Describe what you observe and give a brief
explanation for why (or why not). 3--4 sentences.

**Question 2 (10 pts)**

The leak term in your update rule is -(V - V_reset). What would happen
if you removed this term entirely (i.e. dV = dt/tau \* I_in)? Describe
the qualitative change in behaviour and whether the neuron would still
be a plausible biological model. 3--4 sentences.

  -----------------------------------------------------------------------
  **What this feeds into**

  Your LIFNeuron class with tau=20, V_th=-55, V_reset=-70, dt=0.5 is your
  reference implementation. In Task 3 you will translate each line of
  step() into a digital logic operation. In Task 6 you will run your chip
  at the same parameters and check that the spike timing matches.
  -----------------------------------------------------------------------

+-----------------------------------------------------------------------+
| **Task 3 --- Map the logic**                                          |
|                                                                       |
| Event 3: Fundamentals of Digital Logic \| Pen and paper + Python      |
| optional                                                              |
+-----------------------------------------------------------------------+

**Time estimate:** 90 minutes--2 hours

**Tools needed:** Pencil and paper for diagrams. Python optional to
verify your bit-width answer.

**Submit to:** Discord #z2s-task-3 as image/PDF + commit
lif_logic_map.md to GitHub /docs

**Background**

The session showed that digital logic represents every arithmetic
operation as gates and signals. Your task is to look at the LIF update
rule from your Python implementation and translate each operation into
the digital logic equivalent. This is the step most software engineers
find hardest --- not because it is complex, but because it requires
thinking in a different way. By the end you will have a block diagram
that is the first draft of your chip.

**Part A --- Operation mapping table (40 pts)**

Fill in the table below for each operation in your LIFNeuron.step()
method. For each Python operation, identify the digital logic component
that implements it in hardware.

  ---------------------------------------------------------------------------------
  **Python operation**  **Digital logic component**  **Notes / constraints**
  --------------------- ---------------------------- ------------------------------
  V - V_reset           Subtractor                   Signed arithmetic --- result
                                                     can be negative

  dt / tau \* (\...)    Multiplier or shift          Multiplication is expensive;
                                                     can dt/tau be approximated as
                                                     a power of 2?

  V + dV                Adder / accumulator          Needs to store result --- what
                                                     register holds V?

  V \>= V_th            *\_\_\_\_\_\_\_\_\_\_\_\_*   *\_\_\_\_\_\_\_\_\_\_\_\_*

  V = V_reset (on       *\_\_\_\_\_\_\_\_\_\_\_\_*   *\_\_\_\_\_\_\_\_\_\_\_\_*
  spike)                                             

  return spike          *\_\_\_\_\_\_\_\_\_\_\_\_*   Single-bit output signal

  Store V between steps *\_\_\_\_\_\_\_\_\_\_\_\_*   What type of storage element
                                                     holds state across clock
                                                     cycles?
  ---------------------------------------------------------------------------------

**Part B --- Block diagram (30 pts)**

Using your completed mapping table, draw a block diagram of the digital
LIF neuron. Your diagram must show:

-   Each logic component as a labelled box (subtractor, adder,
    comparator, multiplexer, register)

-   Data signals as arrows connecting components, labelled with the
    signal name (V, dV, I_in, spike)

-   The clock input feeding into the register(s)

-   A reset input that forces V back to V_reset

Hint: the comparator output should connect to a multiplexer that selects
between "V + dV" and "V_reset" as the next value of V.

**Part C --- Bit width analysis (30 pts)**

**Question 1 (15 pts)**

Your membrane potential V ranges from V_reset = -70 mV to approximately
V_th + 15 = -40 mV (allowing for overshoot). The precision you need is
about 0.5 mV per step (matching your dt=0.5 from Task 2). How many bits
do you need to represent V? Show your working. Use the formula: bits =
ceil(log2(range / resolution)).

**Question 2 (15 pts)**

The multiplier for dt/tau = 0.5/20 = 0.025 is expensive to implement
exactly in hardware. Suggest a way to approximate this multiplication
using only bit-shift operations (i.e. dividing by powers of 2). What is
the closest approximation you can achieve, and what error does it
introduce? Would the neuron still fire at approximately the correct rate
with this approximation?

  -----------------------------------------------------------------------
  **What this feeds into**

  Your block diagram is the first draft of your chip design. In Task 4
  you will formalise it into a written hardware spec --- defining the
  exact module interface, signal names, and bit widths. The bit-width
  answer from Part C becomes the signal widths in your Verilog module.
  -----------------------------------------------------------------------

+-----------------------------------------------------------------------+
| **Task 4 --- Write the spec**                                         |
|                                                                       |
| Event 4: Design the Digital Spiking Chip \| Markdown                  |
+-----------------------------------------------------------------------+

**Time estimate:** 1--2 hours

**Tools needed:** Any text editor. Output is a Markdown file.

**Submit to:** GitHub repo /docs/lif_chip_spec.md (commit directly to
the repo)

**Background**

A hardware spec is the contract between the designer and the
implementer. In this case, you are both --- but writing the spec before
writing Verilog forces you to think clearly about what the module needs
to do before you worry about syntax. A well-written spec makes Task 5
straightforward. A vague spec makes Task 5 painful.

**Part A --- Write lif_chip_spec.md (70 pts)**

Your spec must contain all of the following sections. A template is
provided in the GitHub repo at /docs/lif_chip_spec_template.md.

**Section 1: Module overview (10 pts)**

One paragraph. What does this module do? What problem does it solve? Who
would use it?

**Section 2: Port table (20 pts)**

A table with columns: Port name \| Direction \| Width (bits) \|
Description. Must include all inputs and outputs. Required ports:

-   clk --- clock input

-   rst --- synchronous reset

-   I_in --- input current (use the bit width from your Task 3 Part C
    analysis)

-   V_out --- membrane potential output (for observation / debugging)

-   spike --- single-bit spike output

**Section 3: Internal registers (15 pts)**

List every register your module needs. For each: name, width in bits,
initial value, and what it represents.

**Section 4: Behaviour per clock cycle (25 pts)**

This is the most important section. Write pseudocode (not Verilog) for
what happens on every rising clock edge. It must cover:

-   What happens when rst is high

-   The LIF update calculation

-   The threshold comparison

-   The reset-or-update decision (the multiplexer from your block
    diagram)

-   When spike is asserted high and for how long

**Part B --- Self-review checklist (30 pts)**

Before submitting, answer each question in your spec document under a
"Self-review" heading:

3.  Does every signal have a defined bit width? (yes/no + fix any that
    don't)

4.  Is the reset behaviour fully specified? What is V on the first cycle
    after rst goes low?

5.  What happens if I_in and rst are both asserted in the same cycle?

6.  Could another person implement your module in Verilog from this spec
    alone, without asking you questions? If not, what is ambiguous?

  -----------------------------------------------------------------------
  **What this feeds into**

  Your lif_chip_spec.md is the direct input for Task 5. The port table
  becomes your Verilog module declaration. The behaviour section becomes
  the always @(posedge clk) block. If your spec is precise, your Verilog
  will be easy to write and mostly correct on the first try.
  -----------------------------------------------------------------------

+-----------------------------------------------------------------------+
| **Task 5 --- Implement in Verilog**                                   |
|                                                                       |
| Event 5: Intro to Verilog & Hardware Description \| Verilog +         |
| Verilator lint                                                        |
+-----------------------------------------------------------------------+

**Time estimate:** 2--4 hours

**Tools needed:** Verilator (for lint check). Install guide in
/docs/setup_verilator.md in the repo.

**Submit to:** GitHub repo /verilog/lif_neuron.v --- must pass lint
before submitting

**Background**

The session covered Verilog syntax: modules, ports, reg and wire, always
blocks, and sequential logic. Your task is to implement your
lif_chip_spec.md as a synthesizable Verilog module. A starter template
with the port declarations already written is in
/verilog/lif_neuron_template.v --- you fill in the logic.

**Part A --- Implement lif_neuron.v (60 pts)**

Open /verilog/lif_neuron_template.v. The module declaration and port
list are already provided based on the standard spec. Your task is to
fill in:

7.  Internal register declarations --- declare V_mem and any
    intermediate registers you need

8.  The always @(posedge clk) block --- implement your spec's behaviour
    section

9.  The spike output assignment

The template looks like this:

> module lif_neuron #(
>
> parameter WIDTH = 16,
>
> parameter V_TH = 16\'d3800, // -55 mV in fixed-point
>
> parameter V_RESET = 16\'d0, // -70 mV → offset to 0
>
> parameter TAU_INV = 16\'d3 // approx 1/tau as shift
>
> ) (
>
> input wire clk,
>
> input wire rst,
>
> input wire \[15:0\] I_in,
>
> output reg \[15:0\] V_out,
>
> output reg spike
>
> );
>
> // YOUR CODE HERE
>
> endmodule

Note: the template uses fixed-point arithmetic with an offset to avoid
negative numbers. -70 mV is mapped to 0, and -55 mV is mapped to 3800
(in units of 0.01 mV per LSB with 8-bit fractional part). You may adjust
the parameterisation if your spec uses a different encoding --- document
your choice.

**Part B --- Lint check (20 pts)**

Run the following command from the repo root and fix all warnings before
submitting:

> verilator \--lint-only -Wall verilog/lif_neuron.v

Common lint warnings you will likely see and must fix:

-   Width mismatch --- assigning a wider signal to a narrower register

-   Undriven / unused signals --- declared but never assigned or read

-   Blocking vs non-blocking --- use \<= (non-blocking) inside always
    @(posedge clk)

**Part C --- Written questions (20 pts)**

**Question 1 (10 pts)**

In your implementation, what is the difference between a reg and a wire?
Which did you use for V_mem and why? Could you have used the other one?
3--4 sentences.

**Question 2 (10 pts)**

Verilog has two types of assignment inside always blocks: = (blocking)
and \<= (non-blocking). You were told to use \<=. Explain in your own
words why using = inside an always @(posedge clk) block leads to
incorrect simulation behaviour. 3--4 sentences.

  -----------------------------------------------------------------------
  **What this feeds into**

  Your lif_neuron.v is the design under test in Task 6. The testbench
  will instantiate exactly this module, apply a constant I_in, and check
  that a spike appears within a calculated number of clock cycles. A
  lint-clean file is a necessary but not sufficient condition --- Task 6
  will tell you if the logic is correct.
  -----------------------------------------------------------------------

+-----------------------------------------------------------------------+
| **Task 6 --- Simulate and verify --- series capstone**                |
|                                                                       |
| Event 6: Simulating with Verilator \| Verilator + GTKWave             |
+-----------------------------------------------------------------------+

**Time estimate:** 2--4 hours

**Tools needed:** Verilator, GTKWave (or the web-based VCD viewer linked
in the repo)

**Submit to:** Discord #z2s-task-6 with waveform screenshot + final
lif_neuron.v committed to GitHub

**Background**

The session showed how to wrap a Verilog module in a C++ testbench,
compile it with Verilator, and visualise the output as a waveform. Your
task is to run the provided testbench against your lif_neuron.v, observe
the spike waveform, and answer the series' final question: does your
hardware match your Python model?

**Part A --- Run the testbench (40 pts)**

The testbench is in /testbench/tb_lif_neuron.cpp. It applies a constant
I_in=200 (in the fixed-point encoding) for 2000 clock cycles and checks
that:

-   At least one spike occurs within 2000 cycles

-   The spike signal is high for exactly 1 clock cycle

-   V_out returns to V_RESET within 2 cycles of a spike

To compile and run:

> cd testbench
>
> make
>
> ./obj_dir/Vlif_neuron

A passing run prints: PASS: spike detected at cycle N. A failing run
prints: FAIL: followed by the specific check that failed.

Screenshot your terminal output (passing or failing --- we want to see
it either way) and post in Discord.

**Part B --- Waveform analysis (30 pts)**

The testbench generates a VCD file at /testbench/lif_neuron.vcd. Open it
in GTKWave (or the web viewer) and add these signals to the waveform
view: clk, rst, I_in, V_out, spike.

Take a screenshot of your waveform showing at least two full spike
cycles and answer:

10. How many clock cycles between spikes (the inter-spike interval,
    ISI)?

11. What is the value of V_out on the cycle immediately after a spike?

12. Does V_out increase monotonically between spikes, or does it have
    any unexpected shape?

**Part C --- Hardware vs Python comparison (30 pts) --- the series
payoff**

This is the question the entire series has been building toward.

**Step 1**

Run your Task 2 Python simulation with I_in=200 (rescaled to the same
units as your hardware) for the equivalent number of timesteps. Record
the inter-spike interval from the Python model.

**Step 2**

Compare the ISI from your hardware simulation (Part B) with the ISI from
your Python model. They should be close but may not be identical due to
the fixed-point approximation.

**Step 3 --- Written answer (30 pts)**

Write a 150--200 word reflection covering:

-   Does your hardware spike at approximately the same rate as your
    Python model? What is the percentage difference in ISI?

-   If there is a difference, what is the most likely cause? (Think
    about your bit-shift approximation of dt/tau from Task 3.)

-   What would you change in your design to reduce this error?

-   What does it mean that you have a working digital neuron? What could
    you do with this chip next?

+-----------------------------------------------------------------------+
| **Series complete --- what you built**                                |
+-----------------------------------------------------------------------+
| **You now have a complete pipeline:**                                 |
|                                                                       |
| -   Task 1: A biological reference --- annotated neuron diagram +     |
|     voltage trace                                                     |
|                                                                       |
| -   Task 2: A Python reference model --- lif_neuron.py with verified  |
|     spike behaviour                                                   |
|                                                                       |
| -   Task 3: A logic mapping --- every Python operation translated to  |
|     digital hardware                                                  |
|                                                                       |
| -   Task 4: A hardware spec --- lif_chip_spec.md, the contract for    |
|     your implementation                                               |
|                                                                       |
| -   Task 5: A Verilog implementation --- lif_neuron.v, synthesizable  |
|     and lint-clean                                                    |
|                                                                       |
| -   Task 6: A verified simulation --- waveform evidence that your     |
|     chip behaves as designed                                          |
|                                                                       |
| *This is a real portfolio piece. Your GitHub repo tells a coherent    |
| story: here is a neuron, here is the math, here is the logic, here is |
| the hardware, here is the proof it works.*                            |
+-----------------------------------------------------------------------+
