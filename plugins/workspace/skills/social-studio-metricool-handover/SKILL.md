---
name: social-studio-metricool-handover
description: "SOCIAL STUDIO: METRICOOL HANDOVER. Hands a brand's approved posts to Metricool as drafts, never live: reads each post's final words back from the records exactly as filed, stops a post with no final or no picture where the network needs one, asks for the person's own Drive or Dropbox link to each picture, sends each as a draft, keeps the planner link beside the post, and says every time what the person does next in Metricool. A changed post becomes a fresh draft and the old one is named for the person to delete; a moved post is moved on the plan, and in Metricool by the person. Use when the person says “send to Metricool”, “send Friday's posts to Metricool”, “the Saturday post changed, send it again”, “move Saturday's post to Monday”; Italian: «manda i post a Metricool», «manda i post di venerdì a Metricool», «il post di sabato è cambiato, rimandalo», «sposta il post di sabato a lunedì». Never publishes, schedules a live post, edits or deletes anything in Metricool, or sets an AI flag."
---

## Before anything else: is this skill on here?

Before doing any of this skill's work, call the door's `skill_switch` tool with `skill` set to `social-studio-metricool-handover`.

- Carry on with the skill below ONLY if the answer says this skill is a core skill, or that it is on in this workspace.
- If the answer says it is off: stop here. Tell the owner, in their language, that this skill is switched off in this workspace, and do nothing else from this skill.
- In every other case (no answer, an error, the tool is not available, the answer says the switch could not be read, or any answer you do not recognise): stop here. Tell the owner plainly that the skill switch could not be read, so this skill was not used.

# SOCIAL STUDIO: METRICOOL HANDOVER

The one door between the records and Metricool, and it opens one way. This skill only ever **creates drafts** in Metricool. It never publishes, never schedules a live post, never edits, moves or deletes anything there, and never sets an AI declaration. The person approves, schedules and publishes in Metricool, usually from their phone. What goes across is exactly the words the person chose, read back from the records in the same turn they are sent, and never words from this conversation.

Why create only: an edit after a read can land on a post the person scheduled in between, or overwrite a declaration they set; a delete could remove a scheduled post. A create touches nothing already in Metricool, so it cannot collide. The cost is one old draft the person deletes by hand when a post changes, and it is said plainly every time.

Speak as the counterpart the room instruction names, in the person's language: plain words, verdict first, first-person plural, dates dd/mm/yy. **One beat per turn.** No action name, id, revision or code reaches the person; a planner link may be given to them, because it opens their own Metricool.

Read [landing.md](references/landing.md) before any write to the records. On a door that holds acts for approval, keeping the planner link and moving a date wait on the approval page; the draft in Metricool exists from Metricool's receipt, and the summary says both truthfully.

Open with one sentence: “I'll read the final words of each post from your records, then we send them to Metricool as drafts.” / «Leggo dal tuo archivio le parole definitive di ogni post, poi le mandiamo a Metricool come bozze.»

## 1. Which brand, and is Metricool here

1. `list_projects` with `ids: true`; brands are the projects ending in ` SOCIAL`; several and none named: ask which. One handover is for one brand.
2. **The brand's line.** `search_records` with `text: "SOCIAL BRAND: <BRAND>."` (the full stop included, so `NORTH` never finds `NORTH BAKERY`), `state: "live"`, `limit: 50`, no tag, and keep only the line whose words begin exactly `SOCIAL BRAND: <BRAND>.`: its words name the brand's rule tag, its Metricool brand number and time zone, and whether it is the only brand here. Read the tag from those words; never build it from the name, because two brands can make the same slug. No line, or a line that says the Metricool brand is not linked yet: stop, and say the first session links it («set up my social media»).
3. Metricool's `getBrandSettings`. Confirm the brand number from the rule is there, and take the time zone and the connected networks from it. When the rule's number is not in the list, stop: “Your records say this brand is a Metricool brand I can't see from this Claude. Check that Metricool is connected with the account that holds it.” Never send to a brand chosen by its name alone.

When Metricool is not connected in this Claude, say so in one line, that it is a switch in their Claude connectors, and stop.

**Can the records keep a Metricool link here?** Look at the description of the records' link-keeping action in this Claude. When it does not name Metricool planner links, nothing is sent: “Your records can't keep a Metricool link on this workspace yet, so I won't send anything: without the link, a later change couldn't name the old draft for you to delete.” / «Il tuo archivio non può ancora tenere i link di Metricool su questo spazio di lavoro, quindi non mando niente: senza il link, a una modifica non saprei dirti quale vecchia bozza cancellare.» Stop the skill.

## 2. Which posts

`list_tasks`, `project` the campaign, `format: "json"`, `ids: true`. Match the request to the posts by day and code (`P03 · INSTAGRAM · 18:00 · SINGLE OUT NOW`): the date is the deadline, the network or networks and the local time are in the title. The coded task is the only source of a post's day, network and time; nothing is sent for a post that is not one.

- **The practice post** of the first session is `P00` on the brand's standing project, `<BRAND> SOCIAL`, not on a campaign: `list_tasks` with `project` the standing project. For it, every read and write below uses the standing project where it says the campaign.
- **A release post from the artist room** is a post piece on the release project, not a coded task, and no action here can tie a coded task to that piece. Send nothing for it, never send from the piece itself, and never make a second post for it: say “That release post was planned in the release plan, and this pack can't yet take it into the social calendar, so I haven't drafted or sent anything for it.” / «Quel post è stato pianificato nel piano dell'uscita, e questo pacchetto non riesce ancora a portarlo nel calendario social, quindi non ho scritto né mandato niente per quel post.» The other posts go on.

Read back in one line which posts these are. A post whose date is in the past cannot be sent: say so and offer to move it (section 7).

## 3. The final words, read back from the records

First `list_pieces`, `project` the campaign, with no role: the names of the post's pieces (whether `P03 - TEXT` and `P03 - FIRST COMMENT` exist at all), its kept pictures (`P03 - PICTURE 1` …), and the campaign's links.

Then, for each post, `list_pieces`, `project` the campaign, `role: "final"`, `text: true`, `piece` `P03 - TEXT`; and only when a `P03 - FIRST COMMENT` piece exists, the same for it. The records check the text against its stored fingerprint before they return it; that check is theirs, not ours.

- **No first-comment piece at all**: the post simply has no first comment, and goes without one. Nothing stops.
- **A first-comment piece with options but no final**: ask, for that post only, whether it goes without its first comment or they choose one first (POSTS). Never send an option.

- **Any read error, refusal or missing reply stops the whole handover.** Say what failed in plain words. Never fill a text from this conversation, from memory, or from an option.
- **No final text: that post stops.** “Friday's post has no final words yet; say draft Friday's posts and choose one.” / «Il post di venerdì non ha ancora un testo definitivo: di' scrivi i post di venerdì e scegline uno.» The others can go on.
- When the records cannot return text on this workspace yet (the reply has no text), stop the whole handover and say: “Your records can't hand me the final words on this workspace yet, so nothing goes to Metricool: I only send words read back from the records.” / «Il tuo archivio non riesce ancora a ridarmi i testi definitivi su questo spazio di lavoro, quindi a Metricool non va niente: mando solo parole rilette dall'archivio.»

A link titled `P03 · METRICOOL · …` among the campaign's links means this post was sent before: this send is a **replacement** (section 6).

## 4. What Metricool refuses, stopped before sending

Metricool validates a draft like a live post, so these stop that post before anything is sent:

- **Instagram or TikTok with no picture or video**: refused by Metricool even as a draft (measured 21/10/26 for Instagram). A Reel needs a video; a carousel needs two or more pictures. Pinterest needs a picture and a board; YouTube needs a video, a title and whether it is made for kids — ask the person for those, never guess.
- **Bluesky over 300 characters**: stop and say so; the words are the person's to shorten in POSTS, never ours.
- **A network the brand has not connected in Metricool**: stop that network, name it.

Never reword or trim a text to get past a limit or an error.

## 5. The picture links, and the yes

For each post with a picture, ask for **the person's own Drive or Dropbox link to that picture**, shared so anyone with the link can open it, until they have seen the picture in the draft. Say why once: “Metricool takes its own copy from your link, so once you've seen the picture in the draft, the link can be closed again.” / «Metricool si prende una sua copia dal tuo link: quando hai visto la foto nella bozza, puoi richiudere il link.» A Drive link works only when Drive is linked in their Metricool account. The records' own copy of a picture is never made public and never offered.

Then one summary per post, and the question on the buttons: the day dd/mm/yy, the time, the network, the first line of the words, the picture by its file name, "as a draft". “Send these as drafts” / «Mandale come bozze» · “Change something” / «Cambio qualcosa» · “Not now” / «Non ora».

## 6. Send, one post at a time

On their yes, for each post:

1. **Read the final again in this turn**, exactly as in section 3, immediately before the send. What is sent is what that read returned.
2. `createScheduledPost` with:
   - `blogId`: the brand number from section 1;
   - `date`: the post's date and local time with the brand time zone's offset on that date, `YYYY-MM-DDTHH:MM:SS±HH:MM`;
   - `info`, a JSON object with exactly: `text` the final, character for character; `draft: true`; `providers` one `{"network": …}` per network in the title; `publicationDate` `{"dateTime": "YYYY-MM-DDTHH:mm:ss", "timezone": <the brand's zone>}`; `media` the person's links; `firstCommentText` the first comment's final, only when one was read back (left out entirely otherwise); and an empty data object for each network in `providers` (`"instagramData": {}`, `"facebookData": {}` …), carrying only what the person chose that the network requires — Instagram `type` `REEL` for a reel, the YouTube title and made-for-kids answer, the Pinterest board.
   - Nothing else. Never `isAiGenerated`, `isAiGeneratedContent` or `isAigc`, in any value: Metricool's defaults go out, and the declaration stays the person's. Never `boost`, never the review flow, never a thread.
3. **Read the receipt.** It carries `id`, `uuid`, `plannerUrl`, `draft`. If it says `draft` is anything but true, tell the person at once, in plain words, that this post reached Metricool scheduled as a live post, give them its planner link, and ask them to open it now and change it to a draft or delete it; send nothing more until they have.
4. **On a Metricool error**, say it in plain words, unchanged in meaning, and stop that post; never reword the text and retry. The next post can go.
   **When the outcome of a send is unknown** (no receipt came back, the connection dropped, or the same post is being sent again after an interruption): never send it a second time on trust. `getScheduledPosts` with the brand number, the brand's time zone and a range around the post's date (`extendedRange: true`), and look for a draft with exactly the post's text on exactly its date. If it is there, that is the draft: send nothing. That list carries no planner link, so there is no link to keep, and none is ever built from an id: keep nothing in the records, tell the person this post is in Metricool on that day and time but not linked in their records, and a later change to it is matched by its network, day and time in Metricool (as below, for a link that was refused). If it is not there, do not create another: stop, and tell the person, in plain words, to check the planner in Metricool and to contact Stefano. “I can't tell whether this post reached Metricool, so I haven't sent it again. Please look in the Metricool planner, and contact Stefano.” / «Non so se questo post sia arrivato a Metricool, quindi non l'ho rimandato. Controlla il calendario di Metricool e contatta Stefano.»
5. **Keep the link**: `record_link`, `project` the campaign, `title` `P03 · METRICOOL · <uuid>`, `url` the `plannerUrl`, `kind: "review"`, and read its receipt before the next post goes. When it is refused anyway, send nothing more: give the person the planner link in the chat, say plainly that this post is in Metricool but not linked in their records, and that a later change to it will be matched by its day and time in Metricool instead (below).

**Before the yes, look in Metricool for an earlier draft of every post**, linked or not: `getScheduledPosts` with the brand number, the brand's time zone and a range around the post's date (`extendedRange: true`). An earlier draft is the one whose uuid matches the post's newest METRICOOL link, or, when the post has no link, one on the same network at the same day and time. Either way this send is a **replacement**, unless nothing has changed (next paragraph).

**Nothing changed since the last send**: when the post already has a kept planner link, and its final words (read again in this turn), its picture link and its date and time are the same as at that send, send nothing. Say the draft is already in Metricool and give its planner link: “This post is already in Metricool as a draft, and nothing has changed, so I haven't sent it again: <link>.” / «Questo post è già in Metricool come bozza e non è cambiato nulla, quindi non l'ho rimandato: <link>.» Only a changed post becomes a fresh draft.

**A replacement**: it is a fresh draft, sent exactly as above, with a new link beside the old one; the newest link for a post is the live one. Name the old one by its date and time in the summary, so the person knows which to delete. When the post has a link but its draft is no longer listed, it was published or deleted: say you cannot tell which, and ask the person to check in the planner before they publish the new one. When a draft at the same day and time is found for a post with no link, say it looks like an earlier copy and ask before sending; when two such drafts are found, name both and ask which is the earlier copy.

## 7. Moving a post

When the person moves a post («sposta il post di sabato a lunedì»):

1. `list_tasks`, `format: "json"`, `ids: true`; note the old date and the old time (from the title) before anything changes, name the old date and the new one, dd/mm/yy, and ask.
2. On yes, `move_task_date` with `task` the task's id, `date_kind: "deadline"`, `date` `YYYY-MM-DD`, `expected_revision` the task's `dateRevision` from that read, and `words` the person's own words. When the time changes too, `rename` with `kind: "task"`, the task's `id` and the new `title`, keeping its code first.
3. Whether or not the post has a METRICOOL link, look for a draft of it at the **old** date: `getScheduledPosts` with the brand number, the brand's time zone and a range around the old date (`extendedRange: true`). With a link, find its uuid; without one (a send whose link was refused), take a draft on the same network at the old day and time as this post's draft, and say it looks like an earlier copy. No draft found and no link: if no send of this post was ever started, nothing more is needed in Metricool. If a send was ever started and no kept link confirms its outcome, do not treat it as never sent: look by the post's exact text and its **original** date; if found, send nothing and keep nothing (that list carries no planner link, and none is built), and treat it as a draft with no link, matched by network, day and time; if not found, create nothing: stop, and tell the person to check the planner in Metricool and to contact Stefano («Controlla il calendario di Metricool e contatta Stefano»). When a draft was found, this skill does not touch it. Offer two ways on the buttons and let the person pick:
   - **A fresh draft on the new date**, through section 6: same words, same picture link; they delete the old draft themselves, and the summary names it by its old date and time.
   - **They drag it in the planner** to the new day: one gesture, nothing new is created.
   When the post shows as scheduled (not a draft), offer only the second way: “It's scheduled already, so it's yours to move in the planner; I won't create a second copy.” / «È già programmato: spostalo tu nel calendario di Metricool; non ne creo una seconda copia.»

## 8. The summary, every time

After every send, for each post, in plain words, all five points (the house wording is in [SHARED.md](references/SHARED.md), section “The handover sentence, every time”):

1. It is a draft in Metricool, and they publish it there.
2. The "made with AI" declaration is off by default and theirs to set there.
3. The time we sent: the post's day and time in the brand's time zone, as we sent it, and the time Metricool's receipt shows, as it reads, without saying the two are the same. If the planner shows a different hour, they check the account's time zone in Metricool's settings. A post's time is never changed, here or by advice, without the person's yes.
4. For a replacement: which old draft they delete (its date and time; the bin icon in the planner, then Confirm), and that each change costs one old draft deleted by hand; on Metricool's free plan each fresh draft may count against the twenty posts a month.
5. The picture: Metricool takes its own copy from the link, as it did in our one test, but whether it did for this post is not checked here. So: they open the draft in the planner, and only once they see the picture there do they turn the link's sharing off. Say plainly that in our one test Metricool's copy opened for anyone with its address, without a sign-in, so they treat the picture as public once it is sent.

Then what is kept in the records (the planner links), what is held for approval, and anything that stopped and why. When at least one draft reached Metricool, call `show_social_month` once before the last line, so the person sees the month's posts at a glance; where that tool is not in this conversation, say nothing about it. Close with: “They're waiting for you in Metricool.” / «Ti aspettano in Metricool.»

## Never

- Send text the records did not just return from the filed final.
- Send a live post, or anything but `draft: true`.
- Edit, move or delete any post in Metricool: none of Metricool's edit or delete actions is ever called.
- Use the review flow.
- Set any AI declaration.
- Replace a draft without naming the old one the person must delete.
- Reword text to get past a Metricool error or limit.
- Leave the person's picture link shared without telling them to close it once they have seen the picture in the draft.
- Make the records' copy of a picture public.

## Tools

Reads: `skill_switch`, `list_projects`, `list_tasks`, `list_pieces` (with `role: "final"` and `text: true`), `search_records`; Metricool `getBrandSettings`, `getScheduledPosts`. Writes: Metricool `createScheduledPost` (`draft: true` only); `record_link` (`kind: "review"`); `move_task_date`; `rename` (`kind: "task"`, a moved post's time only).

## What is not yet known, and what this skill does meanwhile

- Whether Metricool copies every picture, whether its copy always opens without a sign-in, and whether it is removed when the draft is deleted: one test only, not measured through this connector. Meanwhile: never say a copy was made or removed; the person checks the picture in the draft before turning sharing off, treats a sent picture as public, and the practice post uses a picture they are happy to have public.
- Whether a draft deleted in the planner still counts against the free plan's twenty posts a month. Meanwhile: word it as "may count", never as a fact either way.
- Whether the receipt's time always matches the time sent, and why the planner can show a different hour. Meanwhile: point 3 of the summary, and nothing more.
