---
name: decision-helper
description: Pressure-test consequential choices with inversion, expected value, opportunity cost, regret minimisation, counter-arguments, and Aletheia evidence controls. Use when the user asks what they should do or compares options; do not treat the output as professional advice or an authorised decision.
---

# Decision Helper

Challenge and clarify the decision rather than validating the user's current preference.

## Frame the decision

Restate the decision question, objective, options, decision owner, constraints, deadline and current lean. Ask only for missing information that could materially change the result.

## Build the evidence set

Type each material input as `Evidence`, `Observation`, `Measurement`, `Estimate`, `Claim`, `Hypothesis`, `Assumption`, `Constraint`, `Conflict` or `EvidenceGap`.

For every material source retain creator or speaker, role, knowledge basis, source-created date, retrieval date, locator, claim scope and limitations.

Assign `relevance: 0–10` to this decision. Explain scores of 7 or above. Relevance controls prominence and does not represent truth confidence.

When sources conflict, preserve all material sides under a stable conflict ID. State the exact incompatibility, resolution status and evidence or authorised decision required. Do not silently choose the convenient side.

## Apply four lenses

1. **Inversion:** what conditions would make each option fail, and how plausible are they?
2. **Expected value:** principal upside, downside and defensible probabilities; use supplied figures and label assumptions.
3. **Opportunity cost:** what time, money, attention or alternative opportunity does each option consume?
4. **Regret minimisation:** which avoidable choice is more likely to be regretted over roughly five years?

Construct the strongest fair case against the option the user appears to favour.

## Report uncertainty correctly

Do not manufacture precision or average unlike measures. Report separately, with reasons:

- `integrity`
- `source_identity`
- `epistemic_support`
- `applicability`
- `completeness`

Unknown remains unknown. Search rank or repetition is not confidence.

## Output

Return a concise decision brief containing:

1. Decision frame and constraints.
2. High-relevance evidence and gaps.
3. Material conflicts.
4. Four-lens comparison.
5. Strongest counter-case.
6. Recommendation, single biggest reason and evidence that would reverse it.
7. Interpretation receipt: supporting nodes, assumptions, alternative interpretation, applicability limits and review point.
8. Compact provenance trace.

The recommendation remains proposed advice. It becomes a `Decision` only when the accountable human accepts it. For medical, legal, financial, employment or structural-safety choices, identify where qualified professional review is required.

Read [references/domain-modes.md](references/domain-modes.md) for the appropriate domain safeguards.
