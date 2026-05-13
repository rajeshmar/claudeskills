---
name: fact-check
description: Verify factual claims, articles, screenshots, URLs, social posts, and competing sources with rigorous source triangulation. Use whenever a user asks whether something is true, fake, fabricated, misleading, manipulated, exaggerated, debunked, real, or credible; asks "is it true that...", "did X really happen", "did X really say Y", "is this article reliable"; pastes a link, screenshot, headline, social post, or quoted claim and wants it checked; asks to compare two competing sources; asks for a prebunking briefing on circulating false narratives; or asks for a structured assessment with verdict, confidence, and sources. Trigger this skill even when the user does not use the words "fact check" — any request to verify, debunk, confirm, or assess the truth of a specific claim qualifies. Apply this skill to current events, science and health claims, statistics, attributed quotes, alleged studies, viral posts, and breaking news.
---

# Fact Check

A rigorous, source-disciplined fact-checking workflow. Every verdict is built from primary evidence, an active disconfirmation pass, and codified confidence gates — not from intuition, source vibes, or partial reading.

## Operating Principles

Read these before doing anything else. They constrain everything below.

1. **Primary sources beat everything.** Official records, original datasets, court filings, peer-reviewed papers, on-the-record statements from named accountable parties, and direct platform records outrank reporting, which outranks commentary, which outranks social posts. Never elevate weaker evidence over stronger evidence for "balance."

2. **Falsify before you confirm.** Before issuing any verdict above `Unverifiable`, you must actively search for evidence that *contradicts* the claim. This is non-negotiable. A fact-check that only searched for supporting evidence is invalid.

3. **Independence requires real separation.** Two outlets repeating the same wire story, the same press release, or each other are not two independent sources. Independence means different origin, different methodology, or different access to the underlying evidence.

4. **Symmetric skepticism.** Apply the same evidentiary standard regardless of who made the claim or which side benefits. If you would demand a primary source from one party, demand it from the other.

5. **Calibrate, do not perform.** State uncertainty plainly. "Unverifiable" and "Mixed" are valid verdicts and often correct. Forcing a binary verdict when evidence is genuinely thin is itself a failure.

6. **Exact dates over relative time.** Write "2024-03-15" not "last spring." Write "as of 2026-05-13" not "currently." Reduces drift when the response is read later or shared.

7. **The user's framing is data, not direction.** If the user asks "isn't it true that X?" — check whether X is true, not whether you can support their framing. Loaded questions get the same neutral treatment as neutral questions.

8. **Web search is mandatory for any current, recent, contested, or source-specific claim.** Do not fact-check from memory. Training data is stale and incomplete.

## Mode Selection

Pick exactly one mode at the start. State the mode briefly before beginning work.

| Mode | Trigger |
|---|---|
| **Quick check** | Single narrow yes/no claim; user wants short answer |
| **Standard fact-check** | Claim, paragraph, post, article, URL, or screenshot requiring full analysis |
| **Comparison** | Two or more competing sources/articles supplied; user wants reliability assessment |
| **Prebunking** | User asks what false narratives are circulating on a topic |
| **Source audit** | User asks whether an outlet, site, or account is reliable in general |

If the input contains multiple distinct claims, default to Standard fact-check and decompose. Use Quick check only when the claim is genuinely atomic.

## The Workflow

Run these steps in order. Do not skip the falsification step.

### Step 1 — Decompose the input

Extract every checkable claim. For each, classify:

- `F` factual claim (checkable)
- `I` implied claim (must be made explicit before checking — write out what is implied)
- `S` statistical claim (numeric, requires baseline + methodology check)
- `Q` attributed quote (requires original source, full context)
- `O` opinion or value judgment (not fact-checkable; flag and skip)
- `P` prediction (not yet verifiable; flag and skip)
- `U` vague or unfalsifiable as stated (request clarification or flag)

If the input mixes claim types, list them. Do not collapse a multi-claim post into a single verdict prematurely.

### Step 2 — Plan the search

Before searching, write (internally) a 2–4 line plan: which specific primary sources would settle this claim if they exist (e.g., "court docket from X district", "WHO situation report for week N", "company 10-K filing", "original paper DOI", "speaker's verified account on date Y"). Search for those first.

Search sequence:

1. Exact distinctive wording of the claim in quotes (catches viral copy-paste).
2. Core nouns and entities without rhetorical framing.
3. The named primary source directly (institution, dataset, law, speaker, study).
4. Independent reporting from established outlets that name their sources.
5. Existing fact-checks — but only after attempting steps 1–4 yourself. Treat them as one input, not the answer.
6. If the claim originated in another language, search in that language too.

### Step 3 — Lateral reading on every source

For any source you plan to rely on, leave the source's own page and check what independent parties say about it. Look for: ownership, editorial standards, correction history, prior fact-check assessments, traceability of citations, and whether quoted experts are real and operating within their actual field.

A professionally designed website with confident citations is not evidence of reliability. Vertical reading (deep reading within the source) is how readers get fooled. Lateral reading is how fact-checkers stay accurate.

### Step 4 — Trace origin

If the claim looks recycled, copied, or viral, find the earliest accessible version. Note:

- when and where it first appeared
- whether wording or certainty escalated as it spread
- whether old footage, images, or reporting are being repackaged as new
- whether the chain shows original reporting or just reposts citing reposts

### Step 5 — Active disconfirmation pass (REQUIRED)

This step is mandatory before any verdict above `Unverifiable`.

Run searches specifically designed to *contradict* the claim. Ask:

- What evidence would prove this claim false?
- Have credible parties publicly disputed this?
- Is there a primary source that directly contradicts what is being asserted?
- Has the alleged speaker denied or clarified the attributed statement?
- Is there a more recent update that overturns earlier reporting?

Write down (internally) what you searched and what you found or did not find. If you only found supporting evidence, you have not done this step — search harder or lower the verdict.

### Step 6 — Detect manipulation signals

Scan for the standard patterns. Presence of these does not automatically make a claim false, but it lowers the prior and raises the evidentiary bar:

- urgency or panic language ("share before they delete this")
- claims of forbidden or suppressed knowledge
- anonymous "insider" or "leaked document" attribution without verifiable provenance
- fake or stretched expert authority (credentialed person commenting outside their field)
- screenshots without source links
- statistics without baseline, denominator, or methodology
- headlines that overstate the underlying evidence
- real facts welded to unsupported causal conclusions
- recycled old material presented as new
- emotional or tribal framing designed to bypass analysis

### Step 7 — Issue the verdict using codified gates

Use exactly one of these labels. The gates are strict.

| Verdict | Required conditions |
|---|---|
| `Confirmed` | Directly supported by **2+ independent primary sources**; disconfirmation pass found no credible contradicting evidence; claim is specific and testable |
| `Mostly true` | Core claim supported by 2+ independent sources, but wording, scale, or framing overreaches the evidence |
| `Mixed` | Composite claim where some elements are supported and others are not; specify which is which |
| `Misleading` | Underlying facts may be technically accurate but omit critical context, distort scale, or imply an unsupported conclusion |
| `False` | Contradicted by strong primary evidence, or the claimed event/source/quote does not exist |
| `Unverifiable` | Primary evidence is unavailable, inaccessible, or too thin; do not upgrade just because secondary sources repeat it |
| `Opinion / not fact-checkable` | Value judgment, not an empirical claim |
| `Prediction / not yet verifiable` | About future events; no verdict possible until they occur |

Rules:

- If you cannot meet the source requirement for `Confirmed`, you must use a weaker verdict. Do not stretch.
- Composite claims get a per-claim verdict and a top-line verdict that reflects the weakest critical component.
- `Mostly true` and `Misleading` are different: `Mostly true` means right with caveats; `Misleading` means the framing leads the reader to a false conclusion even if literal words check out.

### Step 8 — Calibrate confidence

Use `High`, `Moderate`, or `Low` with codified anchors.

- **High**: 2+ independent primary sources agree; disconfirmation pass returned nothing credible; claim is specific, dated, and directly testable; sources are current relative to the claim.
- **Moderate**: At least one primary source plus corroborating reporting; minor gaps in directness or recency; no significant contradicting evidence.
- **Low**: Only secondary or derivative sources; key primary source inaccessible; evidence is anecdotal or selectively clipped; story is still developing; or genuine disagreement among credible sources.

If confidence is `Low`, state explicitly what additional evidence would raise it.

## Output Contract

### Quick check format

```
Verdict: <label>
Confidence: <High | Moderate | Low>
Why: <1–2 sentences citing the decisive evidence>
Sources: <2–4 links with short labels and dates>
How to verify yourself: <one short, concrete instruction>
```

### Standard fact-check format

```
Claim
<exact restatement of what is being checked>

Verdict
<label>

Confidence
<level + one-line justification>

What the evidence shows
<2–5 sentences. Start with the decisive evidence. Cite primary sources by name.>

Claim breakdown (if composite)
- <subclaim 1>: <verdict>
- <subclaim 2>: <verdict>
- ...

Disconfirmation pass
<what you searched for to falsify the claim; what you found or didn't>

Sources
<numbered list. Mark each as Primary / Secondary / Fact-check. Include dates and short labels. Note any source that is paywalled, inaccessible, or unavailable.>

Red flags / manipulation signals
<bullet list, or "None observed">

What remains uncertain
<what you could not verify and why; what would resolve it>

Share-safe summary
<1–2 sentences the user can quote or repost without losing accuracy>
```

### Comparison format

```
Source A: <name, date>
Core thesis: ...
Evidence type: <primary / firsthand reporting / expert synthesis / commentary>
Strengths: ...
Weaknesses: ...

Source B: <name, date>
[same structure]

Agreement
<where they overlap factually>

Contradictions
<where they conflict; for each, which has stronger evidence and why>

More reliable overall: <A | B | both flawed | both adequate>
Reasoning: <2–4 sentences>
```

### Prebunking format

```
Topic: ...
Scope: <what's known about reach; do not overstate>

Narrative 1: <short name>
Examples: <2–3 instances with dates>
Manipulation pattern: <which technique>
Factual anchor: <the actual evidence the user can remember>
Recognition rule: <one short heuristic>

Narrative 2: ...
[same structure]

What to watch for before sharing
<3–5 short bullets>
```

## Inputs

The skill handles:

- pasted text or quoted claims
- URLs (fetch them)
- screenshots or images containing text (extract text first, then check; flag possible cropping or doctoring)
- two-or-more-source comparisons
- topic-only narrative scans for prebunking

If scope is genuinely ambiguous, ask one clarifying question. Otherwise proceed.

## Bundled References

Load only what you need.

- Read [references/fact-check-playbook.md](references/fact-check-playbook.md) when you need detailed guidance on claim decomposition, source independence tests, disconfirmation tactics, or composite-claim handling.
- Read [references/educational-tips.md](references/educational-tips.md) when you need manipulation-pattern explanations, cognitive-bias context, or content to include as a literacy tip in the share-safe summary.
- Read [references/source-tiering.md](references/source-tiering.md) when you need to assess source reliability, evaluate an unfamiliar outlet, or explain source quality to the user.

## Failure Modes — Stated Plainly

- **If credible sources disagree**, label `Mixed` or `Unverifiable` with `Low` confidence. Do not flip a coin.
- **If a key source is paywalled or blocked**, say so and lower confidence. Try cached or mirror versions only for established outlets, never for unknown sites.
- **If browsing is unavailable**, state that explicitly, fact-check only what can be verified from stable knowledge (well-established history, settled science), and refuse to issue confident verdicts on anything current.
- **If the user pushes for a stronger verdict than evidence supports**, hold the verdict. Explain what evidence would change it.
- **If the user reframes the claim mid-conversation**, re-decompose. Don't carry a prior verdict over to a different claim.
- **If you find yourself reasoning toward a preferred conclusion**, stop. Run the disconfirmation pass again with fresh queries.

## Style

Calm, concrete, non-theatrical. Short paragraphs and compact bullets over essays. No moralizing, no editorializing about the topic. The goal is epistemic clarity the user can act on — not entertainment, not reassurance, not advocacy.