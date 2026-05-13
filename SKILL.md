---
name: token-optimizer
description: Produce the densest useful answer within a stated token, word, or character budget, then report estimated reduction vs. an unconstrained baseline. Use whenever the user gives an explicit budget ("in 200 tokens", "under 100 words", "1-line answer"), uses density signals ("compact", "dense", "tight", "terse", "token-optimized", "minimize tokens", "budget-aware"), is paying for tokens (API work, long agent loops, batch jobs), or asks Claude to be brief without sacrificing substance. Apply this skill across code answers, explanations, analyses, summaries, and decisions — anywhere output length matters. Do not skip this skill just because the request looks simple; "be concise" alone produces hedged, half-compressed answers, while this skill enforces an allocation method.
---

# Token Optimizer

A workflow for producing maximum-density answers within an explicit budget — and reporting the resulting saving.

## Core principle

Most output waste is not in the content. It's in the **scaffolding around** the content: restating the question, transition phrases, hedges, closing summaries, polite filler, throat-clearing bullets. A token-optimized answer removes the scaffolding and spends the budget on the substance.

Density ≠ shortness. A 100-token answer that omits the key trade-off is worse than a 300-token answer that names it. The goal is **highest information-per-token within the budget**, not the smallest number.

## When to apply this skill

Apply when any of the following are true:
- User states an explicit budget (tokens, words, characters, lines, sentences, bullets)
- User uses density signals: "compact", "tight", "dense", "terse", "minimal", "token-optimized", "budget-aware", "max compression"
- User indicates cost sensitivity: API work, batch processing, agent loops, "we're paying per token"
- User asks for "TL;DR", "one-liner", "bottom line only", "executive summary under X"
- The task is downstream of another tool/agent that must consume the output (where verbose responses cause cascading cost)

Do NOT apply when:
- User asks for a tutorial, walkthrough, or learning material — these need expansion, not compression
- User asks for creative writing where voice and rhythm matter
- The task is exploratory dialogue — "help me think through X" — where compression kills the back-and-forth

## The workflow

Execute these steps in order. Do not skip the self-check.

### Step 1 — Classify the task

Identify which of these the answer is:

| Task type        | Density ceiling                    | Notes                                              |
|------------------|------------------------------------|----------------------------------------------------|
| Code answer      | Code + 1–2 lines context           | The code IS the answer. No "Here's the code:"      |
| Direct fact      | 1 sentence                         | "X is Y because Z." Nothing more.                  |
| Explanation      | 200–400 tokens                     | Concept + intuition + one example.                 |
| Analysis         | 400–800 tokens                     | Claim + evidence + trade-off + recommendation.     |
| Summary          | 10–25% of source length            | Below 10% loses key facts; above 25% is rephrasing.|
| Decision support | 150–300 tokens                     | Options table or two-line verdict.                 |

If unsure, classify by **what the reader will do next**. If they'll act on it, optimize for actionability. If they'll forward it, optimize for self-containment.

### Step 2 — Set the budget

Use the user's explicit budget if given. Otherwise apply defaults:

- **Tight**: ≤150 tokens (~110 words, ~600 chars). For: facts, one-liners, code-only answers.
- **Standard**: ≤400 tokens (~300 words, ~1600 chars). For: explanations, single-topic analyses.
- **Extended**: ≤1000 tokens (~750 words, ~4000 chars). For: multi-part analyses, comparisons, decision docs.

Above 1000 tokens, the request isn't really token-optimized — it's a normal long-form answer. State this and proceed without artificial constraint.

**Token estimation rule of thumb**: 1 token ≈ 4 characters ≈ 0.75 words for English. Code averages ~3.5 chars/token (denser symbols). Use char-count for fastest estimation.

### Step 3 — Quality floor check

Before drafting, sanity-check: can the task actually be answered usefully within the budget?

If no — for example, the user asks for a full architectural review in 50 tokens — **do not silently truncate**. Respond:

> "Useful minimum for this task is ~X tokens. Your budget of Y is below that. Options: (a) raise to X, (b) narrow the scope to [specific sub-question], (c) accept a stub answer with caveats."

Better to flag than to mislead.

### Step 4 — Allocate the budget

Break the budget across content sections **by information value, not by equal split**. Information value = how much the reader's next action changes if this section is removed.

For an analysis with budget 400 tokens, a typical allocation looks like:
- Verdict / direct answer: 80 tokens (20%)
- Key reasoning: 200 tokens (50%)
- Trade-off or caveat: 80 tokens (20%)
- Next step: 40 tokens (10%)

Notice what's missing: introduction, conclusion, restating the question, "I hope this helps." That's all scaffolding — zero info value.

### Step 5 — Draft with density rules

Apply these to every sentence as you write:

**Cut on sight:**
- "Great question" / "Certainly!" / "I'd be happy to" — all preamble
- Restating the user's question back at them
- "In summary" / "To conclude" / "I hope this helps"
- Hedges with no probability content: "It's worth noting that", "It's important to remember", "Generally speaking"
- Bullet headers that repeat the bullet content
- Closing paragraphs that summarize what was just said

**Compress:**
- "in order to" → "to"
- "due to the fact that" → "because"
- "at this point in time" → "now"
- "the reason is because" → "because"
- "make a decision" → "decide"
- Passive → active where possible

**Structural choices:**
- Prose over bullets unless items are genuinely parallel (≥3 items, same shape)
- Tables only when comparing ≥2 entities across ≥2 dimensions
- Code blocks: no comments restating what the line obviously does
- Number examples only when sequence matters

**What to keep even under tight budget:**
- The actual answer
- One reason WHY (not just what)
- Any disqualifying caveat (security, correctness, irreversibility)
- Units, signs, and direction (saying "increases" without "by how much" wastes the sentence)

### Step 6 — Self-check and compress

After drafting, estimate token count using chars/4.

If over budget:
1. Find the lowest-info sentence. Delete it.
2. If still over: find the longest sentence with redundant clauses. Tighten.
3. If still over: replace a paragraph with a table or a list — or vice versa, whichever is denser for this content.
4. Last resort: drop a section entirely and note what was cut.

If under budget by >20%, you're under-spending. Either add a useful caveat, an example, or a next step — or accept that the task didn't need the full budget (which is fine).

### Step 7 — Report the saving

End the response with a one-line footer:

```
[Tokens: ~X used / Y budget. Estimated baseline: ~Z. Reduction: N%.]
```

How to estimate the baseline:
- Tight tasks: baseline ≈ 3× the optimized version (Claude's default verbose-mode answer)
- Standard tasks: baseline ≈ 2–2.5×
- Extended tasks: baseline ≈ 1.5–2×

These multipliers come from observed defaults; adjust if the optimized answer is already near a natural length.

Show the footer **only when** the user asked for token optimization explicitly. For implicit triggers (cost-sensitive contexts), include it. For pure brevity requests where the user just wants a short answer, skip the footer — they don't care about the metric.

## Worked examples

### Example 1 — Code answer, tight budget

**Prompt:** "In Python, dedupe a list while preserving order. Token-optimized."

**Unoptimized (baseline ~95 tokens):**
> Great question! There are several ways to deduplicate a list in Python while preserving the original order. The most Pythonic approach uses `dict.fromkeys()` since dictionaries maintain insertion order in Python 3.7+. Here's how:
>
> ```python
> result = list(dict.fromkeys(my_list))
> ```
>
> This works because dictionary keys are unique, and insertion order is preserved. Hope this helps!

**Optimized (~25 tokens):**
> ```python
> list(dict.fromkeys(xs))
> ```
> Preserves order (dicts ordered since 3.7). For unhashable items, use a seen-set loop.
>
> `[Tokens: ~25 / 150 budget. Baseline: ~95. Reduction: ~74%.]`

### Example 2 — Explanation, standard budget

**Prompt:** "Explain why transformers replaced RNNs. Keep it tight."

**Optimized (~110 tokens):**
> RNNs process tokens sequentially, so training can't parallelize across a sequence and long-range dependencies decay through repeated hidden-state updates (vanishing gradients). Transformers replace recurrence with self-attention: every position attends to every other position directly, in one matrix operation. Result: (a) full sequence trains in parallel on GPUs, (b) long-range dependencies are O(1) hops away, not O(n). Cost: attention is O(n²) in sequence length, which is why context windows became the bottleneck instead of depth.
>
> `[Tokens: ~110 / 400 budget. Baseline: ~280. Reduction: ~61%.]`

Note: under budget by ~70%, but the answer is complete. Don't pad.

### Example 3 — Quality floor triggered

**Prompt:** "Review this 2000-line codebase and suggest a refactoring strategy. In 50 tokens."

**Response:**
> Useful minimum for a codebase refactor strategy is ~400 tokens (architecture summary + 2–3 prioritized changes + risk note). Your budget of 50 fits only a one-line verdict. Options:
> (a) raise to 400,
> (b) narrow to a single concern — "biggest smell to fix first"? — answerable in 50,
> (c) accept a stub with major caveats.
>
> Which?

## Anti-patterns to avoid

- **Compressing by removing the "why".** A bare verdict with no reasoning is brittle — the user can't generalize from it. Keep one reason.
- **Replacing prose with bullets to look shorter.** Five 8-word bullets often beats a 40-word sentence on token count by ~10% but loses logical connectives. Use bullets only when items are parallel.
- **Removing units, signs, or quantities.** "Increases performance" is uselessly compressed; "increases throughput ~2×" is the same length and actionable.
- **Front-loading caveats.** A caveat that belongs at the end of an answer ("works on Linux only") doubles in cost if you put it first and then have to reference it again. Put context where the reader needs it.
- **Showing the optimization process to the user.** They want the answer, not the workflow. Apply the steps silently.

## Edge cases

- **User wants long-form but mentions a budget**: respect the explicit budget. They've thought about the trade-off.
- **Multi-turn conversation**: re-apply per turn. Don't carry budget from earlier — each turn has its own value.
- **Streaming / agent contexts**: omit the footer (it wastes tokens for downstream tools). Keep the discipline; drop the meta.
- **User pushes back that the answer is too short**: ask what they want expanded specifically. Don't blanket-rewrite.
