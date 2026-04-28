---
name: evolution
description: Review the current session end-to-end, extract durable lessons, and turn them into sharper future behavior. Use whenever the user asks Claude to reflect on this session, summarize what happened and what to learn from it, capture mistakes and improvements, learn from the work, strengthen future performance. Also use when the user wants a postmortem, retrospective, self-improvement pass, or wants Claude to consolidate session context into reusable guidance.
---

# Evolution

Use this skill to perform a disciplined retrospective on the current session so future work becomes faster and higher quality.

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

### 4. Persist durable findings — memory or structural fixes

Not every lesson belongs in memory. Route each finding to the right place:

- **Memory** (user / feedback / project / reference, per the system's auto memory rules): stable user preferences, durable collaboration feedback, ongoing project constraints, external resource pointers.
- **Skill edit**: if the lesson is "this skill missed a case" or "this skill's guidance was unclear", propose a SKILL.md change instead of writing memory.
- **CLAUDE.md edit**: if the lesson should bind every session in this repo, propose a CLAUDE.md change.
- **Hook (settings.json)**: if the lesson is an automated behavior ("always run X before Y"), propose a hook — the harness runs hooks, memory does not.

Retrospective-specific memory clarifications (on top of the system's auto memory rules):

- A single in-session correction is not yet a durable preference. Save as **feedback** only if the user signaled it should hold across sessions ("from now on", "always") or showed it repeatedly.
- Anything directly inspectable in the repo (file paths, module locations, code structure) is not memory. Save only the non-obvious *motivation* behind it, as **project**, when it would not be re-derivable from the code.
- A short-lived weekly focus is **do not save** unless the user makes clear it will keep shaping decisions.
- When uncertain between **user** and **project**, ask: "Does this describe the person, or the work they are doing right now?"

Always show what was saved (and the chosen type) or what structural edit was proposed, so the user can correct the classification.

### 5. Report the retrospective

Use this structure unless the user asked for a different format. If a section has nothing real to report, write "None" — do not invent content to fill the structure. For very short or low-content sessions, prefer the minimal version below.

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
- A rule listed here is session-local unless it is also written to **feedback** memory in step 4. Mark each rule as either "→ saved to memory" or "session-only" so the user knows which will actually persist.

## Memory updates
- List any memory saved, updated, or removed, with the chosen type.
- Also list any proposed skill / CLAUDE.md / hook edits.
- If none, say "None."

## Important quality bar

This skill is for learning, not self-congratulation.

- Be candid about mistakes.
- Do not invent lessons where there were none.
- Do not claim improvement without naming the mechanism.
- Do not promote a single in-session comment into a permanent preference. Wait for an explicit signal ("from now on", "always") or a repeated pattern.
- Do not save facts that can be re-derived from the repo (paths, function names, module layout) as memory. Save only the non-obvious motivation behind them.
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