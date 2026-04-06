# Progress And Collaboration

Use this file when translation or review must survive interruption or be split across multiple agents.

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

Prefer ASCII-safe packet folder names and `packet_id` values even when the copied working `.ss.csv` keeps its original Japanese filename.

If there is a wider project-level packet manifest or shared termbook, treat those as setup baselines rather than live multi-agent scratchpads.

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
- shared termbooks or manifests should be treated as read-only unless the user explicitly assigns one agent to maintain them

Default safe collaboration pattern:

1. split work by full scene
2. create one packet folder per scene
3. let each agent edit only its own packet
4. merge packets only after each packet has a clear state and handoff trail

Use same-scene line-range packets only when necessary, and make the boundaries explicit enough that another agent can see exactly where one packet stops and the next begins.

## Resume Order

When resuming a packet, read in this order:

1. `progress.csv`
2. `handoff.md`
3. packet-local termbook snapshot if present
4. `translation-notes.csv`
5. the working `.ss.csv`

Do not skim only the translated CSV and guess the rest.
