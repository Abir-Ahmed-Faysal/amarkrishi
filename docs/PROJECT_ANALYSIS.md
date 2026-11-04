# Project Analysis and UI Prototype Handoff

**Status:** Initial analysis complete; UI implementation is waiting for the user's Figma design.  
**Requirements source:** [Fish Medicine E-commerce PRD](<../মাছের ঔষধ E-commerce Product Requirements Document (PRD).docx>), version 1.1, dated 3 November 2026.  
**Architecture reference:** [MediStore_Client](https://github.com/Abir-Ahmed-Faysal/MediStore_Client).

## Executive summary

The PRD describes a Bangla-first, mobile-first fish-medicine commerce product for fish farmers, with a guided symptom survey, rule-based product suggestions, checkout, delivery, and later salesperson commissions and admin operations. The requested immediate deliverable is only a client-demo UI prototype; the supplied Figma is still pending.

Keep this repository frontend-only for the prototype. Use deterministic synthetic data behind typed mock services, and simulate checkout/order states in the browser. Do not build a backend, database, real auth, gateway, courier integration, or AI suggestions as part of this phase.

## Current workspace findings

- Next.js App Router, TypeScript, React, Tailwind CSS 4, and shadcn/Base UI are already installed. The current package versions include Next.js 16.4.3 and React 19.3.1.
- The app is a starter shell: `src/app/page.tsx` renders a placeholder, `src/app/layout.tsx` has generic metadata and `lang="en"`, and `src/app/globals.css` contains starter theme tokens.
- Existing reusable code is limited to `src/components/ui/button.tsx`, `src/components/theme-provider.tsx`, and `src/lib/utils.ts`; `src/hooks/` is present but empty.
- `README.md` is still the generic Next.js template. Package scripts include `pnpm dev`, `pnpm lint`, `pnpm typecheck`, `pnpm build`, and `pnpm start`; no test runner is configured.
- The installed Next.js package includes local documentation under `node_modules/next/dist/docs/`. Check it before relying on framework APIs because the version may differ from general online examples.
- There is no existing business UI, mock-data layer, backend client, or MCP configuration in this workspace.

## Reference repository findings

The reference organizes its `src/` by responsibility: `actions/`, `app/`, `components/`, `constants/`, `hooks/`, `lib/`, `providers/`, `routes/`, `services/`, and `types/`. It also uses App Router route groups for common, auth, and dashboard layouts; its component directories include common, layout, modules, and UI areas.

This is a useful organizational reference, not a template to copy wholesale. Its README is generic, and its package manifest uses Next.js 16.1.1 / React 19.2.3 rather than this project's versions. Do not copy its dependencies, auth, action, or service implementations. In particular, its public source structure does not provide an MCP setup relevant to this prototype.

## PRD synthesis

### Product and user experience

- Primary audience: fish farmers, including people with limited technical experience and slow rural mobile internet.
- The customer journey should be simple and visual: select fish type and symptoms one question at a time, review rule-based suggestions with a reason, add products, and complete an easy order.
- Bangla-first content, readable Bangla font rendering, large touch targets, responsive/mobile-first layouts, light pages, and persistent call/WhatsApp support are requirements.
- Product information includes image, bilingual/searchable names where supplied, brand/company, category, pack size, price/discount, stock state, ingredients/strength, usage instructions, warnings, storage, and registration number.
- Recommendations must use fish/symptom-to-product mappings and approved content. Show the PRD disclaimer; do not invent a medicine, brand, ingredient, efficacy, or dosage recommendation.
- The PRD includes COD risk review, optional consent-based one-time location capture, free-delivery threshold, cross-sell, survey sharing, and lead follow-up in Phase 1. Any demo interaction must be explicit and synthetic; location permission or collection should not be simulated as if it were real.

### PRD phases

**Phase 1 / MVP:** customer auth concept, catalog and search/filter, product details and stock, guided survey and rule-based results, cart/guest checkout, COD/partial/full payment UX, delivery zones, one courier workflow, order tracking, basic admin order/product/stock screens, basic COD risk/confirmation flow, support links, survey sharing, and admin lead follow-up.

**Phase 2:** salesperson onboarding/dashboard, referral attribution, salesperson-created customer/order flows, commission lifecycle, double-entry ledger and wallet, manual withdrawals and reversals, expanded admin/audit, coupon and multi-courier operations, bundles, and additional reporting.

**Phase 3:** SMS OTP, SMS notifications, AI limited to approved general husbandry tips (never medicine/brand/dose suggestions), automated payouts/refunds, customer returns, reviews, and expanded analytics.

The UI prototype should follow the Figma and the requested demo scope; these phases are requirements boundaries, not a mandate to build every listed screen now.

### Architecture and domain constraints in the PRD

The PRD's eventual production architecture is Next.js frontend → Node.js/Express TypeScript REST API → PostgreSQL/Prisma, with Google/JWT auth and proposed Redis/BullMQ workers. Business modules include auth, users, catalog, survey, checkout/orders, payments, shipments, referral, commissions, ledger/wallet/withdrawals, stock, notifications, settings, and audit.

Money-related production rules (transactional ledger, immutable entries, idempotency, exact decimal currency, snapshotting order prices/settings, and concurrency protection) belong to the future backend and must not be approximated as authoritative frontend logic. The prototype can display computed examples but must label them as simulated.

## Recommended frontend structure

Adopt the reference's responsibility-based grouping gradually, while retaining this repository's current `src/` layout and avoiding empty placeholder folders. Suggested destinations when the Figma surfaces require them:

```text
src/
  app/
    (store)/                  # public storefront, product, survey, cart, checkout, tracking
    (admin)/                  # only agreed Phase 1 admin demo screens
  components/
    common/                   # shared shell/support elements
    store/                    # catalog/product-specific UI
    survey/                   # survey and suggestion UI
    admin/                    # admin demo UI
    ui/                       # existing reusable primitives
  constants/                  # route labels or stable UI constants, if needed
  hooks/                      # reusable interactive hooks
  lib/                        # formatting and small pure helpers
  mocks/                      # typed, deterministic fixture data
  providers/                  # shared client state only when needed
  services/                   # mock services with a future API-compatible boundary
  types/                      # shared frontend domain/view-model types
```

Use Next.js App Router file conventions and route groups to share layouts without adding URL segments. Keep pages/layouts as Server Components by default; add Client Components only where browser state, forms, or event handlers are needed. Do not add backend-oriented server actions; keep UI operations behind a frontend service boundary that can later be switched from mock implementations to the separately specified Express API.

## Mock prototype recommendation

- No new dependency is needed initially. Create small typed fixtures and deterministic mock services for products, fish/symptom mappings, survey results, cart, and demo orders.
- Keep mock computation in service/helper modules rather than embedding business rules in presentational components. Treat pricing, stock, eligibility, and order states as illustrative only.
- Use local component/context state for interaction; persist only non-sensitive demo state (for example, a demo cart) if refresh resilience is necessary. Never persist real phone, address, precise location, credentials, or payment information.
- Use explicit demo states and resettable fixtures so the client can repeatedly demonstrate the same journey.
- Do not wire real Google, payment, courier, email, SMS, WhatsApp API, GeoIP, GPS, or AI services. A normal `tel:`/`wa.me` support link may be added when the client supplies approved contact details.

## Key screens and demo flow to confirm against Figma

1. Storefront and catalog with search, category/problem filters, sort, price/discount, and stock states.
2. Product details with approved use, ingredients, warnings, storage, stock, and required safety disclaimer.
3. Guided fish-type/symptom survey and rule-based suggestion results with "why this" context, approved organic tips, and disclaimer.
4. Cart and checkout with customer/address inputs, delivery zone, price breakdown, payment-choice demonstration, and a clear simulated-order confirmation.
5. Order lookup/tracking demo.
6. Only the Phase 1 admin pages needed for the client walkthrough (likely product/stock, orders, COD confirmation/risk review, and lead follow-up).

Screen order, navigation, visual language, labels, product data, and responsive details must be taken from the Figma and client-provided content rather than guessed.

## Open decisions and content dependencies

The PRD marks these as proposed, undecided, or requiring client confirmation:

- Brand/store name, logo, colors, font, imagery, and final UI hierarchy (Figma pending).
- Approved product catalog, ingredient/strength data, fish/problem mappings, organic advice, and who reviews medicine claims/licensing.
- Delivery-zone definitions and final charges, free-delivery threshold, weight surcharge, high-value order threshold, and first-order advance behavior.
- Whether a survey requires a phone number, who follows up, and what contact consent wording to show.
- Admin confirmation responsibility/timing and final COD risk thresholds/actions; GPS is optional, consent-based, one-time, and privacy-limited.
- Phase 2 commission rate/calculation, minimum withdrawal, fee mode/refund rules, partial-return policy, closure/forfeit policy, salesperson Google login, and reporting permissions.
- Coupon constraints, stock import levels/expiry tracking, product-equivalence approval, and whether brand/company reputation affects ranking.
- Gateway and courier vendor selection, SMS cost, and operational contact details.

Do not silently turn proposed/open decisions into production behavior. For the prototype, use clearly marked sample values only when the Figma requires a visible state.

## MCP decision

No MCP server is needed for the current UI-only prototype: there is no external data system or development integration to expose, and the reference repository has no MCP configuration in its root. Do not create an MCP config merely as part of app architecture. Revisit only if the user identifies a concrete MCP server/tool and the system it should connect to.

## Handoff sequence

1. Receive and inspect the Figma image/assets; confirm the first demo flow and any screens outside Phase 1.
2. Confirm brand/content assets and which proposed values are acceptable as visibly marked mock data.
3. Build the first cohesive customer journey with mock services, matching the design responsively.
4. Add only the admin/demo states the client needs to understand fulfillment.
5. Verify the flow manually and run `pnpm lint`, `pnpm typecheck`, and `pnpm build`.
6. Keep backend, real integrations, and Phase 2/3 features deferred until separately approved.
