# ai-dev-tools

A collection of AI rules for building Node.js applications with an AI assistant (e.g., Junie). The rules guide the AI through a structured development workflow — from defining a feature to implementing it.

## How It Works

The rules are numbered and intended to be followed in order:

| Rule | Purpose |
|------|---------|
| `1-create-feature-tag.md` | Create a unique tag to organize all artifacts for a feature |
| `2-create-scope.md` | Define the high-level scope and boundaries of the feature |
| `3-create-prd.md` | Generate a detailed Product Requirements Document |
| `4-create-tech-stack.md` | Evaluate and document technology choices |
| `5-create-tasks.md` | Break the PRD into an actionable, trackable task list |
| `6-perform-task.md` | Execute tasks one at a time with approval and progress tracking |

All generated artifacts (scope, PRD, tech stack, tasks) are saved in an `/ai-work` directory in the target project.

## Setting Up a Project to Use These Rules

1. **Copy the rules** from `ai-rules/` into your project's `ai-rules/` directory (create it if it doesn't exist).

2. **Set up a guidelines file:** Copy `guidelines-useme.md` from this repository into your project's `.junie/` directory (create it if it doesn't exist) and rename it to `guidelines.md`. This file is automatically read by Junie on every prompt and points the AI to the rules.

3. **Start a session** by telling the AI what feature you want to build. It will follow the rules to guide you through scoping, requirements, tech decisions, and task execution.

## Notes

- Rules are designed for use in **other projects**, not in this repository itself.
- Each rule file contains its own goal, process, and output format — read them to understand what each step produces.
- The AI will ask for confirmation at key decision points and will not proceed without explicit approval.
