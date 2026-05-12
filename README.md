Reproducible FPGA Fault Injection Framework: An Execution Admissibility Suite

1. Executive Summary & Narrowed Scope

This framework is a specialized Safety-Evidence Engine designed for the Integrity Attestation of Hardware-Software Interfaces (HSI) in FPGA-accelerated safety-critical systems.

Unlike general-purpose reliability tools, this framework addresses the specific "Admissibility Gap" in the ISO 26262 / DO-254 V-Model. It provides a cryptographic bridge between FPGA RTL verification and OS-level safety orchestration (e.g., Linux via the ELISA Project), ensuring that the diagnostic signals the kernel relies upon are authentic, untampered, and verified in runtime.

2. Core Innovation: The Execution Admissibility Boundary (EAB)

The primary technical contribution of this work is the shift from simple Reproducibility to Autonomous Admissibility.
Concept	Definition	Evidentiary Value
Reproducibility	The ability to recreate the environment via Dockerized toolchains and CI/CD pipelines.	Proves the toolchain is functional.
Admissibility	The cryptographic proof that a specific benchmark result is authentically derived from an untampered artifact.	Certified Evidence for safety auditors.
The EAB Implementation

To prevent "validity transfer risk," the framework enforces an autonomous Chain of Custody for every fault-injection campaign:

    Artifact Integrity: SHA-256 Hashing of RTL source and synthesized bitstream.

    Environment Provenance: Immutable Docker Digesting to eliminate "silent" toolchain drift.

    Deterministic Reconciliation: A pre-export "Safety Receipt" protocol that binds the execution logs to the hardware provenance.

3. Comparative Analysis

To facilitate external judgment, the following table compares the EAB Framework with prevailing industry methodologies:
Feature	Vendor-Proprietary (Xilinx SEM / Intel FI)	Netlist-Based Research Tools	EAB Framework (Ours)
Primary Goal	Fabric-level error mitigation.	Diagnostic Coverage (DC) calculation.	Runtime Evidentiary Admissibility.
Evidence Model	"Black Box" reports (Vendor Trust).	Raw data logs (Manual Audit).	Cryptographic Safety Receipt.
Vendor Neutrality	None (Proprietary).	Limited (Format-dependent).	High (RTL-level Agnostic).
Auditability	Difficult / Closed.	High, but lacks provenance.	Instant / Self-Verifying.

4. Technical Architecture & Use Case

The framework is optimized for the Independent Verification of safety-critical modules, such as the RISC-V Platform-Level Interrupt Controller (PLIC).
Reference Use Case: RISC-V PLIC on Xilinx Artix-7

    Input: SHA-256 Hash of the PLIC RTL and the target Bitstream.

    Execution: Deterministic SEU injection campaign targeting interrupt priority registers.

    Output: A signed Execution Receipt proving that the 98.5% Diagnostic Coverage (DC) claimed in the FMEDA is consistent with the specific hardware instance managed by the Linux Kernel.

5. Getting Started

To ensure frictionless inspection, the framework is delivered as a "One-Click" Dockerized environment.
Prerequisites

    Docker 24.0+

    Supported EDA Toolchain (Vivado / Quartus / Yosys)

Quick Deployment
code Bash

# Clone the repository
git clone https://github.com/your-repo/fpga-fault-injection-framework.git
cd fpga-fault-injection-framework

# Launch the Admissibility Suite
docker-compose up --build

# Generate a Signed Execution Receipt
./scripts/run_campaign.sh --target risc_v_plic --mode exhaustive

6. Documentation & Evidence

    Formal Specification: Detailed logic of the Execution Admissibility Boundary.

    Evidence Example: A sample JSON "Safety Receipt" showing the cryptographic anchors (Hash, Digest, Signature).

    Partnership Roadmap: Strategic 12-month execution timeline for global certification.

7. Compliance & Standards

This framework is designed to support evidence generation for:

    ISO 26262-8:2018 (Support for safety-related hardware integration)

    DO-254 (Design Assurance Guidance for Airborne Electronic Hardware)

    IEC 61508-2 (Requirements for electrical/electronic/programmable electronic safety-related systems)

Contact: Medesani Ph.D. Massimo/Geometric Foundation
Academic Reference: Under Review at IEEE Transactions on Reliability (2026).
Quick Start

The Admissibility Boundary

Architecture Diagram

Benchmarks: (Link to your Dashboard)
