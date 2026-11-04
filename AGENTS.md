<!-- BEGIN:nextjs-agent-rules -->

# This is NOT the Next.js you know

This version has breaking changes — APIs, conventions, and file structure may all differ from your training data. Read the relevant guide in `node_modules/next/dist/docs/` (resolved from this file's directory; in monorepos the `next` package may not be visible from the repo root) before writing any code. Heed deprecation notices.

This block is written and re-added by `next dev` — verify at `node_modules/next/dist/server/lib/generate-agent-files.js`. Removing it from a diff only re-creates the uncommitted change; committing it with your work keeps the tree clean.

<!-- END:nextjs-agent-rules -->

## Fish Medicine Store Project

- Read [docs/PROJECT_ANALYSIS.md](docs/PROJECT_ANALYSIS.md) and the Bengali PRD before making product or architecture changes.
- This repository is currently a frontend-only prototype. Do not add a backend, database, real authentication, payment, courier, or AI integration unless the user explicitly changes scope.
- Follow the installed Next.js version and its local documentation in `node_modules/next/dist/docs/`; keep App Router pages as Server Components unless a component needs browser state or event handlers.
- Build the UI from the user's Figma/reference assets when supplied. Until then, do not invent brand colors, typography, product imagery, or a finished visual direction.
- Keep the experience Bangla-first, mobile-first, accessible, and usable on slow connections. Do not invent medicine claims, prescriptions, or dosages; only show approved product/safety content and the required disclaimer.
- Use typed mock data behind a small service boundary for prototype interactions. Keep financial and personal information synthetic; never imply that simulated payments or orders are real.
- Preserve the existing `src/` layout and shadcn/Base UI conventions. Reuse installed packages; do not install dependencies or copy the reference repository's package versions without a clear need.
- Validate code changes with `pnpm lint`, `pnpm typecheck`, and, when practical, `pnpm build`. There is no test script configured yet.
