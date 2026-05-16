---
name: skill-upgrader
description: improve, update, refactor, validate, and package existing chatgpt skills based on old skill files, pasted or uploaded chat history, user queries, assistant outputs, feedback, failure patterns, and desired behavior changes. use when the user wants to upgrade a skill, revise a skill.md, improve skill triggers, convert past usage into better instructions, analyze weak skill performance, create an updated skill package, or generate a ready-to-upload skill.zip from an existing skill and real usage examples.
---

# Skill Upgrader

Upgrade existing ChatGPT Skills by comparing the current skill files against real usage evidence: user prompts, assistant outputs, feedback, repeated gaps, failed responses, missing instructions, and desired new behavior. Treat every upgrade as a skill-engineering task: preserve what works, fix what failed, and return a complete improved skill artifact.

## Access and input rules

A skill cannot automatically read all prior ChatGPT conversations unless the relevant content is provided in the current conversation, uploaded as files, exported, pasted, or made available through an enabled connector. If the user asks to upgrade based on "previous chats" but provides no chat content, state this limitation briefly and request or use available inputs.

Accept any of these inputs:
- An existing skill archive (`.zip`) containing one skill.
- A standalone `SKILL.md`.
- Supporting files such as `references/`, `scripts/`, `assets/`, or `agents/openai.yaml`.
- Pasted chat examples containing user queries, skill responses, and follow-up corrections.
- User feedback describing what the old skill missed, misunderstood, or should do better.
- Desired new behavior, output format, trigger phrases, workflows, tools, or quality standards.

When multiple inputs conflict, prioritize in this order:
1. Explicit latest user instruction.
2. User feedback about real skill failures.
3. Actual chat examples showing skill behavior.
4. Existing skill files.
5. General skill design best practices.

## Upgrade workflow

Follow this workflow unless the user explicitly asks for only a small edit.

### 1. Inventory the provided material

Identify:
- Skill name and purpose.
- Existing `SKILL.md` frontmatter and body.
- Supporting resources and whether they are actually referenced.
- User-provided chat examples.
- Observed failure modes.
- Requested new capabilities.
- Expected output deliverable: revised `SKILL.md`, full folder, diff, or ready-to-upload `skill.zip`.

If an uploaded ZIP contains more than one `SKILL.md`, stop and ask the user which skill to upgrade.

### 2. Diagnose skill performance

Compare intended behavior against actual behavior. Look for:
- Weak or missing trigger description.
- Frontmatter description that is too vague, too narrow, too long, or not lowercase.
- Instructions hidden in the body that should be in the trigger description.
- Missing input assumptions.
- Missing workflow steps.
- Missing output templates.
- Missing examples for high-quality outputs.
- Overly generic language that allows weak responses.
- Instructions that are too broad, contradictory, outdated, or duplicated.
- Poor context efficiency caused by putting large reference material directly in `SKILL.md`.
- Missing references to supporting files.
- Missing quality gates, validation steps, edge cases, or refusal/fallback behavior.
- Overuse of scripts where ChatGPT can reason directly, or missing scripts for deterministic tasks.

### 3. Create an upgrade plan

Before rewriting, produce or internally maintain a concise upgrade plan:
- What to preserve.
- What to rewrite.
- What to add.
- What to move into references.
- What to remove.
- What deliverable will be created.

For small edits, summarize the change directly. For full upgrades, include a short "Upgrade summary" in the final response.

### 4. Rewrite the skill

When rewriting `SKILL.md`:
- Keep YAML frontmatter valid and limited to `name` and `description`.
- Keep `name` lowercase, short, and hyphenated.
- Make `description` the triggering mechanism. Include what the skill does and when to use it.
- Do not place critical trigger conditions only inside the body.
- Use imperative instructions for the assistant that will use the skill.
- Make the body a control plane, not a knowledge dump.
- Prefer workflows, decision rules, templates, and examples over abstract explanation.
- Keep large or specialized details in one-level reference files linked from `SKILL.md`.
- Remove placeholder/example files that are not needed.
- Preserve useful user-provided domain conventions.
- Add explicit fallback behavior for missing inputs or insufficient evidence.
- Add output templates when consistency matters.
- Add examples when response quality depends on style, structure, or judgment.

### 5. Improve supporting resources when useful

Create or update supporting files only when they materially improve reliability or context efficiency.

Use `references/` for:
- Detailed playbooks.
- Domain-specific rules.
- Long checklists.
- Example libraries.
- Output templates.
- Evaluation rubrics.
- Troubleshooting guides.

Use `scripts/` only for deterministic repeatable operations such as:
- Validating a known file format.
- Transforming structured data.
- Extracting file metadata.
- Running tests or linting.
- Packaging helper outputs.

Use `assets/` only for final-output assets, templates, or static files.

### 6. Validate the upgraded skill

Before returning a full skill deliverable, check:
- Exactly one top-level skill is included.
- `SKILL.md` exists.
- YAML frontmatter parses correctly.
- Frontmatter includes only `name` and `description`.
- `name` is lowercase and hyphenated.
- `description` clearly explains trigger conditions.
- Referenced files exist.
- No unnecessary placeholder files remain.
- Package size is under 25 MB.
- The skill still matches the user's original purpose.
- The upgrade directly addresses the provided chat failures or requested improvements.

If scripts were added or changed, test representative scripts and report any failures honestly.

### 7. Return the deliverable

Match the user's requested output:
- If they ask for just content, return the revised `SKILL.md`.
- If they ask for an updated package, return a complete `skill.zip`.
- If they ask for review first, provide an upgrade report and wait for requested edits.
- If they provide an old ZIP and ask to update it, return the full repackaged skill, not only a patch.

Always name the packaged archive `skill.zip`.

## Upgrade report format

When presenting an upgrade review, use this structure:

```markdown
# Skill Upgrade Review

## Current skill
- Name:
- Purpose:
- Inputs reviewed:

## Key findings
1. ...
2. ...
3. ...

## Recommended upgrades
| Area | Issue | Upgrade |
|---|---|---|
| Triggering | ... | ... |
| Workflow | ... | ... |
| Outputs | ... | ... |
| Examples | ... | ... |

## Files to change
- `SKILL.md`: ...
- `references/...`: ...

## Risk notes
- ...

## Deliverable
- ...
```

## Diff-style summary format

When returning an updated skill, include a concise summary:

```markdown
## Upgrade summary
- Strengthened the frontmatter trigger description.
- Added a structured workflow for analyzing provided chat examples.
- Added failure-pattern diagnostics.
- Added output templates and validation checklist.
- Removed unused placeholders.

## Files included
- `SKILL.md`
- `agents/openai.yaml`
- `references/...` if applicable
```

## Failure-pattern taxonomy

Use this taxonomy to diagnose old skill behavior:

| Pattern | Meaning | Typical fix |
|---|---|---|
| Trigger miss | Skill would not activate for likely user wording | Rewrite description with specific trigger contexts |
| Generic output | Response is correct but shallow or non-expert | Add output templates, examples, and quality gates |
| Workflow gap | Skill skips an important step | Add ordered workflow and decision points |
| Missing evidence | Skill makes claims without reviewing provided inputs | Add input inventory and citation/evidence rules |
| Context overload | Skill body is too long or theory-heavy | Move details into reference files |
| Tool misuse | Skill uses wrong tool or skips required tool | Add explicit tool-selection rules |
| Weak fallback | Skill fails when input is incomplete | Add assumptions and clarification rules |
| Format drift | Outputs vary too much | Add templates and required sections |
| No validation | Skill creates artifacts without checking them | Add validation checklist and packaging rules |
| User mismatch | Skill optimizes for a generic user, not the intended workflow | Add user-specific examples and conventions |

## Decision rules

Use these rules while upgrading:

- If repeated user prompts ask for the same missing section, add that section to the default output template.
- If assistant outputs are verbose but not actionable, add "lead with answer, then implementation details" guidance.
- If user often asks for GitHub, README, report, skill, slide, document, or spreadsheet outputs, add format-specific templates or composition rules.
- If the same clarification is repeatedly needed, add default assumptions and a compact clarification policy.
- If the old skill produces generic advice, add role, context, constraints, examples, and quality gates.
- If the old skill misses domain-specific expectations, add domain rules or a reference file.
- If the skill should update files, include packaging and validation expectations.
- If the user expects automation across old chats, state that chat history must be provided or connected; do not claim automatic access.

## Clarification policy

Ask at most three clarifying questions when critical information is missing. Prefer proceeding with explicit assumptions when:
- The old skill file is provided.
- At least one chat example is provided.
- The requested upgrade is clear.
- The user asks for a best-effort upgrade.

Ask for clarification when:
- No existing skill content is provided.
- The user wants automatic analysis of inaccessible chat history.
- The desired output type is unclear.
- A ZIP contains multiple skills.
- The requested changes conflict with the existing skill's purpose.

## Example upgrade behavior

User provides an old skill and says: "This skill gave weak generic answers. Upgrade it based on these three chats."

Respond by:
1. Summarizing the old skill purpose.
2. Extracting what the user expected from the chat examples.
3. Listing failure patterns.
4. Rewriting the description and workflow to address the patterns.
5. Adding default output sections and one or two examples.
6. Validating the final structure.
7. Returning the updated `skill.zip` or revised `SKILL.md`.

## Quality bar

An upgraded skill should be:
- More triggerable.
- More specific.
- More reusable.
- More context-efficient.
- More aligned with the user's real workflow.
- More consistent in output format.
- More explicit about inputs, assumptions, tools, and validation.
- Easier for another ChatGPT instance to use without extra explanation.
