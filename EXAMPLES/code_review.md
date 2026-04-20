# Example — AI-Assisted Code Review

A software team uses an AI agent to review pull requests. The AI is given permission to comment on, flag, and request changes on any PR. It is not given permission to merge.

## Actions in the Pipeline

| # | Action | Reversibility | Classification |
|:-:|--------|--------------|----------------|
| 1 | AI reads the PR and generates review comments | Reversible | Reversible |
| 2 | AI flags a PR as blocking | Reversible (the flag can be overridden) | Reversible |
| 3 | AI suggests line-level edits | Reversible | Reversible |
| 4 | Human reviewer approves PR | Reversible in the short window before merge; irreversible after merge | Reversible (until action 5) |
| 5 | Merge PR into main / default branch | **Irreversible with bounded consequence** — the commit history is hard to rewrite once downstream consumers pull | **Irreversible** |
| 6 | Deploy merged code to production | **Irreversible with unbounded consequence** — external users see the change; rollback may require coordinated action and data migrations | **Irreversible** |

## Authority Distribution

- Actions 1, 2, 3 — AI holds review authority. AI may flag, comment, suggest, and halt (in the sense that a blocking flag prevents progression to action 4).
- Action 4 — a human reviewer's approval is itself review-authority-shaped in this partition; the irreversible act is action 5.
- Action 5 — merge — is ratified by a named human (the merger). The AI does not merge, not because AI merging is logically impossible, but because merge is irreversible and Reversibility Partition places irreversible actions on a named principal.
- Action 6 — deploy — is ratified by a named human (the deployer). In systems with CD pipelines, the ratifier may be the merger if deployment is automatic; the partition still holds, it just collapses action 5 and action 6 onto the same principal.

## Observations

- Many code-review tools already implement Reversibility Partition without naming it. GitHub's "review" vs. "merge" distinction is Reversibility Partition applied to version-controlled code.
- The pattern explains *why* auto-merge rules feel uncomfortable to many teams: auto-merge moves ratification authority onto a non-named agent (the rule engine), which violates A2.
- The pattern also explains why "AI-approved PRs auto-merge" workflows typically carry a human override or audit requirement — those mechanisms restore Reversibility Partition compliance.

---

*Example authored for publication as part of the Reversibility Partition spec.*
