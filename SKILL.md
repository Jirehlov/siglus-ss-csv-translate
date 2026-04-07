---
name: siglus-ss-csv-translate
description: Translate and review SiglusEngine `.ss.csv` script packets into Mainland China simplified Chinese for galgame workflows. Use when only `replacement` may be edited, translatable rows must be identified by script surface rather than row kind alone, `_start.ss` may help determine entry-scene order, long-running folder translation should continue packet-by-packet with minimal interruption, and multi-agent packet claims must be coordinated through a shared claim ledger.
---

# Siglus SS CSV Translate

Translate or review Siglus `.ss.csv` packets safely and to a high literary standard.

## Mission

- preserve meaning, dramatic function, reveal timing, and character voice
- produce playable Mainland China simplified Chinese
- maximize uninterrupted forward progress until the requested scope is complete
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
- if readable `kind=3` rows behave as a choice set or mutually exclusive option surface, treat them as read-only choice text unless the user explicitly changes project policy
- never modify menu, system, control, structure, UI, or inline support rows
- never reorder, insert, or delete rows
- never rewrite structural columns
- never edit the original source `.ss.csv` in place
- translate by the agent's own reasoning
- never use machine translation or translation-generation tooling
- local tools may be used only for packet setup, copying, safe writeback, diffing, and validation
- for full-project or full-folder work, inspect `_start.ss` first if it exists and use it as primary evidence for the entry scene and early script flow
- if `_start.ss` is absent or does not yield a trustworthy order, fall back to stable filename order plus neighboring-scene evidence
- do not stop at one packet when the user requested ongoing or full-folder translation; keep taking new packets until the requested scope is complete or a real user-decision blocker appears
- when operating on Windows, avoid PowerShell as the primary read-write path for `.ss.csv` whenever another deterministic local tool is available
- when operating on Windows, avoid sending non-ASCII translation payloads through PowerShell console text or shell pipelines whenever a safer file-based or direct write path is available
- if PowerShell must be used in a Windows environment, treat the writeback as high-risk until the file has been re-opened and verified clean from disk
- keep packet artifacts text-only

## Autonomy

Operate with minimal user interaction and aim to finish the full requested scope without pausing.

Ask the user only when a kana-containing proper noun needs a target hanzi form that cannot be inferred responsibly from local context.

Do not pause merely to ask whether to continue, to summarize interim progress, or to hand off early if more claimable work still exists inside the requested scope.

Do not escalate generic role labels or descriptive speaker tags. Translate them directly into natural Mainland Chinese.

When writeback method is relevant on Windows, explicitly warn the user that PowerShell is a higher-risk path for `.ss.csv` encoding and recommend avoiding it when possible.

When the user asks for folder-scale or route-scale translation, continue packet after packet until there is no unclaimed work left or a genuine naming decision blocks further progress.

## Project Entry And Order

For full-project or folder-scale runs:

1. look for `_start.ss`
2. if it exists, read enough to infer the entry scene and the strongest available early scene flow
3. prefer that evidence when choosing the first packet and the early traversal order
4. if `_start.ss` is missing or inconclusive, fall back to stable filename order plus local scene adjacency
5. use `_start.ss` only as navigation evidence and do not rewrite it as part of script translation

## Packet Model

Treat each scene-level or explicit line-range assignment as one packet.

Each packet should contain:

- the working `.ss.csv`
- `translation-notes.csv`
- `progress.csv`
- `handoff.md`
- optional read-only termbook snapshot

When concurrent agents may exist, keep one shared project-level `claims.csv` adjacent to the packet folders and use it as the single writable coordination ledger across packets.

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

1. For project-scale work, inspect `_start.ss` if present and choose the next packet through the shared claim ledger before editing.
2. Prepare or enter the claimed packet folder.
3. Confirm scene order and neighboring files before drafting.
4. Load packet state, current term governance, and the packet's effective translatable-row set.
5. Translate speaker labels and other stable name-bearing rows that belong to the running script first.
6. Translate dialogue and narration at the semantic-line level, not fragment-by-fragment.
7. Record only decision-critical notes.
8. Run the full QA checklist before considering the packet ready.
9. Refresh `progress.csv` and `handoff.md`.
10. If the requested scope continues, update the claim ledger and immediately claim the next packet instead of stopping.

### Review Mode

1. For project-scale review, choose the next packet through the shared claim ledger before editing.
2. Enter the claimed existing packet.
3. Read packet state and notes before touching the working file.
4. Follow the staged review workflow.
5. Revise for fidelity first and polish second.
6. Re-run the full QA checklist after edits.
7. Refresh `progress.csv` and `handoff.md`.
8. If the requested scope continues, update the claim ledger and immediately claim the next packet instead of stopping.

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
- if several adjacent `kind=3` rows behave like alternate responses or branching choices, keep them read-only even when each row is readable Japanese
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
- the on-disk file remains readable after writeback with no encoding corruption

## Collaboration

Assume peer agents cannot coordinate with you in real time and may not know you exist.

Therefore:

- use one shared `claims.csv` as the only live cross-agent coordination file
- claim a packet before creating or editing its packet folder
- keep one active writable packet claim at a time
- do not edit outside your claimed packet except for the shared `claims.csv`
- do not co-edit one working `.ss.csv`
- do not co-edit one packet-local notes, progress, or handoff file
- do not claim beyond your explicit packet boundary
- after finishing or blocking a packet, update `progress.csv`, `handoff.md`, and `claims.csv` before claiming the next packet
- do not overwrite or steal another active claim; choose a different packet unless the existing claim is clearly terminal
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
