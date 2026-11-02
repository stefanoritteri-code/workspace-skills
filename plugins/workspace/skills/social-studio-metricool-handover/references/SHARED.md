# SOCIAL STUDIO: what every skill relies on

Not a skill. This is the one list of conventions the seven SOCIAL STUDIO skills share, so that a post, its pieces, its rules and its Metricool link can always be matched, by a person or by any of the seven. Each skill repeats the parts it uses in its own words.

## The seven skills, and the order a person meets them

| Folder | Shown as | Names next when it closes |
|---|---|---|
| `social-studio-first-session` | SOCIAL STUDIO: FIRST SESSION | "when you're ready, say plan this month's posts" |
| `social-studio-brand` | SOCIAL STUDIO: BRAND | the next post or plan the change touches |
| `social-studio-month-plan` | SOCIAL STUDIO: MONTH PLAN | "on <draft day> say draft <day>'s posts" |
| `social-studio-posts` | SOCIAL STUDIO: POSTS | "file the pictures" when a picture is missing, otherwise "send <day>'s posts to Metricool" |
| `social-studio-pictures` | SOCIAL STUDIO: PICTURES | "send <day>'s posts to Metricool" |
| `social-studio-metricool-handover` | SOCIAL STUDIO: METRICOOL HANDOVER | "they're waiting for you in Metricool" |
| `social-studio-month-results` | SOCIAL STUDIO: MONTH RESULTS | offers next month's plan |

## The rulings no skill re-opens (21/10/26)

1. One process for any professional who posts: solo, one-writes-one-signs-off, or a company running several artists or clients.
2. Drafts only. These skills never schedule a live post and never publish. The person publishes from Metricool.
3. Create only in Metricool (ruling 11). These skills never edit, move or delete anything in Metricool. A change is a fresh draft, and the person deletes the old one in the planner themselves.
4. Pictures reach Metricool only through the person's own Drive or Dropbox link. The records' copy is never made public.
5. Never set an AI flag. The connector's defaults go out, which means the "made with AI" declaration is off, and the person sets it in Metricool.
6. One workspace per company, one rule tag per artist. The separation is a reading convention the skills keep; the server does not enforce it.
7. The first session is skill seven, two or three short sittings, never one long one.
8. Pictures from a chat: measure first, Claude Code is the fallback.

## Names and keys

| Thing | Kept as | Exact shape |
|---|---|---|
| A brand (artist, client, shop, the person themselves) | an area | Name in CAPITALS: `NORTH BAKERY`. |
| The brand's rule tag | the scope tag on every rule for that brand | `scope:<slug>`, proposed from the area name with the slug rule below, cut to 50 characters: `scope:north-bakery`. **Chosen once, by FIRST SESSION, with a collision check**: before anything is filed under it, `search_records` with that `tag` and `state: "any"`; any record at all means the tag is taken (two names can make the same slug), so it tries `scope:<slug>-2`, then `-3`, until one is empty. The chosen tag is written into the brand's SOCIAL BRAND line, and **every other skill reads the tag from that line, never computes it**. Every skill reads a brand's rules with `search_records`, `tag` that tag, `state: "live"`, `limit: 50`; never with `standing`, which returns every rule of every brand. |
| The brand's line | one decision under the brand's tag, the first ever filed under it | Words: «SOCIAL BRAND: NORTH BAKERY. Rules tag scope:north-bakery. Metricool brand "northbakery" (number 7310321, time zone Europe/London) on Instagram and Facebook. The only brand in this workspace.» The last sentence is either "The only brand in this workspace." or "One of several brands in this workspace." Filed at the questionnaire's start with "Metricool brand not linked yet." in place of the Metricool sentence, then superseded in sitting one when the Metricool brand is confirmed (a supersede keeps the tag). When a second brand starts, FIRST SESSION offers, on the person's yes, to supersede the first brand's line to "One of several brands in this workspace." and move its rhythm from `scope:planning` to its own tag. Every skill finds it with `search_records`, `text: "SOCIAL BRAND: <BRAND>."`, `state: "live"`, no tag, and checks the brand name in its words matches exactly. Skills read the Metricool brand number and time zone from here and check them against Metricool's brand settings before any Metricool call. |
| The brand's standing project | a project under the brand's area | `<BRAND> SOCIAL`: `NORTH BAKERY SOCIAL`. Holds the brand file, the discovery page and the sittings. `list_projects` finding projects whose names end in ` SOCIAL` is how a skill finds which brands exist. |
| The brand file | one saved page on the standing project | Title `BRAND FILE <BRAND>`. Created once with `write_page` `mode: "create"`; every change after that is one dated section added with `mode: "append"` under that exact title, each section headed `## <WHAT CHANGED> — dd/mm/yy`. There is no versioning, so these sections are its history. **Found, never built**: `read_source` with `path: "pages"` lists the saved pages; open the names beginning `brand-file-` and take the one whose title is exactly `BRAND FILE <BRAND>`. (The page path is the slug of the whole title cut to 60 characters, so for a long brand name it is not `brand-file-` plus the brand's tag.) |
| The discovery page | one saved page on the standing project | Title `DISCOVERY <BRAND> dd/mm/yy`. (The brand's name is in the title so two brands set up on the same day cannot collide, since creating an existing title is refused.) |
| "What worked" | a dated section of the brand file | Heading `## WHAT WORKED — <MONTH YYYY> — dd/mm/yy`. MONTH RESULTS appends one per run, and counts them to know whether it is still in the first three check-ins. |
| A rule, a never-do, a lesson, a direction, a reference | a decision under the brand's tag | `record_decision` with `words`, `why` only if the person said it, `tags: ["scope:<slug>"]`. One rule per decision. A changed rule is `supersede_decision` with the real `old_id`; it keeps the old scope tag and takes no tags of its own. |
| The rhythm | a decision (the one rule that may sit outside the brand's tag) | Words begin `SOCIAL RHYTHM:`, for example «SOCIAL RHYTHM: I plan on Mondays, approve on Thursdays and read the month on the first Monday.» Only brand in the workspace: tag `scope:planning`, so THE DAY hears it on a morning it proposes the day. One of several brands: the brand's own tag, and THE DAY does not carry it (a record carries one scope tag only). So every skill that needs the rhythm, for the only brand, also reads `search_records` with `tag: "scope:planning"`, `text: "SOCIAL RHYTHM"`, `state: "live"`. |
| The approver | a decision, and a people card only with a "who they are" line | Words begin `SOCIAL APPROVER:`. |
| A campaign (a month, a single, a tour, a season) | a project under the brand's area | Name begins with the brand: `NORTH BAKERY NOVEMBER`. Made in one step with `make_project_with_tasks`: `name`, `area`, `area_words`, `tasks[]` (at most 50), `note` `{purpose` at most 400 characters`, words}`. |
| A post | a task on the campaign | Title `P03 · INSTAGRAM · 18:00 · SINGLE OUT NOW`, at most 100 characters, the code first. Several networks: `P03 · INSTAGRAM+FACEBOOK · 18:00 · …`. The time is the brand's local time. `deadline` is the publish date, `YYYY-MM-DD`, never in the past. Posted is `close_task`, on the person's word only. Tasks have no notes field, which is why network and time live in the title. |
| A release post from the artist room | a post piece on the release project | Not a post of this pack: no action can tie a coded task to that piece, so the skills say so plainly and never draft, send or duplicate it. Tying it in is app work. |
| The post code | `P01`, `P02` … | Unique within its campaign, numbered in date order when the campaign is made, and never renamed after. It is the only key that matches a post to its pieces and links, because pieces and links belong to the project, not to a task. `P00` is the practice post of the first session, on the standing project. |
| A post's text | a piece | `P03 - TEXT`. `file_piece_text` with `role` `option` (each draft), `final` (the exact words that go to Metricool) or `source` (the person's notes or raw material). `file_name` `P03-TEXT.txt`. |
| A first comment | its own piece | `P03 - FIRST COMMENT`, same roles. |
| A picture or a video | one piece per picture | `P03 - PICTURE 1`, `P03 - PICTURE 2` … one piece each, because a role filter returns only the latest version of that role per piece. A video is `P03 - VIDEO 1`. The one that goes out is `final`; alternatives are `option`. |
| A preview page of an option | a project link | `record_link`, `kind: "option"`, title `P03 · OPTION 2`, a public Claude page that carries the words only, never the person's photos. Offered, never made by default. |
| A Metricool draft | a project link | `record_link`, `kind: "review"`, title `P03 · METRICOOL · <uuid>`, `url` the receipt's `plannerUrl`. The newest METRICOOL link for a post code is the live one. |
| Collaborators | people cards | `make_person` needs a "who they are" line in the person's own words; credits go on with `note_person`. |

**The slug rule** (the same one the house's page landing uses): `name.normalize('NFKD').toLowerCase().replace(/[^a-z0-9]+/g, '-').replace(/^-+|-+$/g, '')`, then cut to 50 characters for a proposed tag (FIRST SESSION only, then the collision check), 60 for a page path (over the whole title).

**Finding the brand.** Every skill except FIRST SESSION starts by finding which brand it is working for: `list_projects` for the projects ending in ` SOCIAL`. None: the person has not set up yet, so the skill says so and offers «set up my social media» / «iniziamo con i social». One: that brand. Several: ask which, on Claude's buttons, before anything else. Then the brand's line (above) gives its tag. No line yet: the first session has not started its filing, so the skill offers «set up my social media» and stops. Only FIRST SESSION makes a brand (its area, its standing project, its line); MONTH PLAN does not. Two brands of one owner are never blended, in one read, one plan or one draft.

## The handover sentence, every time

METRICOOL HANDOVER ends every send with these points, in the person's language, in plain words, all of them, every time. A post is named by its day and date ("Friday's post, 07/11/26"), never by its code:

1. It is a draft in Metricool, and they publish it there.
2. The "made with AI" declaration is off by default and theirs to set there.
3. The time we sent, in the brand's time zone, and the receipt's time as it reads, never claimed to be the same. If the planner shows a different hour, the person checks the account's time zone in Metricool's settings. A time is never changed without the person's yes.
4. When a draft replaces an older one, which old one they delete (the bin icon in the planner, then Confirm), and that one old draft is deleted by hand each time a post changes.
5. The picture: once they see it in the draft in the planner, they turn the link's sharing off again; in our one test Metricool kept its own copy, which opened for anyone with its address, without a sign-in, so a sent picture is treated as public.

The reference wording (English, then Italian):

> Friday's post (07/11/26) is in Metricool as a draft; you publish it from there. Its "made with AI" declaration is off, as Metricool sets it, and it is yours to set there. We sent it for 18:00 on 07/11/26, London time, and Metricool's receipt says 18:00. If the planner shows a different hour, check your account's time zone in Metricool's settings, and don't change the time unless you want it changed. Open the draft and check the picture is there; once it is, you can turn sharing off on the picture's link. In our test, Metricool's copy of a picture opened for anyone with its address, without a sign-in, so treat the picture as public.

> Il post di venerdì (07/11/26) è in Metricool come bozza; lo pubblichi da lì. La dichiarazione «fatto con l'IA» è spenta, come la imposta Metricool, e sta a te impostarla lì. L'abbiamo mandato per le 18:00 del 07/11/26, ora di Londra, e la ricevuta di Metricool dice le 18:00. Se il calendario mostra un'altra ora, controlla il fuso orario del tuo account nelle impostazioni di Metricool, e non cambiare l'ora se non vuoi cambiarla. Apri la bozza e controlla che la foto ci sia; quando c'è, puoi togliere la condivisione al link della foto. Nella nostra prova, la copia di Metricool si apriva per chiunque ne avesse l'indirizzo, senza accesso: considera la foto pubblica.

When a draft replaces an older one, add: "This replaces the draft you got on 05/11/26: delete that one in the planner, with the bin icon and then Confirm. Each change costs one old draft deleted by hand." / «Questa sostituisce la bozza del 05/11/26: cancellala nel calendario di Metricool, con il cestino e poi Conferma. Ogni modifica costa una vecchia bozza da cancellare a mano.»

## The connector actions the pack names

The door's own, from the contract's kept set only: `skill_switch`, `list_projects`, `list_tasks`, `list_people`, `search_records`, `read_source`, `read_reading`, `make_area`, `make_project_with_tasks`, `make_task`, `make_person`, `note_person`, `record_decision`, `supersede_decision`, `write_page`, `file_page_under_project`, `keep_reading`, `move_task_date`, `close_task`, `rename` (with `kind: "task"`, HANDOVER only, for a moved post's time; the contract's merged action, number 32), `open_wait`, `release_wait`, and the file actions `file_piece_text`, `list_pieces`, `record_link`, `request_piece_upload`, `read_piece_upload`.

Metricool's: `getBrandSettings`, `getBestTimeToPostByNetwork`, `getScheduledPosts`, `getAnalyticsAvailableMetrics`, `getAnalyticsDataByMetrics`, and `createScheduledPost` with `draft: true` only. Metricool's edit action and its review flow are never used by any skill, and no skill file names them.

No action name, id, revision, uuid or slot address is ever said to the person. They live inside calls.

## Known limits

Each is a limit the skills state or work within.

1. **The second-brand rhythm move needs the person's yes.** When they decline, the first brand's rhythm stays under `scope:planning` while its line says "One of several brands". BRAND always reads `scope:planning` for a SOCIAL RHYTHM, so it still finds it and offers the move again; the morning read keeps carrying it until then.
2. **Page paths are checked, not reserved.** FIRST SESSION checks that a page's 60-character path is free (`read_source` answers nothing) before it creates the discovery page or the brand file, and shortens the brand's display name with the person when it is taken. A page made outside these skills between that check and the create can still take the path; the create is then refused by the records (they refuse creating an existing path), and nothing is overwritten.
3. **An unlinked earlier draft is matched by network, day and time.** A send whose link was refused after the link check passed has no link, and neither has a draft found again after an unknown outcome, because Metricool's list of drafts carries no planner link and none is ever built. HANDOVER then matches the earlier draft in Metricool by network, day and time, at the current date and, on a move, at the old one. Two drafts on one network at one minute cannot be told apart; the skill then names both and asks the person.
4. **The link check reads the link action's description.** Whether this workspace keeps Metricool links is read from that description; when it does not say so, HANDOVER refuses to send and says why. That is a safe stop, not a fault.
5. **Planning before the first session is finished.** MONTH PLAN may plan right after FIRST SESSION's first step; until the brand file exists, POSTS drafts from the brand's line and the rules filed so far, and says so.
