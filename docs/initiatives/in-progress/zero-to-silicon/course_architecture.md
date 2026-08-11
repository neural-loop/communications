# Zero to Silicon
## Build Your Own Spiking Digital Hardware
**Summer Workshop Series | Open Neuromorphic**

*Series Planning Document | June 2026 Draft*

## Series Overview

Zero to Silicon is a step-by-step public educational track that takes a software engineer or student from zero hardware background to simulating a digital spiking neuron chip. The series is organized as a summer workshop: each event opens with a 60-minute live talk from a domain expert, followed by interactive demos and a structured activity block. All materials are released as Open Educational Resources (OER).

**Track name:** Zero to Silicon  
**Format:** Live online workshop — talk (60 min) + activities (60 min)  
**Audience:** Software engineers, students, and researchers with limited hardware background  
**Total events:** 6 sessions  
**Timing:** Summer 2026 (dates TBD per speaker availability)  
**Materials:** All content released as OER — free to use, share, and cite  
**Platform:** Discord (async challenges + community) + live streaming (talk + Q&A)

## Event Overview

The six events form a continuous curriculum. Each event builds directly on the one before it, culminating in a full simulation of the spiking neuron chip designed across the series.

| # | Event | Status | Speaker | Hosts |
| :--- | :--- | :--- | :--- | :--- |
| **1** | Neuroscience Foundations for Neuromorphic Computation | **Recruiting speaker** | TBD | Rayane / Jose (neuroscientist) |
| **2** | Prototyping an LIF Neuron in Python | **Needs Scheduling** | Jason Eshraghian (@jasnn) | Effiong / Erastus |
| **3** | Fundamentals of Digital Logic for Neuromorphic Engineering | **Idea Phase** | Fabrizio Otto | Jose / Erastus |
| **4** | Design the Digital Spiking Chip | **Idea Phase** | TBD | Jose / Erastus |
| **5** | Intro to Verilog & Hardware Description | **Idea Phase** | Dmitri (Neucom) | Jose / Erastus |
| **6** | Simulating the Spiking Neuron Chip with Verilator | **Idea Phase** | TBD (cont. from Ev. 5) | Jose / Erastus |

## Workshop Format

Every event follows the same two-hour structure. The first hour is a live talk by a domain expert. The second hour is a hands-on activity block — demos, workshops, or coding challenges — facilitated by the ONM team. After the live session closes, a multi-day async challenge runs in Discord with team support.

### Standard session structure

| Time | Block | Description |
| :--- | :--- | :--- |
| **0:00 – 1:00** | **Live Talk (60 min)** | Speaker presents the session topic. ONM team hosts. Live demos run in parallel in the browser for participants to follow. |
| **1:00 – 1:15** | **Live Q&A (15 min)** | Audience questions answered by speaker alongside the ONM team. |
| **1:15 – 1:50** | **Activity Block (35 min)** | Hands-on: demo exploration, coding exercise, or design workshop. Format varies by session (see individual event plans). |
| **1:50 – 2:00** | **Challenge Kickoff (10 min)** | Teams form, problem sets distributed, async challenge launched in Discord. |
| **Post-event** | **Async Discord Challenge** | Multi-day challenge with async support from ONM team. Participants share solutions, ask questions, get feedback. |

---

## Event 1 — Neuroscience Foundations for Neuromorphic Computation
**Status:** Recruiting speaker  
**Hosts:** Rayane Rocha / Jose  

**Producers:**
*   Technical logistics / streaming
*   Challenge host
*   Challenge helpers (?)
*   Browser demos? (Hosted on ONM if possible? What are the constituent parts of demos/where do we find this info - I think we plan to roll this out in the discord resource threads)

**Speaker:** TBD — seeking a neuroscientist comfortable with hardware bridges  
**Contact for speaker recruitment:** rayanerocha090@gmail.com  

### Objective
Build the vocabulary and intuition that every later event depends on. Participants should leave understanding what a neuron is as a dynamical system, why the LIF model is used instead of Hodgkin-Huxley for hardware, and how biological concepts map to chip design constraints.

### Talk outline (draft)
A full outline with speaker notes is available at: `docs.google.com/document/d/1KL1woFMM-Eyn8-DVVWEm7xz12keCAYdTUvAJPwR2HRk`

| Time | Topic | Duration | Key points | Neuromorphic bridge |
| :--- | :--- | :--- | :--- | :--- |
| **T+0** | **What is a neuron?** | 6 min | Action potential, membrane potential, resting potential, leak conductance, threshold, reset. Spike as discrete event. Dendrites, soma, axon. | *Sparsity, asynchrony, communication efficiency* |
| **T+6** | **Excitable membranes** | 8 min | Why the membrane leaks. LIF model: leak, integration, threshold, reset. The time constant. | *Four parameters capture most interesting behavior* |
| **T+14** | **Biophysical spike generation** | 8 min | Action potential internal structure. Hodgkin-Huxley as feedback system. Na+ and K+. | *HH vs LIF: why we choose LIF for hardware* |
| **T+22** | **Synaptic communication** | 8 min | Synapse: weights, delay, temporal summation, coincidence detection. Excitatory vs inhibitory. | *How the synapse maps to hardware* |
| **T+30** | **Excitation and inhibition** | 8 min | E/I balance in depth. Oscillatory regimes, no clock needed. | *Stability constraints in hardware* |
| **T+38** | **Abstraction for neuromorphic systems** | 7 min | What HH has that LIF drops; when that matters. Four things worth keeping. Brief Loihi/SpiNNaker mention. | *What did we preserve? What did we simplify?* |

### Activity block

| Time | Activity | Description | Format / Tool |
| :--- | :--- | :--- | :--- |
| **0:00 – 1:00** | **Live Talk** | Neuroscience foundations: neurons, LIF model, synapses, E/I balance, neuromorphic bridges | Presenter + slides |
| **1:00 – 1:15** | **Live Q&A** | Audience questions, answered by speaker + ONM team | Live (Discord stage / Zoom) |
| **1:15 – 1:35** | **Interactive Demo** | Patch-clamp simulator and LIF visualizer — participants follow along in browser | Browser demo (linked in Discord) |
| **1:35 – 2:00** | **Challenge Kickoff** | Introduce multi-day Discord challenge; teams form, problem sets distributed | Discord + shared doc |
| **Post-event** | **Async Challenge** | Multi-day problem set in Discord; participants solve neuroscience + LIF questions with async team support | Discord threads |

### Action items
*   Recruit neuroscientist speaker — contact rayanerocha090@gmail.com
*   Finalize talk outline with speaker (2 prep calls estimated)
*   Build / source patch-clamp simulator and LIF visualizer for demo block
*   Write Discord challenge problem set based on talk topics
*   Schedule event date (target: Summer 2026, flexible to speaker)

---

## Event 2 — Prototyping an LIF Neuron in Python
**Status:** Needs Scheduling  
**Hosts:** Effiong / Erastus  
**Speaker:** Jason Eshraghian (@jasnn) — to be confirmed for this specific session  

### Objective
Define the mathematical model of a Leaky Integrate-and-Fire (LIF) neuron and build a reference Python implementation using snnTorch. Participants should leave able to write their own LIF class from scratch and understand the math that will later be converted to hardware.

### Key takeaways
*   Write a raw Python class that simulates membrane potential, leak, and spike threshold
*   Understand the LIF equations that underpin every later hardware event
*   Visualize spike trains from a real snnTorch simulation

### Activity block

| Time | Activity | Description | Format / Tool |
| :--- | :--- | :--- | :--- |
| **0:00 – 1:00** | **Live Talk** | Math of the LIF model; build a reference implementation in Python using snnTorch | Presenter + Jupyter notebook |
| **1:00 – 1:15** | **Live Q&A** | Questions from audience on snnTorch, coding, model parameters | Live (Discord stage / Zoom) |
| **1:15 – 1:35** | **Demo: Brian 2** | Simulate a spiking neural network live using Brian 2 — watch spikes render in real time | Live screen share / Colab |
| **1:35 – 2:00** | **Challenge Kickoff** | Build an LIF neuron class from scratch in snnTorch. Simulate membrane potential, leak, threshold, and spike. | GitHub repo + Discord |
| **Post-event** | **Async Challenge** | Extended coding challenge in Discord. Participants submit working LIF implementations; team reviews async. | GitHub + Discord threads |

### Action items
*   Reach out to Jason Eshraghian to confirm interest and schedule a prep call
*   Set up demo: Brian 2 spiking simulation (live screen share or Colab notebook)
*   Create coding challenge: build an LIF neuron class in snnTorch from a template
*   Prepare Jupyter notebooks for talk and activity block

---

## Event 3 — Fundamentals of Digital Logic for Neuromorphic Engineering
**Status:** Idea Phase  
**Hosts:** Jose / Erastus  
**Speaker:** Fabrizio Otto  

### Objective
Give software engineers the EE 101 they need to follow the rest of the series. Participants should leave understanding how digital circuits represent math and biology, and be able to design a single-neuron signal using digital logic.

### Key takeaways
*   Logic gates, clock cycles, binary arithmetic — the basics relevant to neuromorphics
*   How biological spikes are represented as digital signals (AER basics)
*   Bridge: from spiking in Python to spiking in hardware

### Activity block

| Time | Activity | Description | Format / Tool |
| :--- | :--- | :--- | :--- |
| **0:00 – 1:00** | **Live Talk** | Logic gates, clock cycles, digital signal representation, AER basics — EE 101 for software engineers | Presenter + slides |
| **1:00 – 1:15** | **Live Q&A** | Questions on digital logic, signal encoding | Live |
| **1:15 – 1:35** | **Demo** | Interactive logic gate simulator — participants design a basic spiking signal circuit | Browser / shared tool |
| **1:35 – 2:00** | **Challenge Kickoff** | Design a simple AER-encoded spike signal on paper or in a simulator; share in Discord | Discord + pre-read resources |
| **Post-event** | **Async Challenge** | Participants complete a logic design worksheet based on the talk | Discord threads |

### Action items
*   Events team: confirm Fabrizio Otto as speaker; arrange prep call
*   Content team: compile a pre-read list from ONM educational resources
*   Source or build an interactive logic gate simulator for the demo block
*   Write AER encoding worksheet for async challenge

---

## Event 4 — Design the Digital Spiking Chip
**Status:** Idea Phase  
**Hosts:** Jose / Erastus  
**Speaker:** TBD  

### Objective
Translate the Python LIF model from Event 2 into a digital hardware design. Participants learn how to represent a neuron's behavior as a block diagram of digital logic components — the blueprint for the Verilog implementation in Event 5.

### Key takeaways
*   Map LIF equations to digital logic blocks (adders, registers, comparators)
*   Understand the design choices that constrain a real chip (bit width, precision, area)
*   Produce a block diagram that will be implemented in Verilog in Event 5

### Activity block

| Time | Activity | Description | Format / Tool |
| :--- | :--- | :--- | :--- |
| **0:00 – 1:00** | **Live Talk** | Translate the Python LIF model into a digital logic design; introduce chip architecture concepts | Presenter + slides / whiteboard |
| **1:00 – 1:15** | **Live Q&A** | Questions on chip design, logic-to-hardware translation | Live |
| **1:15 – 1:50** | **Design Workshop** | Participants sketch their own LIF chip block diagram; team reviews and gives feedback | Shared doc / Miro / Discord |
| **Post-event** | **Async Challenge** | Refine chip design based on feedback; submit to shared GitHub repo | GitHub + Discord |

### Action items
*   Events team: identify and recruit a speaker with chip design / digital systems background
*   Prepare block diagram template for participants to complete during activity
*   Set up shared design tool (Miro, Google Slides, or equivalent) for live collaboration

---

## Event 5 — Intro to Verilog & Hardware Description
**Status:** Idea Phase  
**Hosts:** Jose / Erastus  
**Speaker:** Dmitri (Neucom) — needs confirmation; alternatively a PhD student working on FPGAs  

### Objective
Introduce Hardware Description Language (HDL) using Verilog. Participants implement the chip designed in Event 4 as a synthesizable Verilog module. By the end, they can define a module, wire inputs and outputs, and describe the LIF neuron's behavior in hardware.

### Key takeaways
*   Verilog syntax basics: modules, ports, registers, always blocks
*   How to describe sequential and combinational logic for a neuron
*   A working (if minimal) LIF neuron Verilog module ready for simulation

### Activity block

| Time | Activity | Description | Format / Tool |
| :--- | :--- | :--- | :--- |
| **0:00 – 1:00** | **Live Talk** | Verilog syntax basics: modules, inputs, outputs, registers. Write a minimal LIF neuron module. | Presenter + live coding |
| **1:00 – 1:15** | **Live Q&A** | Questions on Verilog syntax, HDL concepts | Live |
| **1:15 – 1:50** | **Coding Activity** | Participants write or modify a Verilog module for a basic LIF neuron using a provided template | GitHub template + Colab / local |
| **Post-event** | **Async Challenge** | Complete the LIF Verilog module; run basic syntax checks; share in GitHub repo | GitHub + Discord |

### Action items
*   Events team: confirm Dmitri (Neucom) or source an alternative FPGA / Verilog speaker
*   Content team: create a Verilog template repository on GitHub (scaffold module, ports pre-defined)
*   Prepare syntax reference sheet for participants with no HDL background

---

## Event 6 — Simulating the Spiking Neuron Chip with Verilator
**Status:** Idea Phase  
**Hosts:** Jose / Erastus  
**Speaker:** TBD — preferably the same speaker as Event 5 for continuity  

### Objective
Simulate the chip designed in Events 4 and 5 using Verilator. Participants set up a testbench, run a simulation, visualize spike waveforms, and verify that the hardware behavior matches the Python model from Event 2. This is the series capstone.

### Key takeaways
*   Set up a Verilator testbench from scratch
*   Visualize waveforms: see the "spike" appear as a real digital signal
*   Verify hardware-vs-software parity: does the chip do what the Python model predicted?

### Activity block

| Time | Activity | Description | Format / Tool |
| :--- | :--- | :--- | :--- |
| **0:00 – 1:00** | **Live Talk** | Set up Verilator; write a testbench for the chip designed in Event 4/5; visualize spike waveforms | Presenter + live coding |
| **1:00 – 1:15** | **Live Q&A** | Questions on Verilator setup, waveform debugging | Live |
| **1:15 – 1:50** | **Simulation Workshop** | Participants run the testbench against their Verilog module and share waveform screenshots | GitHub repo + Verilator + Discord |
| **Post-event** | **Async Challenge** | Verify that simulated hardware behavior matches the Python model from Event 2. Final capstone submission. | GitHub + Discord |

### Action items
*   Content team: create a unified GitHub repository housing the full series codebase (Python LIF model + Verilog modules + Verilator testbenches)
*   Write setup guide for Verilator installation (Linux, Mac, and Windows via WSL)
*   Design capstone challenge: participants submit a passing testbench and waveform screenshot
*   Plan post-series retrospective and community showcase of participant work

---

## GitHub Repository Plan
A single public repository will house all code produced across the six events. This ensures participants always have a canonical reference and can see how the codebase evolves from a Python simulation to a verified hardware design.

### Proposed structure

| Folder | Contents |
| :--- | :--- |
| `/python-model` | LIF neuron class from Event 2. snnTorch notebook. Brian 2 demo. |
| `/verilog` | LIF neuron Verilog module from Events 4–5. Port/interface definitions. Participant template. |
| `/testbench` | Verilator testbench from Event 6. Waveform output examples. Verification scripts. |
| `/challenges` | Problem sets for each event's async Discord challenge. Solution stubs. |
| `/docs` | Pre-read lists, reference sheets, slide links, speaker bios. |

### Action items
*   Content team: create the repository under the Open Neuromorphic GitHub org
*   Set up branch protection and contribution guidelines
*   Add README that explains the series and links to each event recording

---

## Open Items & Next Steps

### Speakers still needed
*   **Event 1:** neuroscientist speaker (contact Rayane at rayanerocha090@gmail.com)
*   **Event 4:** chip design / digital systems background
*   **Event 6:** same speaker as Event 5 preferred for continuity

### Outreach to confirm
*   **Event 2:** reach out to Jason Eshraghian (@jasnn) to confirm for this specific coding session
*   **Event 3:** confirm Fabrizio Otto availability and scope
*   **Event 5:** confirm Dmitri (Neucom); explore PhD student alternatives

### Content team
*   Create GitHub repository structure (see above)
*   Build or source: patch-clamp simulator, LIF visualizer, logic gate simulator
*   Write challenge problem sets for all 6 events
*   Prepare Jupyter notebooks for Events 2 and 3
*   Compile pre-read list from ONM educational resources (for Event 3)

### Events team
*   Set dates for all events (target: Summer 2026; flexible to speaker schedules)
*   Confirm streaming platform and Discord challenge infrastructure
*   Design participant registration and OER release workflow

---

## Weekly Take-Home Tasks
Every event is followed by a take-home task. Each task produces one concrete artifact. That artifact is the raw material for the next session. By event 6, the six artifacts chain together into a complete pipeline: from a hand-drawn neuron sketch to a verified hardware simulation.

| # | Task | What participants build | Artifact | Format |
| :--- | :--- | :--- | :--- | :--- |
| **1** | **Sketch the neuron** | Draw + annotate a neuron diagram and voltage trace. Answer 3 written questions on leak, neuromorphic bridges, and spike rate. | Annotated diagram + voltage trace image | Pen/paper or any drawing tool |
| **2** | **Code the neuron** | Write `LIFNeuron` Python class from scratch using only NumPy. Run simulations at 3 input currents. Compare output to Task 1 sketch. | `lif_neuron.py` + spike plot | Python 3 + NumPy + Matplotlib |
| **3** | **Map the logic** | Complete an operation-mapping table (Python → digital gates). Draw a block diagram of the digital LIF circuit. Analyse required bit widths. | Mapping table + block diagram | Pen/paper; Python optional |
| **4** | **Write the spec** | Formalise the block diagram into a hardware spec: port table, internal registers, clock-cycle behaviour pseudocode, self-review. | `lif_chip_spec.md` in GitHub | Markdown / any text editor |
| **5** | **Implement in Verilog** | Fill in the provided Verilog template implementing the spec. Pass `verilator --lint-only` lint check before submitting. | `lif_neuron.v` (lint-clean) | Verilog + Verilator |
| **6** | **Simulate & verify** | Run testbench against `lif_neuron.v`. Capture waveform. Compare hardware inter-spike interval to Python model. Written reflection. | Passing testbench + waveform | Verilator + GTKWave |

### Scoring and participation
Tasks are scored out of 100 points each. For async Discord review the team uses a simplified pass / needs-revision approach. The rubrics and model answers for each task are in the Facilitator Guide document. Full participant problem sets are in the Participant Problem Sets document.

### The artifact chain
The design principle: every artifact produced in one task is the raw material for the next. A participant who reaches Task 6 will compare their hardware waveform directly against the Python simulation they wrote in Task 2, using parameters derived from the voltage trace they sketched in Task 1. The chain is intentional — errors compound forward and become teaching moments.

*   Task 1 sketch → Task 2 Python spec
*   Task 2 Python class → Task 3 translation source
*   Task 3 block diagram → Task 4 chip spec first draft
*   Task 4 spec → Task 5 Verilog target
*   Task 5 Verilog → Task 6 design under test
*   Task 6 verified waveform → portfolio capstone

### Companion documents
*   **Zero to Silicon — Participant Problem Sets:** full task instructions, questions, and code templates for participants
*   **Zero to Silicon — Facilitator Guide:** scoring rubrics, model answers, and common mistakes for each task (team use only)

*Open Neuromorphic | Zero to Silicon | Summer 2026 Draft | All content released as OER*
