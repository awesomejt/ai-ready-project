# Instructions for AI Coding Assistants

## Project Overview & Requirements

[Brief 1-2 paragraph summary. Link to docs/Requirements.md for full details.]

## Technical Stack

[Provide technical stack for project]

- Language: ...
- Framework: ... (exact versions where critical)
- Key tools/commands: `npm run dev`, `pnpm build`, etc.
- Setup: exact commands to get the project running.

## Developer Preferences & Coding Style

- Naming conventions, formatting rules, preferred patterns.
- Examples of good/bad code snippets.
- Linter/formatter rules (e.g., “Always run `prettier --write` before committing”).

## Project Structure

[Adjust or change to meet specific project requirements]

**Root files:**
 * README.md - Main, human-readable instruction for using the project, project purpose, and references to other docs
 * CONTRIBUTING.md - How to contribute to this project (for humans)
 * AGENTS.md - AI README file (this document), all AI assistants start here first
 * TODO.md - TODO list of tasks remaining and accomplished, organized by implementation phase and priority

**Project Documents:**:
 * ./docs/Requirements.md - Project requirements
 * ./docs/Implementation.md - High-level order in which the project will be developed/implemented
 * ./docs/Tech-Stack.md - Technical stack and tools, including versions
 * ./docs/diagrams/* - Project diagram images

**Agent-specific:**
 * ./agents/Memory.md - Summary of chat sessions, AI memory to survive chat compaction and token window limitations
 * ./agents/Decisions.md - Summary of key decisions and milestones
 * ./agents/chats/*.md - Folder for creating a chat log per item or session in markdown format

**Project Code and Build:**
 * ./src/* - main source directory for the project
 * ./build/* - build folder for projects that need to create build artifacts, excluded by Git

**Temporary:**
 * ./working/* - a temporary folder, excluded from Git, for temp/intermediate files like utility scripts or wip files

## Workflow & Guardrails

### One-Time Setup

If the project is freshly cloned, set `.gitmessage` as the commit template

```bash
git config commit.template .gitmessage
```

### Working Folders

Create/use the following directories within the project (excluded by Git):
 - ./working : A working folder for temporary files - like a commit message file, temporary tools, assiting code unrelated to project
 - ./build : a build directory for build artifacts (remove if project doesn't use it)

### Workflow

For each iteration:
 - Plan (with possible research if gaps exist)
 - Prompt developer for critical decisions
 - For non-critical path decisions needed, put into dedicated section in `TODO.md` file
 - Update `TODO.md` for identified tasks to be completed now or later.
 - Evaluate `TODO.md` for priority of execution of tasks
 - Implement identified top priority task
 - Write unit and/or integration tests with industry standard code/case coverage
 - Ensure all tests pass
 - Update all documentation related to the task
 - Update chat log with both the user prompt and response
 - Provide a summary of important decisions in `agents/Decisions.md`

### Chat Log

Store all conversations into the AI chat log folder located at `./agents/chats`.

**File name template:**
`YYYY-MM-DD_HHMM_topic.md`

Example: 2026-04-27_1530_bootstrap-cli.md

Chat Log entry:
 - Topic
 - Date and Time
 - Prompt (if any)
 - Output / Content
 - References

### Git Workflow and Instructions
- Use Conventional Commits.
- Always pull latest before starting work.
- Do not commit secrets or credentials.
- **AI attribution**: Every commit involving AI assistance.
- Use AI Git Commit template: `.gitmessage`

### Documentation Workflow

- Chat transcript:
    - Save full conversation logs in [AI Chat log](agents/chats/)
    - One Markdown file per session or iteration
    - Start from [AI Chat Template](agents/Chat-Template.md)
    - Include user prompts and complete assistant responses
- Session summary:
    - Update [AI Memory](agents/Memory.md) with:
        - major decisions
        - rationale
        - milestones reached
        - unresolved questions and risks
    - Update [AI Decisions](agents/Decisions.md) with:
        - major and minor decisions with date/time
- Task tracking:
    - Update [TODO.md](TODO.md) with actionable tasks and status changes, organized by implementation phase and priority
- Requirements alignment:
    - Read and follow [docs/Requirements.md](docs/Requirements.md) before implementing
    - Update requirements only when scope or behavior changes are approved

## Project Structure Reference

- Read `docs/Requirements.md` for Project requirements
- Read `docs/Architecture.md` for project structure and design
- Read `docs/Tech-Stack.md` for the approved technical stack - langauge, tools, frameworks, libraries
- Read `docs/Implementation.md` for implementation plan and phases




