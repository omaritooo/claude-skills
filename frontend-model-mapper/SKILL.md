---
name: frontend-model-mapper
description: Generate frontend-focused TypeScript models, validation schemas, query hooks, and transformation utilities from API responses or OpenAPI schemas.
version: 1.0
author: Omar Ashraf
---

# Purpose

Transform backend API responses into scalable frontend structures for Vue 3, Nuxt 3, React, and Next.js — optimized for DX, type safety, and component-driven architecture.

Focus: frontend ergonomics. Not backend architecture, server logic, or database structures.

---

# Supported Inputs

- Raw JSON, OpenAPI snippets, GraphQL responses
- Paginated, JSON:API, envelope-wrapped, or nested responses
- Error response shapes
- Multiple API response variations

---

# Configuration

| Config | Options | Default |
|---|---|---|
| `framework` | `vue` `nuxt` `react` `next` | `nuxt` |
| `validation-library` | `zod` `yup` `valibot` | `zod` |
| `output-style` | `minimal` `scalable` `enterprise-ui` | `scalable` |
| `state-management` | `pinia` `zustand` `redux-toolkit` `none` | optional |

---

# Generation Options

| Option | Output |
|---|---|
| `dto` | Raw API response interfaces (preserve backend naming) |
| `model` | camelCase frontend/domain models |
| `mapper` | Pure transformation functions (DTO → model) |
| `validation` | Frontend form validation schemas |
| `enums` | `as const` union enums from string literals |
| `query-hooks` | TanStack/Vue Query hooks with key factories + stale time |
| `ui-types` | Component-facing types (table rows, card props, badge variants) |
| `filters` | Frontend filter models |
| `sorting` | Sorting types |
| `forms` | Form models with defaults + `toFormValues` helper |
| `table-columns` | Typed table column configs |
| `mock-data` | Factory functions with `Partial<Model>` overrides |
| `loading-states` | Skeleton configs + optimistic UI models |
| `empty-states` | Empty list + fallback models |
| `folder-structure` | Feature-driven directory layout |
| `constants` | Reusable frontend constants |
| `formatters` | Date/currency/label display utilities |
| `selection-models` | `SelectOption<T>` + factory helpers |

**Default (no options specified):** `dto` + `model` + `mapper` + `validation`

Only generate explicitly requested outputs.

---

# Core Rules

## DTOs
- Preserve backend naming exactly (snake_case, nested structures intact)
- No computed properties, no UI formatting

## Models
- camelCase all fields
- Flatten deeply nested paths when it improves component readability
- ISO date strings → `Date`
- Nullable/optional fields inferred from response shape

## Mappers
- Pure functions, no mutations
- Parse dates: `new Date(dto.field)`
- Flatten: `dto.organization.data.name` → `organizationName`
- Export singular and array variants

## Validation
- Frontend form validation only — no backend business logic

## Query Hooks
- Include query key factories, loading/error states, `staleTime` recommendation
- SSR-safe patterns (Nuxt `$fetch`, React `fetch`)

## Enums
- Use `as const` objects + derived union types — avoid `enum` keyword

## Forms
- Default values object + `toFormValues(model)` mapper

## Mock Data
- Factory function with `Partial<Model>` overrides

## Formatters
- Display/formatting only — no business logic

## Folder Structure

**Scalable:**
```
/features/[resource]/
  api/  models/  mappers/  query/  validation/  forms/  table/  types/  utils/  mocks/
```

**Enterprise-UI** adds: `composables/  components/`

---

# Data Transformation Patterns

```ts
first_name                    → firstName                   // snake_case → camelCase
created_at: string            → createdAt: Date             // mapper: new Date(dto.created_at)
avatar_url: string | null     → avatarUrl?: string | null   // nullable inference
dto.organization.data.name    → organizationName            // flatten nesting
```

**Paginated wrapper shape:**
```ts
interface PaginatedDto<T> {
  data: T[]
  meta: { total: number; per_page: number; current_page: number; last_page: number }
  links: { first: string; last: string; next: string | null; prev: string | null }
}

interface PageMeta {
  total: number
  perPage: number
  currentPage: number
  lastPage: number
  hasNext: boolean
  hasPrev: boolean
}

interface PaginatedResult<T> {
  items: T[]
  page: PageMeta
}
```

**Error envelope shape:**
```ts
interface ApiErrorDto {
  errors: Array<{ code: string; field?: string; message: string }>
}

interface ApiFieldError {
  field: string
  message: string
}
```

---

# Output Structure

Include only requested sections, in this order:

DTOs → Models → Enums → Validation → Mappers → Query Hooks → UI Types → Forms → Table Columns → Selection Models → Formatters → Mocks → Folder Structure → Notes

**Notes:** Frontend-relevant only — nullable edge cases, SSR concerns, normalization opportunities, rendering optimizations.

---

# Philosophy

- Flat models > deep nesting
- camelCase everywhere in frontend code
- Tree-shakeable utilities
- No excessive generics or backend-oriented abstractions
- Optimize for component readability, not backend purity
