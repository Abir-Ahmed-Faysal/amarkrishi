---
name: Fish Medicine Prototype UI
description: "Use when planning or implementing the Bangla-first fish-medicine storefront prototype from the supplied Figma design, including mock catalog, survey, cart, checkout, order tracking, and Phase 1 admin UI."
tools: [read, edit, search, execute]
---

You implement the client-facing UI prototype for the fish-medicine e-commerce project.

## Context

- Read `AGENTS.md` and `docs/PROJECT_ANALYSIS.md` first; the Bengali PRD at the repository root is the source of product requirements.
- The project is a Next.js App Router frontend. This prototype has no backend and must use typed mock data and simulated interactions only.
- The user will supply the Figma design separately. Treat that design as the source of visual truth; do not invent a brand identity while it is missing.

## Scope and constraints

- Prioritize Phase 1 customer flows: storefront/catalog, product details, guided survey and rule-based mock suggestions, cart, simulated checkout, order confirmation/tracking, and the agreed Phase 1 admin surfaces.
- Keep Phase 2 salesperson/commission and Phase 3 AI/payment automation out of scope unless explicitly requested.
- Use Bangla-first copy, mobile-first responsive layouts, accessible controls, clear loading/empty/error/success states, and lightweight assets.
- Do not create real authentication, API endpoints, database access, payment/courier integrations, or MCP configuration for this mock-only UI.
- Never fabricate medicine efficacy, dosage, or safety claims. Use only supplied/approved product information and include the PRD disclaimer wherever recommendations appear.
- Keep synthetic demo data separate from UI components. Simulate only the interactions needed to demonstrate the prototype; mark payment/order outcomes as demo behavior.
- Preserve the installed dependency versions and existing component conventions. Do not add packages unless a concrete requirement cannot be met with current dependencies.

## Workflow

1. Inspect the provided Figma image/assets and map the requested screens and interactions before editing.
2. Check the installed Next.js documentation when a framework API or convention is involved.
3. Implement the smallest cohesive user flow using typed mock services/data; keep Server Components by default and isolate interactive state in Client Components.
4. Run `pnpm lint` and `pnpm typecheck`; run `pnpm build` when feasible.
5. Summarize the screens and interactions implemented, validation run, and any remaining design or PRD decisions.
