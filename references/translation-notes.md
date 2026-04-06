# Translation Notes CSV

Use this file for the translation-notes CSV that accompanies one working packet.

## Goal

Capture only decisions that materially affect later translation or review quality.

The notes CSV is sparse memory, not a scene summary and not a substitute for `progress.csv` or `handoff.md`.

## Scope

Write notes only for lines that are:

- ambiguous
- rhetorically loaded
- reconstructed from split fragments
- part of a cross-line setup-payoff chain
- translated through compensation rather than direct mirroring
- pending user confirmation
- revised in review for a non-obvious reason
- intentionally kept less explicit to protect reveal timing

Ordinary lines do not need notes.

Keep the notes file packet-local.

## Recommended Columns

- `source_csv`
- `line`
- `writable_indices`
- `category`
- `status`
- `original_excerpt`
- `current_translation`
- `rationale`
- `review_focus`
- `follow_up`

## Recommended Category Tags

- `ambiguity`
- `split-line`
- `wordplay`
- `misnaming-chain`
- `speech-tic`
- `allusion`
- `dialect`
- `compensation`
- `pending-name`
- `review-fix`
- `spoiler-guard`

## Writing Standard

Keep each note:

- short
- concrete
- decision-shaped
- useful for a later agent who did not make the original call

Each note should identify:

- what was uncertain or risky
- what was chosen
- what function needed to be preserved

## Encoding

Write the notes file as proper CSV with correct escaping.

On Windows, prefer UTF-8 with BOM for manual readability.
