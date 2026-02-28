---
version: 1.1.0
timestamp: 2026-02-27 16:21
---
# Rule: Technology Stack Selection and Documentation

## Goal

To guide an AI assistant in evaluating technical requirements from the PRD, proposing appropriate technology options, facilitating user decision-making, and documenting the chosen technology stack.

## When to Use

This rule should be executed **after** creating the PRD (step 3) and **before** creating the task list (step 5). It serves as step 4 in the development workflow.

## Prerequisites

- A feature tag must exist (created via rule `1-create-feature-tag.md`)
- A completed PRD document exists in `/ai-work/{feature-tag}-prd.md`

## Output

- **Format:** Markdown (`.md`)
- **Location:** `/ai-work/`
- **Filename:** `{feature-tag}-techstack.md` (e.g., `01-user-auth-techstack.md`)

## Determining the Mode: First Feature vs. Subsequent Features

Before starting, check the `/ai-work` directory for any existing `*-techstack.md` files.

- **If none exist:** This is the **first feature**. Follow the [Full Tech Stack Process](#full-tech-stack-process).
- **If one or more exist:** This is a **subsequent feature**. Follow the [Tech Stack Changes Process](#tech-stack-changes-process).

---

## Full Tech Stack Process

_Use this process only for the first feature in the project._

### 1. Analyze Technical Requirements

Review the PRD to identify:
- Core functionality requirements
- Performance and scalability needs
- Integration requirements (APIs, databases, third-party services)
- User interface requirements
- Testing and deployment needs
- Development environment constraints
- Security and compliance requirements

### 2. Identify Technology Decision Points

For each category, identify where technology choices need to be made:
- **Frontend Framework** (e.g., React, Vue, Svelte, vanilla JS)
- **Backend Framework** (e.g., Express, Fastify, Nest.js, Next.js API routes)
- **Database** (e.g., PostgreSQL, MongoDB, SQLite, Redis)
- **State Management** (e.g., Redux, Zustand, Context API, MobX)
- **Styling Solution** (e.g., CSS Modules, Tailwind, styled-components, Sass)
- **Testing Framework** (e.g., Jest, Vitest, Playwright, Cypress)
- **Build Tools** (e.g., Vite, Webpack, Turbopack, esbuild)
- **Package Manager** (e.g., npm, yarn, pnpm)
- **Other Libraries/Tools** as needed by the specific feature

### 3. Propose Technology Options

For each decision point, present:
- **2-3 viable options** with brief descriptions
- **Pros and cons** relevant to the project requirements
- **Recommendation** with rationale based on:
  - Project requirements and constraints
  - Team experience (if known)
  - Community support and ecosystem maturity
  - Performance characteristics
  - Development velocity impact

### 4. Present to User

Format the proposal as a clear, scannable document:

```markdown
## Technology Decision: [Category Name]

**Requirement:** [Why this technology choice is needed]

### Option 1: [Technology Name]
- **Pros:** [List key advantages]
- **Cons:** [List key disadvantages]
- **Use Case Fit:** [How well it matches requirements]

### Option 2: [Technology Name]
- **Pros:** [List key advantages]
- **Cons:** [List key disadvantages]
- **Use Case Fit:** [How well it matches requirements]

### Recommendation
[Your recommendation with clear reasoning]

**Your Choice:** _[User fills this in]_
```

### 5. Facilitate User Decision

- Present all technology decisions in a single document
- Allow the user to:
  - Accept recommendations as-is
  - Choose alternative options from the proposals
  - Specify their own preferences not listed
- **Wait for user confirmation** before proceeding to documentation

### 6. Document Final Choices

Once the user has made all decisions, create `/ai-work/{feature-tag}-techstack.md` with:

```markdown
# Technology Stack: [Project/Feature Name]

**Created:** [Date]
**Status:** Approved

## Overview

Brief description of the project and its technical requirements.

## Technology Decisions

### [Category 1]
- **Choice:** [Selected Technology]
- **Rationale:** [Why this was chosen]
- **Version:** [If applicable]

### [Category 2]
- **Choice:** [Selected Technology]
- **Rationale:** [Why this was chosen]
- **Version:** [If applicable]

[Continue for all categories...]

## Development Environment

- **Node Version:** [e.g., 20.x]
- **Package Manager:** [e.g., npm]
- **IDE/Editor:** [If specified]

## Dependencies

### Core Dependencies
```json
{
  "[package-name]": "[version]",
  "[package-name]": "[version]"
}
```

### Development Dependencies
```json
{
  "[package-name]": "[version]",
  "[package-name]": "[version]"
}
```

## Architecture Notes

[Any additional notes about how these technologies will work together, architectural patterns to follow, or important implementation considerations]

## Future Considerations

[Technologies or patterns to consider for future iterations]
```

### 7. Save and Confirm

- Save the completed `{feature-tag}-techstack.md` file to `/ai-work/`
- Confirm with the user that the technology stack is documented and approved
- Note that this document should be referenced during task implementation

---

## Tech Stack Changes Process

_Use this process for every feature after the first one._

### 1. Review Existing Tech Stack

Read the most recent `*-techstack.md` file(s) in `/ai-work/` to understand the established stack.

### 2. Analyze the PRD for New Requirements

Review the current feature's PRD and identify only the technology decisions that are **new or different** from the existing stack:
- New libraries or tools not previously used
- Version upgrades required by this feature
- Replacement of an existing technology
- Additional infrastructure (e.g., a new database, a caching layer)

If the feature requires **no changes** to the existing stack, note this explicitly and skip to step 5.

### 3. Propose Changes Only

For each new or changed technology decision, present options using the same format as the full process (options, pros/cons, recommendation). Do **not** re-document technologies that remain unchanged.

### 4. Facilitate User Decision

- Present only the new/changed decisions for user confirmation
- **Wait for user confirmation** before proceeding to documentation

### 5. Document Changes

Create `/ai-work/{feature-tag}-techstack.md` using the following format:

```markdown
# Technology Stack Changes: [Feature Name]

**Created:** [Date]
**Status:** Approved
**Base Stack:** [Tag of the feature whose techstack this builds upon, e.g., `01-user-auth`]

## Overview

Brief description of why tech stack changes are needed for this feature (or note that no changes are required).

## Changes

### [Category] — [Change Type: Added | Upgraded | Replaced | Removed]
- **Previous:** [Prior technology/version, or "N/A" if newly added]
- **New Choice:** [Selected Technology and version]
- **Rationale:** [Why this change is needed for this feature]

[Repeat for each change. If no changes, state "No changes to the existing tech stack are required for this feature."]

## New Dependencies

### Core Dependencies
```json
{
  "[package-name]": "[version]"
}
```

### Development Dependencies
```json
{
  "[package-name]": "[version]"
}
```

_(Omit dependency sections if there are no new dependencies.)_

## Architecture Notes

[Any notes specific to how new technologies integrate with the existing stack, or omit if not applicable]
```

### 6. Save and Confirm

- Save the completed `{feature-tag}-techstack.md` file to `/ai-work/`
- Confirm with the user that the changes are documented and approved

---

## Interaction Model

1. **Check Phase:** AI checks `/ai-work` to determine if this is the first feature or a subsequent one
2. **Analysis Phase:** AI reviews PRD silently
3. **Proposal Phase:** AI presents technology options (full stack or changes only) with recommendations
4. **Decision Phase:** User reviews and makes choices (may be iterative with discussion)
5. **Documentation Phase:** AI documents final decisions in the appropriate format
6. **Confirmation:** AI confirms completion and readiness to proceed to task implementation

## Important Notes

- **Don't overwhelm:** Only propose decisions for technologies actually needed by the project
- **Be pragmatic:** Consider existing project setup if this is adding to an existing codebase
- **Stay current:** Recommend stable, well-supported technologies unless cutting-edge features are required
- **Document constraints:** If certain choices are constrained by existing decisions, note this clearly
- **Version awareness:** Specify version ranges when important for compatibility

## Example Workflow — First Feature

```
User: "I've got my PRD for feature 01-user-auth. Let's pick the tech stack."

AI: [Checks /ai-work — no existing techstack files found. Uses Full Tech Stack Process.]
AI: [Analyzes requirements from 01-user-auth-prd.md]
AI: "Based on your requirements for user authentication, I've identified 5 key technology decisions. Let me present the options..."
AI: [Presents formatted document with options and recommendations]

User: "I'll go with your recommendations for everything except the database - use PostgreSQL instead of SQLite."

AI: [Creates 01-user-auth-techstack.md with user's choices]
AI: "Technology stack documented in /ai-work/01-user-auth-techstack.md. Key choices:
- Frontend: React 18
- Backend: Express.js
- Database: PostgreSQL (per your preference)
- Testing: Jest
- Styling: Tailwind CSS

Ready to proceed to task creation (step 5)?"
```

## Example Workflow — Subsequent Feature

```
User: "I've got my PRD for feature 02-payment-gateway. Let's do the tech stack."

AI: [Checks /ai-work — finds 01-user-auth-techstack.md. Uses Tech Stack Changes Process.]
AI: [Reviews 01-user-auth-techstack.md and 02-payment-gateway-prd.md]
AI: "The existing stack covers most of what's needed. I've identified 2 changes required for this feature:

1. **New Library — Stripe SDK** (payment processing)
2. **New Library — Webhook middleware** (for Stripe event handling)

[Presents options and recommendations for each]"

User: "Looks good, go with your recommendations."

AI: [Creates 02-payment-gateway-techstack.md documenting only the changes]
AI: "Tech stack changes documented in /ai-work/02-payment-gateway-techstack.md.
Ready to proceed to task creation (step 5)?"
```

## Target Audience

This rule helps both:
- **AI Assistant:** To systematically evaluate options and present clear recommendations
- **Developer/User:** To make informed technology choices that will guide the entire implementation
