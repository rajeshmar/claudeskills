# 🕵️‍♂️ Fact Check Skill

> A rigorous, source-disciplined fact-checking workflow for verifying claims, articles, screenshots, URLs, social posts, statistics, quotes, and competing sources.

Welcome to **Fact Check** — a structured verification skill designed to help ChatGPT assess whether a claim is **true, false, misleading, mixed, unverifiable, or not fact-checkable**.  
It is built for careful source triangulation, primary evidence, active disconfirmation, and clear verdicts users can trust. ✅

---

## ✨ What This Skill Does

The **Fact Check Skill** helps verify:

- 📰 Articles, headlines, and news claims
- 📱 Viral social media posts
- 🖼️ Screenshots or image-based claims
- 🔗 URLs and source reliability
- 💬 Attributed quotes
- 📊 Statistics and numeric claims
- 🧪 Science, health, and research claims
- ⚖️ Political, legal, or public-interest claims
- 🆚 Competing sources or conflicting reports
- 🚨 Emerging false narratives and misinformation patterns

It is especially useful when a user asks:

> “Is this true?”  
> “Did this really happen?”  
> “Is this fake or misleading?”  
> “Did this person actually say that?”  
> “Can you compare these two sources?”  
> “Is this article reliable?”  

---

## 🎯 Core Philosophy

This skill is not built for quick guesses. It is built for **evidence discipline**.

The workflow follows four major principles:

1. **Primary sources first** 🏛️  
   Official records, original datasets, court filings, peer-reviewed papers, direct platform records, and named accountable sources outrank commentary or reposts.

2. **Falsify before confirming** 🔍  
   The skill actively searches for evidence that could disprove the claim before issuing a strong verdict.

3. **Source independence matters** 🧩  
   Multiple outlets repeating the same wire story or press release do not count as independent confirmation.

4. **Uncertainty is allowed** ⚖️  
   If evidence is thin, the skill uses verdicts like `Unverifiable`, `Mixed`, or `Low confidence` instead of forcing a false sense of certainty.

---

## 🧠 Verification Modes

The skill automatically selects one of five operating modes:

| Mode | Best For |
|---|---|
| ⚡ **Quick Check** | One narrow yes/no claim |
| 🧾 **Standard Fact-Check** | Full claim, post, URL, article, or screenshot |
| 🆚 **Comparison** | Two or more competing sources |
| 🛡️ **Prebunking** | Identifying false narratives before they spread |
| 🏛️ **Source Audit** | Assessing whether an outlet, account, or website is reliable |

---

## 🔄 Fact-Checking Workflow

The skill follows a structured verification pipeline:

### 1. Decompose the Claim 🧩

The input is broken into checkable parts:

- `F` — factual claim
- `I` — implied claim
- `S` — statistical claim
- `Q` — attributed quote
- `O` — opinion or value judgment
- `P` — prediction
- `U` — vague or unfalsifiable claim

This prevents one broad post from being judged too quickly.

---

### 2. Plan the Search 🗺️

Before searching, the skill identifies which sources would best settle the claim, such as:

- Official records
- Court dockets
- Government datasets
- Company filings
- Original research papers
- Verified statements
- Platform records
- Independent reporting

---

### 3. Read Laterally 🌐

The skill does not blindly trust a source because it looks professional.

It checks:

- Ownership
- Editorial standards
- Correction history
- Source traceability
- Expert credibility
- Whether other reliable parties support or dispute the claim

---

### 4. Trace the Origin 🧭

For viral or recycled claims, the skill looks for:

- Earliest accessible version
- Reposted or altered wording
- Old media presented as new
- Escalation in certainty
- Missing context

---

### 5. Run a Disconfirmation Pass 🚫

Before giving a strong verdict, the skill searches for evidence that could contradict the claim.

This is one of the most important safeguards in the workflow.

---

### 6. Detect Manipulation Signals ⚠️

The skill watches for common misinformation patterns:

- “Share before they delete this”
- Anonymous insider claims
- Screenshots without links
- Statistics without denominators
- Fake or stretched expert authority
- Emotional or tribal framing
- Old footage reused as new
- Real facts combined with unsupported conclusions

---

## ✅ Verdict System

The skill uses strict verdict labels:

| Verdict | Meaning |
|---|---|
| ✅ **Confirmed** | Strong primary evidence from independent sources supports the claim |
| 🟢 **Mostly True** | Core claim is supported, but wording or framing needs caveats |
| 🟡 **Mixed** | Some parts are true, others are unsupported or false |
| 🟠 **Misleading** | Literal facts may be correct, but the framing distorts the conclusion |
| ❌ **False** | Strong evidence contradicts the claim |
| ⚪ **Unverifiable** | Evidence is too thin or unavailable |
| 💭 **Opinion / Not Fact-Checkable** | Value judgment, not an empirical claim |
| 🔮 **Prediction / Not Yet Verifiable** | Future claim that cannot be checked yet |

---

## 📊 Confidence Levels

Each verdict includes a confidence rating:

| Confidence | When It Applies |
|---|---|
| 🟢 **High** | Multiple strong primary sources agree and no credible contradiction appears |
| 🟡 **Moderate** | At least one primary source plus reliable corroboration |
| 🔴 **Low** | Evidence is limited, derivative, inaccessible, anecdotal, or still developing |

---

## 🧾 Output Formats

The skill supports several structured response formats.

### ⚡ Quick Check

```text
Verdict: <label>
Confidence: <High | Moderate | Low>
Why: <1–2 sentence explanation>
Sources: <2–4 links with labels and dates>
How to verify yourself: <one concrete step>
```

### 🧾 Standard Fact-Check

```text
Claim
<exact claim being checked>

Verdict
<label>

Confidence
<level and short justification>

What the evidence shows
<decisive evidence with citations>

Claim breakdown
- <subclaim>: <verdict>

Disconfirmation pass
<how the claim was tested against contradictory evidence>

Sources
<numbered source list>

Red flags / manipulation signals
<observed signals or none>

What remains uncertain
<remaining gaps>

Share-safe summary
<short accurate summary>
```

### 🆚 Source Comparison

```text
Source A: <name and date>
Core thesis: ...
Evidence type: ...
Strengths: ...
Weaknesses: ...

Source B: <name and date>
Core thesis: ...
Evidence type: ...
Strengths: ...
Weaknesses: ...

Agreement
...

Contradictions
...

More reliable overall:
...
```

### 🛡️ Prebunking Brief

```text
Topic: ...
Scope: ...

Narrative 1:
Examples:
Manipulation pattern:
Factual anchor:
Recognition rule:

What to watch for before sharing:
...
```

---

## 🛠️ Ideal Use Cases

Use this skill when you want ChatGPT to:

- Verify whether a claim is real or fake
- Check if a quote was actually said
- Evaluate whether a screenshot is misleading
- Compare two conflicting articles
- Assess whether a source is credible
- Identify misinformation tactics
- Produce a clear, share-safe summary
- Explain what evidence would change the verdict

---

## 🚀 Example Prompts

Try prompts like:

```text
Is it true that this quote was said by <person>?
```

```text
Fact-check this article and tell me whether it is misleading.
```

```text
Compare these two sources and tell me which one is more reliable.
```

```text
Is this screenshot real, edited, or missing context?
```

```text
Give me a prebunking brief on false narratives about this topic.
```

---

## 📁 Suggested Repository Structure

```text
fact-check-skill/
├── SKILL.md
├── README.md
├── references/
│   ├── fact-check-playbook.md
│   ├── educational-tips.md
│   └── source-tiering.md
└── assets/
    └── examples/
```

---

## 🧪 Quality Standards

This skill is designed to be:

- 🔍 Evidence-first
- 🧠 Skeptical but fair
- ⚖️ Politically neutral
- 🧾 Citation-oriented
- 🧩 Structured and reproducible
- 🚫 Resistant to viral misinformation
- ✅ Clear enough for users to verify independently

---

## ⚠️ Important Notes

This skill does **not** treat popularity as proof.

A claim does not become true just because:

- Many accounts reposted it
- Several outlets copied the same wire story
- A screenshot looks professional
- A website cites itself confidently
- A claim emotionally “feels right”

Evidence quality matters more than volume. 💡

---

## 🤝 Contributing

Contributions are welcome! 😊

Useful improvements may include:

- Better source-tiering rules
- New examples of misinformation patterns
- Additional output templates
- Improved source-audit criteria
- More robust claim-decomposition examples
- Domain-specific fact-checking guidance for science, health, finance, law, or politics

---

## 📌 Roadmap Ideas

- [ ] Add more real-world sample fact-checks
- [ ] Add source reliability scoring examples
- [ ] Add misinformation pattern library
- [ ] Add screenshot verification checklist
- [ ] Add quote verification workflow
- [ ] Add statistical claim validation checklist

---

## 📄 License

Add your preferred license here.

Example:

```text
MIT License
```

---

## ⭐ Final Note

In a world full of fast claims, this skill is built for slower, sharper thinking.  
Verify carefully, cite clearly, and stay honest about uncertainty. 🕵️‍♀️✨

