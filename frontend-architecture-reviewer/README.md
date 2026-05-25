# frontend-architecture-reviewer

A Claude Code skill for reviewing, auditing, and onboarding frontend codebases — Vue 3, Nuxt 3, React, Next.js, and TypeScript projects.

## What It Does

Analyzes frontend codebases against established architecture patterns and produces severity-graded, actionable feedback. Also maps project structure and generates developer onboarding documents.

## Installation

```bash
cp -r frontend-architecture-reviewer ~/.claude/skills/
```

## Commands

| Command | What You Get |
|---|---|
| `/review` | Full architectural review with severity-graded issues |
| `/map` | Annotated folder structure with role labels and warnings |
| `/detect-arch` | Identified pattern + confidence + deviations |
| `/onboard` | Developer onboarding document |
| `/data-flow` | Traced data path: API → mapper → store → component |
| `/smells` | Anti-pattern scan only |
| `/audit [area]` | Deep dive into one area |

### Audit areas
`components` `stores` `api` `ssr` `performance` `testing` `security`

## Example Prompts

```
/map [paste folder tree]

/detect-arch [paste folder tree]

/review [paste component or store code]

/onboard [paste folder tree + key files]

/data-flow [paste feature folder contents]

/audit ssr [paste composables and setup code]

/smells [paste any code]
```

## Severity Scale

| Label | Meaning |
|---|---|
| 🔴 Critical | SSR crash, hydration error, security risk, runtime failure |
| 🟠 Major | Scalability blocker, significant coupling, tech debt |
| 🟡 Minor | DX degradation, missing abstraction |
| 🔵 Suggestion | Optimization or pattern alignment opportunity |

## Architecture Patterns Detected

- Feature-Sliced Design (FSD)
- Atomic Design
- Vertical Slice / Feature-Based
- Layer-Based (Classic)
- Domain-Driven (DDD-influenced)
- Islands Architecture
- Micro-Frontend / Module Federation

## Review Coverage

- Component design (size, separation of concerns, SSR safety)
- State management (Pinia, Zustand, Redux — server vs client state)
- API / data layer (mappers, service abstraction, typed clients)
- SSR / hydration (guards, singleton risk, mismatch detection)
- Performance (reactivity, code splitting, lazy loading)
- Testing architecture
- Security (XSS, token storage, auth guards)

## Architectural References

Feature-Sliced Design · Atomic Design (Brad Frost) · Clean Architecture (Martin) · CQRS · DDD Bounded Contexts · Repository Pattern · PRPL Pattern · Islands Architecture · BFF Pattern · Hexagonal Architecture

## Author

Omar Ashraf
