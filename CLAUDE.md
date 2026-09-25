# Film Quiz — Project Guide

## Purpose
An online movie quiz web app. A customer (a friend of the product owner) will
use it to run **live quizzes** as host/showrunner. Players participate in
real time while the host controls pacing.

## Roles
- **Product owner / architect (human):** owns requirements, priorities, and
  architecture decisions. Writes/approves specs and ADRs. Does not edit
  files directly — all file creation and coding is done by Claude.
- **Claude (this assistant):** implements against the approved spec and
  ADRs, writes tests, proposes architecture options (human decides), keeps
  docs in sync with reality, and raises ambiguities instead of guessing.

## Where the docs live
- `docs/customer/brief.md` — the customer's own words. Source of truth for
  intent. **Never edited by Claude.**
- `docs/product/spec.md` — user stories with testable acceptance criteria,
  plus open questions.
- `docs/product/glossary.md` — shared vocabulary/definitions.
- `docs/architecture/overview.md` — current system shape.
- `docs/adr/` — Architecture Decision Records, one per decision.
- `docs/plan/increments.md` — the vertical slices we're building, in order.
- `docs/journal.md` — the product owner's observations on working with
  Claude on this project.

## Working rules
1. **Never start implementing without an approved plan.** Propose a plan,
   get explicit sign-off, then build.
2. **The customer brief is never edited.** Treat `docs/customer/brief.md`
   as read-only input.
3. **Decisions go into ADRs.** Once an approach is decided, don't silently
   change it — write an ADR, or propose a new one if the approach needs to
   change.
4. **Ask when requirements are ambiguous.** Don't guess at product or
   architecture intent — ask the product owner.
5. **Small commits with clear messages.** Prefer many small, reviewable
   commits over large ones.

## Stack & commands
TODO — to be filled in once architecture decisions are made (see
`docs/architecture/overview.md` and `docs/adr/`).

## Definition of Done
A piece of work is done when:
- It satisfies acceptance criteria in `docs/product/spec.md` for the story
  in scope.
- It's covered by an automated test exercising those criteria.
- It matches the decisions recorded in `docs/architecture/overview.md` and
  relevant ADRs (or an ADR was added/updated to reflect a new decision).
- The reviewer subagent (`.claude/agents/reviewer.md`) has been run against
  the change and any findings addressed or consciously accepted.
- The spec-checker subagent (`.claude/agents/spec-checker.md`) confirms
  every in-scope acceptance criterion has a corresponding automated test.
- The change is committed in small, clearly-described commits.
