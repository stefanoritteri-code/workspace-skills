# Council history and landing

The room instruction governs consent. Apply [landing.md](landing.md): the 120-character title limit, the exact slug rule, confirmed absence before creation, word-first headings, separate attribution, 20,000-character blocks, page limits and non-duplicating recovery. Every write needs the conversation's yes, its own app approval and a fresh request id; read each receipt back. Offer the actual page in one line and wait. File a decision only in the owner's adopted words. Report partial landing as partial. Keep an owner's own clients' names out of seat cards and track records, because those people did not agree to sit in a charter.

## One history under several names

An owner's sittings may already be kept under any of three sets of pages, and all of them are the same history. Read every one that exists before a sitting, deduplicate the same sitting, and never treat an empty new index as no earlier history:

| Kept as | Index | Lessons | A seat's track record |
| --- | --- | --- | --- |
| Board | `pages/board-sittings-index.md` | `pages/board-lessons.md` | `pages/board-seat-<token>-track-record.md` |
| Council | `pages/council-sittings-index.md` | `pages/council-lessons.md` | `pages/council-voice-<token>-history.md` |
| Consiglio (earlier Italian pages) | `pages/consiglio-sedute-indice.md` | `pages/consiglio-lezioni.md` | `pages/consiglio-voce-<token>-storico.md` |

**New material continues the set the owner already has**: the one whose index exists, and when more than one exists, the one with the newest line. An owner with none starts the Board set; in an Italian room its titles are written in Italian — «Seduta del consiglio <gg/mm/aa> — <tema in sei parole al massimo>» and «Verifica del consiglio — <tema> — rileggi i segnali a 60 giorni nella pagina <nome della pagina>» — while the index, lessons and track-record paths keep the fixed English names above. These strings identify stored paths; never rename, move or overwrite an old page, and add an authorised index line pointing at an older page when it helps the next sitting find it.

**A seat's token** is the one its existing history uses. The preamble names the owner's tokens when their seats are kept under other names; otherwise the tokens are the first names `cal`, `derek`, `james`, `jason-david`, `naval`, `oliver`, `ray`, `seth`, and the roles `contrarian`, `first-principles`, `expansionist`, `outsider`, `executor`, `chairman`. A role's older history may sit under `first-fundamentals`, `expansive` or `president`, or the Italian `contrario`, `primi-principi`, `espansivo`, `esterno`, `esecutore`, `presidente`: read it and continue it. Do not guess an old identity from a new name: when the link between an older history and a seat cannot be established from actual index or sitting links, report the gap.

## Titles, paths and sections

A sitting is titled `Board sitting <today, dd/mm/yy> — <topic in at most six words>` in the Board set and `Council sitting <today, dd/mm/yy> — <topic in at most six words>` in the Council set, with today's date taken from the door and never from this file. A second sitting that day adds ` b` after the date; a continuation adds ` — 2`, ` — 3` at the end, keeping any same-day letter. Keep the topic short enough that the suffix survives the 60-character slug.

The path is `pages/<slug>.md` by the slug rule in [landing.md](landing.md). Before every `create`, `read_source` the resulting path. If it exists, change the title and check the new path, because distinct titles can share a truncated slug; failed access is not proof of absence. Never append a new sitting to an old one after a collision. So a sitting titled `Board sitting 03/02/27 — sound studies` lands at `pages/board-sitting-03-02-27-sound-studies.md` and its continuation ends `-sound-studies-2.md`. ⛔ That is the SHAPE; the date in it is an illustration and is never the date you write.

Name the Chairman in the frame as the counterpart's own seat for the verdict, voiced only in Phases 6 and 8, and attribute those words to "Chairman" (in Italian rooms, "Presidente"). Every section heading starts with a word: `## Frame — <today>`, `## Beat 3a — the structural seats — <today>`, `## Verdict — <today>`. The door refuses headings opening with digits, to stop forged attribution. Date and attribute every section.

## Land in this order

| Order | Destination | Content and attribution |
| --- | --- | --- |
| 1 | The sitting page at its checked path | `write_page`, create then append, `author: counterpart`: the original frame and its changes, dated facts and sources, a line naming what was read, the options and any forced ranking, the confirmed bench with each seat's card receipt, and the complete transcript in beat order with every speaker named and the owner's lines quoted exactly as theirs. Verdict and both signals last. |
| 2 | The decision | `record_decision`, `tags: [board]`: the owner's exact adopted words, a `why` only if they spoke one, and the sitting page's confirmed path in `page` (`pages/<slug>.md`), because a decision that names its page is found with its reasoning by the next sitting. A scope tag only for an adopted writing or planning rule. The recommendation stays the Chairman's. |
| 3 | `Board check — <topic> — read the 60-day signals on the page <page name>` (or `Council check — …` in the Council set) | `make_task` with only `request_id`, that `title`, and `deadline` as the check date in `YYYY-MM-DD`, exactly 60 calendar days after today as the door reported it; add `project` only if `search_work` found it and the owner adopted it, by its name, at most 200 characters. |
| 4 | The index | `write_page`, counterpart append, creating on confirmed first use: `date \| topic \| exact decision \| check date \| page name \| page path \| supporting signal \| undermining signal`. Keep every earlier line. |
| 5 | The lessons page | Counterpart append only when a process lesson actually occurred: dated success or failure and its evidence, distinct from any rule the owner adopted. Never create an empty lessons page. |

The task act takes one date and no note, so both signals live on the sitting page and in the index line; its title carries the page name so the check finds the sitting without the index. Surface dates are dd/mm/yy; every tool date argument is `YYYY-MM-DD`. ⛔ Never copy a date out of this file.

Each page write holds at most 20,000 characters; the whole-page ceiling is 512 KB. After each append, `read_source` the page and read `bytes`. ⚠ The append limit counts CHARACTERS and the file limit counts BYTES — 20,000 characters can cost 60,000 bytes — so roll over to a linked "— 2" page once `bytes` passes 440,000 — stricter than the general 480,000 in landing.md, and for a sitting this one governs — and never judge the room left by the character count. Link the parts to each other through approved appends, reserving room for those links, and keep the first page as canonical. Preserve existing words.

If the owner's decision plus its reference exceeds the decision tool's limit, ask for shorter wording rather than truncate or paraphrase it. Ask for missing transcript rather than invent it. An approved adjournment contains actual proceedings only, marked unfinished, with no verdict, decision or check; index it as `date | topic | unfinished — no decision | no check | page name | page path | unset | unset`. Resume from its actual transcript.

## Receipts and the next sitting

A receipt saying the page landed but was not indexed means it exists and `recall` cannot see it: keep its path in the index line and read it by path next time; the index itself is always read by its fixed path. For held, uncertain or dependent writes, follow [landing.md](landing.md): never retry an uncertain page or task, never mint another id, and resume from confirmed receipts. For an uncertain decision, search before the instruction's exact same-id retry. A refusal is said as what was refused and why, and that act stays undone.

The next sitting calls `standing`, searches the question's words and separately `tag: board`, `state: live`, `limit: 50`, then recalls the topic, and reads the index or indexes by path, their last three related sittings (all if fewer), continuations, lessons and relevant track records. ⛔ It does not read `list_waits`, `list_tasks`, `status` or the day, and does not assert what is open, outstanding, late or how the machinery is.

## Close the check

Before action keep the chosen move, baseline, predicted result, failure condition and check date. When the check task surfaces and the owner opens it, read the sitting and ask what they did and what happened. Distinguish their report, observed evidence and other possible causes. On their yes, append to each strong-position seat's track record by its token, counterpart, creating on confirmed first use: date, sitting, decision kind, position, action, baseline and prediction, reported or observed outcome, RIGHT / WRONG / PARTIAL / N/A and why. Include the structural roles and the Chairman; the dual seat keeps its two positions distinct in one history. Untried means N/A — untested, and missing or premature evidence needs a reason. Long-direction signals are early evidence, not final proof.

With approval append outcomes and unresolved signals to the sitting, preserving the verdict and earlier grades. After the track records are confirmed, end with `close_task` on the check task, on the owner's yes: a held or refused close is not completion.
