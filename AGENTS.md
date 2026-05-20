# Instructions for AI Coding Assistants

Start here before doing any work in this repository.

## Project Purpose

This repository is a general AI-ready project template. It is meant to work for interactive AI-assisted work first, while still being structured enough for light agentic workflows.

For project-specific requirements, read `docs/Requirements.md`.

## Required First Reads

Before planning or editing, read:

- `README.md`
- `MEMORY.md`
- `TODO.md`
- `status.yaml`
- `docs/Requirements.md`
- `docs/Tech-Stack.md`
- Any files directly related to the requested task

If the task touches architecture, sequencing, or delivery, also read `docs/Architecture.md` and `docs/Implementation.md`.

## Root Files

The root files are the durable handoff contract:

- `AGENTS.md` - AI assistant instructions.
- `README.md` - human-facing project overview.
- `TODO.md` - task tracking, priorities, blockers, and completed work.
- `MEMORY.md` - persistent decisions, milestones, context, and run notes.
- `status.yaml` - project state for humans and automation.
- `.gitmessage` - Conventional Commit template with AI attribution fields.

## Working Rules

- Check `git status` before editing.
- Pull latest changes before starting when network and permissions allow.
- Do not overwrite user changes.
- Keep edits focused on the current task.
- Record meaningful decisions, blockers, and milestones in `MEMORY.md`.
- Keep `TODO.md` current when tasks are added, started, blocked, or completed.
- Update docs when behavior, setup, requirements, or workflows change.
- Add tests or validation steps appropriate to the project and risk.
- Do not commit secrets or credentials.

## Status Workflow

Use `status.yaml` as the shared state file:

- `active` - work may proceed.
- `paused` - do not perform automated work.
- `blocked` - waiting on a human decision, credential, source file, or validation.
- `working` - a human or agent is actively changing the repo; other agents should skip.
- `error` - repo or automation state is unsafe; stop and request recovery.
- `stopped` - project is complete or intentionally shut down.

Automated agents should set `working` only while actively editing, and return to `active`, `blocked`, `error`, or `stopped` before ending a run.

## Project Structure

```text
/                         # Root folder with the durable handoff files
  README.md               # Human-facing overview and setup
  AGENTS.md               # AI assistant instructions
  TODO.md                 # Prioritized tasks and blockers
  MEMORY.md               # Persistent project memory
  status.yaml             # Agent/human workflow state
  .gitmessage             # Commit template with AI attribution

  docs/                   # Requirements, architecture, stack, implementation notes
    Requirements.md
    Architecture.md
    Tech-Stack.md
    Implementation.md
    diagrams/

  agents/                 # Optional supplemental AI context
    Chat-Template.md      # Template for local or external chat transcripts
    Decisions.md          # Optional decision log when more detail is useful
    Research.md           # Optional research notes and references
    chats/                # Local transcript workspace; transcript files ignored

  src/                    # Project source, when applicable
  build/                  # Build artifacts; ignored by Git
  working/                # Temporary scratch files; ignored by Git
```

## Chat Logs And External Agent Logs

Chat transcript files are useful for context but should not be committed by default. Keep temporary transcripts under `agents/chats/` if needed; Git ignores Markdown files in that folder while keeping the folder placeholder.

Agent workflow managers should copy or mirror full transcripts and runtime logs to their own storage. Hermes-compatible defaults are:

- Runtime logs: `/var/log/hermes`
- Mirrored logs: `/mnt/hermes/logs`
- Project output and transcripts: `/mnt/hermes/output/<project-name>/`

For n8n, OpenClaw, or another orchestrator, use equivalent configured storage.

## Commit Guidance

Use Conventional Commits:

```text
type(scope): short description
```

Include AI attribution for AI-assisted commits using `.gitmessage`.
