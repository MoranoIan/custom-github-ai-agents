# Custom GitHub AI Agents

This repository is a public collection of reusable GitHub Copilot assets for agentic coding workflows. It contains agent definitions, reusable skills, and custom instructions that can be copied into a repository's `.github/` directory and used through GitHub Copilot Chat.

The goal is to provide a lightweight, practical structure for teams or individuals who want to make their coding assistants more consistent, more specialized, and more aligned with their preferred working style.

## What this repository contains

This repository includes three main categories of reusable assets:

- `agents/` — specialized agents for different workflows and review styles.
- `skills/` — reusable capabilities or domain-specific playbooks.
- `instructions/` — custom instruction files that shape assistant behavior.

It also includes a custom NotebookLM research instruction in the instructions folder, which is designed for academic or research-oriented synthesis workflows.

Some files in this repository are adapted from or inspired by assets elsewhere, and these have been tuned for better alignment with the author's workflow and preferences.

## Intended Repository structure

```text
.github/
  instructions/
  skills/
  agents/
```

The repository is intentionally simple and modular:

- `agents/` stores agent definitions for different kinds of tasks.
- `skills/` stores reusable skills that can be attached to broader assistant workflows.
- `instructions/` stores custom instruction files, such as the included NotebookLM research system instruction.

## How to reuse this repository

Copy the `.github/` directory structure into the root of another repository, or copy the relevant folders into your own repository's `.github/` setup.

Once the directory is in place:

1. Open GitHub Copilot Chat in the editor.
2. Choose the relevant agent or instruction for your task.
3. Ask the assistant to perform the work you need.

For example, in VS Code, open Copilot Chat and select an appropriate agent from the available session options.

## ⚠️ Recommended model usage

For day-to-day coding and normal repository tasks, use lower-tier models when practical. For more important reviews, audits, security-oriented work, or high-impact reasoning, use a higher-tier model. (*high-tier models are set to default — requires modification*)

**Also keep in mind**: agentic coding workflows (agents that plan, search, edit, and execute across multiple steps) consume significantly more credits and context window than a standard single prompt-and-response pattern. Scope agent tasks deliberately, and don't reach for an agent when a normal prompt would do.

**The important principle is simple:**

> Always validate the AI's output before accepting it. Review each action before granting permissions or applying a change.

## Contributor guidance

If you want to extend this repository:

- Add a new agent in `agents/` when you need a specialized assistant persona. Use the naming convention `<agent-name>.agent.md`
- Add a new skill in `skills/` when you want reusable workflow logic or domain guidance. Use the naming convention `<skill-name>/SKILL.md`
- Add a new instruction in `instructions/` when you want to define behavior for research, review, documentation, or quality control. Use the naming convention `<instruction-name>.instruction.md`

Keep files consistent, descriptive, and easy to understand. A good public repository asset should be clear enough for others to copy and adapt without a great deal of hidden context.

## Notes

This repository is meant to be a practical starting point. It is not a complete framework by itself, but it is designed to be copied, customized, and expanded for your own workflows.

Use the assets carefully, and always verify output before trusting or applying it.
