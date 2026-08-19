# 11 AI Skills for Knowledge Workers

Adapted from HubSpot's public guide, [11 Ready-to-Install AI Skills for Knowledge Workers](https://offers.hubspot.com/view/ai-skills-knowledge-workers), accessed 18 August 2026.

## Important note

HubSpot describes these as ready-to-install skills, but the page actually supplies prompts that instruct Claude, ChatGPT Work or Codex to create the skills. The prompts below preserve the advertised workflows in original, consolidated wording; they are not verbatim copies of HubSpot's text.

The reference filenames are suggestions rather than mandatory platform conventions. An AI workspace may store the same information under different names.

## Shared Aletheia integrity layer

All 11 skills below use an Aletheia-inspired evidence layer. Skills 4, 7, 8, 9 and 11 apply the enhanced form because their outputs are especially likely to influence decisions.

### 1. Type material statements

Where the distinction matters, label information as:

- `Evidence`
- `Observation`
- `Measurement`
- `Estimate`
- `Claim`
- `Hypothesis`
- `Assumption`
- `Conflict`
- `EvidenceGap`
- `Decision`
- `Constraint`

Do not silently turn an attributed claim, estimate or inference into a fact.

### 2. Record provenance

For every material source, retain as much of the following as is available:

``` yaml
source_id: stable identifier
source_class: primary | secondary | derived | testimony | system-record | unknown
creator_or_speaker: name, role, redacted, or unknown
knowledge_basis: direct | reported | inferred | generated | unknown
source_created_at: ISO date-time or unknown
observed_at: ISO date-time or unknown
retrieved_at: ISO date-time
locator: file, URL, page, lines, message, transcript timestamp, or record ID
claim_scope: what the source can support
limitations: []
privacy_class: public | project-private | restricted
```

Source date and retrieval date are different fields. Current-state claims must be rechecked when their age or changed circumstances could affect applicability.

### 3. Score relevance separately from confidence

Use `relevance: 0–10` only to decide what belongs in the current task or rendition:

| Score | Meaning                                                                             | Normal treatment                                                 |
|------:|-------------------------------------------------------------------------------------|------------------------------------------------------------------|
|     0 | No present task relevance; trivial correction, duplicate or fully superseded detail | Omit from the active output; archive only if audit value remains |
|   1–3 | Peripheral context                                                                  | Usually exclude or place in background                           |
|   4–6 | Material supporting context                                                         | Include when it helps interpretation                             |
|   7–8 | Directly decision-relevant                                                          | Include prominently                                              |
|  9–10 | Outcome-changing, urgent or mandatory                                               | Lead with it and flag for review                                 |

Relevance is not truth, confidence, importance in every context or permission to act. A low-relevance item must still be retained when it is a mandatory constraint, a material conflict side or necessary audit evidence.

### 4. Keep confidence dimensions separate

Do not produce a single averaged confidence score. Where useful, report:

``` yaml
confidence:
  integrity: matched | unverified | mismatch | unknown
  source_identity: confirmed | probable | uncertain | unknown
  epistemic_support: strong | moderate | weak | unsupported | unknown
  applicability: current | partial | outdated | not_applicable | unknown
  completeness: sufficient | material_gaps | incomplete | unknown
  reasons: []
```

Unknown must remain unknown. Every qualitative label needs a short reason.

### 5. Detect and preserve contradictions

When two material sources or nodes cannot both be accepted as stated:

1.  Create a stable `conflict_id`.
2.  Preserve every material side and its source.
3.  State the precise point of incompatibility.
4.  Mark the conflict `unresolved`, `partially_resolved` or `resolved`.
5.  Identify what evidence or authorised decision could resolve it.
6.  Retrieve the conflict whenever a linked claim is used.

Do not treat deletion of one side as resolution. Corrected spelling, formatting noise or exact duplicates need not be promoted into conflicts unless identity or meaning is genuinely uncertain.

### 6. Finish consequential outputs with a compact provenance trace

Record the trigger task, retrieval mode, principal sources, source dates, high-relevance items, conflicts retrieved, excluded or unavailable material, evidence gaps, confidence dimensions and human review points. This describes observable inputs and operations; it must not claim to reveal private chain-of-thought.

### Suggested shared reference files

``` text
/Aletheia/
  source-register.md
  claim-register.md
  conflict-register.md
  evidence-gaps.md
  provenance-trace.md
  interpretation-receipts.md
```

------------------------------------------------------------------------

## 1. The Humanizer — Brand Voice Skill

### Purpose

Learn the user's genuine writing style and apply it when generating new material or revising AI-sounding drafts.

### Inputs

- Three to five genuine writing samples, such as emails, posts or proposals.
- For editing mode: the draft to be revised.
- For generation mode: the subject, audience, format and desired outcome.

### Outputs

- Newly written material that follows the user's voice profile; or
- A revised draft with generic AI mannerisms removed.

### Reference files

``` text
/References/
  writing-samples.md
```

### Copy-paste build prompt

``` text
Build a reusable skill named "humanizer".

Its job is to write in my recognisable voice and to revise drafts that sound generic or machine-generated.

During setup, ask me for three to five substantial samples of my real writing. Store or reference them in /References/writing-samples.md. Analyse recurring features including sentence length, rhythm, vocabulary, directness, formality, humour, paragraph structure, typical openings and closings, and phrases I commonly use or avoid. Create a concise voice profile from evidence in those samples. Do not invent traits that the samples do not support.

Support two operating modes:

1. Generation mode: produce new text using my voice profile while respecting the requested audience, purpose and format.
2. Editing mode: when I ask to humanise a draft, preserve its meaning and factual content while removing generic AI language, empty introductions, needless hedging, inflated corporate wording, repetitive contrasts, excessive em dashes and expressions that do not fit my samples.

If the requested tone differs from my normal voice, retain my underlying style while making the smallest necessary adjustment. Do not introduce facts, quotations or personal experiences that I did not provide.

Apply the shared Aletheia integrity layer proportionately. Record the creator, approximate creation date and context of each writing sample when known. Give greater relevance to samples that match the requested audience and current period. If older and newer samples show materially different voices, preserve that as a dated variation instead of blending them invisibly. Treat exact duplicates, corrected spelling and formatting noise as relevance 0 unless they affect identity or meaning.

Activate when I ask you to write, draft, rewrite, edit or humanise material. Return clean, ready-to-paste text unless I request commentary or tracked changes.
```

------------------------------------------------------------------------

## 2. Inbox Triage and Draft Replies

### Purpose

Convert an inbox into a prioritised action brief and prepare concise replies for review.

### Inputs

- A connected email inbox; or
- Emails pasted or uploaded manually.

### Outputs

- A short inbox overview.
- Messages grouped by priority.
- Identification of urgent and commercially important messages.
- Draft replies for the messages requiring attention.

### Reference files

No reference files are required. It can optionally call the Humanizer skill for the user's writing style.

### Copy-paste build prompt

``` text
Build a reusable skill named "inbox-triage".

Its job is to examine recent unread email, identify what needs my attention and prepare draft responses without sending anything.

When email access is available, review the relevant unread messages. If it is unavailable, ask me to paste or upload the messages. Categorise each message as:

1. Respond today — urgent matters, active clients or leads, deadlines, payment or revenue signals.
2. Respond this week — important but not immediately time-sensitive.
3. Information only — useful context with no reply required.
4. Archive or unsubscribe candidate — low-value mail, resolved threads or recurring noise.

Begin with a two-line overview stating how many messages need action today and whether anything appears urgent, unusual or financially important. For every Respond today item, explain briefly why it belongs there and prepare a short, decisive reply. Use my Humanizer skill when available.

Clearly distinguish facts stated in the email from your interpretation. Flag ambiguous deadlines, uncertain identity, suspicious requests or missing context rather than guessing.

Apply the shared Aletheia integrity layer. Record message sender, sent date, thread or message locator and retrieval date. Give each actionable message a relevance score from 0 to 10 and a short reason; use urgency and commercial impact as separate descriptors rather than allowing either to masquerade as truth confidence. Detect contradictions between messages in the same thread, such as incompatible dates, prices or commitments, and show both sides. Add confidence dimensions only where identity, integrity, applicability or completeness is uncertain.

Never send, delete, archive, unsubscribe from or otherwise alter email. Present all proposed actions and drafts for my approval.

Activate when I say phrases such as "triage my inbox", "check my email" or "what needs me today".
```

------------------------------------------------------------------------

## 3. Content Repurposing

### Purpose

Turn one completed source asset into distinct, platform-appropriate derivative content.

### Inputs

- A video or podcast transcript, article, newsletter, blog post or detailed notes.
- Two or three examples of the user's successful content for each relevant platform.

### Outputs

- A LinkedIn post.
- An email or newsletter section.
- A short blog draft when the source supports one.
- Three short-form hooks or opening lines.

### Reference files

``` text
/References/
  format-patterns.md
  platform-examples.md
```

### Copy-paste build prompt

``` text
Build a reusable skill named "content-repurposer".

Its job is to transform one finished source asset into several pieces that feel native to their destination platforms rather than duplicated across them.

During setup, ask for two or three examples of my published work from each platform I use. Store the examples in /References/platform-examples.md and record the observed format patterns in /References/format-patterns.md. Learn from my real structures, hooks, pacing, paragraph length and calls to action; do not substitute generic platform advice where my examples show a different approach.

When I supply a transcript, article, newsletter or detailed notes, extract the most valuable concrete material: specific examples, numbers, surprising observations, useful explanations, strong opinions and memorable moments. Do not flatten the source into a vague summary.

Produce:

1. One LinkedIn post following my demonstrated structure.
2. One email or newsletter section.
3. One short blog draft if the source contains enough substance.
4. Three short-form hooks suitable for social posts or video openings.

Use the Humanizer skill for my voice. Preserve the source's meaning, do not fabricate supporting facts and mark any detail that needs verification. Separate each deliverable clearly and make it ready to paste.

Apply the shared Aletheia integrity layer. Preserve the source asset's creator, publication or recording date, retrieval date and usable locators such as page, paragraph or transcript timestamp. Score candidate source moments for relevance from 0 to 10 before selecting them. If the source contains internal contradictions or a later source supersedes an earlier claim, do not silently harmonise them. Carry the material conflict or qualification into the derivative content where relevant.

Activate when I ask to repurpose material or provide completed content and request posts or derivatives.
```

------------------------------------------------------------------------

## 4. Decision-Making Skill

### Purpose

Pressure-test a choice using four structured reasoning lenses and a deliberate counter-case.

### Inputs

- A concise description of the decision.
- Available options.
- Relevant constraints or numerical information.
- The option the user currently favours, if any.

### Outputs

- Analysis using inversion, expected value, opportunity cost and regret minimisation.
- The strongest case against the user's current preference.
- A clear recommendation and its principal reason.

### Reference files

No task-specific business reference file is required. For the enhanced Aletheia layer, use:

``` text
/Aletheia/
  source-register.md
  claim-register.md
  conflict-register.md
  evidence-gaps.md
  provenance-trace.md
  interpretation-receipts.md
```

### Copy-paste build prompt

``` text
Build a reusable skill named "decision-helper".

Its job is to challenge and clarify my business decisions, not to validate whichever answer I already prefer.

When I describe a choice, first restate the decision, options, objective and material constraints. Ask only for missing information that could materially change the conclusion. Then examine every viable option through these four lenses:

1. Inversion: identify the conditions that would make the option fail and estimate how plausible they are.
2. Expected value: describe the principal upside and downside, attach approximate probabilities when defensible, use my figures where available and label all assumptions.
3. Opportunity cost: identify what the option consumes or prevents, particularly time, money, attention and alternative opportunities.
4. Regret minimisation: consider which avoidable choice I would be more likely to regret over a five-year horizon.

After the four lenses, construct the strongest fair argument against the option I appear to favour. Do not create a weak counterargument merely to dismiss it. Then recommend one option, explain the single most important reason and state what evidence would reverse the recommendation.

Separate known facts, user-provided estimates and your own assumptions. Do not manufacture precision. If the evidence cannot support a recommendation, say what must be learned first.

Apply the enhanced Aletheia integrity layer:

- Create a bounded decision record containing the decision date, question, objective, options, constraints, decision owner and review date.
- Type each material input as Evidence, Observation, Measurement, Estimate, Claim, Hypothesis, Assumption, Constraint or EvidenceGap and attach a source reference.
- Record source creator or speaker, role, knowledge basis, source date, retrieval date, locator, claim scope and limitations.
- Score each input's relevance to this decision from 0 to 10. Explain all scores of 7 or above. Relevance controls prominence only; it must not be presented as truth confidence.
- Search for material contradictions among the inputs and the options. Create a conflict entry containing every supported side. Do not resolve it without new evidence or an authorised decision.
- Report integrity, source identity, epistemic support, applicability and completeness separately, with reasons. Never average them.
- For the final recommendation, create an interpretation receipt stating the conclusion, evidence used, important assumptions, strongest alternative interpretation, applicability limits, known conflicts, evidence that could overturn it and the required human review.
- End with a compact provenance trace and preserve the recommendation as proposed advice, not as an authorised Decision unless the accountable human accepts it.

Activate when I ask for decision help, ask "should I", or present competing options. Keep the normal response within one page.
```

------------------------------------------------------------------------

## 5. Weekly Business Review

### Purpose

Assemble operational and commercial information into a short weekly management review.

### Inputs

- Pipeline or CRM information.
- Revenue, invoice and payment notes.
- Open tasks and overdue work.
- Content or other meaningful work completed during the week.

### Outputs

- Weekly wins.
- Stalled or slipping work.
- Financial snapshot.
- Pipeline summary and most important follow-up.
- Three impact-ranked priorities for the following week.
- One potentially uncomfortable pattern or avoidance signal.

### Reference files

``` text
/References/
  source-map.md
```

### Copy-paste build prompt

``` text
Build a reusable skill named "weekly-review".

Its job is to create a one-page weekly business review from my own operational records.

During setup, ask where the required information lives: CRM or pipeline, revenue and invoices, payments received, outstanding money, work completed, content published and open tasks. Record the approved locations or connections in /References/source-map.md. If a source cannot be connected, tell me exactly what to paste or upload for each review.

For every weekly run, use this structure:

1. Wins — specific outcomes achieved during the review period.
2. Stalled or slipping — items that missed a deadline or have shown no meaningful movement for at least two weeks.
3. Money — invoiced, received and outstanding amounts, with dates where available.
4. Pipeline — current leads and stages, plus the single follow-up most likely to matter.
5. Next week's three priorities — ranked by expected impact, with one sentence explaining each selection.

Finish with one candid pattern that the evidence suggests I may be overlooking or avoiding. Phrase it as an observation rather than a psychological diagnosis.

Use the dates and figures in the sources. Mark missing, stale or conflicting data instead of silently resolving it. Keep the result short enough to read and act on in roughly 15 minutes.

Apply the shared Aletheia integrity layer. Record the reporting period, creation and retrieval dates of each source, and a locator or system record ID where available. Score candidate items for current-review relevance from 0 to 10; omit 0-rated duplicates and corrected noise from the brief while retaining an audit reference when necessary. Preserve conflicting figures in a conflict entry and report separate confidence dimensions for the financial snapshot, pipeline state and completeness of the week's records.

Activate when I request my weekly review or Friday review. The skill may be scheduled where the platform supports automations, but it must not alter CRM records, tasks or financial data without approval.
```

------------------------------------------------------------------------

## 6. GEO and AEO Content Optimisation

### Purpose

Audit and restructure content so that AI answer engines can understand, extract and cite it more readily.

### Inputs

- A draft or completed article; or
- Text from a published web page.

### Outputs

- A scored audit identifying citation and extraction weaknesses.
- A restructured, more directly answerable version.
- A short FAQ addressing realistic user questions.

### Reference files

No reference files are required. The Humanizer skill can be used to retain the author's voice.

### Copy-paste build prompt

``` text
Build a reusable skill named "geo-optimizer".

Its job is to improve content for generative-engine optimisation and answer-engine optimisation while preserving accuracy, authorship and voice.

For every supplied draft or page, perform two passes.

Pass 1 — Audit. Assess and score:

- Whether the principal question receives a direct answer near the beginning.
- Whether important claims are precise, self-contained and supportable.
- Whether numbers, dates, methods and named entities are included where relevant.
- Whether the author's identity, experience or authority is stated clearly and honestly.
- Whether headings, definitions, paragraphs and lists are easy for both people and machines to parse.
- Whether important claims have appropriate primary or authoritative sources.

Show the material gaps, unsupported claims and ambiguous wording. Do not treat confident phrasing as evidence.

Pass 2 — Revision. Lead with a direct answer, improve heading structure, turn vague statements into precise statements only where the source material supports doing so, and make key passages understandable outside their surrounding paragraph. Add a concise FAQ based on questions a real user might ask an AI system about the subject.

Use the Humanizer skill to retain my style. Do not fabricate credentials, data or citations. Flag claims that require research rather than strengthening them cosmetically.

Apply the shared Aletheia integrity layer to the audit. For every material claim, retain its source, creator, source date, retrieval date, locator, support scope and limitations. Assign relevance 0–10 for the target user question, not for perceived truth. Detect contradictions between the page and cited sources or between cited sources themselves. Report epistemic support, applicability and completeness separately, and never convert search rank or semantic similarity into confidence.

Activate when I mention GEO, AEO, AI search, AI visibility or citable content. Return the audit before the revised version.
```

------------------------------------------------------------------------

## 7. Competitor-Monitoring Skill

### Purpose

Track meaningful competitor and market changes and convert them into sourced strategic intelligence.

### Inputs

- Competitor names and websites.
- Product and pricing pages.
- Newsletters, blogs and social accounts.
- Relevant recruitment, partnership and other public sources.

### Outputs

- An executive summary of material changes.
- Findings grouped by product, positioning, pricing, content, hiring and partnerships.
- Explanation of the likely business significance.
- Three practical response options.
- Links or citations supporting every finding.

### Reference files

``` text
/References/
  competitor-sources.md
/Aletheia/
  source-register.md
  claim-register.md
  conflict-register.md
  evidence-gaps.md
  provenance-trace.md
  interpretation-receipts.md
```

### Copy-paste build prompt

``` text
Build a reusable skill named "competitor-monitor".

Its job is to monitor selected competitors and produce a concise, evidence-linked intelligence brief containing only changes that could affect our decisions.

During setup, ask which organisations to track and collect their official websites, product pages, pricing pages, blogs, newsletters, social accounts, recruitment pages and other approved public sources. Store this watch list in /References/competitor-sources.md together with the date each source was added.

For each run, compare current information with the most recent reliable baseline. Look for material changes in:

1. Product or feature offering.
2. Messaging and positioning.
3. Pricing or commercial packaging.
4. Content and campaigns.
5. Recruitment signals.
6. Partnerships or alliances.

Exclude routine posts and inconsequential changes. For every retained finding, state what demonstrably changed, when it changed if known, the supporting source, why it may matter and what remains uncertain. Clearly label strategic implications as inference rather than fact.

Open with an executive summary naming the most significant movement and any issue needing prompt attention. End with three proportionate actions to consider, such as a content response, sales talking point, positioning review or product question.

Apply the enhanced Aletheia integrity layer:

- Give every material finding a stable ID and type it as Evidence, Observation, Measurement, Estimate, Claim, Hypothesis, Conflict or EvidenceGap.
- Record the source class, publisher or speaker, role, knowledge basis, publication or observation date, retrieval date, exact locator, claim scope and limitations.
- Distinguish `observed_at`, `source_created_at` and `retrieved_at`. Current-state claims must be checked again when the source is stale or the monitored page has changed.
- Score relevance from 0 to 10 against the current monitoring objective. Explain scores of 7 or above. Exclude relevance-0 duplicates and cosmetic changes from the active brief, while preserving any audit locator needed to show what was checked.
- Compare every retained finding with its baseline. If the baseline is missing, label the item provisional and create an EvidenceGap rather than claiming a change.
- Detect contradictions across official pages, archived versions, announcements and reliable third-party reporting. Create a conflict entry, preserve all material sides and state what would resolve it.
- Report integrity, source identity, epistemic support, applicability and completeness separately. Search ranking, prominence and repetition are not truth confidence.
- Create an interpretation receipt for each strategic implication or recommended response, showing the supporting nodes, assumptions, alternative interpretations, applicability, uncertainty and Steward-review point.
- Finish with a provenance trace listing sources searched, dates, exclusions, unavailable material, retrieved conflicts and human review points.

Activate when I request competitor monitoring or a weekly competitor brief. Never invent a comparison when no reliable baseline exists; instead establish the baseline for the next run.
```

------------------------------------------------------------------------

## 8. Weekly Executive Brief

### Purpose

Condense company activity into the developments, risks and decisions that leadership actually needs.

### Inputs

- Company and project updates.
- Metrics and dashboards.
- Meeting records.
- Strategic initiative documents.
- Targets, dependencies and current blockers.

### Outputs

- Executive summary.
- Key wins.
- Emerging or material risks.
- Blocked projects and dependencies.
- Decisions or escalations required.
- Recommended priorities.

### Reference files

``` text
/References/
  source-map.md
/Aletheia/
  source-register.md
  claim-register.md
  conflict-register.md
  evidence-gaps.md
  provenance-trace.md
  interpretation-receipts.md
```

### Copy-paste build prompt

``` text
Build a reusable skill named "executive-brief".

Its job is to turn company updates, metrics and project information into a short weekly briefing designed for leadership decisions.

During setup, ask where authorised company updates, project records, dashboards, metrics, meeting notes and strategic documents are stored. Record these locations in /References/source-map.md. If direct access is unavailable, request the relevant material by upload or pasted text.

For each run, identify the developments with the greatest business impact or urgency. Connect related information across teams where the evidence supports doing so. Do not reproduce every status update.

Use the following structure:

1. Executive summary — the week's most consequential changes.
2. Key wins — measurable progress or completed outcomes.
3. Risks — emerging threats, missed targets or deteriorating indicators.
4. Blocked work — projects, owners, dependencies and duration of blockage where known.
5. Decisions needed — the decision owner, deadline and consequence of delay.
6. Recommended priorities — the actions leadership should consider next.

Distinguish reported facts from analysis and recommendation. Preserve conflicting figures or accounts visibly, identify their sources and request resolution. Do not fill gaps with plausible-sounding status information.

Apply the enhanced Aletheia integrity layer:

- Assign a stable ID and epistemic type to every item capable of changing a leadership decision.
- For each source, retain its owner or author, role, knowledge basis, reporting period, source-created date, retrieval date, locator, support scope, limitations and privacy class.
- Score current-brief relevance from 0 to 10. Explain scores of 7 or above. Mandatory constraints, major conflicts and decision deadlines must be surfaced even if they would otherwise rank lower.
- Detect conflicting metrics, status reports, owners, deadlines and causal explanations. Create one conflict record linking all material sides; state whether it is unresolved, partially resolved or resolved and what evidence or authorised decision is needed.
- Use separate confidence dimensions for integrity, source identity, epistemic support, applicability and completeness. A complete dashboard is not necessarily strong epistemic support, and an authoritative speaker may still be outside the relevant claim scope.
- Date every current-state conclusion and flag expired, stale or future-effective information. Record a review date for volatile claims.
- Give every recommendation an interpretation receipt containing supporting evidence, assumptions, alternative interpretations, known conflicts, applicability limits and the accountable human review point.
- End with a provenance trace covering retrieved sources and conflicts, excluded low-relevance material, evidence gaps, proposed actions and decisions requiring Steward authority.

Activate when I ask for an executive, leadership or company update brief. Keep the result concise, direct and ready to share, but do not distribute it automatically.
```

------------------------------------------------------------------------

## 9. Meeting-Preparation Skill

### Purpose

Combine scattered meeting context into a focused briefing readable in less than five minutes.

### Inputs

- Calendar event and attendee information.
- Previous meeting notes and call summaries.
- Relevant email threads and CRM records.
- Proposals, account notes and unresolved commitments.
- Current, reputable company research.

### Outputs

- Meeting snapshot.
- Relevant history.
- Company or organisational context.
- Likely attendee priorities.
- Talking points and strategic questions.
- Possible objections, risks and sensitivities.

### Reference files

``` text
/References/
  source-map.md
/Aletheia/
  source-register.md
  claim-register.md
  conflict-register.md
  evidence-gaps.md
  provenance-trace.md
  interpretation-receipts.md
```

### Copy-paste build prompt

``` text
Build a reusable skill named "meeting-prep".

Its job is to prepare a concise one-page briefing for an important meeting by gathering the relevant history, current context and unresolved issues.

During setup, ask where approved calendar information, meeting notes, CRM records, call summaries, email threads, proposals, account notes and company research can be found. Record these locations and any access limitations in /References/source-map.md. When sources cannot be accessed, ask me to paste or upload the relevant material.

For a requested meeting, determine the attendees, roles, organisation, meeting purpose and time. Review previous interactions, promises, open opportunities, proposals, blockers and overdue follow-ups. Summarise current company context using timely, reputable sources when external research is permitted.

Produce:

1. Meeting snapshot.
2. Relevant relationship and decision history.
3. Company context and recent developments.
4. Likely priorities of the participants.
5. Recommended talking points.
6. Strategic questions worth asking.
7. Potential objections, risks or sensitivities.

Separate sourced information from reasonable inference. Provide source links and dates for current external claims. Verify ambiguous attendee identities rather than assuming that similar names refer to the same person.

Apply the enhanced Aletheia integrity layer:

- Create a meeting-specific evidence set with stable IDs for attendees, commitments, open questions, proposals, constraints and current company claims.
- Retain each source's author or speaker, role, knowledge basis, source-created date, observed date where relevant, retrieval date, exact locator, claim scope, limitations and privacy class.
- Score information for meeting relevance from 0 to 10. Explain scores of 7 or above. Relevance 0 material such as corrected spelling or exact duplication should not clutter the brief unless it creates a genuine identity issue or audit need.
- Detect contradictions in attendee identity, dates, promises, prices, responsibilities, prior accounts and current external information. Preserve all material sides in a conflict record and do not select a convenient version without support.
- Keep confidence dimensions separate for source integrity, identity, epistemic support, current applicability and completeness. Unknown identity or missing history must remain explicit.
- Give inferred priorities, objections, sensitivities and recommended angles an interpretation receipt: evidence used, inference made, alternative explanation, applicability, uncertainty and potential consequence if wrong.
- Date current company information and flag items requiring rechecking immediately before the meeting.
- End with a short provenance trace and a human-review checklist, particularly for identity, confidentiality, disputed commitments and consequential claims.

Activate when I request meeting preparation, a call brief or help with a calendar event. Keep the briefing readable in under five minutes and do not contact attendees or change the calendar.
```

------------------------------------------------------------------------

## 10. Sales Call Follow-Up Skill

### Purpose

Convert a sales or discovery call into the communications and records needed to advance the opportunity.

### Inputs

- A sales-call transcript or reliable notes.
- Examples of previous follow-up emails.
- Examples of CRM notes and proposal summaries.
- The user's sales communication style.

### Outputs

- Customer-facing follow-up email.
- Structured CRM note.
- Next-step checklist divided by owner.
- Proposal recommendations when buying intent and fit are sufficient.

### Reference files

``` text
/References/
  style-examples.md
```

### Copy-paste build prompt

``` text
Build a reusable skill named "sales-followup".

Its job is to turn a completed sales conversation into a reviewable customer email, an accurate CRM note and a clear next-action plan.

During setup, request representative follow-up emails, CRM records, proposal summaries and other examples of my sales communication. Store or reference them in /References/style-examples.md. Use the Humanizer skill for customer-facing prose when available.

For every call transcript, extract the customer's stated goals, business context, problems, priorities, objections, decision criteria, timing, budget signals, stakeholders, commitments and buying signals. Separate explicit statements from your inference. Identify unresolved questions and potentially important needs, but do not exaggerate intent or invent an opportunity.

Produce four sections:

1. Customer email — brief, specific, non-pushy, confirming the discussion and agreed next step.
2. CRM note — factual and scannable, covering goals, objections, stakeholders, signals, risks and next actions.
3. Action checklist — tasks assigned separately to me and the customer, including dates and dependencies where stated.
4. Proposal guidance — only when the evidence indicates sufficient need, fit and intent; otherwise state what qualification is missing.

Never send the email or update the CRM. Present all drafts for approval. Flag low-quality transcription, uncertain names and contradictory commitments.

Apply the shared Aletheia integrity layer. Anchor material findings to transcript timestamps or note locations and retain the call date, participant identity status and retrieval date. Give proposed actions a relevance score from 0 to 10 based on their connection to the customer's stated goals and agreed next steps. Create a conflict entry for incompatible commitments, prices, deadlines or stakeholder accounts. Label buying intent, implied needs and proposal fit as interpretation unless explicitly stated, with separate confidence reasons and an interpretation receipt for consequential inferences.

Activate when I provide a sales call and ask for follow-up, CRM notes or recommended next steps.
```

------------------------------------------------------------------------

## 11. Customer Feedback Synthesis Skill

### Purpose

Identify repeated customer patterns across multiple feedback channels and translate them into practical business actions.

### Inputs

- Customer interviews.
- Support tickets and community comments.
- Product or service reviews.
- Surveys and NPS responses.
- Sales and onboarding notes.
- Churn or cancellation reasons.

### Outputs

- Executive summary.
- Repeated pain points and friction.
- Recurring feature or service requests.
- Positive sentiment drivers.
- Representative customer language and quotations.
- Recommended product, marketing, support or leadership actions.

### Reference files

``` text
/References/
  source-locations.md
/Aletheia/
  source-register.md
  claim-register.md
  conflict-register.md
  evidence-gaps.md
  provenance-trace.md
  interpretation-receipts.md
```

### Copy-paste build prompt

``` text
Build a reusable skill named "feedback-synthesizer".

Its job is to find meaningful, repeated patterns across customer feedback and turn them into evidence-based actions for product, marketing, sales, support and leadership.

During setup, ask where authorised interviews, support tickets, reviews, surveys, NPS responses, sales notes, churn records, onboarding feedback and community comments are stored. Record the approved sources in /References/source-locations.md. If sources are inaccessible, ask me to paste or upload the feedback.

For each analysis, group the material into recurring themes. Give more weight to patterns observed across independent customers than to an isolated or unusually forceful comment. Evaluate frequency, intensity and likely business impact where the data allows.

Identify:

- Repeated pain points and unmet expectations.
- Common feature or service requests.
- Recurring objections and adoption barriers.
- Positive experiences and retention drivers.
- Words and phrases customers repeatedly use to describe problems and desired outcomes.

Use this report structure:

1. Executive summary.
2. Top pain points.
3. Top requests.
4. Positive sentiment drivers.
5. Customer language and representative quotations.
6. Recommended actions tied to the observed patterns.

Keep direct customer statements distinct from inference. Include counts or proportions when the dataset supports them, state the dataset and time period, and do not present a small or biased sample as representative. Use quotations only when authorised and anonymise personal or sensitive details.

Apply the enhanced Aletheia integrity layer:

- Give every source item and material theme a stable ID. Type inputs and conclusions as Evidence, Observation, Measurement, Estimate, Claim, Hypothesis, Conflict or EvidenceGap as appropriate.
- Record channel, creator or speaker role, knowledge basis, source-created date, event or observation date where available, retrieval date, locator, claim scope, limitations, consent or quotation restrictions and privacy class.
- Score each theme's relevance from 0 to 10 against the stated product or business question. Explain scores of 7 or above. Keep frequency, severity, strategic relevance and truth confidence as separate concepts.
- Detect contradictions across segments, time periods and channels. Do not average them away. Create a conflict entry that shows each material side and whether the difference may arise from customer type, product version, geography, time or methodology.
- Report integrity, source identity, epistemic support, applicability and completeness separately. State sampling and coverage gaps explicitly and leave unknown values unknown.
- Date every theme and test whether older feedback has been superseded by a product, policy or service change. Archive superseded findings rather than treating them as current, while preserving the evidence trail.
- Create an interpretation receipt for every consequential theme or recommended action, naming the supporting items, inclusion and exclusion criteria, alternative interpretations, applicability, conflicts and evidence that would change the conclusion.
- Finish with a provenance trace summarising sources included, date range, excluded or redacted material, high-relevance themes, conflicts, evidence gaps and required human review.

Activate when I ask to synthesise feedback, locate customer patterns or analyse reviews, surveys, interviews or tickets.
```

------------------------------------------------------------------------

## Reference-file summary

| Skill                       | Workflow-specific material                                           | Aletheia layer |
|-----------------------------|----------------------------------------------------------------------|----------------|
| Humanizer                   | `/References/writing-samples.md`                                     | Standard       |
| Inbox Triage                | None required                                                        | Standard       |
| Content Repurposing         | `/References/format-patterns.md`; `/References/platform-examples.md` | Standard       |
| Decision-Making             | None required                                                        | **Enhanced**   |
| Weekly Business Review      | `/References/source-map.md`                                          | Standard       |
| GEO/AEO Optimisation        | None required                                                        | Standard       |
| Competitor Monitoring       | `/References/competitor-sources.md`                                  | **Enhanced**   |
| Weekly Executive Brief      | `/References/source-map.md`                                          | **Enhanced**   |
| Meeting Preparation         | `/References/source-map.md`                                          | **Enhanced**   |
| Sales Call Follow-Up        | `/References/style-examples.md`                                      | Standard       |
| Customer Feedback Synthesis | `/References/source-locations.md`                                    | **Enhanced**   |

All skills may use the shared `/Aletheia/` reference set. The enhanced skills should use the complete set because they generate consequential interpretations or recommendations.

## Practical implementation note

Skills that read email, calendars, CRM systems, websites or company records need suitable connections and permissions. A skill prompt defines how the AI should work; it does not itself provide access to those systems. Start with skills that require no external connection—Humanizer, Decision-Making and GEO/AEO Optimisation—then add connected workflows after checking their data access and approval boundaries.
