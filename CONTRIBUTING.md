# Contributing to OpenPrism Network

Thank you for your interest in contributing. This repository accompanies an architecture and position paper, so contributions naturally take a different form than a typical software project.

---

## Ways to Contribute

### 1. Protocol Design and Formalization

The paper identifies two genuinely open research problems:

- **Output verification consensus** — a protocol for reaching consensus on ML output correctness under floating-point non-determinism across heterogeneous UMA hardware.
- **Tokenomics** — a stable, incentive-compatible economic model for a permissionless inference network.

Contributions here could take the form of:
- Proposed protocol specifications (as issues or pull requests to a spec document)
- Formal analyses or proofs of safety/liveness properties
- Survey of related work that bears on these problems

### 2. Reference Implementation

The paper describes several components that could be prototyped:

- The routing layer (metro-area locality, RTT-based clustering)
- The tolerance-banded fingerprinting comparator
- The static layer ownership / activation-transit protocol
- A node certification benchmark harness

### 3. Benchmarking and Evaluation

- Reproduce or extend the tok/s/W measurements cited in the paper
- Evaluate the batch-only scope claim against real workloads
- Measure RTT distributions across candidate metro-area deployments

### 4. Corrections and Clarifications

If you find factual errors, broken citations, or unclear passages in the paper, please open an issue.

---

## Submitting Changes

1. **Fork** the repository.
2. **Create a branch** with a descriptive name (`fix/tco-formula`, `feat/fingerprinting-spec`, etc.).
3. **Open a pull request** with a clear description of the change and its motivation.

For anything substantive (new protocol proposals, major corrections), please open an **issue first** to discuss before investing significant effort.

---

## Code of Conduct

This project follows the [Contributor Covenant](https://www.contributor-covenant.org/) Code of Conduct. Be respectful, constructive, and honest.

---

## Contact

**Abdalla Doleh** — ai5145@wayne.edu  
ORCID: [0009-0008-5192-2167](https://orcid.org/0009-0008-5192-2167)
