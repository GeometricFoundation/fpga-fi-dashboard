🛡️ Execution Admissibility Boundary: Beyond Reproducibility

While standard CI/CD pipelines and Dockerization ensure environmental reproducibility, this framework is engineered to satisfy the more stringent requirement of Safety-Critical Admissibility. In compliance-heavy sectors (ISO 26262, DO-254), a benchmark is only as valid as its evidentiary provenance. To prevent "validity transfer risk," this suite enforces an autonomous Execution Admissibility Boundary that anchors every result to a verifiable Chain of Custody:

    Artifact Integrity (SHA-256 Hashing): Every fault-injection campaign is cryptographically bound to the unique hash of the source code and the synthesized hardware bitstream.

    Environment Provenance (Container Digesting): Beyond simple versioning, we record the immutable digest of the execution container and the verified identity of the toolchain to eliminate "silent" environment-induced discrepancies.

    Traceability & Reconciliation: The framework implements a pre-export result-receipting protocol. This ensures absolute deterministic reconciliation between the raw execution logs, the generated safety reports, and the final visualization dashboard, providing the quantitative proof required by certification auditors.

By decoupling the Visibility Layer (Dashboards) from the Integrity Layer (Execution Control), this framework transitions from a research tool to a robust evidentiary engine for SIL-3/4 and DAL-A hardware qualification.
Title: Reproducible FPGA Fault Injection Framework

Quick Start: (Docker commands)

The Admissibility Boundary: (Paste the text above here)

Architecture Diagram: (Showing how Hash/Digest are stored)

Benchmarks: (Link to your Dashboard)
