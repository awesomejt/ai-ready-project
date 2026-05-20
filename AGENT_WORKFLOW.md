# Agent Workflow

Operating loop for interactive assistants and recurring local or cloud agents.

## Single Session Mode

Use this mode when a human starts an assistant manually.

1. Read `AGENTS.md`.
2. Read `README.md`, `MEMORY.md`, `TODO.md`, and `status.yaml`.
3. Read project docs relevant to the task, especially `docs/Requirements.md`.
4. Check `git status`.
5. Plan the work, ask for critical decisions, then implement the selected task.
6. Run appropriate tests or validation.
7. Update `TODO.md`, `MEMORY.md`, and docs as needed.
8. Summarize the result and any follow-up.

## Agentic Loop

Use this loop for scheduled or autonomous agents.

1. Pull the latest changes.
2. Read `AGENTS.md`, `MEMORY.md`, `TODO.md`, and `status.yaml`.
3. Append runtime logs to the agent manager's log storage, not to Git.
4. Act on `status.yaml`:
   - `stopped` - halt.
   - `paused` - halt without work.
   - `blocked` - halt until the blocker is resolved.
   - `working` - another worker is active; skip this cycle.
   - `error` - halt and require human recovery.
   - `active` - continue.
5. Pick the highest-priority unblocked task from `TODO.md`.
6. Set `status.yaml` to `working` if multiple agents may run.
7. Work only that task.
8. Update tests, docs, `TODO.md`, and `MEMORY.md`.
9. If blocked, move the task to `Blocked`, set `status.yaml` to `blocked`, and record the exact next human action needed.
10. If complete, move the task to `Done` and return `status.yaml` to `active` unless the project is complete.
11. Commit only coherent changes when the workflow explicitly calls for commits.

## Chat Logs

Full transcripts are not committed. Temporary local transcripts may be written under `agents/chats/`, but Markdown transcript files there are ignored by Git.

Workflow managers should copy transcripts and runtime logs to external storage. Hermes-compatible defaults:

- Runtime logs: `/var/log/hermes`
- Mirrored logs: `/mnt/hermes/logs`
- Project outputs and transcripts: `/mnt/hermes/output/<project-name>/`

For n8n, OpenClaw, or another manager, use equivalent configured output storage.

## Blocker Handling

When blocked:

1. Stop the task.
2. Add or move the task to the `Blocked` section in `TODO.md`.
3. Add a short item to `Needs Attention` if the project uses that section.
4. Update `status.yaml` with `status: blocked`, the reason, phase, worker, and timestamp.
5. Add a concise entry to `MEMORY.md`.

Do not guess on credentials, account access, platform policy, security-sensitive behavior, or current external facts.
