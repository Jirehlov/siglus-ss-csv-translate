# Review Workflow

Use this file when the user asks for proofreading, polishing, or second-pass checking.

Review is a fidelity audit first and a polish pass second.

## Entry

Before editing:

1. read `progress.csv`
2. read `handoff.md`
3. read the packet-local termbook snapshot if present
4. read `translation-notes.csv`
5. re-check scene order and neighboring files if reveal timing matters
6. update `progress.csv` to the review stage

## Pass Order

Run review in this order:

1. mechanical sweep
2. risk-targeted reread
3. scene-level reread
4. cross-packet consistency sweep
5. final QA pass

## Mechanical Sweep

First catch obvious surface problems:

- formatting accidents
- disallowed scripts or symbols
- accidental source-language carryover
- encoding corruption
- inconsistent name forms

## Risk-Targeted Reread

Next reread lines flagged by:

- packet notes
- handoff risks
- known split-line reconstruction
- compensation
- reveal-sensitive wording
- recurring joke chains

## Scene-Level Reread

Then reread the scene as a performed text rather than a set of isolated lines.

Check whether the Chinese still carries:

- speaker voice
- emotional movement
- pacing
- dramatic withholding
- rhetorical force

## Cross-Packet Consistency Sweep

After the scene itself reads correctly, compare it against already-approved neighboring packets for:

- name stability
- place-name stability
- recurring terminology
- repeated speech habits
- callback wording

Do not flatten scene-specific variation that is intentional.

## Exit

Before leaving the packet:

- apply any final fixes
- update `translation-notes.csv` when review changed a non-obvious decision
- refresh `handoff.md`
- refresh `progress.csv`
- run the full QA checklist

Use `reviewed` only when the packet has completed review and post-review validation.
