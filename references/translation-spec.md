# Translation Spec

Use this file when the main skill needs fuller policy detail.

## Mission

Produce high-quality Chinese galgame translation with this priority:

1. Faithfulness
2. Fluency
3. Literary force

Recover the line's communicative effect, not just its surface wording.

Preserve:

- literal meaning
- implied meaning
- tone
- relationship dynamics
- humor, erotic charge, or dramatic pressure
- wordplay, sound-play, allusion, or parody function
- reveal timing and narrative withholding

When forced to choose, preserve meaning and dramatic function first.

## Tool Boundary

The Chinese text itself must be produced by the agent's own reasoning.

Do not use any machine translation engine or translation-generation tool.

Local deterministic tools may be used only for:

- packet creation
- copying
- safe writeback
- diffing
- validation

Do not let tooling decide the wording of the translation.

## Row Mutability Policy

Row kind is a strong hint, not a complete mutability definition.

Default assumptions:

- `kind=1` is normally running-script text
- `kind=2` is normally running-script speaker labeling
- `kind=3` is normally read-only support content

However, do not hard-code mutability from row kind alone.

If local packet evidence or project knowledge shows that a subset of `kind=3` rows are actually running-script dialogue, narration, or interior monologue, treat those rows as translatable.

If a `kind=3` row is acting as a menu item, choice button, system prompt, config text, debug text, identifier, control text, structure, hidden support content, or any other non-script layer, keep it read-only.

The real boundary is running-story script text versus menu, system, UI, and support text.

For `kind=3`, use this priority order:

1. check whether the row visibly behaves like a Japanese line of dialogue, narration, or interior monologue that would be read as part of the running story
2. if it instead behaves like a menu item, choice button, system prompt, config line, debug line, identifier, or other interface text, treat it as non-translatable for this skill
3. if it does not look sentence-like or script-like, treat it as non-translatable
4. if it contains no Japanese characters at all, treat it as non-translatable unless the user explicitly instructs otherwise
5. only after passing that gate, judge whether it belongs to the running script surface or to support structure

This gate is intentionally conservative. A row kind that is usually structural should not be translated merely because it has a writable `replacement` field.

## Working Copy Policy

Never edit the original source `.ss.csv` in place.

Before translation or review edits:

- create or enter the packet folder
- keep the copied working `.ss.csv` as the only writable scene file
- keep packet-local state files beside it

Packet artifacts should remain text-based and easy to inspect.

## Autonomy Policy

Operate with minimal user interaction.

The routine reason to ask the user is unresolved kana proper-noun hanzi confirmation.

For all other uncertainty:

- use local scene context
- use neighboring scene order
- use repetition and callback structure
- preserve ambiguity when the scene still withholds information
- record non-obvious decisions in packet-local notes

## Packet State Policy

Treat each packet as a resumable unit.

Each packet should contain:

- working `.ss.csv`
- `translation-notes.csv`
- `progress.csv`
- `handoff.md`
- optional termbook snapshot

Update packet state:

- before the first edit
- after each stable stop
- before interruption or handoff
- after review

## Scene Order And Reveal Control

Treat filename order as narrative metadata.

Before drafting a scene, identify its neighboring files so later knowledge does not leak backward.

If the current scene frames something as unknown, uncertain, half-seen, or not yet earned:

- keep that uncertainty alive in Chinese
- avoid premature disambiguation
- avoid terminology that reveals later understanding too early

## Name Policy

Translate names before dialogue so repeated labels stay stable.

Rules:

- prefer stable one-to-one mapping for already clear hanzi or kanji forms
- if a kana-containing proper noun needs a target hanzi form and the form is not responsibly inferable, ask the user once in a consolidated batch
- translate generic role labels and descriptive speaker tags directly
- keep approved forms stable across packets

Use the term governance workflow for status tracking.

## Split-Line Policy

If multiple writable fragments share one `line`, treat them as one semantic unit unless strong evidence says otherwise.

When reconstructing:

1. read all writable fragments together
2. inspect nearby units for relational clues
3. search the same `.ss.csv` for open repetitions if needed
4. infer only what the context safely supports
5. draft one full Chinese line mentally
6. distribute the Chinese back into the writable fragments so concatenation reads naturally

Do not translate fragments as if they were standalone lines.

If context supports only tone or force but not a specific hidden word, preserve that uncertainty instead of inventing a false concrete reading.

When a running-script line is distributed across multiple rows of mixed kinds, reconstruct the full visible unit first and then write back only into the rows that belong to the translatable script surface under the current packet's mutability rules.

## Local Exchange Policy

Do not solve risky lines in isolation when adjacent replies carry the payoff.

Before finalizing a difficult stretch, check whether nearby lines form one exchange built on:

- deliberate misnaming
- correction
- sound association
- catchphrase repetition
- misunderstanding
- rhetorical escalation

When they do, plan the whole exchange first.

## Chinese Output Policy

Use modern Mainland China simplified Chinese.

Requirements:

- natural Chinese grammar
- standard Mainland punctuation
- no Japanese punctuation conventions
- no kana
- no Latin letters unless explicitly required by the user
- no Arabic numerals unless explicitly required by the user
- no traditional-character defaults
- no non-Mainland regional defaults unless explicitly requested

Convert count expressions into natural Chinese forms when translated.

## Fidelity Policy

### Voice

Preserve:

- bluntness versus softness
- smugness versus timidity
- childishness versus maturity
- intimacy distance
- comedy rhythm
- recurring speech habits

### Wordplay

Preserve the joke's function, reaction pattern, and local chain even when the exact form must change.

Do not solve weak compensation by adding in-line explanation inside dialogue.

### Allusion And Parody

Make the line playable in Chinese while keeping the same rhetorical role.

### Regional Or Social Coloring

Keep locality or social texture when it affects how the line lands.

### Reveal Pacing

Do not translate an early scene as if later scenes had already explained it.

## Notes Policy

Use the notes CSV as sparse decision memory.

Record only lines that involve:

- ambiguity
- split-line reconstruction
- wordplay or sound-play handling
- compensation
- terminology judgment
- review-stage correction with non-trivial rationale
- spoiler-sensitive restraint

Do not bloat notes with obvious lines.

## Validation Policy

A packet is not ready until it passes both structural and language validation.

Minimum validation expectations:

- only intended running-script rows changed
- row count and order unchanged
- disallowed columns unchanged
- no menu, system, UI, or support rows altered
- output file readable after writeback
- translated text respects target-language constraints
- packet state files refreshed to match the current stage

Use the dedicated QA checklist for the full gate.
