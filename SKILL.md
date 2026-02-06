# Claude Code Project Guide

## 📂 Project Structure & Knowledge Base
I have a set of custom agents and skills defined in markdown files. Please use them as follows:

- **Agents (Personas)**: Located in `hooks/`.
  - When I ask for an architecture review, read and apply `hooks/architect.md`.
  - When I ask for a code review, read and apply `hooks/code-reviewer.md` or `hooks/python-reviewer.md`.
  - When I ask for database help, read and apply `hooks/database-reviewer.md`.

- **Skills (Best Practices)**: Located in `skills/`.
  - **Python**: When writing Python, always refer to `skills/python-patterns` and `skills/python-testing`.
  - **Frontend**: For JS/HTML tasks, refer to `skills/frontend-patterns`.
  - **Postgres**: For SQL tasks, refer to `skills/postgres-patterns`.

## 🚀 Interaction Rules
- Before starting a complex task, search the `skills/` folder for relevant guidelines.
- If I mention a specific role (e.g., "@architect"), please load the corresponding file from `hooks/`.