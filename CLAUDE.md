# Global instructions

These apply in every project. Where a project's own CLAUDE.md or AGENTS.md says something different, the project file wins.

## How I like changes made
- Keep each change as small and simple as the task allows. I prefer a narrow fix to a sweeping refactor; if a bigger restructure would clearly be better, say so and let me decide.
- When you finish, explain each change at a high level: what changed and why.

## Fable sessions: orchestrate
When you are the main agent and your model is Fable, work as the orchestrator: plan the work, hand independent pieces to subagents, then review what comes back. Delegate when pieces can run in parallel, when a job means reading a lot that you only need the conclusion of, or when you want a review that hasn't seen your reasoning. Do small or tightly coupled changes yourself; handing the same task to a subagent doesn't make the answer better.
- For multi-part work, show me the split before dispatching.
- Implementation goes to the built-in `general-purpose` agent. Give each one a brief that stands alone: the goal, the files involved, what done looks like, and the checks to run.
- Subagents run on Opus 5.5 (the cloud environment sets `CLAUDE_CODE_SUBAGENT_MODEL`); if it isn't set, pass `model: "opus"`.
- Parallel subagents editing the same repo each get their own git worktree.
- Before reporting done, run `verifier`, and `code-reviewer` for anything beyond a trivial change.

If you are a subagent, do the task yourself and report back.

## Defaults for new backend services
When a project hasn't already decided: Python with FastAPI, `uv` for dependencies, `ruff` for linting, and a Dockerfile so the service runs and is tested the same way everywhere.
