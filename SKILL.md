---
name: siglus-ss-csv-translate
description: Translate and review SiglusEngine `.ss.csv` script packets into Mainland China simplified Chinese for galgame workflows. Use when only `replacement` may be edited, translatable rows must be identified by whether they belong to the running story script rather than row kind alone, `kind=3` may contain narration-like script lines, menu and system text must remain untouched, scene order controls reveal timing, split lines must be reconstructed at line level, and packet-local state is required for safe resume and collaboration.
---

# Siglus SS CSV Translate

Translate or review Siglus `.ss.csv` packets safely and to a high literary standard.

## Mission

- preserve meaning, dramatic function, reveal timing, and character voice
- produce playable Mainland China simplified Chinese
- keep packet state resumable, reviewable, and collaboration-safe

## Non-Negotiable Constraints

- edit only `replacement`
- do not treat row kind as the sole definition of translatability
- translate only rows that belong to the running story script: dialogue, narration, interior monologue, and speaker labels attached to those lines
- do not translate menu items, choice buttons, system prompts, config text, debug text, scene IDs, file names, resource names, or other non-script interface text
- treat `kind=1` and `kind=2` as the default translatable set only when they serve the running script surface
- treat `kind=3` as read-only by default, except when local packet evidence or explicit project knowledge shows that a subset of `kind=3` rows are actually script lines
- for `kind=3`, apply a script-surface gate before anything else: if the row does not look like a Japanese sentence or line that would be read as part of the running story, treat it as non-translatable
- if a `kind=3` row contains no Japanese characters at all, treat it as non-translatable unless the user explicitly states otherwise
- never modify menu, system, control, structure, UI, or inline support rows
- never reorder, insert, or delete rows
- never rewrite structural columns
- never edit the original source `.ss.csv` in place
- translate by the agent's own reasoning
- never use machine translation or translation-generation tooling
- local tools may be used only for packet setup, copying, safe writeback, diffing, and validation
- keep packet artifacts text-only

## Autonomy

Operate with minimal user interaction.

Ask the user only when a kana-containing proper noun needs a target hanzi form that cannot be inferred responsibly from local context.

Do not escalate generic role labels or descriptive speaker tags. Translate them directly into natural Mainland Chinese.

## Packet Model

Treat each scene-level or explicit line-range assignment as one packet.

Each packet should contain:

- the working `.ss.csv`
- `translation-notes.csv`
- `progress.csv`
- `handoff.md`
- optional read-only termbook snapshot

Prefer one full scene per packet.

Use non-overlapping line-range packets only when full-scene packets are impractical.

## Resume Order

When resuming a packet, read in this order:

1. `progress.csv`
2. `handoff.md`
3. packet-local termbook snapshot if present
4. `translation-notes.csv`
5. the working `.ss.csv`

Do not ignore existing packet state and restart from scratch unless the packet is clearly invalid.

## Workflow Modes

Use the mode that matches the user request.

### Translation Mode

1. Prepare or enter the packet folder.
2. Confirm scene order and neighboring files before drafting.
3. Load packet state, current term governance, and the packet's effective translatable-row set.
4. Translate speaker labels and other stable name-bearing rows that belong to the running script first.
5. Translate dialogue and narration at the semantic-line level, not fragment-by-fragment.
6. Record only decision-critical notes.
7. Run the full QA checklist before considering the packet ready.
8. Refresh `progress.csv` and `handoff.md`.

### Review Mode

1. Enter the existing packet.
2. Read packet state and notes before touching the working file.
3. Follow the staged review workflow.
4. Revise for fidelity first and polish second.
5. Re-run the full QA checklist after edits.
6. Refresh `progress.csv` and `handoff.md`.

### Full Pipeline Mode

Use only when the user explicitly asks for both translation and review in one run.

## Translation Priorities

Use this order:

1. Faithfulness
2. Fluency
3. Literary force

Never trade away meaning, reveal timing, or character voice for surface elegance.

## Core Translation Method

- treat filename order as narrative metadata
- identify translatable rows by script-surface function, not by kind value alone
- for `kind=3`, start by asking whether the row behaves like a Japanese line in the running story rather than a menu, system, control, or support row
- preserve uncertainty until the scene has earned clarification
- translate one local exchange as a unit when setup and payoff span adjacent lines
- treat same-line `kind=1` fragments as one semantic unit unless strong evidence says otherwise
- preserve recurring speech habits, verbal tics, humor mechanics, and relationship distance
- avoid explanation patches inside dialogue
- prefer natural Mainland punctuation and diction
- avoid Latin letters, Arabic numerals, kana, and non-Mainland defaults unless the user explicitly requires otherwise

## Terminology Governance

- translate names before dialogue so speaker labels stay stable
- use the shared termbook only as a read-only baseline unless the user explicitly assigns maintenance ownership
- classify terms by governance state rather than mixing confirmed and tentative decisions together
- keep packet-local discoveries in packet-local notes or handoff until they are ready to be promoted
- let user-confirmed forms override inferred forms immediately

Follow the dedicated term governance reference before creating or revising a shared termbook snapshot.

## Validation

Every packet must pass a deterministic QA pass before it is considered ready.

Validation is not optional after either translation or review.

Do not trust console appearance alone. Validate by re-reading the written file.

Validation must confirm both:

- only intended script-surface rows were translated
- no menu, system, UI, or support rows were altered

## Collaboration

Assume peer agents cannot coordinate with you in real time.

Therefore:

- one packet must have only one active writable owner at a time
- do not co-edit one working `.ss.csv`
- do not co-edit one packet-local notes or handoff file
- treat shared baselines as read-only unless explicit ownership is assigned

## References

- use [`translation-spec.md`](./references/translation-spec.md) for detailed policy
- use [`review-workflow.md`](./references/review-workflow.md) for staged proofreading and polish
- use [`qa-checklist.md`](./references/qa-checklist.md) for mandatory validation gates
- use [`rhetoric-audit.md`](./references/rhetoric-audit.md) for review-layer checks
- use [`progress-collaboration.md`](./references/progress-collaboration.md) for packet layout and resume rules
- use [`termbook-workflow.md`](./references/termbook-workflow.md) for terminology governance
- use [`termbook.md`](./references/termbook.md) for the shared term baseline format
- use [`translation-notes.md`](./references/translation-notes.md) for notes policy
- use [`translation-notes-template.csv`](./references/translation-notes-template.csv) as the notes header template
- use [`progress-template.csv`](./references/progress-template.csv) as the progress header template
- use [`handoff-template.md`](./references/handoff-template.md) as the handoff template
- use [`packet-manifest-template.csv`](./references/packet-manifest-template.csv) only when explicit packet manifests are required
