---
version: 1.6.0
timestamp: 2026-06-12 00:00
---
# Rule: Performing a Task for the Active Feature

## Prerequisites

- `/ai-work/00-feature-status.md` must exist
- A feature must be marked `active`
- A task list must exist at `/ai-work/{feature-tag}-tasks.md`

## Active Feature Protocol

### Source of Truth

- Use `/ai-work/00-feature-status.md` as the source of truth for:
  - the active feature
  - whether a feature is future, planned, active, paused, completed, or archived

### Non-Active Features

- If no feature is currently active, do not perform implementation work and tell the user to activate or switch to a feature first
- Treat `future` features as backlog notes, not currently executable work
- Treat `paused` features as resumable but not currently editable
- Tell the user to switch features first by using the feature-change workflow if they want to resume a paused feature
- Treat completed and archived features as read-only by default
- Refuse to modify scope, PRD, tasks, or implementation for a completed or archived feature unless the user explicitly asks for an exception

## Task Selection Process

Use the active feature from `/ai-work/00-feature-status.md` as the default and expected implementation target.

1. **With Task Number**
   - When given a specific task number, begin work on that task for the active feature after confirming the request is explicit
   - Treat an explicit execution request for that task as approval to start it; do not ask a second generic approval question unless scope remains ambiguous

2. **Without Task Number**
   - Review the active feature task list
   - Identify the next unchecked task
   - Present it to the user
   - State the exact task id and title being approved
   - Ask `Approve this? Y/N.` before proceeding

3. **If the User Also Names a Feature**
   - Treat the active feature as the source of truth
   - If the named feature matches the active feature, proceed normally
   - If the named feature does not match the active feature, do not proceed and tell the user to switch features first by using the feature-change workflow

## Task Execution Rules

- Never start work on any task without explicit user approval
- Complete only the approved task
- Do not silently move to the next task
- Do not ask extra approval prompts beyond task-start approval; routine in-task edits under normal workspace permissions do not require additional approval requests
- Before implementation, read `/ai-work/00-master-techstack.md` when it exists and apply any relevant shared technology decisions alongside the PRD and task list
- Before implementation, if `/ai-work/00-architecture.md` exists, read it once as part of the initial task context
- After that initial read, do not keep re-reading `/ai-work/00-architecture.md` during normal task execution unless the user explicitly asks for that or the flow of work clearly requires revisiting the document
- Before writing code for a non-trivial change, perform an architectural placement check
  - Identify the narrowest existing module, class, component, service, package, or layer that should own the behavior
  - Prefer placing behavior where the responsibility naturally belongs rather than where inputs happen to be available
  - Consider whether the cleanest implementation is to:
    - extend an existing boundary that already owns the concern
    - extract behavior into a new helper, service, module, hook, or component
    - keep the work in a higher-level coordinator because orchestration is genuinely that module's job
  - Choose the option that best preserves cohesion, encapsulation, and dependency direction
  - If the obvious implementation location is architecturally wrong, prefer a small structural improvement over adding more logic to the wrong layer
- If implementation materially changes architecture, clarifies a structural decision, or reveals that the architecture record is stale, update `/ai-work/00-architecture.md` as part of the task work

## Progress Tracking

As each task or sub-task is completed:

1. Update `/ai-work/{feature-tag}-tasks.md` immediately
2. Change `- [ ]` to `- [x]`
3. If the last sub-task under a task is completed and the task itself is satisfied, also check off the parent task
4. Save the file after each update

## General Working Principles

1. Prefer editing existing files when they already own the responsibility; do not force new behavior into an existing file when doing so weakens cohesion or turns it into a grab-bag module
2. Use the PRD as the implementation-facing feature document, the master tech stack as the shared technology baseline when it exists, and the architecture document as the shared structural baseline when it exists
3. Keep domain logic close to domain-owned modules, persistence concerns close to persistence boundaries, presentation logic close to presentation layers, and orchestration in coordinating layers
4. Treat the following as architectural warning signs that should trigger a placement rethink or a small extraction:
   - adding more unrelated logic to a high-level god class, god component, controller, page, or manager
   - placing logic at the call site because it is convenient rather than because it belongs there
   - mixing orchestration, business rules, validation, persistence, transport, and presentation concerns in one unit
   - leaking low-level implementation details across abstraction boundaries
   - growing generic utility files instead of using clearer domain ownership
   - adding mode flags, branching, or duplicate logic where a better boundary would simplify the design
5. When a file, class, or component is already overloaded, treat "add one more thing here" as a code smell and consider extraction or a better ownership boundary
6. Run validation as appropriate using the testing rule
7. Ask clarifying questions if task requirements are ambiguous
8. Do not expand scope without approval
9. Do not run long-running application servers unless explicitly asked
10. Follow `AGENTS.md` for command, style, and environment conventions
