# GAL Logic Archive  
## Digital Audio Patchbay — Atari ST Development Workflow

![Project status](https://img.shields.io/badge/status-engineering%20archive-blue)
![Platform](https://img.shields.io/badge/development%20platform-Atari%20Mega%20ST-lightgrey)
![Logic](https://img.shields.io/badge/programmable%20logic-GAL16V8%20%7C%20GAL20V8-orange)
![Archive](https://img.shields.io/badge/category-engineering%20heritage-brightgreen)

> **Historical programmable-logic files, development notes, photographs, and programming tools used during the development of the RTAL Digital Audio Patchbay.**

---

## Overview

This directory documents the **GAL-based programmable logic** used during the development of the **RTAL Digital Audio Patchbay**.

The patchbay was designed as a digitally controlled audio-routing system. Its control architecture combined an **Intel 80C32 microcontroller**, conventional TTL logic, programmable logic devices, digital-audio receiver circuitry, and later a CPLD-based revision.

The GAL devices were an important part of the original hardware architecture. They allowed several address-decoding, selection, and control functions to be consolidated into compact programmable devices instead of implementing the same logic with a larger number of individual TTL packages.

The GAL source and programming files preserved here are therefore not merely auxiliary files. They are part of the original engineering record of the system.

This archive also documents the development tools used to create and program the devices. During the early 1990s, the GALs were programmed with a dedicated **Atari ST GAL programmer**, connected to the printer port of an **Atari Mega ST**.

---

## Historical context

At the time this system was developed, programmable logic devices provided an effective bridge between conventional TTL logic and more highly integrated programmable components.

GAL devices offered several practical advantages:

- reduction of discrete logic components,
- flexible address decoding,
- implementation of combinational and registered logic,
- simplified PCB routing,
- easier correction of logic functions,
- reproducible hardware revisions,
- and the possibility of preserving the logic design as source and JEDEC files.

The original Digital Audio Patchbay used GAL logic in the first hardware generation. In the later revision, parts of the original **74LS150 multiplexer and GAL logic** were replaced by a CPLD. This reduced component count further and also addressed reliability problems associated with the earlier multiplexer-based implementation.

The files in this directory preserve the earlier GAL-based stage of the design.

---

## Role of the GAL logic in the Digital Audio Patchbay

The exact function of each archived GAL file should be read together with the corresponding schematic and source file. Within the system architecture, programmable logic was used for tasks such as:

- address decoding,
- control-port decoding,
- input-selection logic,
- record-selection logic,
- routing-control functions,
- generation of enable and strobe signals,
- replacement of larger networks of SSI/MSI TTL logic,
- and coordination between the CPU board and the digital-audio matrix.

The relevant hardware sections include:

### SCH-001 — CPU Board

The CPU board contains the central control system:

- Intel 80C32,
- program memory,
- non-volatile memory depending on hardware revision,
- GAL20V8 address logic,
- 74HC573 latch,
- clock and reset circuitry,
- front-panel switches and indicators,
- and the control interface to the audio-matrix hardware.

The GAL on this board performs part of the system address decoding and peripheral-selection logic.

### SCH-002 / SCH-003 — Digital Audio Matrix

The original audio-matrix design used:

- 74LS150 multiplexers,
- GAL logic,
- CS8412 digital-audio receiver circuitry,
- 74LS574 control registers,
- input-selection and record-selection logic,
- and interface circuitry to the CPU board.

In the second hardware revision, the 74LS150 and GAL-based selection logic were replaced by a CPLD.

---

## Devices

The Atari ST programming system associated with this archive supported the following device families:

- **GAL16V8**
- **GAL16V8A**
- **GAL20V8**
- **GAL20V8A**

The actual GAL type used by each logic design should be stated in the source-file header, JEDEC file, schematic, or device label.

Typical file formats include:

| Extension | Purpose |
|---|---|
| `.JED` | JEDEC fuse map used for programming |
| `.EQN` | Logic equations |
| `.GAL` | GAL source or project file, depending on the software |
| `.PLD` | Programmable-logic source file |
| `.TXT` | Notes, pin assignments, equations, or programming information |
| `.BIN` | Binary export, where applicable |

Because several historical GAL-development programs used proprietary or loosely standardized source formats, the original files should be preserved unchanged.

---

## Original Atari ST development system

The GAL devices were programmed using an **Atari Mega ST** and a dedicated programmer connected to the computer's **Centronics-compatible printer port**.

The programming hardware was a compact design with only a small number of integrated circuits. One of the clearly identified components is a:

- **CD4094** — 8-stage serial-in/parallel-out shift register with output latch.

The CD4094 allowed multiple programming and control signals to be generated through a small number of printer-port lines. The remaining circuitry provided signal conditioning, switching, readback, and the voltages required by the GAL programming algorithm.

The programmer was a separate unit from the EPROM programmer used in the same development environment.

### Programming systems

The two historical programming devices were used:

| Function | Programmer |
|---|---|
| EPROM programming | **Junior Prommer** for Atari ST |
| GAL programming | **MAXON MGP / MPG 16/20** for Atari ST |



The historical name appears in contemporary sources in both forms:

- **MGP 16/20**
- **MPG 16/20**

For clarity, this archive uses **MAXON MGP/MPG 16/20** unless a photograph, manual, disk label, or original file establishes one spelling conclusively.

---

## GAL programmer software

The preserved screenshot appears to show the **MAXON GAL programmer software Version 2.0**.

The GEM application includes the menu structure:

```text
Datei
Typ
Bearbeiten
Compiler
Extras
```

The screenshot also shows:

- GAL type selection,
- GAL16V8/A and GAL20V8/A support,
- fuse-matrix editing,
- product-term information,
- XOR configuration,
- SYN and AC0 configuration bits,
- registered and combinational output configuration,
- source-file information,
- and automatic determination of the required programming-cycle count.

The dialog visible in the screenshot reads:

```text
Bitte GAL zum Bestimmen
der Brennzyklenzahl einsetzen
```

Available selections:

```text
16V8/A
20V8/A
Abbruch
```

This matches contemporary descriptions of the MAXON programmer software, which was expanded in Version 2.0 with an integrated two-pass logic compiler.

The compiler could process:

- Boolean logic equations,
- function tables,
- state machines,
- and mixed descriptions.

A Quine–McCluskey-based optimizer was also included.

---

## Suggested archive structure

```text
GAL/
├── README.md
│
├── source/
│   ├── original/
│   │   ├── <original GAL source files>
│   │   └── <original equation files>
│   │
│   └── documented/
│       ├── <commented or transcribed sources>
│       └── <pin-assignment documentation>
│
├── jedec/
│   ├── <original .JED files>
│   └── checksums.txt
│
├── docs/
│   ├── GAL_LOGIC_OVERVIEW.md
│   ├── PIN_ASSIGNMENTS.md
│   ├── PROGRAMMING_WORKFLOW.md
│   └── FILE_INVENTORY.md
│
├── images/
│   ├── gal_programmer_external.jpg
│   ├── gal_programmer_internal.jpg
│   ├── gal_programmer_pcb.jpg
│   ├── eprom_and_gal_programmers.jpg
│   └── maxon_gal_software_v2.png
│
└── references/
    ├── historical-notes.md
    └── source-provenance.md
```

Original files should remain in `source/original/` and should not be edited. Any reformatted, commented, or reconstructed version should be stored separately in `source/documented/`.

---

## Recommended image placement

### GAL programmer — external view

```markdown
![MAXON MGP/MPG 16/20-compatible GAL programmer — external view](images/gal_programmer_external.jpg)
```

*External view of the dedicated GAL programmer used with the Atari Mega ST.*

---

### Programmer interior

```markdown
![GAL and EPROM programmer hardware — internal view](images/gal_programmer_internal.jpg)
```

*Internal view of the historical programming equipment. The GAL programmer and the separate Junior Prommer EPROM programmer were both connected to the Atari ST printer port.*

---

### GAL programmer PCB

```markdown
![GAL programmer PCB with CD4094 shift register](images/gal_programmer_pcb.jpg)
```

*GAL programmer circuitry. The CD4094 shift register is clearly visible and was used to generate multiple programming-control signals from the Atari ST printer-port interface.*

---

### Software screenshot

```markdown
![MAXON GAL programmer software Version 2.0 on Atari ST](images/maxon_gal_software_v2.png)
```

*MAXON GAL programmer software Version 2.0 running under GEM. The dialog identifies GAL16V8/A and GAL20V8/A devices and determines the required number of programming cycles.*

---

## Historical programming workflow

A typical development and programming sequence was:

```text
Logic concept
      │
      ▼
Pin assignment
      │
      ▼
Boolean equations / function table / state machine
      │
      ▼
Compilation and logic minimization
      │
      ▼
JEDEC fuse-map generation
      │
      ▼
GAL inserted into programmer
      │
      ▼
Device identification / programming-cycle determination
      │
      ▼
Blank check
      │
      ▼
Programming
      │
      ▼
Verification
      │
      ▼
Installation in Digital Audio Patchbay
      │
      ▼
Functional test in the complete system
```

Unlike modern USB programmers, the historical system relied directly on the Atari ST and the external printer-port programmer. Timing, signal sequencing, device algorithms, and much of the user interface were handled by the Atari software.

---

## Preservation principles

This directory is intended as an engineering archive. The following principles should be observed:

### Preserve original files

Do not overwrite or convert original files in place.

Original timestamps, filenames, capitalization, and binary content may contain useful historical information.

### Record checksums

Checksums should be created for all original source and JEDEC files:

```bash
sha256sum source/original/* jedec/* > checksums.txt
```

### Separate fact from reconstruction

Any reconstructed pin assignment, retyped equation, converted file, or inferred device function should be clearly marked as:

- **verified**,
- **transcribed**,
- **reconstructed**,
- or **unconfirmed**.

### Preserve obsolete formats

Even when an original file cannot be opened with current software, it should remain in the archive. Future emulation, reverse engineering, or recovered software may make the file accessible again.

### Do not reprogram irreplaceable devices without a backup

Before attempting to read, erase, or reprogram an original GAL:

1. photograph the device and its label,
2. record its position in the system,
3. read it with a compatible programmer where possible,
4. save multiple copies of the resulting JEDEC data,
5. calculate checksums,
6. and verify the dump before carrying out any destructive operation.

Some devices may have had the security fuse set and therefore may not be readable.

---

## File inventory

The table below should be completed as the historical files are added.

| File | Device | Hardware location | Function | Status |
|---|---|---|---|---|
| `TBD` | GAL20V8 | CPU board | Address decoding | Original file to be identified |
| `TBD` | GAL16V8 / GAL20V8 | Audio matrix | Selection/control logic | Original file to be identified |
| `TBD` | — | Atari ST | Compiler/project file | Original file to be identified |
| `TBD` | — | Atari ST | JEDEC programming file | Original file to be identified |

---

## Documentation template for each GAL

For every device, create a short document using this pattern:

```markdown
# Device designation

## Hardware location

Board:
Schematic:
Reference designator:

## Device

Type:
Manufacturer:
Package:
Date code:

## Function

Describe the logical function of the device.

## Inputs

| Pin | Signal | Description |
|---|---|---|

## Outputs

| Pin | Signal | Description |
|---|---|---|

## Source files

| File | Description |
|---|---|

## JEDEC files

| File | SHA-256 |
|---|---|

## Verification status

- [ ] Source opens in original software
- [ ] Source compiles
- [ ] JEDEC file generated
- [ ] Generated JEDEC matches archived JEDEC
- [ ] Device pinout checked against schematic
- [ ] Function checked against hardware
```

---

## Relationship to the CPLD revision

The GAL files document the first programmable-logic generation of the Digital Audio Patchbay.

In the later hardware revision:

- the original 74LS150 multiplexer and GAL logic were replaced by a CPLD,
- several control functions were consolidated,
- PCB complexity was reduced,
- and the temperature-sensitive reliability issue associated with the original LS150 implementation was eliminated.

The GAL and CPLD directories should therefore be regarded as two stages of the same design evolution:

```text
Discrete TTL
     │
     ▼
TTL + GAL logic
     │
     ▼
CPLD-based integration
```

Preserving both stages makes it possible to follow the engineering decisions and hardware development over time.

---

## Why this archive matters

This material documents a period in which sophisticated digital-audio hardware could be developed with:

- an 8-bit microcontroller,
- standard TTL logic,
- early programmable logic devices,
- hand-created schematics,
- self-built programming hardware,
- and an Atari Mega ST as the development workstation.

The GAL files reveal logic that is otherwise invisible when examining the completed hardware. Without the original source and JEDEC data, an important part of the system architecture would be lost.

This archive therefore preserves not only a finished device, but also the tools, methods, intermediate technologies, and engineering decisions behind it.

---

## Known uncertainties

The following details are not yet fully verified and should remain explicitly marked as such:

- the exact model spelling **MGP 16/20** versus **MPG 16/20**,
- the identity of every IC in the surviving GAL programmer photograph,
- the exact hardware revision of the programmer,
- the complete original programmer documentation,
- and the assignment of each surviving GAL source file to its physical device.

The software screenshot and contemporary reports strongly support identification of the system as the **MAXON GAL programmer Version 2.0 for GAL16V8/A and GAL20V8/A**. Final confirmation should ideally come from an original disk label, manual, invoice, PCB marking, or executable file.

---

## Historical references

- [ST-Computer 11/1990 — Upgrade für GAL-Prommer MGP](https://stcarchiv.de/st-computer/1990/11/news)
- [ST-Magazin 02/1992 — GAL-Programmierer: Selbstgebranntes…](https://stcarchiv.de/st-magazin/1992/02/gal-programmierer)
- [ST-Computer 02/1988 — Junior Prommer](https://stcarchiv.de/st-computer/1988/02/junior-prommer)

These links are provided for historical identification and technical context. All trademarks and product names belong to their respective owners.

---

## Archive provenance

The hardware, GAL files, photographs, and related documentation originate from the development environment used for the **Digital Audio Patchbay** project.

The programmer hardware was used with an Atari Mega ST during the original development period. The surviving photographs show both the dedicated GAL-programming hardware and the separate EPROM-programming hardware.

Where original documentation is unavailable, identification is based on:

- the surviving hardware photographs,
- visible component markings,
- the remembered Atari ST workflow,
- the preserved software screenshot,
- supported GAL device types,
- and comparison with contemporary magazine reports.

---

## License

Unless otherwise noted, original project documentation and newly created explanatory material in this repository are released under the **GNU General Public License v3.0**.

Historical third-party software, screenshots, trademarks, magazine material, and product names remain the property of their respective rights holders and are included only where legally permitted for documentation, identification, and preservation.

See the repository-level [`LICENSE`](../LICENSE) file for details.

---

## Project

**RTAL Digital Audio Patchbay**  
**Engineering Heritage Archive**

A preserved record of the hardware, firmware, programmable logic, development tools, and engineering history of a digitally controlled audio-routing system.
