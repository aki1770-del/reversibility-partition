# References, Prior Art, and Synonym Mapping

This spec does not claim invention of the pattern it names. The pattern has independent institutional roots across decades and independent code-level seeds in active repositories. This document records credit, maps synonyms, and discloses the co-creation context of this specification.

## Institutional Roots

**45 CFR §46 — the U.S. Common Rule (1974; revised 2017).**
The Common Rule separates **IRB review authority** (institutional, collective) from **Principal Investigator commitment authority** (named, individual). IRB reviews research protocols; the PI is the named principal who commits subjects to protocol execution. This is the institutional prototype of Reversibility Partition.
Verification: U.S. Department of Health and Human Services, Office for Human Research Protections. 45 CFR 46, Subpart A. Primary: <https://www.ecfr.gov/current/title-45/subtitle-A/subchapter-A/part-46>. Backup (non-interactive): <https://www.govinfo.gov/app/details/CFR-2023-title45-vol1/CFR-2023-title45-vol1-part46>.

**ICH E6(R2) — Good Clinical Practice (International Council for Harmonisation, 2016).**
ICH E6(R2) §4 codifies the investigator's accountability as distinct from the ethics-committee review function. The investigator (a named individual) is accountable for protocol execution; the ethics committee reviews.
Verification: ICH E6(R2) Addendum. Primary PDF: <https://database.ich.org/sites/default/files/E6_R2_Addendum.pdf>. Backup (landing page): <https://www.ich.org/page/efficacy-guidelines>.

## Independent Code-Level Seeds

Two recent open-source repositories independently implement the pattern described here, without either using the term "Reversibility Partition." Their existence motivated the view that the pattern needs a shared name.

**`nwspk/politech-awards-2026`.**
Implements a review/ratify separation in a political-technology-awards pipeline: AI agents (`scripts/jury-run.py`, Project Mirror v2 evaluators) produce per-project scored rationales across 321 projects — a reversible review activity. Human CODEOWNERS then vote on iteration pull requests (48-hour deadline, majority wins) to ratify which rationale becomes canonical — the commitment activity. The agent-side output is revisable; the human-side vote closes the iteration. This is the review/ratify separation axis of Reversibility Partition, not the full pattern (the human-ratified artifact here is editorial, not subject-affecting). Credited as a partial seed.
Verification: <https://github.com/nwspk/politech-awards-2026>

**`cogdeasy/med-react-app`.**
Implements a state machine with transitions `pending_summary → summary_generated` (AI, reversible) and `under_review → approved/rejected` (human, irreversible for the consultation's effect on downstream record). The state machine encodes Reversibility Partition directly. Caveat: the implementation lives on a Devin-AI scaffold branch rather than `main`; the repo is a seed, not a production deployment. The pattern match is on shape, not on scale of use.
Verification: <https://github.com/cogdeasy/med-react-app>

These seeds are credited here because the specification synthesises their shape into named vocabulary. They are not downstream users of this spec; they are predecessors.

## Synonym Mapping

The same pattern has been referred to under various names in different literatures and project drafts. For vocabulary continuity, the following are treated as synonyms of Reversibility Partition v0.1:

| Synonym | Usage |
|---------|-------|
| **Tiered ethics** | Used in early internal drafts of the pattern. Emphasises the ethical-review tier vs. the commitment tier. |
| **Review / commitment separation** | Used in clinical-research literature. Emphasises the separation of functions. |
| **Investigator accountability pattern** | Used in GCP literature. Emphasises the named principal. |
| **IRB / PI partition** | Used in human-subjects-research literature. The domain-specific form. |
| **Human-in-the-loop at the irreversible step** | Used in AI-safety literature. Emphasises the agent partition under the AI-era application. |

Implementations may use these synonyms, but conformance with this spec requires the five minimal-implementation requirements in SPECIFICATION.md §7, independent of which term is used.

## Co-Creation Disclosure

This specification was drafted by a named human principal working with AI assistants (Claude-family large language models) in an internal governance workspace. The pattern itself pre-dates the drafting; the act captured here is naming, synthesis, and publication.

The AI assistants contributed to:
- Locating institutional precedents (Common Rule, ICH E6, NASA HRMRB).
- Drafting candidate axiom phrasings.
- Generating the three examples.

The named human principal committed to:
- The decision to publish.
- The choice of name ("Reversibility Partition").
- The specific axioms and decision boundary.
- Credit to institutional precedents and seed repositories.
- Submission of this repository and its citation metadata.

This disclosure follows the same pattern the specification describes: review authority was distributed; ratification authority rests with the named human principal.
