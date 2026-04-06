# Termbook Workflow

Use this file to govern terminology across packets without turning the shared termbook into a live scratchpad.

## Governance States

Use these states consistently:

- `user-confirmed`
- `project-fixed`
- `pending-user-confirmation`
- `packet-local-tentative`

## State Meanings

### User-Confirmed

Use when the user explicitly approved the Chinese form.

This state overrides all others.

### Project-Fixed

Use when the form is stable enough to be treated as the project baseline even without direct user confirmation.

Promotion into this state should be deliberate, not casual.

### Pending User Confirmation

Use when a kana-containing proper noun still needs a target hanzi form that cannot be inferred responsibly.

Do not use this state for generic role labels or descriptive tags that should simply be translated.

### Packet-Local Tentative

Use when a packet needs a provisional term to keep working but the form is not yet ready to govern the project.

Keep these decisions packet-local until reviewed.

## Promotion Rules

- promote to `user-confirmed` immediately after explicit user confirmation
- promote to `project-fixed` only when the evidence is strong and the term is ready for cross-packet reuse
- do not promote unresolved packet-local decisions directly into the shared baseline during normal packet work

## Packet Snapshot Rules

- snapshot the shared baseline into the packet before heavy editing when helpful
- treat the packet snapshot as read-only reference, not a second shared termbook
- if review changes the governing form of a term, update the packet state and the shared baseline deliberately rather than informally

## Review Interaction

During review, check whether:

- approved terms stayed stable
- tentative terms should remain tentative
- a packet-local term now deserves promotion
- a previously fixed term needs reconsideration because new context changed the interpretation

## User Escalation

Ask the user only when the unresolved item truly needs explicit confirmation and the risk of guessing is material.

Batch such questions when possible.
