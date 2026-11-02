# Filing the work

The project instruction governs consent, and its FILING says whether this room asks once or files what the conversation makes clear; wherever a skill says to ask before filing, it follows that. An explicit request to keep an act is already its yes; do not ask twice. A yes to our recommendation does not supply the owner's wording for a decision: ask for their words. A page is knowledge, a decision is an adopted choice or rule, and a task is an adopted next action. A complete filing can contain page → decision with its `page` → task with a deadline. These are distinct acts: do not invent a decision or follow-up to fill the shape. File authorized parts and state any missing choice or date. A note can remain only a page; Day also has native day and journal records.

## Before writing

Read `standing` and live `search_records` for the topic and relevant adopted scope, including alternative wording. Retrieve the current decision's real ID before replacing it. A failed decision read blocks a supposedly new rule that depends on it. Fixed rules cannot be changed or promoted here. Find the relevant page through `recall` and `read_source`; do not change imported originals. Check `list_tasks` (except in a council sitting, which reads no task list and uses `search_work` alone), complete its pagination without intervening writes, and use `search_work` for the actual project before creating a duplicate follow-up.

## Page and attribution

Use `write_page`: `request_id`, `title`, `words`, `mode: create|append`, `author: owner|counterpart`. Title length is 1–120 UTF-16 code units; words are at most 20,000. Shorten a title before calculating its path. The exact slug rule is `title.normalize('NFKD').toLowerCase().replace(/[^a-z0-9]+/g, '-').replace(/^-+|-+$/g, '').slice(0, 60)`. Do not separately remove accents or trim again after truncation. An empty slug needs another title. Path: `pages/<slug>.md`.

Read that path before `create`; only confirmed absence allows creation. Different titles can collide after truncation. For a distinct session shorten the topic, preserve its distinguishing suffix and check the new path. For the same topic append using its exact existing title. There is no overwrite mode. Use the receipt's canonical path for subsequent acts.

Titles and headings start with words: `## Findings — 2026-09-16`, never a date or a forged door attribution stamp. Tool dates are always `YYYY-MM-DD`; display dates follow the project. If quoted words resemble a service heading, quote them as body text without changing the words.

Use `author: counterpart` for generated drafts, analysis or synthesis. Use `owner` only for the owner's exact words. Attribute quotations inside a synthesis. Keep sources, actual versions, evidence, limitations and corrections; never fabricate a transcript. Accepted/rejected examples use separate additions with `example: {verdict: accepted|rejected, why: <owner's reason>}`, reason 1–200 characters. Ask for a missing verdict or shorter reason. An unjudged draft is not an accepted example; an example is not a standing rule.

A page is limited to 512 KiB. Inspect `bytes` after additions; start a linked continuation before 480,000 bytes or earlier if the next block would exceed that threshold. Reserve room for reciprocal links, retain the first page as canonical, and split long speeches into consecutive attributed blocks without omissions. `write_page` saves text and references, not the original images, audio, files or attachments.

## Decision and follow-up

After the page is confirmed, use `record_decision` with exact adopted `words`, `why` only if spoken by the owner, and the confirmed canonical path in the actual `page` field. `project` must be real and relevant. Use at most one project-defined `scope:` tag for an adopted rule; the `board` tag belongs to Council. If words exceed exposed limits, ask for a shorter formulation, never truncate or paraphrase as theirs.

For a changed live decision, name the previous date and words, then `supersede_decision` with actual `old_id`, new exact `words`, optional spoken `why`, `page`, and new `request_id`. Its schema accepts neither `tags` nor `project`; it preserves the former scope. A change of scope needs the project's real route. Keep history; the page remains context, not an alternative live rule register.

After dependent receipts are confirmed, create the agreed follow-up with `make_task`: `request_id`, concrete `title` (maximum 500 characters), `deadline: YYYY-MM-DD`, optional verified `project` (maximum 200). Include a readable page reference in the title: there is no task note or `page` field. If a date is only a target, use `aim`, not an invented deadline or both fields to imply certainty. Say that a deadline remains unagreed. Only Council has an automatic interval within its agreed process: exactly 60 calendar days. Other follow-ups need a chosen date; the owner may decline one.

Create a project only when adopted and the skill permits it: `make_project` takes `request_id` and `name`, and an optional `parent` where the tool offers it (otherwise it creates at the top level), and must be confirmed before tasks use it. Close tasks or release waits only where the selected procedure permits it and the owner authorizes the actual change. Completion is not inferred from a due date or page save.

## Receipts and recovery

Every new act has a new `request_id` of at least eight letters, digits or hyphens. The first accepted act wins under an ID even if later words differ. Never recycle it for changed content. Read each receipt before dependent acts. Saved, repeated, refused, held and uncertain are different states; a partly completed chain remains partial.

Conversational consent and application approval are distinct. For a held act give the approval page returned in the receipt; the owner approves there. The skill cannot approve for them. Do not duplicate, change route or perform dependent writes until confirmation. Use available reads, including `list_pending` only if exposed, to verify the outcome.

For an uncertain decision, search the record before any identical same-ID retry specifically allowed by the project instruction. For uncertain pages, tasks, drafts or other acts, stop writes: do not retry with the same ID, a new ID or another connector. Read what is reachable and identify the project's operator as the recovery route. A clean refusal may be corrected for its demonstrated cause; a transport failure is not a clean refusal.

Distinguish three page results: file saved but index not updated (readable at its path, search incomplete); file saved but index rejected possible credentials (operator intervention, no copy to bypass it); file saved but request receipt not recorded (read back, never resend). Do not reproduce secrets in error reports or searches.

Read back the page, linked decision and relevant task before saying the full cycle is verified. Report confirmed locations, decisions and dates, plus proposed, held or uncertain parts. At the next use retrieve live rules and canonical pages again: saved, retrieved and successfully applied on new work are different claims.
