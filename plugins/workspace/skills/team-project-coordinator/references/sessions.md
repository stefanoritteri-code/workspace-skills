# Project sessions: PROJECT · LANE n/N

Work that takes more than one sitting runs in numbered sessions, so the owner always knows what to say to start the next one and any fresh chat can carry on without anyone remembering an id, a link or which chat it was. Everything lives in the owner's records, where a chat finds it by the project's name alone:

- **The project**, named as the owner calls it.
- **One card per lane**, named `PROJECT · LANE`, which every session of that lane takes up in turn, so the trail never splits.
- **One plan page per project**, titled `PLAN · PROJECT` and filed under the project. The plan page is the authority.
- **One handover page per lane**, titled `HANDOVER · PROJECT · LANE`, holding what the next chat needs.

This is the owner's own work rather than this person's round, so a session reads no team record, records no team receipt and runs whether the PROJECT COORDINATOR is switched on or off. When it is off, say so once in the opening line and carry on, because the owner asked for this session directly.

## Names

- PROJECT is the owner's name for the work. LANE is a kind of work that moves on its own, in one or two plain words such as BUILD, LEGAL, MARKETING or MONEY (in the owner's language). A lane is never split so fine that it only makes paperwork, nor so wide that it hides a blocker.
- n/N is this session's number out of the sessions planned for the lane; N may be "?" until a session can set it. Work that needs one sitting is `PROJECT · LANE` with no number.
- One chat is one session, with one finish line written before the work starts. A session that stops before its finish line is UNFINISHED, never DONE, and keeps its number.
- The words PLAN and HANDOVER stay in English in every language, because a page is found by its title and a fixed word is what lets any chat work out where the page is.

## The two pages and their identity

- The plan's title is `PLAN · PROJECT`, for example `PLAN · NEW ALBUM`; a lane's handover title is `HANDOVER · PROJECT · LANE`. A path comes from its title by the slug rule in [landing.md](landing.md): `pages/plan-new-album.md`, `pages/handover-new-album-mixing.md`.
- A page can only grow, so every update appends one section holding the whole plan, or the whole handover, as it now stands, never a change on its own. The newest section is the one in force, complete by itself, and the earlier sections are its history.
- Every plan section opens with one line naming it: `Plan for PROJECT, update k by LANE session n, built on update j by LANE session m, in force from dd/mm/yy; it replaces every earlier section.` The first section says `built on no earlier update`; a reconciled section adds `, merging` and the opening line of every section it merged; a section carrying other lanes' waiting changes adds `, carrying the waiting changes of LANE, LANE`. Two chats can still write the same k, so the number alone never names a section: the whole line does, and the same k from another writer is how an overlap shows. Every handover section opens with `Handover for PROJECT · LANE, session n of N, dd/mm/yy.` That opening line is the page's identity: a page at the expected path whose newest section names another project or lane is not this one's page, however its path came out, because two long titles can fold to the same 60 characters. Say so, and on the owner's yes give this page a shorter title that keeps its own project and lane, check that its path is free, and use that title from then on.
- The card keeps each page's actual title and path in its open loops, as `PLAN: title | path` and `HANDOVER: title | path`, and every later write uses exactly that title, because `write_page` names a page by its title and a different title is a different page.
- The plan holds one table, `| Lane | Session | State | Starts | Finish line |`. State is DONE, NEXT, RUNNING (a chat is on it now), UNFINISHED (stopped before its finish line; it carries on under the same number) or LATER. Starts is a date, or `event: what; watcher: who notices, how often, and that they then put the session on the owner's list`. Below the table: each lane's handover title, the needs between lanes (“LEGAL 2 needs MONEY 1's figures”), and any change to N with its reason.
- The handover section says where the session stands, what was decided in the owner's own words, the next move with its start line, and where the results are, as links the owner can open on a phone, never a file's place on a computer.
- Write either page with `write_page`: a fresh `request_id`, the `title` from the card, `words`, `mode` (`create` only after `read_source` on its path finds no page there, `append` afterwards) and `author` `counterpart`, because the page is this counterpart's account; quote the owner's own decisions inside it as theirs.
- File the plan under the project once, after the page exists: `file_page_under_project` with a fresh `request_id`, `page` (the page reference, the path without the folder or `.md`), `project` (the project's `id` from `list_projects` with `format` `json` and `ids` true) and `words` (the owner's own words that asked for or agreed to the plan, exactly as said). The page then shows on the project in the owner's app; later sections need no new filing.

## The lane card

Write it with `report_thread`:

- `name`: `PROJECT · LANE` exactly, with no session number, because a search for the next session must still find it.
- `project_id`: the project's id, once the project exists.
- `stage`: begins `Session n of N:` and says where it stands. It is never the single word RUNNING, which the record refuses.
- `next_move`: the exact line to say next, for example `say "continue NEW ALBUM MIXING 2"` or `say "start NEW ALBUM MIXING 3"`, with `whose_move` and, when known, `next_move_on`.
- `open_loops`: `PLAN: title | path`; `HANDOVER: title | path`; `PLAN READ AT PICKUP: …`, the whole opening line of the plan section this session started from; `HELD BY: …` while a chat holds the lane; `SAFE TO CLOSE: yes` or `SAFE TO CLOSE: no, what is still unsaved or waiting`; `PLAN UPDATE WAITING: …` while a plan section waits for approval (see below); and `Formerly: old name` on a renamed card.
- `references`: `{kind: "project", id}` and, when there is one, the next session's task.
- `evidence`: at least one entry: `conversation` for this session, `artifact` with the page path for each page written, each with its `reference`, `summary` and `at`.
- `expected_revision` 0 without `thread_id` makes a card, and only when the lookup below found none for the lane; otherwise send the card's `thread_id` and the `revision` last read. A refusal for a stale revision means another chat changed the card: read it again, tell the owner what changed, and never send the older words over it.
- Money, legal and health matters and anything from a private archive stay off the card, as in the rest of this skill; a lane about one of them has a card naming the lane and the next move only.
- A lane is marked done only when its last session ends, with `update_thread` on the owner's words. A card marked done is final, so a lane that comes back later gets a new card.

## Finding the work by name

When the owner says “continue [name]”, “start [name]”, «continua [nome]», «riprendi [nome]» or «inizia [nome]», the name is PROJECT and LANE, sometimes with n, in any letter case, with or without the dot. Compare names ignoring letter case, the dot, hyphens and extra spaces, and always at whole words: ALBUM never matches inside ALBUMS.

1. **Every project reading.** Call `list_projects` with `format` `json` and `ids` true. Each project whose whole name equals the first words said gives one reading, with the words after it as the LANE and n. Keep every reading: with projects called ALBUM and ALBUM MIXING, “continue ALBUM MIXING” is both ALBUM MIXING with no lane said and ALBUM's MIXING lane.
2. **Each reading's cards.** For each reading's project, call `read_threads` with its `project_id` and `lifecycle` `all`, then with `query` set to the project's name, following `next_cursor` as `cursor` until it comes back empty; when a page's `coverage` says `changed`, read again from the start once. The search matches the typed letters anywhere in a card's name, lowercased, so the query carries the project's name alone: the owner rarely types the dot that sits between project and lane. A card belongs to the project only when its `project_id` is that project's `id`, or when it has no `project_id` (its project still waits for approval) and its name, after any leading label, is the project's name, the dot, then the lane. A card carrying another project's id never counts, whatever its name says.
3. **One reading must stand.** A reading stands when its project has a card or a plan row for the lane said, or when no lane was said and the project has exactly one live lane. When more than one reading stands, give the short choice below; when none stands but a project matched, say so and offer its lanes or a new lane. When no project matched at all, go to the closest names below.
4. **Read the pages.** Take the titles and paths from the card's open loops, or work them out from the two titles when the card has none. Read each with `read_source` to its end, passing `next` back as `from` until `next` is absent, because the newest section is last, and keep each page's `modified`. Check each newest section's opening line against the project and lane before believing it, and write the plan's newest opening line, whole, on the card as `PLAN READ AT PICKUP` at the first turn of work.
5. **Say it first.** Before doing anything else, say in plain words where it stands (the plan's newest section, the card's stage, the handover's newest section), this session's finish line and the next move, so the owner can see the pickup is right. Then begin.

The lookup never asks the owner for an id, a link or a chat, and never picks one silently:

- **Nothing matches:** build the candidates first: every project from `list_projects` (with `include_finished` true as well, saying which are finished), and every card from `read_threads` with `lifecycle` `all` and no query, following `next_cursor` to the end. Then give the closest names among them, those sharing a word with what was said or spelt one or two letters away, and ask which they meant, or whether to set it up as new work. When a read stopped early or its `coverage` said `changed`, say that the list of near names may be incomplete.
- **More than one fits:** two projects, two readings or two cards could be meant. Give one short choice listing each with its stage and date, and wait.
- **Two cards for one lane:** the trail has split. Show both and ask which one carries on; the other is marked done on the owner's words.

## When the card and the plan disagree

The plan page is the authority, because it is the one record every session updates in the same way, with the owner's yes behind it; a card is one chat's reading. Read both, say what each says, say which wins and why, and never settle it silently.

- **A stale card:** the card's `observed` time from `read_threads` is older than the plan page's `modified` from `read_source`, or its session number is behind the plan. The plan wins; bring the card in line with it at the first turn of work.
- **A card ahead of the plan, or saying something else:** for example the card says a session finished that the plan still shows as RUNNING. The plan stands until it is brought up to date; offer to append the newer state on the owner's yes, because a card alone never changes the plan.
- **No plan page at its path, or one that is another project's:** say so plainly. The card and the handover are all there is; offer to write the plan from them on the owner's yes, and until then nothing is called the plan.

## Every plan snapshot is a merge by lane

Other lanes append to the same plan while this session works, and a page cannot refuse a section written on an older plan. The newest section can itself be a snapshot built on an older plan, so it is never copied forward as it stands. Each row of the plan's table belongs to the lane in its Lane column, and so do that lane's handover title and any change to its N: only that lane's sessions change them. The needs between lanes belong to no lane.

Every snapshot (at a close, at a halfway close, and after a waiting update is settled) is built the same way:

1. **Read it fresh.** Read the plan page again with `read_source`, to its end, immediately before building the snapshot, and list every section's opening line.
2. **Name it.** k is the highest update number on the page plus 1, and the section it is built on is the newest one on the page; both go into its opening line, with this lane and session.
3. **This lane's rows** come from this session's work.
4. **Every other lane's rows come from that lane's own newest section:** the newest section that lane wrote, or that carried its waiting changes; when the lane has written none, from the newest section on the page. A section is never the source of another lane's rows because it is newest, so a stale snapshot is never copied forward.
5. **The lines no lane owns** start from the section recorded at pickup and take every change each later section made to them (what differs between that section and the section its opening line says it was built on), with this session's own changes. When two sections changed the same line differently, stop, show the owner both, and ask which stands; never pick one silently.
6. **Write it** with `write_page`, `mode` `append`, and say in one line when other lanes' work arrived since pickup and was kept.
7. **Read back and verify.** Read the page with `read_source` once the section is on it, and check line by line that each other lane's rows in your section equal that lane's own newest section now on the page, that every change to the lines no lane owns is there, and that no other section sits between the one you built on and yours or carries your update number. When any check fails, say which, and append one reconciled section built by steps 1 to 6, its opening line merging every section it took rows from; then read back and verify again.
8. **Record it.** Put the whole opening line of the section now in force on the card as `PLAN READ AT PICKUP`, because any later snapshot of this session starts from it.

## A plan update waiting for approval

On a door that holds acts for approval, a plan section can wait there while the page still shows the older plan. A second snapshot built on that older plan would undo the waiting one the moment both are approved, so:

- Before sending any plan section, call `list_pending` where this door offers it and read the card's open loops. When a plan section for this project is still waiting (its words open with `Plan for PROJECT, update`), or the card says `PLAN UPDATE WAITING`, send no new plan section. Say that the earlier update waits for the owner's approval, and keep this session's changes on the card instead, as `PLAN CHANGES NOT YET IN THE PLAN: …`.
- After sending a plan section that is held, write `PLAN UPDATE WAITING: update k by LANE session n, sent dd/mm/yy` on the card.
- The first chat that finds the waiting update applied (on the page) or declined (gone from `list_pending`, and not on the page) takes the waiting note away and, on the owner's yes, appends one snapshot by the merge above that carries the full set of changes still waiting: each lane card's `PLAN CHANGES NOT YET IN THE PLAN`, applied to that lane's rows as step 4 takes them, its opening line naming every lane whose waiting changes it carries. Its read-back verifies, as a written step, that each lane's rows equal that lane's own newest section with that card's listed changes on top, and only then takes the listed changes off each card. The plan in force is always the newest section actually on the page.

## Holding a lane

Sessions run one after another, one chat at a time.

- At its first turn of real work, the chat writes `HELD BY: the session n chat, since dd/mm/yy hh:mm` and `SAFE TO CLOSE: no, the session is under way` in the card's open loops, and takes HELD BY away at its last turn.
- HELD BY is a note, never a lock: two chats can still both write the card. A chat that finds another chat's HELD BY says so plainly, “Another chat has held this lane since dd/mm/yy hh:mm and may still be open”, and asks the owner what to do: carry on here, in which case the note is replaced and the card says the lane was taken over on the owner's word, or leave it to the other chat. It never takes a lane over on its own.

## Starting or continuing a session

- **An unfinished session comes first.** When the lane has a session that is UNFINISHED, or RUNNING with nobody holding it, “continue …” resumes that session under its own number, from its handover. “start …” for that lane says the session is unfinished and asks whether to carry it on or close it as it stands before the next one begins.
- **Otherwise, with a plan:** n is the lane's NEXT session in the plan. When the owner names another number, say what the plan shows and ask. Without a number, take the NEXT session.
- **With no plan yet:** propose it in plain words: the lanes, each session with its finish line, N or "?". On the owner's yes, in this order, reading each answer before the next act: the project with `make_project` (`request_id`, `name` as the owner said it), only when `list_projects` has no project by that name; the plan page; its filing under the project; the lane card. On a door that holds acts for approval each of the first three waits for the owner's approval there: say what waits, write the card with `report_thread` without `project_id` meanwhile, and add the project once it exists.
- Then put this session's finish line on the card and start the work.
- Consent follows the room instruction's FILING rule. Where it asks once, the owner's yes to running the work in sessions covers the plan and handover updates of that project's sessions; where it asks every time, ask in one line at the session's close.

## Closing a session, the same way every time

1. **The plan:** unless an earlier update still waits (see above), append the whole plan as it now stands, built by the merge above on a fresh read of the page. A session that reached its finish line is DONE and the next one NEXT, with N changed and its reason, said to the owner as “now 2 of 6, because …”. A session that stops before its finish line is UNFINISHED, and NEXT does not move.
2. **The handover:** append a section with `write_page` to the lane's handover (`mode` `create` the first time, after `read_source` finds nothing at its path), opening with its identity line. For an unfinished session it says exactly where the work stopped.
3. **Read both back** with `read_source`, so “saved” is said only of what is actually on the page; for the plan this is the verify step above.
4. **The card,** with `report_thread`: `stage` `Session n of N:` with what was done, HELD BY taken away, and `next_move` the next start line: `continue PROJECT LANE n` for an unfinished session, `start PROJECT LANE n+1` after a finished one. Write `SAFE TO CLOSE: yes` only after step 3 found both sections on their pages; otherwise `SAFE TO CLOSE: no` with what is unsaved or waiting for approval.
5. **The owner's list:** after a finished session, offer the next one as one task with `make_task`: a fresh `request_id`, `title` `PROJECT · LANE n/N · YOU (minutes to start, what closes it): say "start PROJECT LANE n" - finish line`, `project` the project's name, and a `deadline` or `aim` on the earliest date it can really be done, never today by default. Read `list_tasks` with that `project` first so the session is never put on the list twice. Only the next session of each lane goes on the list; a session that waits on an event stays in the plan with its watcher. A date already recorded moves only on the owner's word.
6. **The last line,** only after step 3: “Next: start PROJECT LANE n+1, date or event. You can close this chat now.”, or for an unfinished session “Next: continue PROJECT LANE n. You can close this chat now.” When something is not saved, say what instead.

## “Where are we on PROJECT?” / «A che punto siamo con PROGETTO?»

Read the plan's newest section, the project's lane cards and its tasks (`list_tasks` with `project`), and answer with one short board: each lane at its n/N, what needs the owner, what is unfinished, what runs without them, what is parked and until when. A lane with no card yet has simply not started.
