# OpenPrism Network

**An Open, UMA-First Architecture for Democratizing Distributed AI Inference**

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.20465112.svg)](https://doi.org/10.5281/zenodo.20465112)
[![License](https://img.shields.io/badge/license-Apache%202.0-blue.svg)](LICENSE)

---

This repository accompanies a position and architecture paper proposing OpenPrism Network — an open, UMA-first distributed inference fabric for transformer-based LLMs. The paper claims no original experimental results and is explicit about what is working, what is estimated, and what is unsolved. This README is primarily an invitation to collaborate on the unsolved parts.

**Paper:** [10.5281/zenodo.20465112](https://doi.org/10.5281/zenodo.20465112)

---

## Open Research Problems

The paper identifies two problems that are central to the architecture and, to our knowledge, unsolved. We state them here in the hope that others will take them on.

### Problem I — Consensus for ML output verification under floating-point non-determinism

The verification scheme compares outputs of $k$ independent computations and accepts on majority agreement. The difficulty is that "agreement" is not exact-match: the same model, given the same input, produces non-bitwise-identical logits across heterogeneous UMA hardware due to differing silicon generations, accelerator kernels, and floating-point reduction orders. Naive cryptographic fingerprinting therefore fails — honest nodes legitimately disagree at the bit level. Autoregressive decoding amplifies this: even a small per-step disagreement probability $\epsilon$ causes whole-sequence agreement to degrade roughly as $(1-\epsilon)^L$, so for any non-zero $\epsilon$ there is a horizon $L^*$ beyond which majority agreement breaks down without intermediate resynchronisation.

**The open problem** is a consensus protocol that:
- (a) canonicalises outputs into a representation stable across honest heterogeneous hardware,
- (b) defines a tolerance band wide enough to admit honest floating-point variation yet narrow enough to reject a fabricated or substituted result,
- (c) bounds autoregressive error amplification via intra-sequence checkpointing, and
- (d) is cheap enough that verification cost does not dominate inference cost.

This is distinct from general blockchain consensus (ordering a ledger); the hard part is deciding whether two high-dimensional floating-point tensors represent "the same computation."

### Problem II — Dynamic layer reassignment without full weight redistribution

Static layer ownership is efficient while membership is stable: weights stay resident and only activations transit the network. The problem arises when a node owning layers $i$–$j$ departs — those layers must be served by another node, which naively requires transferring their full weights across the network, defeating the purpose of static ownership.

**The open problem** is a reassignment protocol that rebalances ownership as membership changes while keeping weight movement sublinear in model size. Candidate directions include pre-staged replicas on a bounded number of standby nodes, erasure-coded layer shards reconstructable from survivors, and overlapping ownership regions that degrade gracefully. None of these is obviously optimal under realistic institutional churn rates.

---

## Community Benchmarks (Open Call)

The paper frames three measurements that would independently validate or falsify the architecture's load-bearing claims. Each is scoped so that a single result — even from two nodes and a weekend — is useful and publishable on its own. **Results for any of F1–F3 will be cited back in future revisions.**

**(F1) Perf-per-watt under verification.**
Does a $k=3$-verified UMA deployment come within $5\times$ of a batched-GPU baseline on the same model and quantisation? Published MLPerf-Inference v5.0 and community llama.cpp numbers put the unverified gap near one order of magnitude; a controlled run with a wall-power meter and the $\times 3$ verification overhead applied turns that into a real comparison.

**(F2) Honest-replica disagreement ε.**
What is $\epsilon$ between two Tier-1A nodes running identical greedy weights, and what per-token horizon $L^*$ does it imply for tolerance-band consensus? Equipment required: two nodes, the same model checkpoint, a 1k-prompt eval set, and token-by-token divergence logging. This is the cheapest of the three studies and the most informative — it independently validates or rules out the entire fingerprinting scheme.

**(F3) Churn re-dispatch overhead.**
Under a controlled-churn workload, what fraction of completed-job energy is spent re-dispatching layer shards lost to node departures? Institutional churn-rate distributions from the volunteer-computing literature supply a defensible input; a small prototype supplies the dispatcher cost.

Passes and failures are equally welcome. Open an issue to discuss methodology or share preliminary results.

---

## Other Contribution Areas

Beyond the open problems and benchmarks, contributions are welcome on:

- **Routing policy** — locality-aware scheduling, cluster formation, RTT measurement
- **Node certification** — the tok/s/W benchmark harness and Tier-1A/1B classification criteria
- **Reference runtime components** — activation-transit protocol, async queue, settlement event logs
- **Tokenomics** — incentive-compatible economic model for a permissionless inference network (also genuinely unsolved)
- **Corrections** — factual errors, broken citations, or unclear passages in the paper

See [CONTRIBUTING.md](CONTRIBUTING.md) for how to engage.

---

## Citation

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

Or use [CITATION.cff](CITATION.cff) for automated citation tools.

---

## License

Protocol specification and reference components are released under the [Apache 2.0 License](LICENSE).

**Abdalla Doleh** — Department of Industrial & Systems Engineering, Wayne State University  
ORCID: [0009-0008-5192-2167](https://orcid.org/0009-0008-5192-2167) · ai5145@wayne.edu
