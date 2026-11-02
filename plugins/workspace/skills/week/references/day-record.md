# Proposed and accepted day

Read [landing.md](landing.md) for consent, IDs, holds and uncertain outcomes. `propose_day` and `accept_day` write only today or tomorrow in the workspace time zone. A later date can be discussed or filed as an authorized page/task, but not called an accepted saved day. `read_day` must precede any write; an existing accepted day is revised only on explicit request. Show the differences first.

Use `propose_day` once for a complete proposal: new `request_id`, `date`, `lines`, optional `instruction` containing only the owner's actual words and optional `note` clearly our explanation. Do not send `coverage` to this tool. Each of 1–24 lines has `at`, `words`, `origin`:

- `appointment`: only an event actually read from a calendar, with `calendar`, `all_day` and, for timed events, required `calendar_timezone`. Clarify a missing time zone instead of inventing one. For an all-day event use `at: all day`, `all_day: true`; do not add a time zone absent from the source.
- `chosen-block`: something placed by the owner; no calendar fields.
- `suggestion`: our proposed arrangement, even if it resembles a habit; no calendar fields.

Select only events on the date being saved; a 48-hour read does not put tomorrow's appointments into today. Update stale/incomplete source coverage first. Do not invent a line to save an empty day or omit commitments to fit the schema; agree a valid representation. A conversational three-line suggestion at close is not a full persisted proposal.

Present the proposal and wait for acceptance. On the owner's yes, `accept_day` gets a new ID, `date`, `from_proposal` from the latest confirmed proposal receipt, the agreed `lines`, and `corrections` only in their exact words if any. If the owner directly dictates and asks to save a day without a proposal, omit `from_proposal`.

`accept_day.coverage` is required, 1–12 source entries: `source`, `kind: recorded|possible|not-checked`, `outcome: read|returned-nothing|failed|not-checked`, `detail`, optional `checked_at` when checked. Distinguish empty response from failure or not asked. Follow exposed field limits. Do not turn a failed calendar into an empty/free one.

A stale proposal is refused: reread, show what changed and resolve the new acceptance before writing different content. Keep history. On confirmed acceptance reread `read_day` to verify the right date and chosen lines. Held or uncertain does not mean accepted; do not duplicate or continue dependent acts. A saved day does not edit external calendars.
