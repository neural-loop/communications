**Zero to Silicon**

Build Your Own Spiking Digital Hardware

Summer Workshop Series \| Open Neuromorphic

*Series Planning Document \| June 2026 Draft*

# **Series Overview**

Zero to Silicon is a step-by-step public educational track that takes a
software engineer or student from zero hardware background to simulating
a digital spiking neuron chip. The series is organized as a summer
workshop: each event opens with a 60-minute live talk from a domain
expert, followed by interactive demos and a structured activity block.
All materials are released as Open Educational Resources (OER).

**Track name:** Zero to Silicon

**Format:** Live online workshop --- talk (60 min) + activities (60 min)

**Audience:** Software engineers, students, and researchers with limited
hardware background

**Total events:** 6 sessions

**Timing:** Summer 2026 (dates TBD per speaker availability)

**Materials:** All content released as OER --- free to use, share, and
cite

**Platform:** Discord (async challenges + community) + live streaming
(talk + Q&A)

# **Event Overview**

The six events form a continuous curriculum. Each event builds directly
on the one before it, culminating in a full simulation of the spiking
neuron chip designed across the series.

  ----------------------------------------------------------------------------------
  **\#**   **Event**                **Status**     **Speaker**        **Hosts**
  -------- ------------------------ -------------- ------------------ --------------
  **1**    Neuroscience Foundations **Recruiting   TBD                Rayane / Jose
           for Neuromorphic         speaker**      (neuroscientist)   
           Computation                                                

  **2**    Prototyping an LIF       **Needs        Jason Eshraghian   Effiong /
           Neuron in Python         Scheduling**   (@jasnn)           Erastus

  **3**    Fundamentals of Digital  **Idea Phase** Fabrizio Otto      Jose / Erastus
           Logic for Neuromorphic                                     
           Engineering                                                

  **4**    Design the Digital       **Idea Phase** TBD                Jose / Erastus
           Spiking Chip                                               

  **5**    Intro to Verilog &       **Idea Phase** Dmitri (Neucom)    Jose / Erastus
           Hardware Description                                       

  **6**    Simulating the Spiking   **Idea Phase** TBD (cont. from    Jose / Erastus
           Neuron Chip with                        Ev. 5)             
           Verilator                                                  
  ----------------------------------------------------------------------------------

# **Workshop Format**

Every event follows the same two-hour structure. The first hour is a
live talk by a domain expert. The second hour is a hands-on activity
block --- demos, workshops, or coding challenges --- facilitated by the
ONM team. After the live session closes, a multi-day async challenge
runs in Discord with team support.

## **Standard session structure**

  -----------------------------------------------------------------------------
  **Time**         **Block**        **Description**
  ---------------- ---------------- -------------------------------------------
  **0:00 -- 1:00** **Live Talk (60  Speaker presents the session topic. ONM
                   min)**           team hosts. Live demos run in parallel in
                                    the browser for participants to follow.

  **1:00 -- 1:15** **Live Q&A (15   Audience questions answered by speaker
                   min)**           alongside the ONM team.

  **1:15 -- 1:50** **Activity Block Hands-on: demo exploration, coding
                   (35 min)**       exercise, or design workshop. Format varies
                                    by session (see individual event plans).

  **1:50 -- 2:00** **Challenge      Teams form, problem sets distributed, async
                   Kickoff (10      challenge launched in Discord.
                   min)**           

  **Post-event**   **Async Discord  Multi-day challenge with async support from
                   Challenge**      ONM team. Participants share solutions, ask
                                    questions, get feedback.
  -----------------------------------------------------------------------------

# **Event 1 --- Neuroscience Foundations for Neuromorphic Computation**

**Status:** Recruiting speaker

**Hosts:** Rayane Rocha / Jose

Producers:

Technical logistics / streaming

Challenge host

Challenge helpers (?)

Browser demos? (Hosted on ONM if possible? What are the constituent
parts of demos/where do we find this info - I think we plan to roll this
out in the discord resource threads)

**Speaker:** TBD --- seeking a neuroscientist comfortable with hardware
bridges

**Contact for speaker recruitment:** rayanerocha090@gmail.com

## **Objective**

Build the vocabulary and intuition that every later event depends on.
Participants should leave understanding what a neuron is as a dynamical
system, why the LIF model is used instead of Hodgkin-Huxley for
hardware, and how biological concepts map to chip design constraints.

## **Talk outline (draft)**

A full outline with speaker notes is available at:
docs.google.com/document/d/1KL1woFMM-Eyn8-DVVWEm7xz12keCAYdTUvAJPwR2HRk

  ---------------------------------------------------------------------------------------
  **Time**   **Topic**          **Duration**   **Key points**            **Neuromorphic
                                                                         bridge**
  ---------- ------------------ -------------- ------------------------- ----------------
  **T+0**    **What is a        6 min          Action potential,         *Sparsity,
             neuron?**                         membrane potential,       asynchrony,
                                               resting potential, leak   communication
                                               conductance, threshold,   efficiency*
                                               reset. Spike as discrete  
                                               event. Dendrites, soma,   
                                               axon.                     

  **T+6**    **Excitable        8 min          Why the membrane leaks.   *Four parameters
             membranes**                       LIF model: leak,          capture most
                                               integration, threshold,   interesting
                                               reset. The time constant. behavior*

  **T+14**   **Biophysical      8 min          Action potential internal *HH vs LIF: why
             spike generation**                structure. Hodgkin-Huxley we choose LIF
                                               as feedback system. Na+   for hardware*
                                               and K+.                   

  **T+22**   **Synaptic         8 min          Synapse: weights, delay,  *How the synapse
             communication**                   temporal summation,       maps to
                                               coincidence detection.    hardware*
                                               Excitatory vs inhibitory. 

  **T+30**   **Excitation and   8 min          E/I balance in depth.     *Stability
             inhibition**                      Oscillatory regimes, no   constraints in
                                               clock needed.             hardware*

  **T+38**   **Abstraction for  7 min          What HH has that LIF      *What did we
             neuromorphic                      drops; when that matters. preserve? What
             systems**                         Four things worth         did we
                                               keeping. Brief            simplify?*
                                               Loihi/SpiNNaker mention.  
  ---------------------------------------------------------------------------------------

## **Activity block**

  --------------------------------------------------------------------------------
  **Time**         **Activity**       **Description**           **Format / Tool**
  ---------------- ------------------ ------------------------- ------------------
  **0:00 -- 1:00** **Live Talk**      Neuroscience foundations: Presenter + slides
                                      neurons, LIF model,       
                                      synapses, E/I balance,    
                                      neuromorphic bridges      

  **1:00 -- 1:15** **Live Q&A**       Audience questions,       Live (Discord
                                      answered by speaker + ONM stage / Zoom)
                                      team                      

  **1:15 -- 1:35** **Interactive      Patch-clamp simulator and Browser demo
                   Demo**             LIF visualizer ---        (linked in
                                      participants follow along Discord)
                                      in browser                

  **1:35 -- 2:00** **Challenge        Introduce multi-day       Discord + shared
                   Kickoff**          Discord challenge; teams  doc
                                      form, problem sets        
                                      distributed               

  **Post-event**   **Async            Multi-day problem set in  Discord threads
                   Challenge**        Discord; participants     
                                      solve neuroscience + LIF  
                                      questions with async team 
                                      support                   
  --------------------------------------------------------------------------------

## **Action items**

-   Recruit neuroscientist speaker --- contact rayanerocha090@gmail.com

-   Finalize talk outline with speaker (2 prep calls estimated)

-   Build / source patch-clamp simulator and LIF visualizer for demo
    block

-   Write Discord challenge problem set based on talk topics

-   Schedule event date (target: Summer 2026, flexible to speaker)

# **Event 2 --- Prototyping an LIF Neuron in Python**

**Status:** Needs Scheduling

**Hosts:** Effiong / Erastus

**Speaker:** Jason Eshraghian (@jasnn) --- to be confirmed for this
specific session

## **Objective**

Define the mathematical model of a Leaky Integrate-and-Fire (LIF) neuron
and build a reference Python implementation using snnTorch. Participants
should leave able to write their own LIF class from scratch and
understand the math that will later be converted to hardware.

## **Key takeaways**

-   Write a raw Python class that simulates membrane potential, leak,
    and spike threshold

-   Understand the LIF equations that underpin every later hardware
    event

-   Visualize spike trains from a real snnTorch simulation

## **Activity block**

  --------------------------------------------------------------------------------
  **Time**         **Activity**       **Description**           **Format / Tool**
  ---------------- ------------------ ------------------------- ------------------
  **0:00 -- 1:00** **Live Talk**      Math of the LIF model;    Presenter +
                                      build a reference         Jupyter notebook
                                      implementation in Python  
                                      using snnTorch            

  **1:00 -- 1:15** **Live Q&A**       Questions from audience   Live (Discord
                                      on snnTorch, coding,      stage / Zoom)
                                      model parameters          

  **1:15 -- 1:35** **Demo: Brian 2**  Simulate a spiking neural Live screen share
                                      network live using Brain  / Colab
                                      2 --- watch spikes render 
                                      in real time              

  **1:35 -- 2:00** **Challenge        Build an LIF neuron class GitHub repo +
                   Kickoff**          from scratch in snnTorch. Discord
                                      Simulate membrane         
                                      potential, leak,          
                                      threshold, and spike.     

  **Post-event**   **Async            Extended coding challenge GitHub + Discord
                   Challenge**        in Discord. Participants  threads
                                      submit working LIF        
                                      implementations; team     
                                      reviews async.            
  --------------------------------------------------------------------------------

## **Action items**

-   Reach out to Jason Eshraghian to confirm interest and schedule a
    prep call

-   Set up demo: Brian 2 spiking simulation (live screen share or Colab
    notebook)

-   Create coding challenge: build an LIF neuron class in snnTorch from
    a template

-   Prepare Jupyter notebooks for talk and activity block

# **Event 3 --- Fundamentals of Digital Logic for Neuromorphic Engineering**

**Status:** Idea Phase

**Hosts:** Jose / Erastus

**Speaker:** Fabrizio Otto

## **Objective**

Give software engineers the EE 101 they need to follow the rest of the
series. Participants should leave understanding how digital circuits
represent math and biology, and be able to design a single-neuron signal
using digital logic.

## **Key takeaways**

-   Logic gates, clock cycles, binary arithmetic --- the basics relevant
    to neuromorphics

-   How biological spikes are represented as digital signals (AER
    basics)

-   Bridge: from spiking in Python to spiking in hardware

## **Activity block**

  --------------------------------------------------------------------------------
  **Time**         **Activity**       **Description**           **Format / Tool**
  ---------------- ------------------ ------------------------- ------------------
  **0:00 -- 1:00** **Live Talk**      Logic gates, clock        Presenter + slides
                                      cycles, digital signal    
                                      representation, AER       
                                      basics --- EE 101 for     
                                      software engineers        

  **1:00 -- 1:15** **Live Q&A**       Questions on digital      Live
                                      logic, signal encoding    

  **1:15 -- 1:35** **Demo**           Interactive logic gate    Browser / shared
                                      simulator ---             tool
                                      participants design a     
                                      basic spiking signal      
                                      circuit                   

  **1:35 -- 2:00** **Challenge        Design a simple           Discord + pre-read
                   Kickoff**          AER-encoded spike signal  resources
                                      on paper or in a          
                                      simulator; share in       
                                      Discord                   

  **Post-event**   **Async            Participants complete a   Discord threads
                   Challenge**        logic design worksheet    
                                      based on the talk         
  --------------------------------------------------------------------------------

## **Action items**

-   Events team: confirm Fabrizio Otto as speaker; arrange prep call

-   Content team: compile a pre-read list from ONM educational resources

-   Source or build an interactive logic gate simulator for the demo
    block

-   Write AER encoding worksheet for async challenge

# **Event 4 --- Design the Digital Spiking Chip**

**Status:** Idea Phase

**Hosts:** Jose / Erastus

**Speaker:** TBD

## **Objective**

Translate the Python LIF model from Event 2 into a digital hardware
design. Participants learn how to represent a neuron's behavior as a
block diagram of digital logic components --- the blueprint for the
Verilog implementation in Event 5.

## **Key takeaways**

-   Map LIF equations to digital logic blocks (adders, registers,
    comparators)

-   Understand the design choices that constrain a real chip (bit width,
    precision, area)

-   Produce a block diagram that will be implemented in Verilog in Event
    5

## **Activity block**

  --------------------------------------------------------------------------------
  **Time**         **Activity**       **Description**           **Format / Tool**
  ---------------- ------------------ ------------------------- ------------------
  **0:00 -- 1:00** **Live Talk**      Translate the Python LIF  Presenter + slides
                                      model into a digital      / whiteboard
                                      logic design; introduce   
                                      chip architecture         
                                      concepts                  

  **1:00 -- 1:15** **Live Q&A**       Questions on chip design, Live
                                      logic-to-hardware         
                                      translation               

  **1:15 -- 1:50** **Design           Participants sketch their Shared doc / Miro
                   Workshop**         own LIF chip block        / Discord
                                      diagram; team reviews and 
                                      gives feedback            

  **Post-event**   **Async            Refine chip design based  GitHub + Discord
                   Challenge**        on feedback; submit to    
                                      shared GitHub repo        
  --------------------------------------------------------------------------------

## **Action items**

-   Events team: identify and recruit a speaker with chip design /
    digital systems background

-   Prepare block diagram template for participants to complete during
    activity

-   Set up shared design tool (Miro, Google Slides, or equivalent) for
    live collaboration

# **Event 5 --- Intro to Verilog & Hardware Description**

**Status:** Idea Phase

**Hosts:** Jose / Erastus

**Speaker:** Dmitri (Neucom) --- needs confirmation; alternatively a PhD
student working on FPGAs

## **Objective**

Introduce Hardware Description Language (HDL) using Verilog.
Participants implement the chip designed in Event 4 as a synthesizable
Verilog module. By the end, they can define a module, wire inputs and
outputs, and describe the LIF neuron's behavior in hardware.

## **Key takeaways**

-   Verilog syntax basics: modules, ports, registers, always blocks

-   How to describe sequential and combinational logic for a neuron

-   A working (if minimal) LIF neuron Verilog module ready for
    simulation

## **Activity block**

  --------------------------------------------------------------------------------
  **Time**         **Activity**       **Description**           **Format / Tool**
  ---------------- ------------------ ------------------------- ------------------
  **0:00 -- 1:00** **Live Talk**      Verilog syntax basics:    Presenter + live
                                      modules, inputs, outputs, coding
                                      registers. Write a        
                                      minimal LIF neuron        
                                      module.                   

  **1:00 -- 1:15** **Live Q&A**       Questions on Verilog      Live
                                      syntax, HDL concepts      

  **1:15 -- 1:50** **Coding           Participants write or     GitHub template +
                   Activity**         modify a Verilog module   Colab / local
                                      for a basic LIF neuron    
                                      using a provided template 

  **Post-event**   **Async            Complete the LIF Verilog  GitHub + Discord
                   Challenge**        module; run basic syntax  
                                      checks; share in GitHub   
                                      repo                      
  --------------------------------------------------------------------------------

## **Action items**

-   Events team: confirm Dmitri (Neucom) or source an alternative FPGA /
    Verilog speaker

-   Content team: create a Verilog template repository on GitHub
    (scaffold module, ports pre-defined)

-   Prepare syntax reference sheet for participants with no HDL
    background

# **Event 6 --- Simulating the Spiking Neuron Chip with Verilator**

**Status:** Idea Phase

**Hosts:** Jose / Erastus

**Speaker:** TBD --- preferably the same speaker as Event 5 for
continuity

## **Objective**

Simulate the chip designed in Events 4 and 5 using Verilator.
Participants set up a testbench, run a simulation, visualize spike
waveforms, and verify that the hardware behavior matches the Python
model from Event 2. This is the series capstone.

## **Key takeaways**

-   Set up a Verilator testbench from scratch

-   Visualize waveforms: see the "spike" appear as a real digital signal

-   Verify hardware-vs-software parity: does the chip do what the Python
    model predicted?

## **Activity block**

  --------------------------------------------------------------------------------
  **Time**         **Activity**       **Description**           **Format / Tool**
  ---------------- ------------------ ------------------------- ------------------
  **0:00 -- 1:00** **Live Talk**      Set up Verilator; write a Presenter + live
                                      testbench for the chip    coding
                                      designed in Event 4/5;    
                                      visualize spike waveforms 

  **1:00 -- 1:15** **Live Q&A**       Questions on Verilator    Live
                                      setup, waveform debugging 

  **1:15 -- 1:50** **Simulation       Participants run the      GitHub repo +
                   Workshop**         testbench against their   Verilator +
                                      Verilog module and share  Discord
                                      waveform screenshots      

  **Post-event**   **Async            Verify that simulated     GitHub + Discord
                   Challenge**        hardware behavior matches 
                                      the Python model from     
                                      Event 2. Final capstone   
                                      submission.               
  --------------------------------------------------------------------------------

## **Action items**

-   Content team: create a unified GitHub repository housing the full
    series codebase (Python LIF model + Verilog modules + Verilator
    testbenches)

-   Write setup guide for Verilator installation (Linux, Mac, and
    Windows via WSL)

-   Design capstone challenge: participants submit a passing testbench
    and waveform screenshot

-   Plan post-series retrospective and community showcase of participant
    work

# **GitHub Repository Plan**

A single public repository will house all code produced across the six
events. This ensures participants always have a canonical reference and
can see how the codebase evolves from a Python simulation to a verified
hardware design.

## **Proposed structure**

  -----------------------------------------------------------------------
  **Folder**                  **Contents**
  --------------------------- -------------------------------------------
  **/python-model**           LIF neuron class from Event 2. snnTorch
                              notebook. Brian 2 demo.

  **/verilog**                LIF neuron Verilog module from Events 4--5.
                              Port/interface definitions. Participant
                              template.

  **/testbench**              Verilator testbench from Event 6. Waveform
                              output examples. Verification scripts.

  **/challenges**             Problem sets for each event's async Discord
                              challenge. Solution stubs.

  **/docs**                   Pre-read lists, reference sheets, slide
                              links, speaker bios.
  -----------------------------------------------------------------------

## **Action items**

-   Content team: create the repository under the Open Neuromorphic
    GitHub org

-   Set up branch protection and contribution guidelines

-   Add README that explains the series and links to each event
    recording

# **Open Items & Next Steps**

## **Speakers still needed**

-   Event 1: neuroscientist speaker (contact Rayane at
    rayanerocha090@gmail.com)

-   Event 4: chip design / digital systems background

-   Event 6: same speaker as Event 5 preferred for continuity

## **Outreach to confirm**

-   Event 2: reach out to Jason Eshraghian (@jasnn) to confirm for this
    specific coding session

-   Event 3: confirm Fabrizio Otto availability and scope

-   Event 5: confirm Dmitri (Neucom); explore PhD student alternatives

## **Content team**

-   Create GitHub repository structure (see above)

-   Build or source: patch-clamp simulator, LIF visualizer, logic gate
    simulator

-   Write challenge problem sets for all 6 events

-   Prepare Jupyter notebooks for Events 2 and 3

-   Compile pre-read list from ONM educational resources (for Event 3)

## **Events team**

-   Set dates for all events (target: Summer 2026; flexible to speaker
    schedules)

-   Confirm streaming platform and Discord challenge infrastructure

-   Design participant registration and OER release workflow

# **Weekly Take-Home Tasks**

Every event is followed by a take-home task. Each task produces one
concrete artifact. That artifact is the raw material for the next
session. By event 6, the six artifacts chain together into a complete
pipeline: from a hand-drawn neuron sketch to a verified hardware
simulation.

  ------------------------------------------------------------------------------
  **\#**   **Task**      **What participants **Artifact**        **Format**
                         build**                                 
  -------- ------------- ------------------- ------------------- ---------------
  **1**    **Sketch the  Draw + annotate a   Annotated diagram + Pen/paper or
           neuron**      neuron diagram and  voltage trace image any drawing
                         voltage trace.                          tool
                         Answer 3 written                        
                         questions on leak,                      
                         neuromorphic                            
                         bridges, and spike                      
                         rate.                                   

  **2**    **Code the    Write LIFNeuron     lif_neuron.py +     Python 3 +
           neuron**      Python class from   spike plot          NumPy +
                         scratch using only                      Matplotlib
                         NumPy. Run                              
                         simulations at 3                        
                         input currents.                         
                         Compare output to                       
                         Task 1 sketch.                          

  **3**    **Map the     Complete an         Mapping table +     Pen/paper;
           logic**       operation-mapping   block diagram       Python optional
                         table (Python →                         
                         digital gates).                         
                         Draw a block                            
                         diagram of the                          
                         digital LIF                             
                         circuit. Analyse                        
                         required bit                            
                         widths.                                 

  **4**    **Write the   Formalise the block lif_chip_spec.md in Markdown / any
           spec**        diagram into a      GitHub              text editor
                         hardware spec: port                     
                         table, internal                         
                         registers,                              
                         clock-cycle                             
                         behaviour                               
                         pseudocode,                             
                         self-review.                            

  **5**    **Implement   Fill in the         lif_neuron.v        Verilog +
           in Verilog**  provided Verilog    (lint-clean)        Verilator
                         template                                
                         implementing the                        
                         spec. Pass                              
                         verilator                               
                         \--lint-only lint                       
                         check before                            
                         submitting.                             

  **6**    **Simulate &  Run testbench       Passing testbench + Verilator +
           verify**      against             waveform            GTKWave
                         lif_neuron.v.                           
                         Capture waveform.                       
                         Compare hardware                        
                         inter-spike                             
                         interval to Python                      
                         model. Written                          
                         reflection.                             
  ------------------------------------------------------------------------------

## **Scoring and participation**

Tasks are scored out of 100 points each. For async Discord review the
team uses a simplified pass / needs-revision approach. The rubrics and
model answers for each task are in the Facilitator Guide document. Full
participant problem sets are in the Participant Problem Sets document.

## **The artifact chain**

The design principle: every artifact produced in one task is the raw
material for the next. A participant who reaches Task 6 will compare
their hardware waveform directly against the Python simulation they
wrote in Task 2, using parameters derived from the voltage trace they
sketched in Task 1. The chain is intentional --- errors compound forward
and become teaching moments.

-   Task 1 sketch → Task 2 Python spec

-   Task 2 Python class → Task 3 translation source

-   Task 3 block diagram → Task 4 chip spec first draft

-   Task 4 spec → Task 5 Verilog target

-   Task 5 Verilog → Task 6 design under test

-   Task 6 verified waveform → portfolio capstone

## **Companion documents**

-   Zero to Silicon --- Participant Problem Sets: full task
    instructions, questions, and code templates for participants

-   Zero to Silicon --- Facilitator Guide: scoring rubrics, model
    answers, and common mistakes for each task (team use only)

*Open Neuromorphic \| Zero to Silicon \| Summer 2026 Draft \| All
content released as OER*
