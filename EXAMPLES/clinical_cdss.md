# Example — Clinical Decision Support

**Pending ARBITER review for patient-data leakage before publication.**

This example is constructed from publicly documented clinical-decision-support patterns. It uses no real patient data, no identifiable case, and no internal protocol details from any specific operating system. It demonstrates how Reversibility Partition applies to the general shape of AI-assisted clinical workflows.

---

## Setting

A clinical decision support (CDSS) pipeline assists a single treating clinician. The pipeline ingests patient data (sequencing, labs, imaging), proposes candidate interventions, and requires clinician commitment before any intervention is administered.

## Actions in the Pipeline

| # | Action | Reversibility | Classification |
|:-:|--------|--------------|----------------|
| 1 | Ingest patient data; generate candidate interventions | Reversible (no external effect yet) | Reversible |
| 2 | Rank candidates by predicted benefit / risk | Reversible | Reversible |
| 3 | Flag ethics or safety concern on any candidate | Reversible (a flag can be reviewed and lifted) | Reversible |
| 4 | Order reagents / preparatory work for the chosen candidate | Partially reversible (reagents have shelf life and opportunity cost) | **Irreversible with bounded consequence** |
| 5 | Administer the intervention to the patient | Not reversible | **Irreversible with unbounded consequence** |

## Authority Distribution

Under Reversibility Partition:

- Actions 1, 2, 3 are **reversible** → AI agents hold review authority freely. AI agents may flag candidates, rank them, propose alternatives, halt the pipeline for review.
- Action 4 is **irreversible with bounded consequence** → requires both AI review and a named clinician ratification. The ratification event is logged with enough context to reconstruct the AI review state at ratification time.
- Action 5 is **irreversible with unbounded consequence** → requires AI review, named clinician ratification, and a post-hoc audit obligation (a third party can reconstruct the review state at the time of ratification).

## What Is Not Partitioned by Agent Class

Note that in this example:

- A clinician who disagrees with the AI ranking in action 2 is still exercising **review** authority when they flag it for reconsideration. They do not need ratification authority to flag.
- Conversely, an AI agent does not acquire ratification authority for action 5 simply by being well-calibrated. Ratification is fixed on a named clinician because action 5 is irreversible, not because the AI is error-prone.

The partition tracks the action, not the agent.

## Halt Behavior

Any review agent — AI or human, ethics-reviewer or safety-monitor — may halt the pipeline before action 4 or action 5. Only the named clinician may restart.

## Freshness

Action 5 ratification requires that the most recent review event is within a system-defined interval (e.g., "review state must be no older than 24 hours"). If the interval is violated, ratification re-requests review before proceeding.

## What This Example Illustrates

- The AI / human partition that appears in most CDSS architectures is a **coincidence** of Reversibility Partition applied to a domain where most irreversible actions also happen to be actions that a human has traditionally performed.
- The pattern generalises: a CDSS that added a new action type (say, automated reagent preparation) would classify it by reversibility, not by "was this previously a human action."
- The Common Rule (45 CFR §46) and ICH E6(R2) already enforce the pattern for human-only clinical research. Reversibility Partition names the shape they already implement.

---

*Example authored for publication as part of the Reversibility Partition spec. No patient data, no identifiable case, no operating-system-specific protocol details are used.*
