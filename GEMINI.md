# Gemini CLI Configuration (GSD)

This project uses the **Get Shit Done (GSD)** system for meta-prompting and context engineering.

## Slash Command Support

The following GSD commands are available. When a command is invoked (e.g., `/gsd:help`), the corresponding definition file in `.gemini/commands/gsd/` should be read and followed as a system instruction.

### Available Commands

- `/gsd:new-project` - Initialize a new project with a brief
- `/gsd:create-roadmap` - Create a roadmap and phase breakdown
- `/gsd:map-codebase` - Map an existing codebase (brownfield)
- `/gsd:plan-phase <N>` - Create an execution plan for Phase N
- `/gsd:execute-plan <path>` - Execute a specific PLAN.md file
- `/gsd:execute-phase <N>` - Execute all plans in Phase N in parallel
- `/gsd:status` - Check the status of background agents
- `/gsd:progress` - Check project status and next actions
- `/gsd:verify-work <N>` - Perform User Acceptance Testing for Phase N
- `/gsd:plan-fix <plan>` - Plan fixes for issues found during verification
- `/gsd:complete-milestone` - Archive the current milestone and prep for the next
- `/gsd:discuss-milestone` - Brainstorm goals for the next milestone
- `/gsd:new-milestone <name>` - Create a new milestone with phases
- `/gsd:add-phase <desc>` - Add a phase to the end of the roadmap
- `/gsd:insert-phase <N> <desc>` - Insert a phase at a specific position
- `/gsd:remove-phase <N>` - Remove a future phase
- `/gsd:discuss-phase <N>` - Gather context for Phase N
- `/gsd:research-phase <N>` - Perform deep research for Phase N
- `/gsd:list-phase-assumptions <N>` - Surface assumptions before planning
- `/gsd:pause-work` - Create a handoff file when stopping
- `/gsd:resume-work` - Restore context from a previous session
- `/gsd:resume-task <id>` - Resume an interrupted subagent task
- `/gsd:consider-issues` - Review deferred issues and enhancements
- `/gsd:add-todo [desc]` - Capture a todo from the conversation
- `/gsd:check-todos [area]` - List and work on pending todos
- `/gsd:help` - Show the command reference

## Implementation Guide for Gemini Agents

When you see a command starting with `/gsd:`, follow these steps:

1.  **Locate the Command Definition:**
    - Look in `.gemini/commands/gsd/[command-name].md` (local install)
    - If not found locally, check `~/.gemini/commands/gsd/[command-name].md` (global install)

2.  **Read the Definition:**
    - Parse the `<objective>`, `<reference>`, and any other instructional blocks.
    - If the command references workflows (e.g., `@~/.gemini/get-shit-done/workflows/...`), read those files as well to understand the full procedure.

3.  **Execute the Instructions:**
    - Follow the workflow precisely.
    - Use the specified templates from `.gemini/get-shit-done/templates/` or `~/.gemini/get-shit-done/templates/`.
    - Adhere to the principles in `.gemini/get-shit-done/references/` or `~/.gemini/get-shit-done/references/`.

4.  **Confirm Completion:**
    - Once the command's objective is met, inform the user and suggest next steps as defined in the GSD system.
