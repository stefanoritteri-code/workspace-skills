# Production tasks and waits

Read current `list_tasks`, `list_waits` and `search_work` before changing work; complete task pagination before writes. Do not duplicate an existing adopted follow-up. Apply [landing.md](landing.md) for attribution, exact decisions, dates, holds and receipts.

An adopted new project uses `make_project` with only new `request_id` and `name`; confirm it before creating its tasks. A task uses actual title/project and an agreed deadline, or an honest target as `aim`. Do not create a project merely because a page was saved.

`open_wait` needs an existing open task, `waiting_on`, and the owner's actual `because`, with project if necessary. Confirm a prerequisite task before opening the wait. A prepared draft is not a sent request and does not justify a response wait. A person's missing card does not make a wait invalid or authorize card creation.

Use `close_task` only for actual authorized completion, with the real task and project to disambiguate. Use `release_wait` only when the awaited thing is actually reported/observed received, with the actual task and `waiting_on`. If the tool calls for confirmation, resolve it with the owner before `confirm: true`. A completed task does not automatically release a wait. A passed date is not completion. Reread changed state after confirmed receipts; refusals, holds and uncertainties remain visible.
