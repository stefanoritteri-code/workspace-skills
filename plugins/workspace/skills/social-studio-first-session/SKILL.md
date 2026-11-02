---
name: social-studio-first-session
description: "SOCIAL STUDIO: FIRST SESSION. The deep beginning of a person's social media, for one brand at a time, whether they already have a look or have none: a short questionnaire, then two or three short sittings that end in the brand file (audience, the ninety-day result, voice, look, never-dos, references, themes, channels, approver and rhythm), a first fortnight's plan and one practice draft taken all the way to Metricool and deleted again. Picks up where the last sitting stopped. Use when the person says “set up my social media”, “let's start with social”, “start my social media from nothing”, “set up social for an artist or a client”, “carry on with the social setup”; Italian: «iniziamo con i social», «sistemiamo i miei social», «partiamo con i social», «riprendiamo la configurazione dei social». Never publishes anything. Changing rules after setup is SOCIAL STUDIO: BRAND; planning a month is MONTH PLAN."
---

## Before anything else: is this skill on here?

Before doing any of this skill's work, call the door's `skill_switch` tool with `skill` set to `social-studio-first-session`.

- Carry on with the skill below ONLY if the answer says this skill is a core skill, or that it is on in this workspace.
- If the answer says it is off: stop here. Tell the owner, in their language, that this skill is switched off in this workspace, and do nothing else from this skill.
- In every other case (no answer, an error, the tool is not available, the answer says the switch could not be read, or any answer you do not recognise): stop here. Tell the owner plainly that the skill switch could not be read, so this skill was not used.

# SOCIAL STUDIO: FIRST SESSION

The beginning every later social skill stands on. A professional who posts for work leaves it with three things: a brand file that says who they are talking to and how they sound and look, the rules every draft will follow, and the whole road walked once, from a draft in Claude to a draft in Metricool and back out again. It is a studio session, not a form: the person is shown real things and chooses; they are never asked to describe a style in adjectives.

Speak as the counterpart the room instruction names, in the person's language: plain words, verdict first, first-person plural, dates dd/mm/yy. **One beat per turn, then stop and let them answer**: one question, one summary to correct, or one set of examples to choose from. No action name, id, tag or code ever reaches the person; the fields named below belong inside calls. The reasons in this file are never spoken.

Read [landing.md](references/landing.md) before the first write and follow it for request ids, receipts, held acts and recovery. Read [claude-native.md](references/claude-native.md) for the question buttons and for Claude Design. On a door that holds acts for approval, every write below waits for the owner's yes on the approval page; say so once, and never say a thing is filed before its receipt says so.

## The shape of it

- **The questionnaire** (about ten minutes, one question per turn).
- **Sitting one, discovery** (about thirty minutes): the outcome, the audience, the channels, three themes; then the look, Path A or Path B.
- **Sitting two, the road** (about thirty minutes): three finished examples, practice at changing and approving, one practice draft to Metricool and deleted, the first fortnight, the rhythm.
- **The result**: the brand file, written once.

Two or three short sittings, never one long one: never start the next sitting in the same go unless the person asks for it, because a forty-five-minute sitting is already too long for a working week. Every answer is filed as it is settled, so any sitting can stop and the next picks up.

Open with one sentence: “I'll check what we already have for your social media, then we start where it stopped.” / «Guardo cosa abbiamo già per i tuoi social, poi ripartiamo da dove ci eravamo fermati.»

## 1. Which brand, and where we are

A brand is whoever the posts speak for: the person themselves, their shop, an artist or a client they run. One brand per run. Two brands of one owner are never blended: not in one questionnaire, not in one brand file, not in one look.

Read first, then speak:

1. `list_projects` with `ids: true`. A project named `<BRAND> SOCIAL` is a brand already started; note its id.
2. For a brand already started: its line, `search_records` with `text: "SOCIAL BRAND: <BRAND>."`, `state: "live"`, `limit: 50`, no tag, which names the brand's rule tag; then `search_records` with that `tag`, `state: "live"`, `limit: 50`, and (for the only brand in the workspace) with `tag: "scope:planning"`, `text: "SOCIAL RHYTHM"`; then `read_source` with `path: "pages"` to list the saved pages, and open the ones titled `DISCOVERY <BRAND> …` and `BRAND FILE <BRAND>` that exist (found by listing, never by building a path); then `list_tasks` with `project` the standing project, `format: "json"`, `ids: true`, for the sittings.
3. Metricool's `getBrandSettings`, for the brands, their networks and time zones. If Metricool is not connected in this Claude, say so in one line — “Metricool isn't connected in this Claude yet; it's a switch in your Claude connectors. We can do the questionnaire and sitting one without it.” / «Metricool non è ancora collegato in questo Claude; si attiva nei connettori di Claude. Il questionario e la prima seduta li facciamo anche senza.» — and carry on.

Then one line on where we are, in plain words, and the next step: «Il questionario è fatto, la prima seduta no: partiamo da lì.» When the brand file already exists, the first session is done: say so and offer BRAND for changes («le regole del mio profilo») or MONTH PLAN («pianifica i post del mese»).

When the person runs several brands from this workspace and has not said which this is for, ask, with the existing ones and "a new one" on Claude's buttons.

## 2. The questionnaire, before the first sitting

**At its start, make the place the answers live.** Ask the brand's name if it is not plain, and whether it is the only brand they run from this workspace or one of several (artists, clients, shops). Propose the name in CAPITALS and, on their yes:

- `make_area` with that name, unless an area of that name already exists (a workspace with no live area refuses the one-step project action, so the area comes first).
- `make_project_with_tasks`: `name` `<BRAND> SOCIAL`, `area` the brand's area, `area_words` one plain line on what the area is for ("the social media of North Bakery"), `tasks` the sittings and the practice post, all undated — `SITTING ONE · DISCOVERY`, `SITTING TWO · THE ROAD`, `P00 · INSTAGRAM · 10:00 · PRACTICE POST` (the network the person posts on most) — and `note` `{purpose: "Who <BRAND> talks to on social media, how it sounds and looks, and the rules every post follows.", words: one line on when it started}`. Each sitting is dated with `move_task_date` once its day is agreed.
- **The brand's tag, chosen once.** Propose `scope:<slug>` from the brand's name (the slug rule in landing.md, cut to 50 characters). Before anything is filed under it, `search_records` with that `tag`, `state: "any"`, `limit: 50`: any record at all means another brand already uses it (two names can make the same slug), so try `scope:<slug>-2`, then `-3`, until one comes back empty. The person never hears the tag.
- **The brand's line, the first record under that tag**: `record_decision`, `words` «SOCIAL BRAND: <BRAND>. Rules tag scope:<chosen>. Metricool brand not linked yet. <The only brand in this workspace. | One of several brands in this workspace.>», `tags: ["scope:<chosen>"]`. Every other skill finds the brand's tag in these words and never builds it. Every rule below goes under this tag.
- **When this is a second brand.** Read the other brands' lines (`search_records`, `text: "SOCIAL BRAND:"`, `state: "live"`). When one of them still says "The only brand in this workspace.", that brand's rhythm sits under `scope:planning`. Say so in one line, and on the person's yes: `supersede_decision` of that brand's line with the same words ending "One of several brands in this workspace."; read its rhythm (`search_records`, `tag: "scope:planning"`, `text: "SOCIAL RHYTHM"`, `state: "live"`), file the same words again with `record_decision` under that brand's own tag, then `supersede_decision` of the planning one with «SOCIAL RHYTHM: moved to <THAT BRAND>'s own rules on dd/mm/yy.». Say plainly that the morning read will no longer carry either brand's rhythm. Without their yes, nothing moves, and the new brand's line still says "One of several brands".

Then the questions, one per turn, in the person's language, proposing an answer wherever the record already holds one:

1. What the business is, in a sentence.
2. Who buys, books or listens, and why they choose you.
3. The one result wanted in ninety days, in business terms: bookings, shop visits, enquiries, listeners, sign-ups. Ask what it is today, so the result has a baseline.
4. What you never want to sound like.
5. Six accounts, posts or brands you love and three you dislike, with why for each. Links are welcome; the why matters more than the link.
6. What you can realistically supply: photos, video, time each week, a photographer.
7. Who approves a post before it goes out.
8. (Already asked at the start: whether this is the only brand here. It decides where the rhythm is filed in section 4.)

Show the answers back as one short summary and ask for corrections. On their yes:

- **Before creating, check the page's path.** A page's path is the slug of its whole title cut to 60 characters (the rule in landing.md), so two long titles can share one. Work out the path of `DISCOVERY <BRAND> dd/mm/yy` and `read_source` it: when something is already there, the title is too long to tell apart; agree a shorter display name for the brand's pages with the person (their words) and check again. Never create over a path that answers.
- `write_page`, `mode: "create"`, `author: "counterpart"`, their answers quoted as theirs, title `DISCOVERY <BRAND> dd/mm/yy`; read the path from the receipt and `file_page_under_project` with that page slug, the standing project's id and a line of the person's words.
- Each never-do as its own `record_decision`, `words` beginning `NEVER:` in their wording, `tags: ["scope:<chosen>"]`.
- The approver as `record_decision`, `words` beginning `SOCIAL APPROVER:`, same tag. When the approver or the photographer has no card and the person wants one, `make_person` with the "who they are" line in the person's own words (it is required), and `note_person` for what they do on this brand.

File only what the person said. A gap stays a gap and is named, never filled.

Close the questionnaire by agreeing the day of sitting one, dating it with `move_task_date` (`date_kind: "deadline"`, the task's `dateRevision` from `list_tasks` as `expected_revision`, the person's words), and stopping.

## 3. Sitting one, discovery

Start by reading the discovery page and the brand's rules again, and say in one line what is settled.

**The four answers**, one per turn: the one main outcome (from question 3, said back as a sentence); the priority audience; the channels (only those Metricool's brand settings show connected, or those they will connect); three content themes, which we propose from the questionnaire and they adjust. Show a one-page summary back for correction before anything is filed, then file each as a `record_decision` under the brand's tag, words beginning `SOCIAL OUTCOME:`, `SOCIAL AUDIENCE:`, `SOCIAL CHANNELS:`, `SOCIAL THEMES:`.

When the Metricool brand is confirmed, link it once: `supersede_decision` of the brand's line (its real `old_id` from the read), `words` «SOCIAL BRAND: <BRAND>. Rules tag scope:<chosen>. Metricool brand "<name>" (number <blogId>, time zone <zone>) on <networks>. <The only brand in this workspace. | One of several brands in this workspace.>». The supersede keeps the tag. Every later skill reads the Metricool brand from this line; never guess it from the name.

**Then the look. Ask which is true** on the buttons: “I already have a look I like” / «Ho già uno stile che mi piace» · “I have no real style yet” / «Non ho ancora uno stile».

### Path A — they already have a look

Read their recent posts from Metricool: `getAnalyticsAvailableMetrics` with the network and `connector: "posts"`, and for Instagram also `connector: "reels"`, because reels sit in their own source; then `getAnalyticsDataByMetrics` with the brand number and the per-post metrics each source lists (one source per request), over the last twenty to sixty posts, reels and feed posts together. Walk them a few at a time as **keep, refine or retire**, with the numbers beside each one and the brand's average beside the numbers, never a number alone. Write the look down from the real posts: what the pictures share, the type, the colour, how the words sit. Then show two or three small refinements on one of their own real photos, and let them choose.

File the look as decisions in words under the brand's tag (`SOCIAL LOOK:` lines, one rule each), only the ones they accept.

### Path B — no style yet

Three contrasting directions, shown as real finished mock posts at phone size, never as adjectives, with the person's own photos where they have supplied them. Show them on a Claude Design canvas in their own Claude when Claude offers one here; until that canvas is known to stay private to them, their photos go in the chat beside each direction and never onto the canvas. Without a canvas, show each direction in the chat as the post itself, words and layout described, with their photo beside it. Then this-or-that questions, one per turn, until one direction stands. **They pick one, never a blend**: when they ask for "a bit of both", show what the blend looks like and ask which of the two it is closer to.

File the pick as a decision in words: `words` beginning `SOCIAL DIRECTION:` (what the direction is and why they chose it), and each reference that led to it as `SOCIAL REFERENCE:` (the reference and the reason), all under the brand's tag. The canvas stays private in their Claude; never record a link to it and never make their photos public.

The direction is a **trial**: it is tested in real posts for two to four weeks before it is locked. Say so plainly; the trial's dates are filed in sitting two, once the first fortnight's first post is known. Never lock a look before its trial.

Close sitting one by agreeing the day of sitting two, dating it, and stopping.

## 4. Sitting two, the road

Read the brand's rules and the discovery page again, and say in one line what is settled.

**Three finished examples at phone size**, in the brand's voice and look: an announcement, a useful or storytelling post, and a sales post. The person practises the three moves every week will need, on one of them: asking for a change in their own words, approving it, and undoing a change. Then they choose the example to take down the road.

**The whole road once, on the practice post `P00`.** Say first what it is: a real draft in Metricool that nobody will see, which they will delete themselves at the end; on Metricool's free plan it may count as one of the month's twenty posts. Then:

1. Date the practice post with `move_task_date` to a day at least a week ahead, on their yes.
2. File the chosen text the way SOCIAL STUDIO: POSTS files a final: `P00 - TEXT`, `role: "final"`, on the standing project, the exact words.
3. Hand the send to SOCIAL STUDIO: METRICOOL HANDOVER and follow it as written there: it asks for the picture link, reads the final back, sends a draft, records the link and gives the summary. This skill never sends anything to Metricool itself. For the picture, ask for one the person is happy to have public, never a private photo, because Metricool may keep its own copy and, in one test, that copy opened without a sign-in. The link is their own Drive or Dropbox link.
4. They open the planner link, find the draft, and delete it themselves: the bin icon, then Confirm. Walk them to it, one step per turn.
5. Once they have seen the picture in the draft, they turn the link's sharing off again.
6. On their word that the draft is deleted, `close_task` on the practice post.

**After Path B, the trial's dates.** Ask how long the trial runs, two to four weeks from the first post. Then read the whole statement back exactly as it would be filed — «SOCIAL TRIAL: trying <the direction, in a few words> from dd/mm/yy to dd/mm/yy; the look is not locked until it is adopted.» — and file it only on the person's yes to that exact wording; a change of words is read back again before filing. Then, before the plan is made: `record_decision`, `words` that statement, `tags: ["scope:<chosen>"]`. MONTH PLAN reads this live trial and puts the word trial in the plan's note; MONTH RESULTS names it when it has ended; BRAND adopts or restores it, in the person's words.

**The first fortnight.** Agree the posts of the first two weeks and make them with SOCIAL STUDIO: MONTH PLAN, as that skill reads.

**The rhythm.** Agree three days: the day they plan, the day they approve, the day the month is read. File it once with `record_decision`, `words` beginning `SOCIAL RHYTHM:` in their wording («SOCIAL RHYTHM: I plan on Mondays, approve on Thursdays and read the month on the first Monday.»). The tag depends on the answer at the start: the only brand in this workspace → `tags: ["scope:planning"]`, so the morning read says “today is your approval day” on the mornings it proposes the day; one of several brands → `tags: ["scope:<chosen>"]`, and say plainly that the morning read will not carry it for this brand.

## 5. The result: the brand file

Draft the brand file from what is filed, show it whole, and check its path first exactly as for the discovery page (the path of `BRAND FILE <BRAND>` must not answer to `read_source`; if it does, agree a shorter name with the person and use it in the title). On their yes write it once: `write_page`, `mode: "create"`, `author: "counterpart"` (with the person's own lines quoted and attributed), title `BRAND FILE <BRAND>`. Read the path from the receipt, then `file_page_under_project` with that page slug and the standing project's id.

Its sections, in this order: purpose · audience · the ninety-day outcome and its baseline · voice, with three examples of how they sound and one of how they never do · look rules · do and don't examples · references, each with its reason · content themes · channels and cadence · approver · fixed versus experimental (after Path B, the direction is experimental, with the trial's two dates, until BRAND adopts or restores it) · what worked (empty, "first check-in after the first month").

It is never rewritten. Every later change is one dated section added with `mode: "append"`, by BRAND or MONTH RESULTS. Say so once: “Every change from now on is added as a dated section, so the file keeps its own history.” / «Ogni modifica da qui in poi si aggiunge come sezione datata, così il file tiene la sua storia.»

The enforceable lines are already decisions: the never-dos, the voice and look rules, the approver and any trial under the brand's tag; the rhythm under the brand's tag too, except for the only brand in a workspace, whose rhythm is under `scope:planning` so the morning read hears it. That is what every other skill reads. When Claude offers a Design System here, offer to keep the brand's visual rules there too, as a copy; the brand file stays the master.

## 6. Close

One short paragraph: what is filed (the brand file, the rules, the rhythm, the first fortnight), what is held for approval if the door holds acts, what is still open and whose move it is. Then the next phrase, in their language: “When you're ready, say plan this month's posts.” / «Quando vuoi, di' pianifica i post del mese.»

## The check-ins after the first session

MONTH RESULTS adds a "what worked" section each month and, while the brand file holds three or fewer of them, asks whether the look still feels right. BRAND offers two or three refresh directions each quarter. This skill does not run them.

## Never

- Make the person describe a style in adjectives.
- Blend two directions, or two brands of one owner.
- Lock a look before its trial.
- Run two sittings in one go unless the person asks.
- File anything the person did not say.
- Record a link to the person's photos, or make them public.
- Send anything to Metricool itself: the practice draft goes only through METRICOOL HANDOVER.

## Tools

Reads: `skill_switch`, `list_projects`, `list_tasks`, `search_records`, `read_source`, `list_people`; Metricool `getBrandSettings`, `getAnalyticsAvailableMetrics`, `getAnalyticsDataByMetrics` (Path A). Writes: `make_area`, `make_project_with_tasks`, `move_task_date`, `record_decision`, `supersede_decision` (a correction to a rule filed earlier in the session), `write_page` (`create`, then `append`), `file_page_under_project`, `make_person`, `note_person`, `close_task` (the practice post only, on the person's word). The practice text and draft: through POSTS and METRICOOL HANDOVER.

## What is not yet known, and the wording to use

- Metricool's post analytics may not carry every field (reels are read from their own source on Instagram). In Path A say what came back and nothing more: when the posts carry no picture, show the post's date and words and ask the person to open it in Metricool to see it; when fewer than twenty posts come back, say how many.
- A draft created then deleted may count against the free plan's twenty posts: word the practice «it may count as one of the month's twenty posts», never as a fact either way.
- Use a Design canvas only when Claude offers one in this conversation, and put the person's photos on it only once it is known to stay private to them; otherwise show the directions in the chat.
- Whether Metricool always keeps its own copy of a picture, whether that copy always opens without a sign-in (it did in one test) and whether it is removed when the draft is deleted are not measured through the connector. Meanwhile the practice draft uses a picture the person is happy to have public, never a private photo, and they check the picture in the draft before turning the link's sharing off.
