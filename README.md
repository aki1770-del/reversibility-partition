# Reversibility Partition

A governance pattern that distributes oversight authority by **the reversibility of the action**, not by **the class of the agent** (AI vs. human).

## The Pattern in One Paragraph

In systems where AI agents and human principals collaborate on high-stakes decisions, it is common to partition authority by agent class — AI recommends, human decides. Reversibility Partition names a different partition: **any agent, human or AI, may hold review authority over reversible actions; only a named human principal may ratify irreversible actions.** The partition tracks the action's undo cost, not the reviewer's substrate. When the action can be unwound cheaply, the reviewer's class does not matter. When the action commits resources or subjects irrevocably, a named principal must be in the loop.

## Why a Name Matters

The pattern has independent seeds in at least two active repositories (see [REFERENCE.md](REFERENCE.md)), multiple long-standing institutional precedents (Common Rule §46.116; ICH E6(R2)), and internal implementations across unrelated organizations. What is missing is a **shared vocabulary** — a single name, a citable spec, and prior-art credit in one place. This repository is that name.

## Contents

- [SPECIFICATION.md](SPECIFICATION.md) — formal statement: definitions, axioms, decision boundary, anti-patterns, edge cases, minimal implementation
- [EXAMPLES/clinical_cdss.md](EXAMPLES/clinical_cdss.md) — applied to clinical decision support
- [EXAMPLES/code_review.md](EXAMPLES/code_review.md) — applied to AI-assisted code review
- [EXAMPLES/autonomous_systems.md](EXAMPLES/autonomous_systems.md) — applied to autonomous-vehicle safety
- [REFERENCE.md](REFERENCE.md) — prior-art seeds, institutional roots, synonym mapping
- [CITATION.cff](CITATION.cff) — citation metadata (Zenodo DOI pending)

## Who This Is For

- System designers building AI-human collaborative pipelines for regulated or high-consequence decisions
- Researchers mapping AI-governance patterns who want a citable name for the "AI reviews, human commits" shape
- Maintainers of projects that already implement this shape — we want to know if the name maps onto what you are building

## Status

This is a naming-and-specification contribution. It does not claim invention. It claims that the pattern is common enough to deserve a shared term, with credit.

## License

MIT — see [LICENSE](LICENSE).
