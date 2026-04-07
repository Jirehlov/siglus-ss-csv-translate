# Progress And Collaboration

Use this file when translation or review must survive interruption or be split across multiple agents.

## Project Entry

For full-project or folder-scale runs:

1. look for `_start.ss`
2. if it exists, use it as the primary clue for the entry scene and early script flow
3. if it does not exist or does not settle the order clearly, fall back to stable filename order and neighboring-scene evidence
4. do not rewrite `_start.ss` as part of packet translation

## Packet Model

Treat each assignment as one packet.

Preferred packet granularity:

- one full scene per packet

Fallback packet granularity:

- one explicit non-overlapping line range inside one scene

Avoid mixed or fuzzy packet boundaries.

## Packet Folder Layout

One packet folder should contain only packet-local writable files:

- working `.ss.csv`
- `translation-notes.csv`
- `progress.csv`
- `handoff.md`
- optional read-only termbook snapshot

Alongside the packet folders, keep one shared project-level `claims.csv` as the only cross-packet writable coordination ledger when concurrent agents may exist.

Prefer ASCII-safe packet folder names and `packet_id` values even when the copied working `.ss.csv` keeps its original Japanese filename.

If there is a wider project-level packet manifest or shared termbook, treat those as setup baselines rather than live multi-agent scratchpads. The claim ledger is the one shared writable exception.

## Claim Ledger

Use `claims.csv` to coordinate packet ownership across agents that cannot talk to each other.

The ledger should record at least:

- packet identifier
- source scene
- scope
- owner label
- current status
- claimed time
- updated time
- next action or resume note

Claim protocol:

1. read `claims.csv` before choosing work
2. choose only an unclaimed packet or a packet with no active owner
3. write your claim before editing the packet
4. re-read the ledger and continue only if no competing active claim covers the same packet
5. edit only the claimed packet plus the shared `claims.csv`
6. when the packet becomes translated, reviewed, blocked, or intentionally released, update the ledger immediately
7. only then claim the next packet

Keep one active writable claim at a time.

## Progress File

Use `progress.csv` as the terse machine-readable state ledger.

Recommended status values:

- `not-started`
- `translating`
- `translated`
- `reviewing`
- `reviewed`
- `blocked`
- `needs-name-confirmation`

Recommended update moments:

- before the first edit
- after each completed batch
- before any handoff or interruption
- after finishing review

Keep the file short and current.

## Handoff File

Use `handoff.md` as the human-readable continuation note.

It should answer:

- what packet this is
- what is already complete
- where to resume next
- which lines or motifs are risky
- whether user confirmation is needed
- whether review is still pending

If another agent resumes the packet later, they should be able to continue without reconstructing your intent from scratch.

## Collaboration Rules

Assume peer agents do not know you exist and cannot coordinate with you in real time.

Therefore:

- one packet should have only one active writable owner at a time
- no two agents should edit the same working `.ss.csv`
- no two agents should co-edit one packet-local notes, progress, or handoff file
- no agent should work outside its claimed packet except for the shared `claims.csv`
- active claims should stay explicit and current in `claims.csv`
- shared termbooks or manifests should be treated as read-only unless the user explicitly assigns one agent to maintain them

Default safe collaboration pattern:

1. split work by full scene
2. claim one scene packet through `claims.csv`
3. create one packet folder per claimed scene
4. let each agent edit only its own claimed packet
5. update packet state and the claim ledger before taking new work

Use same-scene line-range packets only when necessary, and make the boundaries explicit enough that another agent can see exactly where one packet stops and the next begins.

## Resume Order

When resuming project-level work, read in this order:

1. `_start.ss` if the project entry order is still unclear
2. `claims.csv`
3. the chosen packet's `progress.csv`
4. the chosen packet's `handoff.md`
5. packet-local termbook snapshot if present
6. `translation-notes.csv`
7. the working `.ss.csv`

When resuming one known packet directly, read in this order:

1. `progress.csv`
2. `handoff.md`
3. packet-local termbook snapshot if present
4. `translation-notes.csv`
5. the working `.ss.csv`

Do not skim only the translated CSV and guess the rest.
