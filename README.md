# OpenPrism Network

**An Open, UMA-First Architecture for Democratizing Distributed AI Inference**

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.20465112.svg)](https://doi.org/10.5281/zenodo.20465112)
[![License](https://img.shields.io/badge/license-Apache%202.0-blue.svg)](LICENSE)

---

## Overview

Large-language-model (LLM) inference is increasingly concentrated in dedicated GPU data centres and closed API platforms, raising barriers for institutions that want to run, study, or contribute to AI infrastructure. OpenPrism Network is an open, UMA-first distributed inference architecture that enables smaller organizations to participate as operators, builders, and researchers rather than only as customers.

### Key Design Decisions

- **Static layer ownership** — transformer layers are statically owned by nodes so that weights stay resident; only activations transit the network.
- **Blockchain restricted to settlement** — the blockchain layer handles reputation, settlement, and payment only, never compute.
- **Tolerance-banded fingerprinting** — output integrity is established by multi-node redundancy with fingerprint comparison, not zero-knowledge proofs.
- **Metro-area locality routing** — inference is kept within low-latency metro-area clusters.
- **Scoped to batch/throughput workloads** — explicitly not a real-time inference network.

### Deployment Models

| Model | Description |
|-------|-------------|
| **Model 1 — Distributed Mesh** | Harvests idle institutional UMA capacity (lab workstations, teaching-cluster Macs, biotech machines already powered for a primary purpose). |
| **Model 2 — UMA Micro Data Center** | Purpose-built facility deployable by resource-constrained organizations as a sovereign inference facility. |

---

## Paper

This repository accompanies the position and architecture paper:

> Abdalla Doleh, "OpenPrism Network: An Open, UMA-First Architecture for Democratizing Distributed AI Inference," 2025.  
> **Zenodo DOI:** [10.5281/zenodo.20465112](https://doi.org/10.5281/zenodo.20465112)

The paper claims no original experimental results. All quantitative figures are drawn from publicly available benchmarks and published specifications, cited explicitly. Performance per watt is reported honestly — UMA nodes *lose* on operational efficiency against batched data-centre GPUs in the scoped regime. The architecture's advantage is on capital cost in the harvested-capacity model, on participation breadth, and on data sovereignty.

### Open Research Problems

The paper frames two genuinely unsolved problems:

1. A consensus protocol for ML output verification under floating-point non-determinism across heterogeneous UMA hardware.
2. A stable, incentive-compatible tokenomics model for a permissionless inference network.

---

## Repository Structure

```
openprism_network/
├── README.md          — this file
├── LICENSE            — Apache 2.0
├── CITATION.cff       — machine-readable citation
├── CONTRIBUTING.md    — contribution guide
└── .gitignore         — excludes local submission dirs and build artifacts
```

Submission-ready LaTeX source (`zenodo_submission/`, `fgcs_submission/`) and journal template files are kept locally and excluded from this repository via `.gitignore`.

---

## Building the Paper

Requirements: `pdflatex`, `bibtex` (TeX Live 2023+ recommended).

```bash
# Zenodo whitepaper (standard article class)
cd zenodo_submission
pdflatex openprism-whitepaper.tex
pdflatex openprism-whitepaper.tex  # cross-references

# FGCS journal submission (Elsevier CAS single-column)
cd fgcs_submission
pdflatex main.tex
bibtex main
pdflatex main.tex
pdflatex main.tex
```

> **Note:** The FGCS build requires the Elsevier CAS template files (`cas-sc.cls`, `cas-common.sty`, `cas-model2-names.bst`, `thumbnails/`) from the [Elsevier CAS LaTeX templates](https://www.elsevier.com/researcher/author/tools-and-resources/latex). These are not redistributed here.

---

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md). Contributions welcome on:

- Protocol design and formalization
- Reference implementation components
- Benchmark and evaluation methodology
- Open research problems listed above

---

## Citation

If you use this work, please cite using [CITATION.cff](CITATION.cff) or:

```bibtex
@misc{doleh2025openprism,
  author       = {Doleh, Abdalla},
  title        = {{OpenPrism Network}: An Open, {UMA}-First Architecture
                  for Democratizing Distributed {AI} Inference},
  year         = {2025},
  doi          = {10.5281/zenodo.20465112},
  url          = {https://doi.org/10.5281/zenodo.20465112},
  note         = {Position and architecture paper}
}
```

---

## License

Protocol specification and reference components are released under the [Apache 2.0 License](LICENSE).

---

## Author

**Abdalla Doleh**  
Department of Industrial & Systems Engineering, Wayne State University, Detroit, MI, USA  
ORCID: [0009-0008-5192-2167](https://orcid.org/0009-0008-5192-2167)  
Email: ai5145@wayne.edu
