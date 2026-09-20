# CMOS Two-Stage Operational Amplifier Using Cadence Virtuoso

## 📌 Project Overview

This project presents the design and simulation of a **two-stage CMOS operational amplifier (Op-Amp)** using **Cadence Virtuoso** and the **GPDK090 (90 nm) technology library**.

The project focuses on transistor-level analog IC design, beginning with the CMOS Op-Amp schematic and progressing through testbench development and circuit-level simulation.

The designed amplifier consists of:

* Differential-input first stage
* Active-load/current-mirror circuitry
* Common-source second gain stage
* Bias-current generation
* Miller compensation network
* Output stage

The current stage of the project includes **schematic design, testbench development, and DC, AC, and transient analysis**.

The next stage is the physical implementation of the design using **Virtuoso Layout Suite**, followed by **DRC, LVS, parasitic extraction, and post-layout simulation**.

---

## 🎯 Objectives

The main objectives of this project are:

* Design a transistor-level two-stage CMOS operational amplifier.
* Understand the operation of differential-input amplifiers.
* Implement current-mirror and biasing circuits.
* Implement a second-stage common-source amplifier.
* Add frequency compensation for stable operation.
* Create a simulation testbench in Cadence Virtuoso.
* Perform DC operating-point analysis.
* Perform AC small-signal analysis.
* Perform transient analysis.
* Design the physical layout of the Op-Amp.
* Verify the layout using DRC.
* Verify schematic-to-layout correspondence using LVS.
* Perform post-layout simulation after parasitic extraction.

---

## 🛠️ Tools and Technology

| Parameter              | Details                              |
| ---------------------- | ------------------------------------ |
| EDA Tool               | Cadence Virtuoso                     |
| Simulator              | Spectre                              |
| Technology             | GPDK090                              |
| Technology Node        | 90 nm                                |
| Design Type            | Analog CMOS IC                       |
| Circuit                | Two-Stage CMOS Operational Amplifier |
| Schematic Editor       | Virtuoso Schematic Editor            |
| Simulation Environment | Cadence ADE / ViVA                   |
| Layout Tool            | Virtuoso Layout Suite                |
| Verification           | DRC / LVS                            |
| Future Analysis        | PEX / Post-Layout Simulation         |

---

# 🏗️ Op-Amp Architecture

The designed Op-Amp follows a conventional two-stage CMOS architecture.

### Basic signal flow

```text
              ┌─────────────────────┐
 VIN+ ───────►│                     │
              │ Differential        │
 VIN− ───────►│ Input Stage         │
              │                     │
              └──────────┬──────────┘
                         │
                         ▼
              ┌─────────────────────┐
              │ Second Gain Stage   │
              │ Common Source       │
              └──────────┬──────────┘
                         │
                         ▼
                       VOUT
```

The first stage converts the differential input voltage into a single-ended signal and provides voltage gain.

The second stage provides additional voltage gain and drives the output node.

A compensation network is included to improve frequency stability.

---

# 🔬 Transistor-Level Architecture

The transistor-level design contains the following functional blocks:

```text
                  VDD
                   │
                   │
             Bias Circuit
                   │
                  Q8
                   │
                   ▼

       Differential Input Stage
       
             Q1        Q2
              │        │
            VIN−      VIN+
              │        │
             Q3        Q4
              │        │
              └────┬───┘
                   │
                  Q5
                   │
                   ▼

              First-Stage
                Output
                   │
                   │
                 RC
                   │
                 CC
                   │
                   ▼

             Second Stage
               
                Q6
                 │
                VOUT
                 │
                Q7
                 │
                VSS
```

> **Note:** The exact transistor connections and device dimensions are defined by the project schematic and should be treated as the source of truth for the layout.

---

# 📐 Circuit Components

The main circuit elements are:

### Q1–Q2 — Differential Input Pair

Q1 and Q2 form the differential input stage.

They respond to the difference between:

```text
VIN+
VIN−
```

The differential input voltage is:

$$
V_{id}=V_{IN+}-V_{IN-}
$$

---

### Q3–Q4 — Active Load / Current-Mirror Section

Q3 and Q4 provide the active-load/current-mirror functionality of the first stage.

This converts the differential signal into a suitable single-ended signal for the second gain stage.

---

### Q5 — Bias / Current Source Device

Q5 participates in establishing the required bias current for the first stage.

---

### Q6–Q7 — Second Gain Stage

The second stage is implemented as a common-source gain stage.

It provides additional voltage gain and drives the output node:

```text
VOUT
```

---

### Q8 — Bias Circuit

Q8 belongs to the bias-current generation circuitry.

The bias network establishes the operating current required by the amplifier.

---

### RC and CC — Frequency Compensation

The compensation network consists of:

```text
RC
CC
```

It is connected between the appropriate first-stage/second-stage nodes according to the schematic.

The compensation network is used to control the amplifier's frequency response and improve stability.

---

# 🖥️ Design Flow

The project follows the standard analog CMOS design flow:

```text
Specification
     │
     ▼
Circuit Architecture
     │
     ▼
Transistor-Level Schematic
     │
     ▼
Op-Amp Symbol Creation
     │
     ▼
Testbench Development
     │
     ▼
DC Operating Point Analysis
     │
     ▼
AC Analysis
     │
     ▼
Transient Analysis
     │
     ▼
Physical Layout
     │
     ▼
DRC
     │
     ▼
LVS
     │
     ▼
Parasitic Extraction
     │
     ▼
Post-Layout Simulation
```

---

# 1️⃣ Creating the Project Library

The project was started in **Cadence Virtuoso** using the GPDK090 technology library.

A dedicated library and cell were created for the Op-Amp design.

The technology library provides:

* NMOS devices
* PMOS devices
* Design-rule information
* Device models
* Layout layers
* Simulation models

---

# 2️⃣ Creating the Op-Amp Schematic

The transistor-level schematic was created using the Virtuoso Schematic Editor.

The schematic contains:

* NMOS transistors
* PMOS transistors
* Bias circuitry
* Differential input pair
* Second gain stage
* Compensation network
* Power supply connections

The main external terminals are:

```text
VIN+
VIN−
VDD
VSS
VOUT
```

---

# 3️⃣ Creating the Op-Amp Symbol

After completing the transistor-level schematic, an Op-Amp symbol was generated.

The symbol contains five main external pins:

```text
        VDD
         │
         ▼
     ┌─────────┐
VIN+ ┤         │
VIN− ┤  OpAmp  ├── VOUT
     │         │
     └─────────┘
         │
        VSS
```

The symbol is then used as the DUT in the simulation testbench.

---

# 4️⃣ Creating the Testbench

A separate testbench cell was created:

```text
OpAmp_tb
```

The testbench contains:

* Op-Amp DUT
* Input voltage sources
* VDD supply
* VSS/GND
* Output load capacitor
* Simulation connections

The general testbench structure is:

```text
                   VDD
                    │
                    ▼
                ┌───────┐
 VIN+ ─────────►│       │
                │ OpAmp ├────── VOUT
 VIN− ─────────►│       │
                └───────┘
                    │
                   VSS
                    │
                   GND

             VOUT ── Cload ── GND
```

---

# 5️⃣ DC Operating Point Analysis

The first simulation step is the **DC operating-point analysis**.

The purpose is to verify that the amplifier is correctly biased.

The DC analysis helps determine:

* Transistor operating points
* Node voltages
* Branch currents
* Bias currents
* Device operating regions

Before performing AC analysis, the circuit should have a valid DC operating point.

---

# 6️⃣ AC Small-Signal Analysis

AC analysis is used to study the frequency response of the Op-Amp.

For the AC testbench:

```text
VIN+ → DC bias + AC excitation
VIN− → DC bias
```

A typical setup is:

```text
VIN+:
DC = 1.1 V
AC magnitude = 1 V

VIN−:
DC = 1.1 V
AC magnitude = 0 V
```

This allows the small-signal response of the amplifier to be analyzed around the selected common-mode operating point.

The AC response can be used to evaluate:

* Voltage gain
* Frequency response
* Bandwidth
* Unity-gain frequency
* Phase response
* Phase margin

The voltage gain is:

$$
A_v=\frac{V_{OUT}}{V_{IN}}
$$

and the gain in decibels is:

$$
A_v(dB)=20\log_{10}|A_v|
$$

---

# 7️⃣ Transient Analysis

Transient analysis is used to observe the time-domain behavior of the Op-Amp.

A time-varying input such as a pulse or sinusoidal signal can be applied to the input.

The transient response can be used to study:

* Output response
* Rise time
* Fall time
* Slew rate
* Settling behavior
* Output swing
* Saturation/clipping behavior

The input and output waveforms are observed using **Cadence ViVA**.

---

# 📊 Simulation Status

| Analysis               | Status         |
| ---------------------- | -------------- |
| Schematic              | ✅ Completed    |
| Op-Amp Symbol          | ✅ Completed    |
| Testbench              | ✅ Completed    |
| DC Operating Point     | ✅ Performed    |
| AC Analysis            | ✅ Performed    |
| Transient Analysis     | ✅ Performed    |
| Gain/Phase Evaluation  | 🔄 In progress |
| Layout                 | 🔄 In progress |
| DRC                    | ⏳ Pending      |
| LVS                    | ⏳ Pending      |
| Parasitic Extraction   | ⏳ Pending      |
| Post-Layout Simulation | ⏳ Pending      |

---

# 🧩 Physical Layout — Current Stage

The physical implementation is currently being developed using **Cadence Virtuoso Layout Suite**.

The layout contains the transistor-level implementation corresponding to:

```text
Q1
Q2
Q3
Q4
Q5
Q6
Q7
Q8
```

The layout process includes:

* Device placement
* Diffusion formation
* Poly gate formation
* Contacts
* Metal routing
* Vias
* Power routing
* Input routing
* Output routing
* Compensation component implementation

The layout is being developed to maintain correspondence with the original schematic.

---

# 🔍 DRC and LVS — Next Verification Stage

After completing the physical layout, the following verification steps will be performed.

## Design Rule Check — DRC

DRC will be used to check whether the physical layout satisfies the design rules of the selected technology.

Typical checks include:

* Minimum metal width
* Minimum spacing
* Poly width
* Diffusion spacing
* Contact enclosure
* Via enclosure
* Well rules
* Metal-to-metal spacing

The target is:

```text
DRC Errors = 0
```

---

## Layout Versus Schematic — LVS

LVS will compare the extracted layout netlist against the original schematic netlist.

The LVS verification should confirm:

* Same number of devices
* Correct device types
* Correct device connections
* Correct terminal names
* Correct circuit topology
* Correct transistor dimensions where applicable

The target is:

```text
LVS = CLEAN / MATCHED
```

---

# 🚧 Current Project Status

The project is currently at the **schematic simulation and initial physical-layout stage**.

### Completed

* [x] Cadence Virtuoso environment setup
* [x] GPDK090 technology setup
* [x] Two-stage CMOS Op-Amp architecture
* [x] Transistor-level schematic
* [x] Op-Amp symbol
* [x] Testbench
* [x] DC operating-point analysis
* [x] AC analysis
* [x] Transient analysis
* [x] Initial layout development

### In Progress

* [ ] Complete physical layout
* [ ] Implement RC compensation components in layout
* [ ] Complete all routing
* [ ] Power and ground routing
* [ ] Input/output pin verification

### Planned

* [ ] DRC
* [ ] LVS
* [ ] Parasitic extraction
* [ ] Post-layout simulation
* [ ] Compare pre-layout and post-layout performance
* [ ] Final documentation

---

# 📁 Suggested Repository Structure

```text
CMOS-Two-Stage-OpAmp/
│
├── README.md
│
├── schematic/
│   ├── opamp_schematic.png
│   └── opamp_symbol.png
│
├── testbench/
│   └── opamp_testbench.png
│
├── simulation/
│   ├── dc/
│   ├── ac/
│   └── transient/
│
├── layout/
│   ├── opamp_layout.png
│   ├── drc/
│   └── lvs/
│
├── results/
│   ├── dc_results.png
│   ├── ac_gain.png
│   ├── phase_response.png
│   └── transient_response.png
│
└── docs/
    └── project_report.pdf
```

---

# 📈 Performance Parameters to Report

After completing the simulations, the following parameters can be added to this README:

| Parameter            |          Result |
| -------------------- | --------------: |
| Supply Voltage       |             TBD |
| DC Gain              |             TBD |
| Unity-Gain Bandwidth |             TBD |
| Phase Margin         |             TBD |
| Gain Bandwidth       |             TBD |
| Slew Rate            |             TBD |
| Power Consumption    |             TBD |
| Load Capacitance     |             TBD |
| Technology           | GPDK090 / 90 nm |

> Numerical values will be added after the corresponding simulations are finalized.

---

# 🧠 Key Concepts Learned

This project provides practical experience with:

* CMOS analog circuit design
* Differential amplifiers
* Current mirrors
* Bias circuits
* Common-source amplifiers
* Two-stage Op-Amps
* Miller compensation
* Small-signal analysis
* Frequency response
* AC analysis
* Transient analysis
* Cadence Virtuoso
* Spectre simulation
* ViVA waveform analysis
* CMOS physical layout
* DRC
* LVS
* Parasitic extraction

---

# 🚀 Future Work

The next phase of the project will focus on completing the physical implementation.

The planned workflow is:

```text
Complete Layout
      ↓
DRC
      ↓
Fix DRC Violations
      ↓
LVS
      ↓
Fix LVS Mismatches
      ↓
Parasitic Extraction
      ↓
Post-Layout Simulation
      ↓
Compare Pre-Layout vs Post-Layout
      ↓
Final Performance Analysis
```

The post-layout results will be used to study the effect of parasitic resistance and capacitance on gain, bandwidth, phase margin, and transient performance.

---

# 📚 References

1. Cadence Virtuoso documentation and simulator environment.
2. GPDK090 technology documentation available with the installed PDK.
3. Standard CMOS analog integrated-circuit design references.
4. GitHub documentation for repository and README organization.

---

# 👨‍💻 Author

**Sujanmulk Nikash Kalyan Kumar**

B.Tech — Electronics and Communication Engineering

Mahatma Gandhi Institute of Technology (MGIT)

---

## ⭐ Project Status

**Status:** 🚧 Work in Progress

**Current milestone:** Schematic + Testbench + DC/AC/Transient Analysis + Initial Layout

**Next milestone:** Complete Layout → DRC → LVS → Post-Layout Simulation
