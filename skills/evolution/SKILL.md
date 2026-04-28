---
name: evolution
description: Review the current session end-to-end, extract durable lessons, and turn them into sharper future behavior. Use whenever the user asks Claude to reflect on this session, summarize what happened, capture mistakes and improvements, learn from the work, strengthen future performance. Also use when the user wants a postmortem, retrospective, self-improvement pass, or wants Claude to consolidate session context into reusable guidance.
---

# Evolution

Use this skill to perform a disciplined retrospective on the current session so future work becomes faster, safer, and higher quality.

## When this skill is appropriate

Use it when the user wants any of the following:

- a session recap or retrospective
- a summary of the problem solved and how it was solved
- a list of mistakes, dead ends, or avoidable rework
- lessons Claude should internalize for future sessions
- concrete improvements to speed, quality, verification, or collaboration

If the user asks to remember stable preferences or collaboration guidance beyond this session, also save the relevant parts to memory.

## Goals

Produce a compact but useful learning artifact that helps Claude improve, not just summarize.

Specifically:

1. Reconstruct the session's real objective.
2. Identify what actions materially moved the work forward.
3. Separate signal from noise, including wasted motion and mistakes.
4. Extract reusable heuristics for future work.
5. Propose a better/faster path if one exists.
6. Save stable user guidance to memory when appropriate.

## Workflow

### 1. Rebuild the session timeline

Review the current conversation and any directly relevant files or diffs from this session.

Capture:

- what the user actually wanted
- what constraints mattered
- what was tried
- what succeeded
- what failed or caused churn
- what remains unresolved, if anything

Do not pad the recap with routine tool chatter.

### 2. Distill the key learnings

Extract lessons under these lenses when applicable:

- **Problem**: what needed to be done
- **Approach**: how it was solved
- **Mistakes**: wrong assumptions, missed instructions, unnecessary work, verification gaps
- **Prevention**: how to avoid repeating those mistakes
- **Optimization**: faster or cleaner approaches that would likely work next time
- **User preferences**: stable preferences the user revealed

Prefer concrete lessons over generic advice.

Bad: "communicate better"

Good: "Before editing multiple files for a new behavior, first confirm whether an existing project skill or CLAUDE.md instruction already dictates the workflow."

### 3. Turn lessons into reusable guidance

Convert findings into short, actionable rules Claude can apply later.

Examples:

- "When the user asks for a new skill, define the trigger conditions in the description, not buried in the body."
- "When the user wants self-improvement, separate durable feedback from one-off task details before writing memory."
- "If a better solution exists, state the tradeoff clearly instead of rewriting history to make the first path look ideal."

### 4. Save durable memory when warranted

If the retrospective reveals stable user preferences, workflow guidance, or long-lived project context, save it using the memory system.

Only save information that is likely to matter in future conversations. Do not save ephemeral task logs.

#### How to classify memory writes

Use these rules when deciding what to save:

- **user**: facts about the user that likely remain true across projects, such as role, expertise, goals, or durable preferences
- **feedback**: instructions about how Claude should work with the user, especially corrections, validated approaches, and collaboration preferences
- **project**: non-obvious context about the current project, business constraints, deadlines, motivations, or stakeholders that is not reliably derivable from the codebase
- **reference**: pointers to external systems or resources where future context can be found; do not use this for files, paths, or docs that already live inside the repository or local workspace
- **do not save**: ephemeral task history, routine session logs, temporary decisions, or facts that can be re-derived by reading the code, git history, or local files

Use these quick tests:

- If it would still matter in a different repository, it is usually **user** or **feedback**.
- If it matters because of this project's current business context, it is usually **project**.
- If it is only a short-lived weekly focus, temporary execution state, or current-task status update, default to **do not save** unless the user explicitly indicates that the time window or deadline will continue to shape future decisions.
- If it tells Claude where to look outside the repo, it is usually **reference**.
- If it points to a file path, module location, route file, AGENTS.md, CLAUDE.md, or code structure that is already inside the repo or local workspace, do not save it as **reference** or **project** memory just because it is useful.
- If it names files, functions, code structure, or implementation details that can be inspected directly, do not save it as memory unless the non-obvious part is the motivation or constraint behind it.

When uncertain between **user** and **project**, ask: "Does this describe the person, or the work they are doing right now?"

When uncertain between **project** and **do not save**, ask: "Is this an ongoing project constraint, or just this week’s status / this task’s temporary state?"

Examples:

- "Auth rewrite is driven by compliance requirements" -> usually **project**
- "This week the team is mostly cleaning up skills" -> usually **do not save** unless the user makes clear that this time window will keep affecting future prioritization
- "Merge freeze starts 2026-05-02" -> usually **project**, because the dated constraint will affect future decisions until it passes

### 5. Report the retrospective

Use this structure unless the user asked for a different format:

## Session objective
- What the user wanted in 1-3 bullets.

## What happened
- The key path taken.
- Important decisions or turning points.

## What worked
- 2-5 concrete things worth repeating.

## Mistakes and waste
- 0-5 concrete mistakes, blind spots, or unnecessary steps.

## How to avoid those mistakes next time
- Specific behavioral corrections.

## Better or faster path
- A shorter or higher-quality route, if one exists.
- If the original path was already good, say so plainly.

## Reusable rules for future sessions
- Short imperative bullets Claude can internalize.

## Memory updates
- List any memory saved, updated, or removed.
- If none, say "None."

## Important quality bar

This skill is for learning, not self-congratulation.

- Be candid about mistakes.
- Do not invent lessons where there were none.
- Do not claim improvement without naming the mechanism.
- Keep recommendations grounded in what actually happened in the session.
- Prefer a short truthful retrospective over a long vague one.

## If the user wants only a minimal version

Return just:

- objective
- outcome
- mistakes
- future rule(s)

## If the user asks Claude to "learn" or "strengthen itself"

Treat that as:

1. produce the retrospective,
2. save durable guidance to memory where appropriate,
3. explicitly call out which lessons are durable enough to reuse.

Do not imply hidden self-modification beyond the session and memory system.

## Example prompts this skill should handle

- "回顾一下这个 session，提炼要点和错误。"
- "总结这次你是怎么解决问题的，下次怎么更快。"
- "做个复盘，把值得记住的协作习惯记下来。"
- "Reflect on this session and tell me what you should do differently next time."