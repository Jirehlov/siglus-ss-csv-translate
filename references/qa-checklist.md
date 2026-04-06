# QA Checklist

Run this checklist after translation and again after review.

## Structural Gate

Confirm that:

- only `replacement` was edited
- only intended running-script rows were changed
- row kind was not used as the sole mutability test
- any translated `kind=3` rows first passed the script-line Japanese surface-text gate
- any `kind=3` rows with no Japanese characters were left untouched unless the user explicitly required otherwise
- any translated `kind=3` rows are confirmed to be running-story dialogue, narration, or interior monologue
- menu items, choice buttons, system prompts, config text, debug text, identifiers, and support rows remain untouched
- row count, row order, and structural columns are unchanged
- the written file can be re-opened successfully after writeback
- on Windows, PowerShell was avoided for the `.ss.csv` write path whenever a safer local tool was available
- if PowerShell was used, the file was treated as untrusted until a clean readback check passed

## Language Surface Gate

Confirm that translated rows satisfy the target-language constraints currently required by the job.

By default, check for:

- Mainland simplified character forms
- natural Chinese punctuation
- no unintended kana
- no unintended Latin letters
- no unintended Arabic numerals
- no placeholder corruption
- no mojibake
- no unexpected replacement characters
- no unintended fallback to question marks

If the user explicitly requested exceptions, apply those exceptions deliberately rather than by accident.

## Translation Fidelity Gate

Spot-check whether the packet still preserves:

- literal meaning
- implied meaning
- voice and register
- joke mechanics
- setup-payoff linkage
- reveal timing
- ambiguity where ambiguity is still required
- script narration carried in non-default row kinds, when applicable

## Term Consistency Gate

Confirm that:

- packet terms follow the current term governance state
- approved names remain stable
- review edits did not reintroduce older rejected wording
- packet-local tentative terms are documented if they remain unresolved

## Packet State Gate

Confirm that:

- `progress.csv` matches the packet's real stage
- `handoff.md` matches the packet's real resume point and risk profile
- `translation-notes.csv` reflects non-obvious decisions and meaningful review changes

## Validation Method

- perform the final validation after writes are complete
- validate by re-reading the written file directly
- validate the file from disk with the intended encoding rather than by console appearance
- treat unstable or partial observations as incomplete validation and rerun the check deterministically

Do not mark a packet ready until every applicable gate passes.
