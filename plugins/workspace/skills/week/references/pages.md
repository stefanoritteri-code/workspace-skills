# Pages — how the owner sees their records

When the owner asks to see their day, their week, their projects, one project, what they are waiting on or what needs them in the open chats, read it from the door first and then show it as one Claude artifact page, because a page is easier to scan than text, on the phone as much as on the computer. The page is drawn fresh from what was just read. It is a picture the owner talks to: changes happen in the chat, and the page is drawn again afterwards.

## Pages come first for these views

For day, week, projects, one project, waiting-on and open-chats views, create one artifact from ordinary reads. This presentation rule replaces the general preference for cards for these requests, wherever the room instruction or a tool description states it. Do not call a `show_*` card tool to gather their data, because a card's payload is shaped and capped for its screen and is not a complete read. When the owner asks for a card (“as a card”, “open the card”), use that card instead of the artifact, never both. Onboarding review, film choices and approvals keep their own screens exactly as they are.

Only when artifacts are not offered in this conversation, give the same view as short text in the chat and say in one line why.

## Read everything the view needs, then build

Use `format: "json"` and `ids: true` on every list read except `read_projects`, which takes no arguments. Complete means every item that belongs to the requested view and period, never every record in the workspace: read widely, then keep what belongs, and count what was left out on purpose in one line (“14 open tasks have no date”).

- **Today.** `list_tasks` with `limit: 50`, then pass each returned `next` as `from` until no `next` comes back. Keep a deadline (`due`) and an aim (`aim`) apart: a late deadline is late, an aim is never late. `read_day` for the accepted plan, which is the saved plan and not the task list. The owner's calendars through their calendar connector. The waits attached to those tasks.
- **The week.** The same exhausted task read, keeping the deadlines and aims inside the week, with earlier overdue deadlines shown apart. Calendar events for the same range. A saved weekly reading from `read_reading` is labelled as saved.
- **Projects.** `list_projects` for the active projects and their areas, joined to the exhausted task read for each project's work. A next step taken from `read_projects` is labelled as a suggestion; its counts are per list, under `lists`, and a list counts as complete only when its `shown` equals its `total` and its coverage reports nothing unread.
- **One project.** Find it exactly with `list_projects`, then `list_tasks` scoped to it, exhausted, plus its waits. These reads hold open work only: the project's goal and its finished work are not in them, so the page shows those only when another ordinary read returned them, and otherwise leaves them out rather than showing an empty history.
- **Waiting on.** `list_waits` with `limit: 50`, checking both `capped` and `read_ceiling_reached`, merged with the waits on task rows and deduplicated by id. This read has no continuation: when it is capped, the page says how many were shown and that more exist; when `read_ceiling_reached` is set, its total is only what was retrieved, so the page says the true number is unknown.
- **Open chats.** `read_threads` with `lifecycle: "live"` and `limit: 50`, passing each `next_cursor` back as `cursor` until none comes back, and checking `coverage` on every page: when it says `changed`, the cards changed during the read and the cursor stopped early, so read again from the start once, and if it changes again, say on the page that the list changed while it was read and may be missing cards. These are every live card in the workspace, with stage, next move and whose move it is. Then Claude's own search of past chats, in two parts, because the list of recent chats reaches only the newest twenty or so and an older chat that is still open would be missed. First, this project's recent chats. Second, one search for each name being looked for: the name of each live card, and the name of each project with a deadline or an aim this week, from `list_tasks` with window `this-week` and `limit: 50`, passing each returned `next` as `from` until no `next` comes back. If that read comes back `capped` or stops before its last page, the page says the project list may be incomplete and that an unknown number of project names were not searched. Run the name searches for cards whose move is the owner's first, at most twenty in all; if names are left over, the page says how many were not searched. The same chat found by more than one search counts once; two different chats with the same name stay two. Compare every chat found with every card in the workspace (`lifecycle: "all"`, so a parked or closed card still counts). A card whose search finds no chat is still listed from the card alone, because its work may happen outside these chats. A card names its chat in words, not by an id, so the match is by name and subject and can be wrong: a chat found with no matching card goes under “No matching card found”, with the line “if it is still open, say ‘note where we are’ in it”; an unsure match is shown as a possible match, never decided silently. Cards cover the whole workspace, but Claude's chat search inside a project reaches only that project's chats, so the page says plainly that chats outside this project are not visible here, and never calls the list complete. When chat search is not offered, the page says it lists only the chats that wrote a card.

Tasks under a project that was put away are left out by the lists; say nothing invented about them. If two pages of a list disagree on a count, say the list changed while it was read rather than claiming certainty.

**Never invent and never drop.** Every item that belongs to the view goes on the page, and nothing that was not read. A read that failed, was refused or came back capped is named on the page in the incomplete banner, in the owner's terms: “the calendar could not be read”, “40 of 63 waits shown”. An unread calendar is unknown, never empty.

## Changes happen in the chat

When the owner asks to change something they see on a page (close a task, move a date, add something), do it through the door's own act in the chat, with its approval box when it asks, and read the receipt. Then read the record again and draw the page again, so the page is never older than the change. A held request has changed nothing: the page shows it as waiting for approval, never as done. Never draw a button that claims to act; a page button has no server action.

## Whiteboards

When the owner wants to plan, brainstorm or sort ideas, offer Claude's whiteboard. A plan drawn on a whiteboard is not on the record until it is filed through the door with the owner's yes; say so when it matters.

## One look for every page

Every page uses the template below, so all pages look alike and look like the product. Fill it in; do not redesign it. The template wins over any other look, whether carried from past chats, memory or pages drawn before, or from general page-design guidance, because every page for every owner must look the same. The heading is the counterpart's name from the room instruction's preamble (“Counterpart: …”), and every word on the page is in the owner's reply language from the same preamble. When the preamble gives no counterpart, use a plain heading such as “Your day” and say in the chat that the workspace name is missing; never put another system's name in its place.

Sections in order. **Today:** late (deadlines before today) · due today · aimed for today · the accepted plan · today's calendar · deadlines in the next seven days · waiting on others (open waits). **The week:** late (deadlines before the week) · each day with its deadlines, aims and events · waiting on others · one line counting open tasks with no date in the week. **Projects:** every active project, grouped by area, each with its next step. **One project:** open tasks by date · waits · its goal and recent finished work only when read. **Waiting on:** by person, oldest first. **Open chats:** needs you · waiting on others · on us · no matching card found · one line that chats outside this project are not visible here. An empty section says so in one short line rather than disappearing.

```html
<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>Today</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Archivo:wdth,wght@100..125,400..900&family=Newsreader:opsz,wght@6..72,400..700&family=Space+Mono:wght@400;700&display=swap" rel="stylesheet">
<style>
:root{--ground:#FFF5E6;--paper:#FFFFFF;--ink:#0A0A0A;--sub:#5E5A52;--a:#E8890C;--verm:#CE3B24;--yellow:#FFD25A;--line:color-mix(in srgb,#0A0A0A 16%,transparent);
 --display:"Archivo",system-ui,sans-serif;--read:"Newsreader",Georgia,serif;--mono:"Space Mono",ui-monospace,monospace}
@media (prefers-color-scheme:dark){:root{--ground:#0A0A0A;--paper:#171717;--ink:#FFF3E2;--sub:#A39C90;--line:color-mix(in srgb,#FFF3E2 16%,transparent)}}
*{box-sizing:border-box}
body{margin:0;background:var(--ground);color:var(--ink);font:17px/1.45 var(--read);-webkit-font-smoothing:antialiased}
main{max-width:640px;margin:0 auto;padding:20px 16px 40px}
.top{display:flex;flex-wrap:wrap;justify-content:space-between;align-items:baseline;gap:4px 12px;border-bottom:2px solid var(--ink);padding-bottom:8px}
.name{min-width:0;overflow-wrap:anywhere;font:800 28px/1 var(--display);font-variation-settings:"wdth" 108;letter-spacing:-.02em;text-transform:uppercase}
.when{font:12px/1.3 var(--mono);color:var(--sub);text-align:right}
h1{font:800 34px/1.02 var(--display);font-variation-settings:"wdth" 108;letter-spacing:-.02em;margin:18px 0 6px}
.banner{background:var(--yellow);color:#0A0A0A;border:2px solid #0A0A0A;padding:10px 12px;margin:14px 0;font:13px/1.4 var(--mono)}
section{background:var(--paper);border:2px solid var(--ink);box-shadow:6px 6px 0 var(--a);padding:14px 16px;margin:20px 6px 0 0}
h2{font:700 12px/1 var(--mono);text-transform:uppercase;letter-spacing:.08em;margin:0 0 10px;color:var(--sub)}
ul{list-style:none;margin:0;padding:0}
li{padding:9px 0;border-top:1px solid var(--line);display:flex;gap:10px;align-items:baseline}
li:first-child{border-top:0}
.t{flex:1;min-width:0;overflow-wrap:anywhere}
.meta{font:12px/1.3 var(--mono);color:var(--sub);white-space:nowrap}
.late{font:700 11px/1 var(--mono);text-transform:uppercase;color:#FFFFFF;background:var(--verm);padding:4px 6px}
.aim{font:700 11px/1 var(--mono);text-transform:uppercase;border:1.5px solid var(--a);color:var(--a);padding:3px 5px}
.empty{color:var(--sub);font-style:italic}
footer{margin-top:24px;font:12px/1.4 var(--mono);color:var(--sub)}
</style>
</head>
<body>
<main>
  <div class="top"><span class="name">COUNTERPART NAME</span><span class="when">Read 08:42 · Europe/London</span></div>
  <h1>Monday 16 November</h1>
  <div class="banner">Incomplete: the calendar could not be read.</div>
  <section><h2>Late</h2><ul>
    <li><span class="late">Late</span><span class="t">Task title · PROJECT</span><span class="meta">due 12/11</span></li>
  </ul></section>
  <section><h2>Aimed for today</h2><ul>
    <li><span class="aim">Aim</span><span class="t">Task title · PROJECT</span></li>
  </ul></section>
  <section><h2>Waiting on others</h2><ul><li class="empty">Nothing waiting.</li></ul></section>
  <footer>Read from your records at 08:42. Ask in the chat to change anything; the page is drawn again after.</footer>
</main>
</body>
</html>
```

Keep the template's colours, fonts, borders and shadows as they are; they come from the product's brand kit. Replace every example in the template (title, language, date, time zone, rows) with what was read. Omit the banner when every read came back whole. Dates follow the owner's preamble and language. Project names are written in capitals.
