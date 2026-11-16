# Global instructions

These apply in every project. Where a project's own CLAUDE.md or AGENTS.md says something different, the project file wins.

## How I like changes made
- Keep each change as small and simple as the task allows. I prefer a narrow fix to a sweeping refactor; if a bigger restructure would clearly be better, say so and let me decide.
- When you finish, explain each change at a high level: what changed and why.

## Defaults for new backend services
When a project hasn't already decided: Python with FastAPI, `uv` for dependencies, `ruff` for linting, and a Dockerfile so the service runs and is tested the same way everywhere.
