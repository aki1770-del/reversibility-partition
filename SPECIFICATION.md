# Reversibility Partition — Specification v0.1

**Version:** 0.1 (pre-publication draft)
**Status:** Draft for first-contribution publication
**License:** MIT

---

## 1. Pattern Statement

**Reversibility Partition** distributes oversight authority over a multi-step process by the **reversibility of each action**, rather than by the **class of the agent** executing or reviewing the action.

> **Review authority** — the authority to flag, question, propose changes to, or temporarily halt a pending action — may be held by any agent, including AI agents.
>
> **Ratification authority** — the authority to commit to an action whose effect cannot be unwound cheaply — must be held by a named human principal.

The partition tracks the action's undo cost. It does not track the reviewer's substrate.

## 2. Definitions

| Term | Definition |
|------|------------|
| **Action** | A step in a multi-step process that has an observable effect on the world or on other steps. |
| **Reversibility** | The cost of undoing the action's effect before consequence propagates. |
| **Reversible action** | An action whose undo cost is less than or comparable to the cost of doing it again. |
| **Irreversible action** | An action whose undo cost substantially exceeds the cost of doing it again. Includes actions that commit scarce resources, expose a subject to consequence, or propagate externally. |
| **Review authority** | The authority to flag, question, propose modification, or temporarily halt a pending action. |
| **Ratification authority** | The authority to commit to an irreversible action, transitioning it from "pending" to "executed." |
| **Named principal** | A specific identified human, holding ratification authority by name and not by role-class. |
| **Halt** | A reversible suspension of a process, pending further review. |
| **Restart** | Resumption of a halted process. In this spec, restart authority mirrors ratification authority: only a named principal may restart. |

## 3. Axioms

**A1.** Review authority may be distributed freely, including to AI agents. Because review is itself reversible, review errors are correctable and do not compound.

**A2.** Ratification authority must be held by a named human principal. Because ratification commits to an irreversible action, ratification errors are not cheaply correctable and must carry named accountability.

**A3.** Any agent participating in the process may invoke review. Only the named principal may invoke ratification.

**A4.** Any agent with review authority may halt a process. Only the named principal may restart a halted process.

**A5.** Ratification requires current review state. Stale review (state that has been superseded by new evidence, new objection, or the passage of a configured freshness window) is insufficient.

## 4. Decision Boundary

For each action type in a system that adopts this pattern:

1. Classify the action as **reversible** or **irreversible**. Classification must be public and auditable.
2. For reversible actions: review authority suffices. Any agent may review. Review may halt.
3. For irreversible actions with **bounded consequence**: review authority + ratification authority. Review by any agent; ratification by the named principal.
4. For irreversible actions with **unbounded consequence** (consequences propagate beyond the originating system — external publication, subject infusion, resource broadcast): review + ratification + **post-hoc audit obligation**. The ratification event is recorded such that a third party can reconstruct the review state at the time of ratification.

## 5. Anti-patterns

The following are common partitions that are **not** Reversibility Partition and should not be confused with it:

- **Agent-class partition** — "AI agents review; human agents ratify" — is *coincident* with Reversibility Partition in many present-day systems, because AI agents happen to be assigned review roles. It is not *equivalent*: a human agent in a review role still holds review authority, not ratification authority, and an AI agent could in principle hold ratification authority in a system that explicitly delegates it (though such delegation is outside the scope of this spec). The partition is about the **action**, not the **agent**.
- **Role-based access control (RBAC)** — "admins ratify; users review" — partitions by persistent role, not by action reversibility. A single agent may have ratification authority for action X and only review authority for action Y under Reversibility Partition.
- **Consensus / quorum voting** — ratification authority under this pattern is held by a **named individual**, not by a majority. Voting schemes are a different pattern.
- **Tiered escalation** — an escalation ladder where reviews bubble up to higher authorities partitions by *severity*, not by *reversibility*. The two often coincide but are distinct dimensions.

## 6. Edge Cases

**Partial reversibility.** Some actions are reversible up to a threshold (e.g., a message is retractable for 30 seconds). Conservative default: treat as irreversible. If the system adopts a more permissive treatment, document the threshold explicitly.

**Contested reversibility.** If reviewers disagree on whether an action is reversible, treat as irreversible until the partition for that action type is formally classified.

**Time-shifted reversibility.** Some actions become less reversible over time (a data commit becomes irreversible once replicated; a synthesized compound becomes irreversible once cured). The classification should attach to the **latest moment** at which ratification is still meaningful.

**Distributed irreversibility.** When a pipeline of actions is individually reversible but collectively irreversible (each step small; the composition commits resource), the ratification point is the transition into the composition, not each step.

**Principal unavailability.** If the named principal is unreachable, the process halts. A system adopting Reversibility Partition must specify its behavior on principal unavailability in advance: either (a) indefinite halt, or (b) delegation to a successor principal whose name is pre-declared. Default: indefinite halt.

## 7. Minimal Implementation Requirements

An implementation claiming to conform to Reversibility Partition v0.1 must:

1. **Classify each action type** as reversible or irreversible, with the classification visible to all participating agents.
2. **For each irreversible action type, name a principal.** The principal is identified by a stable identifier (not merely by role).
3. **Record ratification events** with enough context to reconstruct the review state at the time of ratification. Minimum record: timestamp, ratifier identifier, identifiers of review agents whose state was consulted, and the action identifier.
4. **Enforce halt authority** — any review agent must be able to transition an irreversible pending action to halted, blocking ratification until a named principal restarts.
5. **Define freshness.** Document the maximum interval between the most recent review event and a valid ratification. If this interval is violated, ratification must re-request review.

Non-conformant implementations may still use the vocabulary; conformance requires all five above.

## 8. Relationship to Institutional Precedents

Reversibility Partition pre-dates the AI / human distinction. It was codified in human-only institutional designs across multiple decades:

- **45 CFR §46** (the U.S. Common Rule, 1974; revised 2017) — separates Institutional Review Board (IRB) **review** authority from Principal Investigator (PI) **commitment** authority. IRB reviews; PI ratifies.
- **ICH E6(R2)** (International Council for Harmonisation Good Clinical Practice, 2016) — specifies that investigator accountability is distinct from ethics-committee review.

The AI-era application is: because AI agents may safely occupy **review** roles (review is reversible), the old institutional partition's shape transfers forward without rewriting its core logic.

## 9. Open Problems (v0.1 does not resolve)

- **Quantitative reversibility metrics.** The spec treats reversibility as a binary property; in practice it is graded. A successor version may introduce a reversibility scale or cost-of-undo metric.
- **Principal succession semantics.** Default is indefinite halt; successor-principal delegation is out of scope.
- **Inter-system partitions.** When two Reversibility-Partition systems interoperate, the partition of the whole is not defined here.
- **Automation-eligibility of ratification.** This spec fixes ratification on a named human. The conditions under which ratification could be safely automated (if any) are deliberately unspecified; this is a research question, not a design choice of v0.1.

## 10. Versioning

This specification follows semantic versioning. v0.1 is a first-published draft. Incompatible changes will bump to v1.0. Conforming implementations should cite the version they target.

## 11. Credit

See [REFERENCE.md](REFERENCE.md) for prior-art seeds, institutional roots, synonym mapping, and co-creation disclosure.
