# Installation

This pack contains 11 independent Codex-style skills. Each folder under `skills/` contains a valid `SKILL.md`, optional references and UI metadata.

## Install one skill

Copy the chosen skill folder into the target Codex skills directory. For example, copy:

```text
skills/decision-helper/
```

to:

```text
<codex-skills-directory>/decision-helper/
```

Restart or reload the target environment if it does not detect newly added skills automatically.

## Install all 11

Copy every child directory under `skills/` into the target Codex skills directory. Do not add an extra `skills/skills/` nesting level.

## Individual archives

The `dist/individual/` distribution contains one ZIP archive per skill. Extract an archive so its top-level folder contains `SKILL.md` and `agents/openai.yaml`.

## Whole-pack archive

The whole-pack archive is intended for transfer, review and version control. Extract it first, then install the required child skill folders.

## Connections and permissions

The packages define workflows; they do not grant access to email, calendars, CRM systems, websites or private records. Connected actions remain governed by the target environment and the user's authorisation. Drafting a message never authorises sending it.

## Aletheia status

These skills implement an Aletheia-informed workflow layer. They do not claim full Aletheia Protocol conformance and do not replace the canonical Protocol 0.5.0-rc.2 specification. Relevance 0–10 is a local selection field, not epistemic confidence.
