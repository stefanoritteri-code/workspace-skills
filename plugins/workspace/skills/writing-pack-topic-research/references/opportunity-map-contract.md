# Topic Opportunity Map contract

> Reference for writing-pack-topic-research. Read when the owner asks for a map, tracker, comparison grid, or reusable opportunity analysis.

The Topic Opportunity Map is one durable document with a comparison table inside it. The clusters are records that share the same fields and get re-rated on every refresh, so they belong in the table; the scope, the ranking, and the reason the leader wins stay prose.

## Where it lives

- Always: the full map in the chat.
- In the room: on their yes, a page in their library via `write_page` (`author: counterpart`), titled as below. Pages can only be appended to: a refresh is a dated `append` that restates the scope line, the ranking, and only the rows that changed or are new; a cluster's current state is its most recent row.
- Terminal: the brain's notebooks, under `ideas-lab/topic-research/map-<topic-slug>.md`, edited in place.

## Title

`Topic Opportunity Map: <topic>` unless the owner supplies a project name.

## Required structure

Begin with a compact scope block: the decision, audience, platforms, formats, timeframe, research date, and material limitations. Follow it with a ranked opportunity summary in prose: which cluster leads, which is the credible runner-up, and the one reason the ranking could flip. Then the table, titled `Opportunity clusters: <topic>`. Keep only the top three to six clusters that could plausibly win; a cluster the owner would never select does not earn a row.

Columns, and no more:

| Column | Meaning |
|---|---|
| **Cluster** | the stable name — the row's identity on every later refresh; name it after the audience tension, not a keyword that will drift |
| **Tension and promise** | the audience problem underneath the cluster and the result most sources offer |
| **Evidence** | the strongest representative sources with creator, format, and relative performance when established |
| **Sources** | the canonical link, or the strongest one when several support the row |
| **Saturation** | low · moderate · high · unclear |
| **Counter-signal** | the strongest evidence against the pattern |
| **Unclaimed gap** | the specific audience, question, proof, consequence, or format weakly served |
| **Recommended angle** | an original, useful direction the owner could test |
| **Status** | watch · candidate · selected · tested · retired |
| **Confidence** | the calibrated label (confirmed / early / low) |
| **Researched** | when this row's evidence was last checked — what makes a stale conclusion visible six weeks later |

One line per cell; no cell runs past two lines. Leave a cell empty rather than filling it with a guess. Order rows by Status so watch and candidate rows separate from the ones already selected or retired. Preserve enough source detail in each row that a later conversation can inspect and refresh the conclusion without redoing the whole study.

## Evidence semantics

Include only sources actually read. Never create illustrative entries that look like evidence. When several sources support one cluster, keep them together and distinguish creator-relative performance from raw popularity. Leave unknown values unknown.

When updating, read the existing map first, match rows by the **Cluster** name and its audience tension, and revise the changed cells. A genuinely new cluster is a new row. Never rebuild the table to apply an edit: recreating rows destroys the Researched dates and any status the owner set by hand, which is the whole reason the map is durable. Do not create a duplicate map because the topic spelling changed.

## Refresh behavior

On refresh, preserve earlier Researched dates and statuses rather than stamping every row with today. Add recent signals, mark stale conclusions by moving Status or lowering Confidence, and say whether the opportunity ranking changed. A removed source does not remain active evidence. If the owner corrects a source, revise the affected row and rerun its conclusion.

## Companion brief

The map holds the structured evidence. A Topic Research Brief holds the narrative decision and recommendation. Name both when they exist so future conversations can find the evidence and understand why the selected opportunity won.
