# Increments

Work is planned and delivered as small vertical slices — each one should
be independently demoable and move end-to-end through the system (not a
horizontal layer like "just the backend").

## Increment template
Copy this block per increment.

```
## [INC-NNN] <short title>

**Goal:** what user-visible capability this delivers.

**Stories covered:** US-NNN, US-NNN

**Acceptance criteria:** (link to spec.md entries, or restate if narrower)
- [ ] ...

**Architecture impact:** any ADRs this touches or requires.

**Status:** planned | in progress | done
```

## Backlog

Criterion numbers below refer to the order of acceptance criteria within
each story in `docs/product/spec.md`.

## [INC-001] Walking skeleton

**Goal:** a participant can open a deployed URL, play one seeded round,
guess tiles, see answers revealed, and get a completion message, with no
login and no admin UI.

**Stories covered:** US-104, US-105, US-106, US-108 (all partial), NFR-001

**Acceptance criteria:**
- [ ] US-104 criteria 1–2 (tile grid grouped by tier, free order), using
      one seeded round. Not criterion 3 (personal window → INC-005).
- [ ] US-105 criteria 1–3 and 5 (tile page, unlimited replay, generic
      wrong message, nothing reveals the answer). Not criterion 4
      (wrong-guess counting → INC-005).
- [ ] US-106 criteria 1, 2 and 4 (reveal, field disappears, server-side
      checking). Not criterion 3 (per-tile stats → INC-005).
- [ ] US-108 criterion 1 (completion message). Not criterion 2 (re-open
      as revealed → INC-002).
- [ ] NFR-001, all criteria.
- [ ] Until matching strictness is configurable (INC-004), guesses are
      matched "exact" as defined in the glossary (case-insensitive),
      against the title and accepted variants.
- [ ] Progress is kept for the current browser session only; the
      completion message shows when all tiles are solved in that session.
      Saving across visits arrives in INC-002.
- [ ] The app is deployed to a URL by a CI/CD pipeline.

**Architecture impact:** requires ADRs for the stack, hosting, CI/CD, and
media storage/processing (blurred covers, metadata stripping, opaque URLs
for NFR-001).

**Blocked by open questions:** tile numbering (US-104).

**Status:** planned

## [INC-002] Accounts and saved progress

**Goal:** a participant can sign up and log in with email/password, and
their progress is saved so they can resume later.

**Stories covered:** US-101 (partial), US-102 (partial), US-107, US-108
(rest)

**Acceptance criteria:**
- [ ] US-101 criteria 1, 2 and 5 (welcome page, email/password sign-up
      with nickname, open sign-up). Not criterion 3 (third-party login →
      INC-007) or criterion 4 (nickname on leaderboards → INC-005).
- [ ] US-102 criterion 1 (password login only), and criterion 2 except
      the window clause (→ INC-005).
- [ ] US-107, all criteria.
- [ ] US-108 criterion 2 (completed round re-opens as revealed).

**Architecture impact:** requires ADRs for authentication and
persistence of accounts and progress.

**Blocked by open questions:** nickname uniqueness; password reset.

**Status:** planned

## [INC-003] Admin content creation

**Goal:** the owner can create a round, add tiles with uploads and
variants, publish it, and edit it, without seeded data.

**Stories covered:** US-202 (partial), US-203, US-204 (partial), US-205,
US-103 (partial)

**Acceptance criteria:**
- [ ] US-202 criteria 1 (name, tile count, and difficulty tiers only;
      other settings → INC-004 and INC-005) and 2 (unpublished rounds
      hidden).
- [ ] US-203, all criteria, with the interim "exact" matching from
      INC-001.
- [ ] US-204 criterion 1, without the launch window: publishing makes the
      round visible and playable. Not criteria 2–3 (windows → INC-005).
- [ ] US-205, all criteria.
- [ ] US-103 criterion 1 (list of published rounds), so more than one
      published round can be reached.
- [ ] One seeded owner account is the only account with access to the
      admin area; no role management (→ INC-007).

**Architecture impact:** media upload pipeline must produce assets that
satisfy NFR-001; may require an ADR on upload handling.

**Blocked by open questions:** tile count and "fully configured" (US-202/
203/204); clip length enforcement.

**Status:** planned

## [INC-004] Multiple rounds

**Goal:** participants can browse rounds by genre, and admins can set
genre and matching strictness per round.

**Stories covered:** US-103 (rest), US-202 (partial)

**Acceptance criteria:**
- [ ] US-103 criteria 2–3 (genre filter, untagged rounds).
- [ ] US-202 criterion 1: genre tag and answer-matching strictness
      settings, replacing the interim "exact" matching.

**Architecture impact:** none expected.

**Blocked by open questions:** genre tag count.

**Status:** planned

## [INC-005] Timing and round leaderboard

**Goal:** rounds run on launch and personal windows with wrong-guess
penalties, close behavior, per-tile stats, and a per-round leaderboard.

**Stories covered:** US-101 (partial), US-102 (rest), US-104 (rest),
US-105 (rest), US-106 (rest), US-109 (partial), US-202 (rest), US-204
(rest)

**Acceptance criteria:**
- [ ] US-101 criterion 4 (nickname is the identity shown on
      leaderboards).
- [ ] US-102 criterion 2, window clause (window keeps counting real
      elapsed time while away).
- [ ] US-104 criterion 3 (personal window).
- [ ] US-105 criterion 4 (wrong guesses counted).
- [ ] US-106 criterion 3 (per-tile aggregate stats).
- [ ] US-109 criterion 1 (round leaderboard).
- [ ] US-202 criterion 1: duration, wrong-guess penalty, and close
      behavior settings.
- [ ] US-204 criteria 1 (launch window starts on publish), 2 and 3.
- [ ] Scoring & Timing Rules in `docs/product/spec.md`.

**Architecture impact:** may require an ADR on time handling (server
clock as source of truth, window evaluation).

**Blocked by open questions:** competitive layer confirmation; others'
guesses vs. aggregate stats; hard cutoff; unfinished players on
leaderboards; retroactive penalties after variant edits (US-205).

**Status:** planned

## [INC-006] All-time leaderboard and profile

**Goal:** participants can see an all-time leaderboard, first-finisher
recognition, and their own profile.

**Stories covered:** US-109 (rest), US-110

**Acceptance criteria:**
- [ ] US-109 criteria 2–3 (all-time leaderboard, first finisher).
- [ ] US-110, all criteria.

**Architecture impact:** none expected.

**Blocked by open questions:** competitive layer confirmation; all-time
aggregation; first finisher definition.

**Status:** planned

## [INC-007] Roles, third-party login, Danish

**Goal:** the owner can manage admin access, participants can log in with
Google or Meta, and the UI is available in Danish.

**Stories covered:** US-201, US-101 (rest)

**Acceptance criteria:**
- [ ] US-201, all criteria.
- [ ] US-101 criterion 3 (Google/Meta sign-up), and US-102 criterion 1
      for linked third-party providers.
- [ ] Danish UI, scope pending the language open question.

**Architecture impact:** requires ADRs for third-party identity
providers and internationalization.

**Blocked by open questions:** language (Danish support).

**Status:** planned
