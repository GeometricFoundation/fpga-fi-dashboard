Technical Specification: Execution Admissibility Boundary (EAB)

This repository implements the Execution Admissibility Boundary (EAB), a formal framework designed to transition FPGA fault-injection from a "testing activity" to a "certified evidence generation process" for safety-critical systems (ISO 26262, DO-254).
1. Core Definitions: Reproducibility vs. Admissibility

To satisfy the rigorous requirements of ASIL-D or DAL-A hardware qualification, we must distinguish between the ability to run a test and the ability to trust its results.
Term	Scope	Objective
Reproducibility	Environment	The capability of an independent party to recreate the exact execution state using our Dockerized Environment and CI/CD Pipelines. It proves the toolchain is functional.
Admissibility	Evidence	The cryptographic proof that a specific benchmark result is authentically derived from a specific, untampered artifact. It proves the result is valid for certification.
2. The Admissibility Matrix (Chain of Custody)

The framework enforces a strict Hardware-Software Interface (HSI) Integrity layer. No result is considered "Admissible" unless it satisfies the following cryptographic reconciliation:
Phase 1: Input Provenance (The Immutable Anchor)

Every execution starts by generating a unique Provenance ID based on:

    Source Code Hash: SHA-256 of the RTL/HDL source files.

    Bitstream Hash: SHA-256 of the synthesized bitstream (post-layout).

    Toolchain Digest: A unique identifier/digest of the Docker container and EDA tool version (Vivado/Quartus/Yosys).

Phase 2: Deterministic Process

The Fault Injection Campaign is governed by Deterministic Parameters:

    Fault Model: SEU (Single Event Upset) or MBU (Multiple Bit Upset) targeting specific LUT/FF/BRAM coordinates.

    Campaign Seed: A fixed seed ensuring that the fault sequence can be audited and verified by a 3rd party assessor.

Phase 3: Output (The Safety Receipt)

The final output is a Signed Execution Receipt. This is not a simple log file, but a structured evidence package that binds the Provenance ID to the Fault Coverage Results. Any discrepancy between these layers invalidates the claim.
3. Reference Case Study: RISC-V PLIC Validation

To demonstrate the efficacy of the EAB framework, we provide a specific validation scenario for a RISC-V Platform-Level Interrupt Controller (PLIC).

    Target Artifact: Open-source RISC-V PLIC (RTL).

    Hardware Platform: Xilinx Artix-7 FPGA (Fabric-level injection).

    Safety Goal: ASIL-B (Automotive Safety Integrity Level).

    Objective: Verify that a transient fault in the interrupt priority logic does not lead to a "silent" failure of the Safety-Critical Interrupt Service Routine (ISR).

    Admissibility Claim: The framework generates an Execution Receipt proving that the claimed 98.5% Diagnostic Coverage (DC) was calculated using the exact RTL version integrated into the final SoC, with zero environmental drift.

4. Why This Framework Is Necessary

Traditional vendor-proprietary tools focus on Offline Validation. However, modern safety-critical systems require Independent Verification (ISO 26262-8).

By using terms like Cryptographic Proof, Tamper-Proof Trace, and Formal Admissibility Logic, this framework solves the "Validity Transfer Risk"—the dangerous assumption that a reporting dashboard is an adequate substitute for the actual integrity of the execution runtime.

Our "few lines of code" serve as the Interface Layer for this complex verification logic, providing a standardized, vendor-neutral bridge for Assessor-grade evidence generation.
