# Example — Autonomous Vehicle with Human Disengage

A semi-autonomous vehicle operates under an assisted-driving mode. The vehicle's AI handles longitudinal and lateral control. A human driver is present and may disengage the autonomous mode at any time.

## Actions in the Pipeline

| # | Action | Reversibility | Classification |
|:-:|--------|--------------|----------------|
| 1 | AI perception system classifies objects in the scene | Reversible (re-classification on next frame) | Reversible |
| 2 | AI path planner selects a trajectory | Reversible (next frame planning updates) | Reversible |
| 3 | AI executes minor lateral / longitudinal adjustment | Reversible (next frame overrides) | Reversible |
| 4 | AI or human initiates a major maneuver (lane change, exit) | Partially reversible | **Irreversible with bounded consequence** |
| 5 | AI or human commits to a collision-imminent maneuver (hard brake, emergency swerve) | Not reversible | **Irreversible with unbounded consequence** |
| 6 | Human disengages autonomous mode | Reversible (can re-engage) | Reversible |

## Authority Distribution

This example contains a case that the previous two do not: **action 5 may need to be initiated by the AI, under time pressure, with no opportunity to obtain named-principal ratification.**

Reversibility Partition handles this with an explicit exception:

> When an irreversible action is necessary under time pressure insufficient for named-principal ratification, the AI may execute the action *only* if:
> - (a) the action is the least irreversible option among those available to avoid a worse irreversible outcome;
> - (b) the action is logged with enough context for post-hoc review;
> - (c) the system has named, in advance, the class of exceptions that may bypass ratification.

This is a constrained exception, not a dissolution of the partition. The named-principal remains in the loop via post-hoc audit.

## Observations

- The emergency-bypass exception is where most published AI-safety disagreements live. Reversibility Partition does not resolve them — it names them. Concretely: *the conditions under which an AI may ratify an irreversible action without a named principal are a policy question, not a pattern question.*
- Disengagement (action 6) is reversible for the autonomous system and makes ratification authority return to the human driver. The human driver is always the named principal for actions 4 and 5; disengagement is the human's mechanism for asserting that role.
- Systems that permit AI ratification of action 5 under emergency conditions must document the emergency class explicitly (A5 + §7.5 freshness). Implicit emergency classes are a non-conformance.

---

*Example authored for publication as part of the Reversibility Partition spec.*
