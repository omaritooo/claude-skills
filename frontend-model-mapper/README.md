# frontend-model-mapper

A Claude Code skill for transforming backend API responses into scalable, type-safe frontend TypeScript structures.

## What It Does

Paste in a raw API response and get back production-ready frontend artifacts:

- TypeScript DTOs, domain models, and mapper functions
- Zod / Yup / Valibot validation schemas
- TanStack Query / Vue Query hooks
- Table column configs, form models, mock factories
- UI types, formatters, selection models, and more

## Installation

```bash
cp skills.md ~/.claude/skills/frontend-model-mapper.md
```

## Quick Start

Paste an API response and prompt:

```
Map this API response → dto, model, mapper, validation
```

Or with full config:

```
Map this response → all options
framework: nuxt
output-style: enterprise-ui
validation-library: zod
```

## Generation Options

| Option | Output |
|---|---|
| `dto` | Raw API interfaces (snake_case preserved) |
| `model` | Frontend camelCase domain models |
| `mapper` | DTO → model transformer functions |
| `validation` | Form validation schemas |
| `enums` | `as const` union types |
| `query-hooks` | TanStack / Vue Query hooks |
| `ui-types` | Table rows, card props, modal payloads |
| `forms` | Form models + default values |
| `table-columns` | Typed column configs |
| `selection-models` | `SelectOption<T>` helpers |
| `formatters` | Date / currency / label utilities |
| `mock-data` | Factory functions with overrides |
| `loading-states` | Skeleton + optimistic UI models |
| `empty-states` | Empty list helpers |
| `constants` | Reusable frontend constants |
| `filters` | Frontend filter models |
| `sorting` | Sort types |
| `folder-structure` | Feature-driven directory layout |

**Default** (when no options specified): `dto` + `model` + `mapper` + `validation`

## Configuration

| Option | Values | Default |
|---|---|---|
| `framework` | `vue` `nuxt` `react` `next` | `nuxt` |
| `validation-library` | `zod` `yup` `valibot` | `zod` |
| `output-style` | `minimal` `scalable` `enterprise-ui` | `scalable` |
| `state-management` | `pinia` `zustand` `redux-toolkit` `none` | optional |

## Supported Input Shapes

- Plain JSON responses
- JSON:API (`data` + `included` + `meta` + `links`)
- Paginated list responses
- Error envelopes
- Nested / deeply relational structures
- OpenAPI response snippets
- GraphQL responses
- Multiple response variations

## Example Prompts

```
# Default artifacts
Map this API response → dto, model, mapper

# Full stack for a feature
Map this response → model, mapper, query-hooks, table-columns, forms, mock-data
framework: nuxt

# React dashboard
Map this response → model, mapper, query-hooks, ui-types, table-columns
framework: react
output-style: enterprise-ui

# Yup validation for Vue
Map this response → validation, forms
framework: vue
validation-library: yup
```

## What It Won't Do

- Backend architecture or database modeling
- Server-side validation logic
- Business rule enforcement
- Backend framework code (Express, Fastify, Laravel, etc.)

## Author

Omar Ashraf
