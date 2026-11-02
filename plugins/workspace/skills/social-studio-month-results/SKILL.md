---
name: social-studio-month-results
description: "SOCIAL STUDIO: MONTH RESULTS. Reads a brand's last month on social media from Metricool against the month before, every number beside its previous month, and says in three sentences the best post, one thing to stop and one to try. Asks which posts past their date really went out and marks only those done, writes the month into the campaign's overview, files the lessons as rules the next drafts follow, adds a dated “what worked” section to the brand file, and in the first months asks whether the look still feels right. Use when the person says “what did last month's posts do”, “how did social go this month”, “read the month”, “social results”; Italian: «com'è andato il mese sui social», «leggiamo il mese», «i risultati social del mese». An empty month is said plainly, never filled with an invented number. Ends by offering next month's plan."
---

## Before anything else: is this skill on here?

Before doing any of this skill's work, call the door's `skill_switch` tool with `skill` set to `social-studio-month-results`.

- Carry on with the skill below ONLY if the answer says this skill is a core skill, or that it is on in this workspace.
- If the answer says it is off: stop here. Tell the owner, in their language, that this skill is switched off in this workspace, and do nothing else from this skill.
- In every other case (no answer, an error, the tool is not available, the answer says the switch could not be read, or any answer you do not recognise): stop here. Tell the owner plainly that the skill switch could not be read, so this skill was not used.

# SOCIAL STUDIO: MONTH RESULTS

The monthly read, and the loop that makes next month's drafts better. The numbers stay in Metricool; what comes back into the records is three sentences, the month's account on the campaign, and the lessons as rules. A number is never given alone: it always has last month's number beside it, because a number without a baseline cannot be judged.

Speak as the counterpart the room instruction names, in the person's language: plain words, verdict first, first-person plural, dates dd/mm/yy. **One beat per turn.** No action name, id, tag, code or metric code reaches the person; say "reach", "saves", "the Friday post".

Read [landing.md](references/landing.md) before any write and [claude-native.md](references/claude-native.md) for the buttons. On a door that holds acts for approval, every write waits for the owner's yes there; never say one landed before its receipt.

Open with one sentence: “I'll read last month and the month before from Metricool, then we see what worked.” / «Leggo da Metricool il mese scorso e quello prima, poi vediamo cosa ha funzionato.»

## 1. Which brand, which months

1. `list_projects` with `ids: true`; brands are the projects ending in ` SOCIAL`; several and none named: ask which. One brand per read.
2. The brand's line: `search_records` with `text: "SOCIAL BRAND: <BRAND>."`, `state: "live"`, no tag; its words name the brand's rule tag (never build it), the Metricool brand number and time zone. Then `search_records` with that `tag`, `state: "live"`, `limit: 50`: the rules, the outcome and its baseline, any `SOCIAL TRIAL`.
3. The month: the last whole calendar month, unless the person names another, and the month before it. Say both in one line: «Ottobre 2026 contro settembre 2026.»
4. Metricool's `getBrandSettings`: confirm the brand number and take the time zone and networks.

## 2. The numbers

For each network: `getAnalyticsAvailableMetrics` with the network and `connector: "posts"`, and **for Instagram also `connector: "reels"`**, because Metricool keeps reels in their own source (Instagram feed posts are the `IGPO…` fields, reels the `IGRE…` fields: date, content, reach, saved, shares, interactions, views); for any other network, ask for its metrics with no connector and read every post source it lists. Then the account-level connector it offers, such as followers over time. Then `getAnalyticsDataByMetrics` with the brand number, the metrics listed for each source, leaving out any Metricool marks deprecated (never two sources in one request), and `from`/`to` covering each of the two months in the brand's time zone: one read per source per month, the same metrics in both months.

A reel is a post. Posts published, the best post and the per-post average count feed posts and reels together, and a month with only reels is not an empty month. Where a measure exists for one source and not the other, say which posts it covers.

Then, from what came back and nothing else:

- **The month against the month before**, for the few numbers that matter to this brand's outcome: posts published, reach, engagement, saves, followers gained, link clicks where the brand drives to a shop or a booking page. Each one as «reach 4,210, against 3,380 in September». When a number came back for one month and not the other, say it cannot be compared and why; never estimate it.
- **The best post**, by the measure that serves the outcome, with its number beside the previous month's best post on the same measure and the previous month's average per post («reach 1,240; September's best was 860, its average 410»).
- **One thing to stop, and one to try.** Each in a sentence, from the posts themselves (the format, the time, the theme, the words), and each with the number that shows it beside the same number for the previous month («reels averaged 620 reach this month, against 540 in September; single pictures 210, against 300»). When the previous month has no posts of that kind, say the comparison cannot be made rather than give the number alone. When the month is too thin to say, say so.

**An empty month is said plainly**, only when every post source, reels included, came back empty: «A ottobre Metricool non riporta post pubblicati per questo brand, quindi non c'è niente da confrontare.» No number is invented, and no lesson is drawn from nothing.

When it helps the person to see it, and Claude offers a Dashboard here, show the two months on one Dashboard page, every number with its source named as Metricool and its month, beside the three sentences. Without one, a short table in the chat.

## 3. Which posts went out

Metricool's scheduled list leaves out published posts, so this skill cannot see what was published. `list_tasks` for the brand's campaigns, `format: "json"`, `ids: true`: name the posts whose date has passed and that are still open, and ask the person which went out, on the buttons where there are few. **Only the ones the person confirms** are closed: `close_task` with `task` the post's title and `project` the campaign. A post they say did not go out stays open; offer to move it, which is METRICOOL HANDOVER («sposta il post di sabato a lunedì»).

## 4. Keep the month

Show what will be kept, then on the person's yes:

**The campaign's overview.** `read_reading` with `subject: "project"` and `key` the campaign's project id, to get its current revision and its brief. Then `keep_reading`, `subject: "project"`, `key` the same id, `expected_revision` the revision `read_reading` returned (0 if none), `words` the overview's prose with the month's account added (the three sentences and the comparison), and `brief` sent again, carried exactly as `read_reading` returned it — the same purpose, `next_dated` and `waiting_on` — with one line added to `where_we_are` for the month (at most four lines; replace the oldest month's line when full). The brief must be sent again: an overview kept with prose only loses its brief (measured in the records' code 22/10/26). When the revision has moved since the read, read again and show the change before keeping.

**The lessons as rules.** Each lesson the person accepts, one per decision, in their words or in our wording they approve: `record_decision`, `words` the rule («Reels with a face in the first second: keep them at two a week»), `why` the numbers that show it, `tags` the brand's tag from its line. A lesson that changes a live rule is a `supersede_decision` of that rule, with its real `old_id`. Lessons the person does not accept are not filed.

**The brand file's "what worked".** `read_source` with `path: "pages"` to list the saved pages, open the `brand-file-…` page titled exactly `BRAND FILE <BRAND>` (never build its path), and count its sections headed `## WHAT WORKED`. Then `write_page`, `mode: "append"`, `author: "counterpart"`, title exactly `BRAND FILE <BRAND>`, one section `## WHAT WORKED — <MONTH YYYY> — dd/mm/yy` with the comparison, the best post, the stop and the try, and the lessons filed.

**The early check-in.** While the brand file holds three or fewer "what worked" sections, counting this one (about days 30, 60 and 90 after the first session), ask once: “Does the look still feel right?” / «Lo stile ti sembra ancora giusto?» A no is the cue for SOCIAL STUDIO: BRAND («cerchiamo un nuovo stile»); this skill changes no look. When a live `SOCIAL TRIAL` ended this month, say so and name BRAND for adopting or restoring.

## 5. Close

One short paragraph: the two months compared in one line, what was kept (the overview, the rules, the brand file section), what is held for approval, which posts are now done and which stay open. Then offer next month: “Shall we plan next month? Say plan this month's posts.” / «Pianifichiamo il mese prossimo? Di' pianifica i post del mese.» Last, when the month was kept, call `show_social_month` once so the person sees the month at a glance; where that tool is not in this conversation, say nothing about it.

## Never

- Give a number without the previous month's beside it.
- Invent a number, or draw a lesson from an empty month.
- Close a post the person has not confirmed went out.
- File a lesson the person did not accept.
- Change the look; that is BRAND's, on the person's words.
- Keep the numbers in the records beyond the month's account: they stay in Metricool.

## Tools

Reads: `skill_switch`, `list_projects`, `list_tasks`, `search_records`, `read_reading`, `read_source` (to count the "what worked" sections); Metricool `getBrandSettings`, `getAnalyticsAvailableMetrics`, `getAnalyticsDataByMetrics` for two months. Writes: `close_task`, `keep_reading`, `record_decision`, `supersede_decision` (a lesson that changes a live rule), `write_page` `mode: "append"` (one dated "what worked" section per run).

## What the figures may not carry

Metricool's post analytics may not return every field, and which fields each network's sources carry is measured for Instagram only. Meanwhile: name only what came back and say what did not; name "the best post" by its date and first words when the reply carries no picture.
