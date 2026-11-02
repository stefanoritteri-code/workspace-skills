---
name: social-studio-month-plan
description: "SOCIAL STUDIO: MONTH PLAN. Plans a month, a release, a tour or a season of social posts for one brand: reads the brand's rules, the dates that matter (releases, launches, events already on the record) and Metricool's best times to post, proposes a calendar with one dated post per line, and on the person's yes makes it as one campaign with a task per post, so every post shows on the day, the week and the projects pages beside the rest of the work. Adds a single post to a campaign already made. Use when the person says “plan this month's posts”, “a social calendar for the new single”, “a social calendar for the tour”, “plan next month on social”, “add a post on Saturday”; Italian: «pianifica i post del mese», «un calendario social per il nuovo singolo», «un calendario social per il tour», «aggiungi un post sabato». Never touches the Metricool schedule; drafting the words is SOCIAL STUDIO: POSTS; planning the music release is the music skill, whose release posts come in here."
---

## Before anything else: is this skill on here?

Before doing any of this skill's work, call the door's `skill_switch` tool with `skill` set to `social-studio-month-plan`.

- Carry on with the skill below ONLY if the answer says this skill is a core skill, or that it is on in this workspace.
- If the answer says it is off: stop here. Tell the owner, in their language, that this skill is switched off in this workspace, and do nothing else from this skill.
- In every other case (no answer, an error, the tool is not available, the answer says the switch could not be read, or any answer you do not recognise): stop here. Tell the owner plainly that the skill switch could not be read, so this skill was not used.

# SOCIAL STUDIO: MONTH PLAN

A month of posts, planned once, so the week only has to draft. The plan is a calendar the person can read in ten seconds: which day, which network, what time, what each post is for. On their yes it becomes one campaign with one dated task per post, and from then on every post sits on THE DAY, THE WEEK, THE WORK and PROJECTS with the rest of their work.

Speak as the counterpart the room instruction names, in the person's language: plain words, verdict first, first-person plural, dates dd/mm/yy. **One beat per turn.** Propose the whole calendar; composing is our job and choosing is theirs. No action name, id, tag or post code is spoken as a code: say "the Friday post", and let the code live in the title.

Read [landing.md](references/landing.md) before any write and [claude-native.md](references/claude-native.md) for the buttons. On a door that holds acts for approval, the campaign waits as one act on the approval page; say so, and never say it is made before the receipt.

Open with one sentence: “I'll read your rules, the dates coming up and when your audience is online.” / «Leggo le tue regole, le date in arrivo e quando il tuo pubblico è online.»

## 1. Read before proposing

1. **The brand.** `list_projects` with `ids: true`; brands are the projects ending in ` SOCIAL`. None: offer «set up my social media» / «iniziamo con i social» and stop. Several and none named: ask which, on the buttons. One plan is for one brand.
2. **The rules.** First the brand's line: `search_records` with `text: "SOCIAL BRAND: <BRAND>."`, `state: "live"`, no tag; its words name the brand's rule tag (never build it) and whether it is the only brand here. No line: offer «set up my social media» and stop. Then `search_records` with that `tag`, `state: "live"`, `limit: 50`. From them: the channels, the cadence, the themes, the never-dos, the rhythm (for the only brand in a workspace, also `search_records` with `tag: "scope:planning"`, text `SOCIAL RHYTHM`), any live `SOCIAL TRIAL`, and the `SOCIAL BRAND` line with the Metricool brand number and time zone.
3. **The dates that matter.** `list_projects` and `list_tasks` (with `window: "this-week"` and bare, and `project` for a release or tour named in the request) for release days, launches, gigs, openings, deadlines already on the record. Ask for any the person mentioned that the record does not hold; never invent one.
4. **The campaigns already running.** The brand's other campaigns and their open posts, so the plan does not double a day.
5. **A release the release plan already planned.** When the request is for a release (“a social calendar for the new single”) and the release plan made its project, that project already holds the release's posts. They are never planned again: follow [release-posts.md](references/release-posts.md) to bring them in, and the release project is that release's campaign.
6. **The best times.** Metricool's `getBestTimeToPostByNetwork`, for each network in the plan, with the brand number, the brand's time zone, and a range of at most one week (ask for the coming week; the shape repeats). Check the number and the time zone against `getBrandSettings` first. When Metricool is not connected or refuses, say so in one line and propose times from the rules, called our suggestion.

## 2. Propose the calendar

One table, one line per post, in date order:

| Post | Day | Network | Time | What it is | Theme |
|---|---|---|---|---|---|
| Friday's post | Fri 07/11/26 | Instagram | 18:00 | Single out now: the cover and one line | Release |

Rules for the proposal:

- Follow the brand's cadence and channels exactly. When the request asks for more than the cadence (a release week), say so and propose the extra posts as extra.
- Times from the best-time read, rounded to the quarter hour, in the brand's local time, with the reason in a clause on the first line it applies to («18:00, when your audience is most online on Fridays»).
- Every post serves one theme and, where the brand has an outcome, says how it moves it.
- No date in the past, ever: the first post is tomorrow at the earliest, unless the person asks for today and today's time is still ahead.
- If the brand is on Metricool's free plan, it allows twenty posts a month: when the month's plan alone would pass twenty, say so before the yes, and that drafts may count too. (Measured on one free account, 21/10/26.)
- When a live `SOCIAL TRIAL` covers these weeks, say the posts are part of the trial.
- When something visibly crowds the plan (the person's own release week, a tour), say what you'd leave out.
- For a release the release plan already planned, its release posts lead the table, marked as coming from the release plan, and only extra posts are proposed around them.

Then ask on the buttons: “Make this plan” / «Crea questo piano» · “Change something” / «Cambio qualcosa» · “Not now” / «Non ora».

## 3. Make the campaign

On their yes, `make_project_with_tasks` in one step. For a release the release plan already planned there is no new campaign: its release posts are brought in by [release-posts.md](references/release-posts.md), and each extra post is added to the release project as in section 4.

- `name`: the brand and what the campaign is, in CAPITALS: `NORTH BAKERY NOVEMBER`, `NORTH BAKERY CHRISTMAS`.
- `area`: the brand's area. `area_words`: one plain line on what the area is for.
- `tasks`: one per post, in date order, codes numbered from `P01`. `title` exactly `P03 · INSTAGRAM · 18:00 · SINGLE OUT NOW` — the code, the network or networks joined with `+`, the local time, then what it is in a few capital words — at most 100 characters; `deadline` the publish date as `YYYY-MM-DD`. At most 50 posts.
- `note`: `purpose` at most 400 characters, what the campaign is for and the outcome it serves (after a first session's Path B, or under a live trial, it begins "Trial:"); `words` the plan in a few sentences.

**A title or a purpose a limit would refuse is shortened with the person, never cut by us.** A dated task's title over 100 characters, or a purpose over 400, refuses the whole campaign, and nothing is made. So count before sending; when a line is over, propose a shorter one and ask.

After the receipt (or, on a door that holds acts, after the owner approves), read it back with `list_tasks`, `project` the campaign, `format: "json"`: say how many posts were made and the first and last date. Tell the person once where they see it: “They're on your week and on the campaign's page in PROJECTS.” / «Li trovi nella tua settimana e nella pagina della campagna, in PROGETTI.»

## 4. One more post on a campaign already made

When the person adds one post («aggiungi un post sabato»): read the campaign's tasks with `list_tasks`, `project` the campaign, take the next free code (never reuse one, even of a post put away), propose the line, and on yes `make_task` with the same title shape, `deadline` the date and `project` the campaign. Read it back.

## 5. A new artist or client

A new artist or client is set up by FIRST SESSION, which makes their area, their standing project and their brand's line in its first few minutes, so every other skill can find them. When the request names a brand that has none of these, say so and offer «set up social for <name>» / «iniziamo con i social per <nome>»: the questionnaire can pause straight after that first step, and the plan can be made then; say plainly that until the first session is finished, the drafts follow only the rules filed so far (POSTS says the same). This skill never makes an area or a campaign for a brand that is not set up, because POSTS, PICTURES and HANDOVER could not find it afterwards.

## 6. Close

One short paragraph: the campaign made (or held), how many posts, the first and last date, anything left out. Then the next phrase, taken from the rhythm: “On Thursday, say draft Friday's posts.” / «Giovedì di' scrivi i post di venerdì.» Where no rhythm is filed, name the day before the first post. Last, when the campaign was made, call `show_social_month` once so the person sees the new posts on the month at a glance; where that tool is not in this conversation, say nothing about it.

## Never

- Date a post in the past.
- Send a title or purpose a limit would refuse without shortening it with the person.
- Touch the Metricool schedule: this skill reads best times and nothing else in Metricool.
- Blend two brands in one plan.
- Rename a post's code after the campaign is made.
- Plan a release post again that the release plan already made, or make a campaign beside a release project.
- Make an area or a campaign for a brand that FIRST SESSION has not set up.

## Tools

Reads: `skill_switch`, `list_projects`, `list_tasks`, `search_records`, and for a release post `list_pieces` and `show_social_month`; Metricool `getBrandSettings`, `getBestTimeToPostByNetwork`. Writes: `make_project_with_tasks`, `make_task` (one added post, or a release post brought in with `piece_id`, on the person's yes).
