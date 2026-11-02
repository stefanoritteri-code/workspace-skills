# A release post from the release plan

The release plan (the music skill's release recipe) makes a release's posts as planned posts on the release project: each has a name ("Release post 1"), a planned day and often a caption kept as an option, and none has a code. Social Studio works on coded posts. So a release post is brought into the social calendar once, as a coded post linked to the planned one, and only on the person's yes. From then on it is an ordinary post: the coded post is the post, and the planned one is where it came from. Never draft, send or make a second post from the planned post itself, because two posts for one release day would be two social systems.

This file is the same in MONTH PLAN, POSTS and METRICOOL HANDOVER.

## 1. Can this workspace link them?

Look at the description of `make_task` in this Claude. When it offers no `piece_id`, the link can't be made here yet. Say “That release post was planned in the release plan, and this pack can't yet take it into the social calendar, so I haven't drafted or sent anything for it.” / «Quel post è stato pianificato nel piano dell'uscita, e questo pacchetto non riesce ancora a portarlo nel calendario social, quindi non ho scritto né mandato niente per quel post.» Do nothing more for that post. The other posts go on.

## 2. Find the release posts, and the ones already brought in

1. **The release project**: `list_projects` with `ids: true`. It is the project the release plan made, holding the release-day task and the posts.
2. **The days**: `show_social_month` for each month the release covers. A release post not yet brought in is listed under the release project with no `taskId`. One already brought in is listed by its coded title. When the month view is not in this conversation, ask the person which day each post was planned for. Never guess a day.
3. **The ids and links**: `list_pieces`, `project` the release project, with no role. This lists every piece by its exact name and `piece_id`, including a planned post that has no caption, which a read filtered by role would leave out.
4. **The captions**: `list_pieces`, `project` the release project, `role: "option"`, `text: true`. A planned post missing from this read simply has no caption.
5. **The codes already used**: `list_tasks`, `project` the release project, `format: "json"`, `limit: 50`, sending `next` back as `from` until `next` is absent, so no page is missed. Open tasks are only part of the history: a post that was drafted, sent or dropped can still have pieces (`P03 - TEXT`, `P03 - PICTURE 1`) and links (`P03 · METRICOOL · …`) named by its code, so also read the piece names and the link titles from the same read in step 3, which returns the project's links beside its pieces. The next free code is one above the highest code found anywhere in these reads. A code that left no task, piece or link names nothing, so it cannot collide.

Whether a planned post is already brought in is never decided from a title, because a title can be shortened. The records decide it by the link itself: a second coded post for the same planned post is refused, and the refusal names the coded post that already has it. So never bring it in twice: when the records answer that it is already on the calendar, go on with the coded post they name.

## 3. Ask, then bring it in

Propose one line per release post: its day, the network and the local time from the brand's channels, rhythm and best times (our suggestion when Metricool is not here), and the caption it carries. Ask on the buttons: “Put it in the social calendar” / «Mettilo nel calendario social» · “Change something” / «Cambio qualcosa» · “Not now” / «Non ora».

On the person's yes, one `make_task` for each release post:

- `project`: the release project, because a post can only be linked on its own project.
- `title`: `P01 · INSTAGRAM · 18:00 · RELEASE POST 1`. That is the next free code from step 5 of section 2 (never reuse one), the network or networks joined with `+`, the local time, then the release post's name in capitals. At most 100 characters. A longer title is shortened with the person, never cut by us.
- `deadline`: the planned day, as `YYYY-MM-DD`.
- `piece_id`: that post's id from `list_pieces`.
- `request_id`: a fresh one for each post.

The receipt says the post is linked. When the records answer that the post is already on the calendar, nothing new was made: go on with the coded post they name. When they refuse for another reason (the post is not a post, it is on another project, or this workspace does not have it), say so in plain words and do nothing more for that post.

On “Not now”, say “It stays in the release plan, and I haven't drafted or sent anything for it.” / «Resta nel piano dell'uscita, e non ho scritto né mandato niente per quel post.»

## 4. Then the ordinary path

The coded post is now a post like any other, and the release project is its campaign. For it, every read and write that says the campaign uses the release project, the way the practice post uses the standing project. A caption the release plan kept is one of the options POSTS shows. It is filed as an option under the post's text piece (`P01 - TEXT`) like the others, and it is never the final without the person's choice.
