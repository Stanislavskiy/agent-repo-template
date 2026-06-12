# AGENT ENTRY POINT
> Read this file first. Load additional context only as needed per the routing table below.

## Project Identity
| Key | Value |
|-----|-------|
| Name | `[PROJECT_NAME]` |
| Type | `[web-app \| api \| monorepo \| data-pipeline \| library]` |
| Primary language | `[LANG@VERSION]` |
| Framework | `[FRAMEWORK@VERSION]` |
| Infrastructure | `[cloud-provider] · [container/orchestration] · [db]` |

## Context Routing — load ONLY what your task needs
| Task type | Load |
|-----------|------|
| New feature / module | `.agents/context/conventions.md` + `.agents/context/architecture.md` + `.agents/context/domain.md` |
| Bug fix | `.agents/context/conventions.md` + `.agents/context/architecture.md` |
| Refactor / code quality / tests / CI | `.agents/context/conventions.md` |
| Infra / DevOps | `.agents/context/architecture.md` |
| Data model / DB change | `.agents/context/domain.md` + `.agents/context/architecture.md` |
| Deep context needed | `docs/` (source of truth — do not edit unless explicitly asked) |
| Quick question | This file only |

## Repo Structure
```
.agents/                 ← agent context root (you are here)
  AGENTS.md              ← entry point (this file)
  context/
    architecture.md      ← system design, services, data flow, infra
    conventions.md       ← second routing layer → principles/ (load before principles/)
    domain.md            ← entities, business rules, glossary
  principles/            ← agent-only principles (not derived from /docs)
    distilled/           ← READ-ONLY · auto-generated from /docs
  adr/
    YYYYMMDD-[slug].md   ← ADRs (append-only)
  prompts/
    [task-slug].md       ← reusable task prompt templates
docs/                    ← single source of truth (human/agent authored)
src/                     ← application source (project-specific)
```

## Hard Constraints
```
PROTECTED PATHS   : [e.g. src/core/auth/, infra/prod/]
FORBIDDEN LIBS    : [e.g. moment.js, lodash in hot paths]
REQUIRED PATTERNS : [e.g. all DB access via repository layer]
DATA SENSITIVITY  : [NONE | PII | PHI | PCI]
AUTH BOUNDARY     : [e.g. never write auth logic outside src/auth/]
LANG VERSION LOCK : [e.g. Node 22, Python 3.12, no experimental APIs]
```

## Active Focus
> _Optional — 1–2 sentences on the current sprint objective. Delete when not relevant._