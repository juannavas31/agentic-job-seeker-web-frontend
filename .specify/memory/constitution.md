<!--
Sync Impact Report
- Version change: template placeholder -> 1.0.0
- Modified principles: none (initial constitution)
- Added sections: Core Principles, Technology and UI Constraints, Development and Quality Workflow, Governance
- Removed sections: none
- Follow-up TODOs:
  - TODO(RATIFICATION_DATE): confirm the original project adoption date.
-->

# Agentic Job Seeker Constitution

## Core Principles

### I. Core Stack and Strict Typing

The application MUST use Next.js App Router, React 19, and TypeScript in strict mode. The
`pages/` directory is forbidden. The compiler MUST enable `noUncheckedIndexedAccess: true`,
and `any` is forbidden. Zod MUST validate environment variables, API payloads, Server
Action inputs, and structured LLM outputs. These rules provide a predictable, type-safe
foundation and prevent unvalidated data from crossing system boundaries.

### II. Mantine-First UI and Styling

Mantine MUST be the primary component and styling system across the application, including
`@mantine/core`, `@mantine/hooks`, `@mantine/form`, `@mantine/notifications`,
`@mantine/modals`, and `@mantine/dates` when needed, plus `@tabler/icons-react`. Tailwind
CSS and competing UI libraries are forbidden unless explicitly amended by this constitution.
Mantine style props and centralized `MantineProvider` theme tokens take precedence. Custom
states and layouts MUST use CSS Modules with Mantine CSS variables and
`postcss-preset-mantine`; raw inline style strings and scattered ad-hoc stylesheets are
forbidden. The unified theme MUST define typography, spacing, radii, primary color, and
hydration-safe light and dark color schemes.

### III. Mobile-First Responsive Ergonomics

Every page, dashboard, job card, resume and application diff view, agent stream, modal,
and drawer MUST be designed mobile-first and verified from 375px-wide mobile viewports
through desktop viewports. Mantine responsive props, `SimpleGrid`, `Stack`, `Group`,
`Drawer`, `Modal`, and responsive `AppShell` patterns MUST prevent horizontal overflow and
clipped action bars. Interactive controls MUST retain comfortable touch targets and legible
typography. Shared navigation and approval actions MUST remain reachable without
horizontal scrolling.

### IV. Server-First React Rendering

React Server Components MUST be the default for all components. A component MUST add
`"use client"` only when browser APIs, event listeners, Mantine interactive hooks or
providers, or genuinely local interactive agent state require it. React 19 `useActionState`
and `useFormStatus` MUST support form mutations, `useOptimistic` MUST provide immediate
feedback for reversible updates, and `use()` MUST unwrap promises. `forwardRef` is forbidden;
components pass `ref` as a standard prop. Components MUST NOT use `useEffect` for data
fetching.

### V. Observable and Streamed Agentic UX

Every AI agent interaction, including job matching, resume tailoring, cover-letter
generation, and interview preparation, MUST stream incremental output so users receive
progressive results without synchronous multi-second UI freezes. Multi-step workflows MUST
display clear status updates and expose intermediate outputs for inspection on mobile and
desktop. Agent progress, errors, and approval points MUST remain understandable at each
workflow step.

### VI. Authentication and Authorization

Authentication MUST be delegated to an external identity system, such as Keycloak, that
validates credentials and returns a JWT for backend interactions. Regular users MUST access
only their own resumes, searches, applications, and related data. Administrator users MUST
be authorized for administrative tasks, including user management. The authentication system
MUST define each user's regular-user or administrator role. Authentication behavior MUST be
covered by unit tests and end-to-end tests.

### VII. Secure URL-State Architecture and Quality

Search queries, filters, pagination, and active view or drawer state MUST use URL search
parameters when they are shareable or navigable. Client state MUST remain minimal, and all
LLM credentials and API keys MUST remain server-side. Application code MUST be organized
under `src/` using `src/app/`, `src/features/<domain>/`, `src/theme/`, and
`src/components/ui/`. Unit and component tests MUST accompany implementation, and
end-to-end tests MUST cover mobile and desktop viewports.

## Technology and UI Constraints

The App Router implementation is the sole Next.js routing architecture. Mantine, React 19,
strict TypeScript, Zod, and the directory structure above are required. Introductions of
alternate routing, validation, styling, or UI systems require an explicit constitutional
amendment and migration rationale.

## Development and Quality Workflow

Feature work MUST begin with tests that cover the affected behavior, rendering mode,
authorization boundary, and responsive viewport as applicable. Pull requests and reviews
MUST verify every applicable principle and must reject code that introduces forbidden
patterns or bypasses validation, authorization, streaming, or accessibility requirements.
Implementation changes MUST preserve server-first boundaries, keep secrets on the server,
and remain independently testable.

## Governance

This constitution supersedes informal project practices. Amendments require a documented
proposal, explicit maintainer approval, and a migration plan for affected code. A MAJOR
version change is required for incompatible governance or principle removals or
redefinitions. A MINOR version change is required for each new principle or section or
materially expanded guidance. A PATCH change is required for clarification, wording, typo,
or other non-semantic refinements. All pull requests and design reviews MUST verify
compliance, and intentional exceptions MUST be recorded with rationale and a removal plan.

**Version**: 1.0.0 | **Ratified**: TODO(RATIFICATION_DATE): confirm original adoption date | **Last Amended**: 2026-11-21
