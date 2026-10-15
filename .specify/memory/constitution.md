<!--
Sync Impact Report
Version change: unversioned scaffold -> 1.0.0
Modified principles: none (initial constitution)
Added sections: Project Constraints; Development Workflow and Quality Gates
Removed sections: none
Follow-up TODOs: none
-->
# RSS Feed Reader Constitution

## Core Principles

### I. Secure by Default
Treat subscription URLs and feed content as untrusted input. In the MVP, adding a
subscription MUST only store and display its URL; it MUST NOT trigger a network request.
Any approved feature that fetches feeds MUST restrict requests to supported web protocols,
block loopback and private-network destinations, apply timeouts and response-size limits,
and recheck destinations after redirects to prevent server-side request forgery. Never
render feed-provided HTML unless it has been sanitized with a maintained, purpose-built
sanitizer. Secrets MUST NOT be committed to the repository.

### II. Maintainable, Layered Design
Keep the ASP.NET Core Web API responsible for subscription data and server-side operations,
and the Blazor WebAssembly frontend responsible for user interaction. Keep API contracts
explicit and dependencies flowing through the established application boundaries. Prefer
the simplest design that supports the approved scope; do not add persistence, background
services, parsing libraries, or abstractions before a feature requires them. This preserves
the project's incremental path without burdening the proof of concept.

### III. Verifiable Code Quality
Every change MUST build successfully and include automated tests for new or changed
behavior at the relevant unit or API boundary. Tests MUST cover applicable success,
invalid-input, and failure cases. Changes to shared contracts or communication between the
frontend and backend MUST include integration-level coverage. Before delivery, run the
applicable tests and build checks, and resolve failures introduced by the change.

### IV. Explicit MVP Scope
The MVP is limited to adding a subscription by URL and displaying the subscription list.
Subscriptions are in memory; the MVP does not fetch or parse feeds, persist data, remove
subscriptions, or display feed items. Work beyond this boundary MUST be identified as a
separate, approved feature before implementation. Extended-MVP behavior, including manual
refresh and feed-item display, MUST remain distinct from MVP requirements.

### V. Clear Contracts and User Outcomes
User-visible behavior and frontend/backend API contracts MUST be defined consistently in
the feature requirements. The subscription list MUST reflect successful additions
immediately. When an approved operation can fail, requirements MUST define the user-facing
failure outcome; implementation MUST report failures explicitly rather than presenting
them as successful results. Keep messages and data presentation understandable for the
single-user, local application.

## Project Constraints

The application uses an ASP.NET Core Web API backend and a Blazor WebAssembly frontend,
and MUST remain buildable and runnable on Windows, macOS, and Linux. For MVP, the backend
stores subscriptions in memory and exposes operations to add and list them. Feed fetching,
RSS/Atom parsing, persistent storage, automatic polling, feed-item display, and rich HTML
rendering are outside MVP scope. They may be introduced only through separately specified
and approved work that follows the security and quality principles above.

## Development Workflow and Quality Gates

Feature specifications MUST state scope, observable outcomes, and relevant failure and
boundary cases before implementation tasks are approved. Plans and tasks MUST preserve the
MVP/Extended-MVP boundary and identify the affected frontend, backend, and API contract
surfaces. Before delivery, review changes for this constitution's security, scope,
maintainability, and quality requirements; run the relevant .NET build and automated tests.
Features introducing network access, persistence, or feed-content rendering MUST include
requirements and tests for their security and failure boundaries.

## Governance

This constitution governs feature specifications, plans, tasks, implementation, and
reviews. A conflict MUST be resolved by changing the subordinate artifact or by amending
this constitution; an implementation MUST NOT silently waive a principle. Amendments
require a documented rationale and review by the project maintainers before adoption.
Every amendment MUST update the version and last-amended date and include a sync impact
report. Use semantic versioning: MAJOR for incompatible governance changes or removal of
a principle, MINOR for a new principle or materially expanded requirements, and PATCH for
clarifications or non-semantic wording changes.

Feature reviews MUST check scope and quality-gate compliance, and MUST identify any
unresolved conflict before implementation or delivery. The constitution is reviewed when
the project's scope or architecture changes materially and during relevant feature
reviews.

**Version**: 1.0.0 | **Ratified**: 2026-10-15 | **Last Amended**: 2026-10-15
