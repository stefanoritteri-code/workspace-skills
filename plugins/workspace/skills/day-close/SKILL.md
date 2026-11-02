---
name: day-close
description: "Close the owner's working day. Use when the owner says — English: “close the day”, “Close the day.”, “shutdown”, “wrap up”, “wrap up today”, or that they are done for today; Italian: «chiudiamo la giornata», «chiudi la giornata», «fine giornata», «per oggi ho finito». The board, the waits and the machinery are read first; two questions; decisions, the journal line, tasks and waits filed, tasks closed and waits lifted through the door on the owner's yes only; nothing said today left unfiled without asking; tomorrow proposed; then the push stops. Also answers to its former name, “close the day”."
---

# Close the day

A habit that takes a few minutes and ends with the push switched off. Speak as the counterpart the room instruction names, in the owner's language from its preamble: plain words, verdict first, first-person plural, no recap openers, no emoticons, no ids on the surface. Who the owner is, their rhythm and what they protect come from the preamble and their planning rules, never from this file.

Before the first question, say in one sentence what you are about to do — “I'll read the board, then two questions.” / «Leggo la bacheca, poi due domande.» The reasons written into this file — what went wrong on a given date — are for whoever maintains it and are never spoken.

Where the room instruction's preamble says this room FILES WHAT IS CLEAR, each “ask once” below becomes: file what the conversation makes plain and read the receipt back, asking first only when it is unclear what the owner meant.

A note on a person filed here carries `author: owner` when the words are the owner's and `counterpart` when they are ours; ask which if it is not obvious from how they said it.

Request ids for every write: letters, digits and hyphens, at least eight characters, INVENTED FRESH for each thing filed — today's date and a few random characters, never an id copied from this file and never one from an earlier day. ⛔ The first request accepted under an id wins and the words are not compared, so a new thing sent under a used id is answered with the old receipt and NEVER WRITTEN, and the room would say it is on the board when it is not. Reuse an id only when retrying the very same call. Read [landing.md](references/landing.md) before the first write.

## 0. Read the board first

Call `standing`, then `list_tasks` (following `next` to the end, with no write in between; use only the fields this door's tool offers) and `list_waits`, and then `status`, BEFORE the first question, and hold what they say for sections 3, 4 and 6. `standing` opens every conversation about the owner's work, and a night with nothing decided would otherwise propose tomorrow having never read the rulings.

⚠ THIS IS WHERE A CLOSE GOES BLIND. A close once reported "nothing waiting on anyone else" while the wait it had opened forty-five minutes earlier, in the same conversation, was open in the store. So what is open and what is waiting come from these calls and from nowhere else — never from memory, never from what this conversation happens to have filed, never from silence. If either call is refused, say so in one line and do not assert that anything is or is not outstanding. Both are capped: when either says it showed some of more, say so rather than presenting the part as the whole.

`status` is the same rule for the machinery: nothing about how the system is, whether an engine ran, or whether anything needs the owner overnight is said before that call. Where the preamble says the owner watches an engine room, its three answers stay three: an engine is quiet (not named at all), loud (its own sentence read back), or its status could not be established — which means it was NOT read and is never called fine or clear; if it says the machinery is not reachable from this record, say that in one line and assert nothing else about it. Where the owner has no engine room, the call is still made and nothing about machinery is said unless its answer carries something, or the sign-in line says it is short.

## 1. The two questions, one at a time

Ask, and wait for the answer to each:

1. “What moved today?” / «Cosa si è mosso oggi?»
2. “What did you decide today, if anything?” / «Cosa hai deciso oggi, se qualcosa?»

If the owner answers both in one message, take them as answered. “Nothing” / «niente» to either is an answer. Any further question serves an actual filing choice, never a closing ritual.

## 2. What the owner decided

For each thing they state as decided:

- Call `standing`, then `search_records` with state `live` and the key words, and again with the words a newer decision would use. Say in one line what those searches found, or that they found nothing; if the door could not search, say that, leave the gap open, and file nothing on that subject tonight.
- If a live decision on the same subject came back, the question names the replacement: “This replaces the decision of dd/mm/yy, '…'. File it as the replacement, in your words: '…'? Reason: '…' or none.” / «Sostituisce la decisione del gg/mm/aa, "…". La archivio come sostituta, con le tue parole: "…"? Motivo: "…" o nessuno.» If no live decision came back: “File it? In your words: '…'. Reason: '…' or none.” / «La archivio? Con le tue parole: "…". Motivo: "…" o nessuno.» If the matching decision is standing, say it cannot be replaced from here and file nothing.
- Use the owner's words as they said them. If they run past what the door accepts (a few sentences), ask for the short form and file that.
- Name a project only when the owner names it or the search shows it. If the door refuses the project, ask how it reads on the board and try once more.
- On their yes and only then: `supersede_decision` with that record's id when it is a replacement, otherwise `record_decision`. An explicit ask to keep it was already the yes.
- Read the receipt back in the owner's words, never by id. A refusal is said as the refusal it is and that item stops. Not confirmed means search the record before any retry.
- If they mark something tentative, or ask what you think, nothing is filed and you say so. Never file your own suggestion.

## 3. What moved, and what to do

- Say what moved back in two or three lines, in the owner's words. Check `list_journal` so the same line is not filed twice, then ask once: “File that as today's journal line?” / «La archivio come riga di diario di oggi?» On their yes, `journal_note` with those words and author `owner`.
- If something they named as moved is a task on the board, ask once: “Mark [task] done?” / «Segno [task] come fatto?» On their yes, `close_task` with the title as it reads there, and the project too when the door says more than one task shares the title. A task with an open wait closes with the wait still on it, and the receipt says so: finishing the work is not the thing arriving. A refusal — already done, dropped, more than one by that name — is read back as a refusal and that item stops; never send the same call again.
- If they say something they were waiting for has arrived, ask once: “Lift the wait on [who] for [task]?” / «Tolgo l'attesa su [chi] per [task]?» On their yes, `release_wait` with the task and the full `waiting_on`; if the tool asks for confirmation, get the owner's before sending `confirm: true`. A wait already lifted says so with its date; read that back and file nothing.
- If they name something to do, ask once: “Put it on the board under [project]?” / «La metto in bacheca sotto [progetto]?» On their yes, `make_task` with their title, and the project only if they named one. A date is an `aim` unless they promised it to somebody outside, which is a `deadline`; never both, and never an invented date.
- If they say they are waiting on somebody or something — a person, a delivery, an invoice, an answer — ask once: “Mark [task] as waiting on [who or what], because [why]?” / «Segno [task] in attesa di [chi o cosa], perché [motivo]?» A wait hangs on an open task: when there is none, make the adopted task first and wait for its receipt. On their yes, `open_wait`, with `because` in their words. The receipt says whether the person has a card here; if none, say so in one line and offer the card — `make_person`, on their yes, with their own line on who the person is and how they are reached if they say. The wait holds either way, so the card is an offer and never a condition.
- A note on a person: read `list_people` and their file first, then `note_person` on the existing card, following the room instruction on where a note goes.

## 3a. Two rounds of buttons, with ticks

The asks of sections 2 and 3 and the sweep of 3b are put to the owner as two rounds of Claude's question buttons, several picks allowed (ticks), in their language; read [claude-native.md](references/claude-native.md) for the buttons and their fallback. Every rule above still decides what each act needs: a decision's exact words, its replacement named, its reason; anything still unclear — which project, which wait, author — is asked in words before the round, never guessed into an option.

- **Round one, after sections 2 and 3:** “What shall I file?” / «Cosa archivio?» — one tick per prepared act. The question itself sets out, numbered, exactly what each act will file: the decision in the owner's words (and, for a replacement, which decision it replaces, and the reason), the journal line, the task to mark done, the wait to lift, the new task, the new wait. Each option is that number and a few words naming the act, so a short label never stands for words the owner has not seen in full.
- **Round two, the sweep of 3b:** “File these? Tick what goes on the board.” / «Li archivio? Spunta cosa va in bacheca.» — one tick per open commitment found.

Where the room FILES WHAT IS CLEAR, the rounds carry only what is unclear. A tick is the owner's yes to the exact words set out for that option and nothing more; what is left unticked is not filed and is said back. File the ticked ones in order, reading each receipt back before the next; a refusal stops that item and anything that hangs on it — a wait whose task was not made is not opened, and never on a task with a similar name. When more acts are waiting than fit on one question, the rest go in a numbered list answered in words, in the same round.

## 3b. The sweep — nothing lives only in this conversation

Before tomorrow is proposed, read back through everything the owner said today — in the two questions and in passing — and list, in one message, every piece of work, deadline, person or wait they named that is NOT on the board or in the record: the brief somebody brought with its submission date, the person still to find, the call they mean to make. Genuine open commitments only, never every passing idea. Then ask once, as round two of section 3a. File each one ticked with `make_task` in their words — `deadline` when the date was promised to somebody outside (a submission date is one), `aim` when it is their own — under the project they named, reading each receipt back before the next. Anything they leave out is said back as “kept only in this conversation, and gone tomorrow” / «resta solo in questa conversazione, e domani non c'è più», because that is the truth of it. A brief told once only to a close, with its due date, lived in the room's notes and the next morning could not see it: the close is where the day's words become the record's, or they are lost.

## 4. Tomorrow, proposed

Read tomorrow with `read_day` and the owner's live planning rules (`search_records`, `tag` `scope:planning`, `state` `live`, `limit` 50) before mentioning it: an accepted day for tomorrow is read back, never proposed over. Otherwise, from the board, the record and the conversation only — and if either read in section 0 was refused, say so on that line rather than filling it from the conversation — propose in up to three lines: the one deep thing for tomorrow, in the owner's deep-work window; up to two small things for the window their rhythm gives to small work; anything waiting on someone else, with what it waits for and since when. If the record gives nothing for the deep thing, ask what it is instead of naming one. If tomorrow is a rest day by the preamble's rule, propose it only if the owner has said they are working it or asks; never refuse or flag rest-day work they have chosen. Read tomorrow's calendars by CALLING the calendar tool this project holds, and name first anything touching the people or time the preamble protects; “the calendar is not connected here” / «il calendario qui non è collegato» is said only when there is no such tool or the call came back refused, and an all-clear is never asserted unread. Save a whole day only when the owner asks for it, following [day-record.md](references/day-record.md); three conversational lines are not a saved proposal.

## 5. The moment

When there is room and the owner is not tired, ask once: “Anything from today worth keeping as a moment?” / «C'è qualcosa di oggi che vale la pena tenere come momento?» If they give one, say it back in one line and ask once: “File it?” / «La archivio?» On their yes, `journal_note` with their words and author `owner`. Never infer feelings, family structure or relationships.

## 6. Close

Report what moved, what was filed, what is open, what is waiting and on whom, and what is tomorrow, in that order, in plain words and without ids. ⚠ IF ANYTHING AT ALL WAS WRITTEN TONIGHT — a task made, a wait opened, a task closed, a wait lifted — call `list_tasks` and `list_waits` AGAIN and report what they say now. The section 0 lists were read before those writes, so reporting from them is the same blindness one step later. Only when nothing was written do the section 0 lists still stand. Name held or uncertain acts as such.

Then, where the owner watches an engine room, the machinery from the `status` call: **as many lines as there are loud engines, each in its own words**, and then how many could not be established, with the reason. ⛔ NO LENGTH BUDGET HERE, and that is deliberate: a budget written beside a fidelity rule wins, and the read would keep two engines and drop the rest. One evening seventeen engines were loud at once, and a budget would have dropped most of them. Never softened, never merged, and never a claim that anything is fine. An engine loud and stale is said as both. Engines and flags are the operator's; read the findings here, and when something is the operator's, follow the room instruction: say it once, do what can be done here, offer once to file it.

Any offer to file an engine finding comes before this and is answered first. Then call `show_today` once, so the owner sees the day's page in its evening state; where that tool is not in this conversation, say nothing about it. Then the closed ending, one line and nothing after it: “The day is closed.” / «Giornata chiusa.» Then stop. No push at close of day; no “one more thing”, no question, no button.

## How the room learns

When the owner corrects the close and asks you to keep it, the room instruction's KEEPING AND RULES files it as a rule with its scope. The first time they correct something here, say it once — “When you correct me and say «remember that», I file the rule in your words and read it back.” / «Quando mi correggi e dici “ricordatelo”, archivio la regola con le tue parole e te la rileggo.» Read [access.md](references/access.md) for how calendars and mail are read.

## Tools

Reads: `standing`, `search_records`, `list_tasks`, `list_waits`, `list_journal`, `list_people`, `read_source`, `read_day`, `search_work`, `status`; `list_pending` only where exposed. Writes, each on the owner's yes: `record_decision`, `supersede_decision`, `journal_note`, `close_task`, `release_wait`, `make_task`, `open_wait`, `make_person`, `note_person`; `propose_day` and `accept_day` only when the owner asks to save tomorrow. Calendars through the connector.

<tone_preference>Keep outputs reasonably concise. One question at a time. Plain words, in the owner's language, no ids. End by stopping.</tone_preference>
