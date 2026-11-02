---
name: social-studio-pictures
description: "SOCIAL STUDIO: PICTURES. Keeps each picture or video of a planned post on its campaign, one file per picture, so a post's words, pictures and Metricool link are kept together. Checks the file type first (PNG, JPEG, GIF, WebP, MP4, QuickTime or WebM; an iPhone photo is exported as JPEG first), sends the file, and says it is kept only when the receipt says so. Pictures still to come from a photographer are marked as waiting, and released when they arrive. Use when the person says “file the pictures”, “these are for Friday's post”, “keep these photos for the campaign”, “the photographer sent the shots”, “we're waiting on the photos”; Italian: «archivia le foto», «queste sono per il post di venerdì», «il fotografo ha mandato le foto», «aspettiamo le foto». Never makes or edits a picture. Sending a picture to Metricool is SOCIAL STUDIO: METRICOOL HANDOVER, by the person's own Drive or Dropbox link."
---

## Before anything else: is this skill on here?

Before doing any of this skill's work, call the door's `skill_switch` tool with `skill` set to `social-studio-pictures`.

- Carry on with the skill below ONLY if the answer says this skill is a core skill, or that it is on in this workspace.
- If the answer says it is off: stop here. Tell the owner, in their language, that this skill is switched off in this workspace, and do nothing else from this skill.
- In every other case (no answer, an error, the tool is not available, the answer says the switch could not be read, or any answer you do not recognise): stop here. Tell the owner plainly that the skill switch could not be read, so this skill was not used.

# SOCIAL STUDIO: PICTURES

The campaign's picture shelf. Each picture is kept on the campaign as its own piece, named for its post, so it is always clear which picture goes with which words. The records' copy is private: it is never the picture Metricool gets. Metricool gets the person's own Drive or Dropbox link at handover.

Speak as the counterpart the room instruction names, in the person's language: plain words, verdict first, first-person plural, dates dd/mm/yy. **One beat per turn.** No action name, id, code or upload address ever reaches the person.

Read [landing.md](references/landing.md) before any write, for request ids, receipts and held acts. On a door that holds acts for approval, each upload waits for the owner's yes on the approval page before it can be sent; say so, and never say a picture is kept before its receipt says it is complete.

Open with one sentence: “I'll check which posts need pictures, then keep each one with its post.” / «Guardo quali post hanno bisogno di foto, poi tengo ognuna col suo post.»

## 1. Which brand, which posts

1. `list_projects` with `ids: true`; brands are the projects ending in ` SOCIAL`; several and none named: ask which. Then the campaign the pictures are for.
2. `list_tasks`, `project` the campaign, `format: "json"`, `ids: true`, for the posts and their dates.
3. `list_pieces`, `project` the campaign: it returns the campaign's id (`project_id`), and each post's pieces. The pictures already kept are the pieces named `P03 - PICTURE 1`, `P03 - PICTURE 2`, `P03 - VIDEO 1`.
4. The brand's line, `search_records` with `text: "SOCIAL BRAND: <BRAND>."`, `state: "live"`, no tag, names the brand's rule tag (never build it); then `search_records` with that `tag`, `state: "live"`, `limit: 50`: the look rules, so a picture that breaks one (a never-do about faces, logos, text on pictures) is named before it is kept.

Match each picture to a post with the person: “This one for Friday's post?” Never guess which post a picture is for.

## 2. Before a slot is opened: the type and the size

Accepted: **PNG, JPEG, GIF, WebP, MP4, QuickTime (.mov) and WebM**, up to 64 MB each. Anything else is refused by the records, so ask before opening anything:

- An iPhone photo (HEIC) or a RAW file: “That one is in a format the records can't keep. Export it as JPEG or PNG and send me that.” / «Questa è in un formato che l'archivio non tiene. Esportala in JPEG o PNG e mandami quella.»
- Over 64 MB: ask for a smaller export.

Know the exact size in bytes and the exact type before opening the slot; the slot is opened for that size and that type only.

## 3. Keep the picture

For each picture, one at a time:

1. **Name the piece.** The next free number for that post: `P03 - PICTURE 1`, then `P03 - PICTURE 2`. A video is `P03 - VIDEO 1`. The picture that goes out is `role: "final"`; an alternative the person wants kept is `role: "option"`. One piece per picture, always, because a piece shows only its latest version of each role.
2. **Open the slot**: `request_piece_upload` with `project_id` from `list_pieces`, `piece` the name (a new picture piece is started by its name), or instead `piece_id` from `list_pieces` when adding a version to a picture piece already kept (exactly one of the two), `role`, `file_name` the file's own name, `size` the exact bytes, `media_type` the exact type (`image/png`, `image/jpeg`, `image/gif`, `image/webp`, `video/mp4`, `video/quicktime`, `video/webm`). Keep the `request_id`.
3. **Send the bytes** within ten minutes: one raw POST of exactly `size` bytes to the slot's address, with `Content-Type` the same type. This is done by Claude, never by the person, and the address is never shown to them. In Claude Code, Claude sends it from the file on the person's computer. In any other Claude, see section 4.
4. **Read the receipt**: `read_piece_upload` with the same `request_id`. Only `complete` means kept; say so then, and not before: “Friday's picture is kept with the post.” / «La foto di venerdì è con il suo post.» Anything else is said as it is: still waiting, expired (open a fresh slot), or refused with its reason in plain words.

When the door refuses a piece by name because this workspace has not been updated for it yet, say: “Pictures can't be kept on this workspace yet; the words are safe, and the pictures can go to Metricool from your own link at handover.” / «Su questo spazio di lavoro le foto non si possono ancora archiviare; i testi sono al sicuro, e le foto arrivano a Metricool dal tuo link al momento dell'invio.» Then stop this skill; never work around it.

## 4. When this Claude cannot send a file

Whether a Cowork chat or a claude.ai chat can send a picture's bytes to a slot is not yet measured. So: try only where Claude can reach the file and make the request itself; when it cannot, say so plainly, without blaming the person:

“This Claude can't send the picture into your records itself. Two ways: open this project in Claude Code on your computer and say file the pictures there, or skip it, because Metricool only needs your own Drive or Dropbox link at handover.” / «Questo Claude non riesce a mettere la foto nel tuo archivio da solo. Due strade: apri questo progetto in Claude Code sul computer e di' lì archivia le foto, oppure lascia stare, perché a Metricool basta il tuo link di Drive o Dropbox al momento dell'invio.»

Never ask the person to send the bytes themselves, run a command or handle an address.

## 5. Pictures still to come

When a post waits on a photographer or a designer: `open_wait` with `task` the post's title, `project` the campaign, `waiting_on` who (their name as the person says it), `because` what is owed («the cover photo for the Friday post»). It shows on THE DAY. When the pictures arrive and are kept: `release_wait` with the same `task`, `project` and `waiting_on`, on the person's word that it came.

## 6. Close

One short paragraph: which pictures are kept, for which posts; which posts still have none; what is waiting and on whom. Say they are kept with the campaign, beside the words, and listed on the campaign's page in PROJECTS, where each one opens. Then the next phrase: “When you're ready, say send Friday's posts to Metricool.” / «Quando vuoi, di' manda i post di venerdì a Metricool.» Last, when a picture was kept, call `show_social_month` once so the person sees where the month stands; where that tool is not in this conversation, say nothing about it.

## Never

- Make, edit, crop, filter or retouch a picture.
- Show an upload address, or ask the person to handle one.
- Open a slot for a type or size the records refuse; name the accepted types and ask for an export.
- Say a picture is kept before the receipt says complete.
- Make the records' copy of a picture public, or offer it to Metricool.

## Tools

Reads: `skill_switch`, `list_projects`, `list_tasks`, `list_pieces`, `search_records`. Writes: `request_piece_upload`, `read_piece_upload` (the receipt), `open_wait`, `release_wait`.

## What is not yet known, and what this skill does meanwhile

- Whether a Cowork chat or a claude.ai chat can send a picture's bytes into a slot. Meanwhile: section 4; try only where Claude can reach the file itself, and otherwise offer Claude Code or the person's own link at handover.
