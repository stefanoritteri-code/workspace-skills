---
name: social-studio-posts
description: "SOCIAL STUDIO: POSTS. Drafts the words of a brand's planned posts in its own voice and rules, two or three options per post, and keeps every option on the campaign; the one the person chooses is filed as the final, word for word, which is exactly what will later go to Metricool. Also the first comment, and credits for the people in the post. Use when the person says “draft Friday's posts”, “three options for the release post”, “write this week's posts”, “redo the Saturday post”, “a shorter version of that one”; Italian: «scrivi i post di venerdì», «tre opzioni per il post dell'uscita», «scrivi i post della settimana», «rifai il post di sabato». Never marks a text final without the person's choice and never posts. Pictures are SOCIAL STUDIO: PICTURES; sending to Metricool is METRICOOL HANDOVER."
---

## Before anything else: is this skill on here?

Before doing any of this skill's work, call the door's `skill_switch` tool with `skill` set to `social-studio-posts`.

- Carry on with the skill below ONLY if the answer says this skill is a core skill, or that it is on in this workspace.
- If the answer says it is off: stop here. Tell the owner, in their language, that this skill is switched off in this workspace, and do nothing else from this skill.
- In every other case (no answer, an error, the tool is not available, the answer says the switch could not be read, or any answer you do not recognise): stop here. Tell the owner plainly that the skill switch could not be read, so this skill was not used.

# SOCIAL STUDIO: POSTS

The weekly writing desk. Each planned post gets two or three real options in the brand's own voice, short enough to judge on a phone, each different in its approach and not just its wording. The person chooses; the chosen words are filed as the final exactly as they will appear, because those exact words, and nothing else, are what METRICOOL HANDOVER sends.

Speak as the counterpart the room instruction names, in the person's language: plain words, verdict first, first-person plural, dates dd/mm/yy. **One beat per turn**: one post's options at a time, unless the person asks to see them all. No action name, id, tag or code reaches the person ("the Friday post", never "P03").

Read [landing.md](references/landing.md) before any write and [claude-native.md](references/claude-native.md) for the buttons and Claude Design. On a door that holds acts for approval, each filing waits on the approval page; never say a text is filed before its receipt.

Open with one sentence: “I'll read the posts planned, your voice and your rules, then bring you options for the first one.” / «Leggo i post in programma, la tua voce e le tue regole, poi ti porto le opzioni per il primo.»

## 1. Read before writing

1. **The brand.** `list_projects` with `ids: true`; brands are the projects ending in ` SOCIAL`. None: offer «set up my social media» and stop. Several: ask which. Never write for two brands in one go.
2. **The posts.** `list_tasks` with `project` the brand's campaign, `format: "json"`, `ids: true`; the posts are the tasks whose titles begin with a code (`P03 · INSTAGRAM · 18:00 · SINGLE OUT NOW`). Match the request to them by day ("Friday's posts" is every post whose deadline is that Friday). When no planned post matches, say so and offer MONTH PLAN («aggiungi un post venerdì»); never invent a post.
   **A release post from the release plan.** The release plan keeps a release's posts as planned posts on the release project, with no code. When the post asked for is one of them, follow [release-posts.md](references/release-posts.md): on the person's yes it becomes a coded post linked to the planned one, and then it is drafted like any other, with the release project as its campaign. Never draft from the planned post itself and never make a second post for it. The other posts go on.
3. **What is filed already.** `list_pieces` with `project` the campaign: an existing `P03 - TEXT` final means this post already has its words; say so and ask whether they want to redo it.
4. **The rules.** The brand's line first: `search_records` with `text: "SOCIAL BRAND: <BRAND>."`, `state: "live"`, no tag; its words name the brand's rule tag (never build it). Then `search_records` with that `tag`, `state: "live"`, `limit: 50`: never-dos, voice rules, themes, the approver, any live trial, the rhythm; for the only brand in the workspace, the rhythm is read with `tag: "scope:planning"`, `text: "SOCIAL RHYTHM"`.
5. **The voice.** The brand file: `read_source` with `path: "pages"` to list the saved pages, then open the `brand-file-…` page titled exactly `BRAND FILE <BRAND>`; never build its path. No brand file yet (the first session is not finished): write from the brand's line and the rules filed so far, and say once that the drafts follow only the rules filed so far until the first session is finished («finish setting up my social media»). From the brand file, when there is one: the voice examples, the do and don't examples, the look, and every "what worked" section. The most recent lessons outrank older ones.
6. **The people.** `list_people` for anyone the post credits (a photographer, a featured artist, a venue's manager).

## 2. The options

For each post, two or three options. Each one:

- obeys every never-do and voice rule, checked line by line before it is shown, and it says nothing the brand does not know to be true (a date, a price, a guest);
- fits the network: Instagram's caption limit of 2,200 characters, Bluesky's 300, X at 280 unless the person says their account allows long posts; hashtags only where the brand's rules use them;
- takes a different approach from the others (a line from the person, a question, a story, a plain announcement), labelled in a word so the person can choose by the approach;
- comes with its first comment when the brand uses one, shown under it.

Show each option at phone size: the words as they will read, line breaks where they will fall. When there is a picture to see with the words, and Claude offers a Design canvas here, the option can sit on the canvas with the picture; until the canvas is known to stay private to the person, their photos go in the chat, never onto it.

**File every option as it is shown**: `file_piece_text`, `project` the campaign, `piece` `P03 - TEXT`, `role: "option"`, `file_name` `P03-TEXT.txt`, `text` the option exactly. The first comment is its own piece, `P03 - FIRST COMMENT`. Every version is kept, so nothing the person liked is lost when they change their mind. When the person gives raw material (their notes, a voice memo's words, the press release), file it once as `role: "source"`.

**A preview page, only when asked.** When the person wants an option to share with someone (the approver, a manager), offer a Claude page with the words only, never their photos, because that page is public once its link is kept. On yes, make it, then `record_link`, `project` the campaign, `title` `P03 · OPTION 2`, `url` the page's public link, `kind: "option"`.

## 3. The choice and the final

Ask on the buttons, one per option plus “Change it” / «Modificala». A change is in the person's words: write the new version, show it, file it as another option.

**The final is the person's choice, never ours.** Only when they choose one, in so many words or by the button for that option: `file_piece_text`, `piece` `P03 - TEXT`, `role: "final"`, `text` exactly the chosen words, every character as shown, nothing tidied after the choice. The same for the first comment. Read the receipt and say: “Friday's post is final. Those are the exact words that will go to Metricool.” / «Il post di venerdì è definitivo: sono esattamente le parole che andranno a Metricool.»

A final changed after it was sent to Metricool is a new final; say plainly that the old draft in Metricool keeps the old words until METRICOOL HANDOVER sends a fresh one, and the person deletes the old one there.

## 4. Credits

When a post credits someone, on the person's yes: `note_person` on their card, `author: "owner"` if the words are the person's, saying what they are credited for, on which post and date («credited for the photos in the Friday post, 07/11/26»). No card, and the person wants one: that is a card with a "who they are" line in the person's words, made only on their yes.

## 5. Close

One short paragraph: which posts now have a final, which have options waiting for a choice, which have no picture yet. Then the next phrase: when a picture is missing, “When the pictures are ready, say file the pictures.” / «Quando le foto sono pronte, di' archivia le foto.»; otherwise, from the rhythm, “When you're ready, say send Friday's posts to Metricool.” / «Quando vuoi, di' manda i post di venerdì a Metricool.» Last, when words were filed, call `show_social_month` once so the person sees the month's posts at a glance; where that tool is not in this conversation, say nothing about it.

## Never

- Mark a text final without the person's choice.
- Change a single character of a final after the choice.
- Put the person's photos on a public page or, until measured, on a Design canvas.
- Post, schedule or send anything to Metricool.
- Write for two brands in one go.

## Tools

Reads: `skill_switch`, `list_projects`, `list_tasks`, `list_pieces`, `search_records`, `read_source`, `list_people`. Writes: `file_piece_text` (`option`, `final`, `source`), `record_link` (`kind: "option"`, a Claude preview page with words only), `note_person` (credits), `make_task` (a release post brought in, with `piece_id`, on the person's yes). Reads for a release post: `show_social_month`.
