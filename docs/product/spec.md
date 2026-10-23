# Product Spec

Derived from `docs/customer/brief.md` plus a requirements interview with the
product owner on 2026-09-25 (see `docs/journal.md` if notes were added
there). Terms below are defined in `docs/product/glossary.md`.

## Status
Draft — stories reflect product-owner decisions from the interview, but are
not yet implementation-approved (see CLAUDE.md working rule 1), and the
Open Questions below need the actual customer's input before some details
are final.

## Scoring & Timing Rules

These rules are referenced by several stories below rather than repeated in
each one.

- Each round has a host-configured **duration** (e.g. 2 weeks), a
  **wrong-guess penalty** (default +30 seconds), and a **close behavior**
  (reveal or lock unfinished tiles).
- The duration is used two ways:
  1. **Launch window** — starts the instant the round is published. All
     participants who start the round during this window share that same
     start instant.
  2. **Personal window** — for a participant who first opens the round
     after the launch window has elapsed, the same duration is used as
     their own countdown, starting when they open it.
- A participant's **adjusted completion time** = (moment they correctly
  guess the round's last unsolved tile) − (their applicable window's start
  instant) + (wrong-guess penalty × their total wrong guesses in the
  round).
- Leaderboards (per-round and all-time) rank participants by lowest
  adjusted completion time.
- When a participant's window (launch or personal) ends, their unfinished
  tiles are revealed or locked per the round's configured close behavior.
  This does not affect tiles they already solved.

## Participant Stories

### US-101 Sign up for an account
As a new participant, I want to create an account, so that my quiz progress
and results are saved and linked to me.

**Acceptance criteria**
- [ ] Given a first-time visitor, when they open the app, then they see a
      welcome page describing what the quiz is about, with options to sign
      up or log in.
- [ ] Given the welcome page, when the visitor signs up, then they can
      create an account by providing a nickname, full name, email address,
      and password.
- [ ] Given the welcome page, when the visitor signs up, then they can
      alternatively continue with a supported third-party account provider
      (e.g. Google or Meta) instead of entering an email/password.
- [ ] Given an account is created, then the chosen nickname — not the full
      name or email — is the identity shown on leaderboards and to other
      participants.
- [ ] Given account creation is open, then any visitor can sign up without
      an invitation, approval, or access code.

**Status:** draft

### US-102 Log in and resume later
As a returning participant, I want to log in, so that I can continue where
I left off.

**Acceptance criteria**
- [ ] Given an existing account, when the participant logs in (password or
      linked third-party provider), then they see their previously saved
      progress across all rounds.
- [ ] Given a participant is mid-round, when they log out or close the app
      and return later, then previously solved tiles remain revealed and
      their window continues counting real elapsed time toward their
      adjusted completion time.

**Status:** draft

### US-103 Browse rounds and genres
As a participant, I want to see the quiz's rounds and browse by genre, so
that I can choose what to play.

**Acceptance criteria**
- [ ] Given a logged-in participant, when they open the main quiz menu,
      then they see a list of published rounds.
- [ ] Given the main quiz menu, when the participant browses by genre
      instead, then they see rounds filtered to that genre tag.
- [ ] Given a round has no genre tag, then it still appears in the plain
      round listing (but not under any genre filter).

**Status:** draft

### US-104 Start a round and pick tiles freely
As a participant, I want to choose any tile in a round freely, so that I
can play the clips I want in the order I want.

**Acceptance criteria**
- [ ] Given a round the participant has access to, when they open it,
      then they see the round's tiles grouped by difficulty tier, as
      configured by the host for that round.
- [ ] Given the tile grid, when the participant selects any unsolved tile,
      then it opens regardless of whether other tiles have been completed
      (no forced order).
- [ ] Given a participant opens a round for the first time after its
      launch window has already elapsed, then their personal window starts
      at that moment (see Scoring & Timing Rules).

**Status:** draft

### US-105 Listen to a clip and guess
As a participant, I want to listen to an audio clip and type my guess, so
that I can identify the movie.

**Acceptance criteria**
- [ ] Given an unsolved tile, when opened, then the participant sees a
      blurred cover (or a question-mark placeholder), a player, and a
      free-text answer field.
- [ ] Given the tile page, when the participant presses play, then the
      tile's audio clip plays and can be replayed an unlimited number of
      times.
- [ ] Given the free-text field, when the participant submits a guess that
      doesn't match the correct title or an accepted variant, then they
      see a generic "wrong, try again" message and can guess again
      immediately, with no limit on attempts.
- [ ] Given a wrong guess, then it is counted toward that participant's
      wrong-guess total for the round (used for the timing penalty and
      aggregate stats), even though it doesn't block further guessing.
- [ ] Given an unsolved tile, then nothing delivered to the client reveals
      its answer (see NFR-001).

**Status:** draft

### US-106 See the answer revealed on a correct guess
As a participant, I want to see the full answer once I guess correctly, so
that I get confirmation and details.

**Acceptance criteria**
- [ ] Given a correct guess (matching the title or an accepted variant,
      per the round's configured matching strictness), when submitted,
      then the blurred cover is replaced by the real cover, with the
      movie title and composer shown beside it and the premiere year
      shown below.
- [ ] Given a correct guess, then the free-text field disappears and no
      further guesses can be submitted for that tile.
- [ ] Given a correct guess, then the participant sees aggregate stats for
      that tile: how many participants have guessed it correctly, and how
      many total wrong attempts have been made on it — not other
      participants' individual guessed text.
- [ ] Given a guess, then correctness is decided server-side, and the
      reveal data is delivered only in the response to a guess the server
      verified as correct (see NFR-001).

**Status:** draft

### US-107 Automatic progress saving
As a participant, I want my progress saved automatically, so that I don't
have to finish a round in one sitting.

**Acceptance criteria**
- [ ] Given a correct guess on a tile, then that tile's solved state is
      saved to the participant's account immediately.
- [ ] Given a participant returns to a partially completed round, then
      previously solved tiles are already shown revealed, and unsolved
      tiles remain playable.

**Status:** draft

### US-108 Complete a round
As a participant, I want to know when I've finished a round, so that I get
a clear sense of completion and my result.

**Acceptance criteria**
- [ ] Given a participant correctly guesses the last unsolved tile in a
      round, then they see a congratulatory completion message.
- [ ] Given a completed round, when the participant re-opens it later,
      then every tile shows its revealed answer, clips remain playable,
      and no tile offers a free-text field or further guessing.

**Status:** draft

### US-109 Compete on the leaderboard
As a participant, I want to see how I rank, so that I can compete on speed
and accuracy.

**Acceptance criteria**
- [ ] Given a round in progress or completed, then the participant can
      view that round's leaderboard, ranked by adjusted completion time
      (see Scoring & Timing Rules).
- [ ] Given any round a participant has completed, then their adjusted
      completion time also counts toward a single combined all-time
      leaderboard spanning all rounds.
- [ ] Given a round, when a participant is the first to complete it, then
      they receive a permanent "first finisher" recognition on their
      profile and on that round's leaderboard, which stays even if their
      completion time is later beaten by another participant (exact
      definition of "first" pending customer input — see Open Questions).

**Status:** draft

### US-110 View profile
As a participant, I want a profile page, so that I can see my own results
and recognitions.

**Acceptance criteria**
- [ ] Given a logged-in participant, when they open their profile, then
      they see their nickname, their all-time leaderboard position, and
      any "first finisher" badges they've earned.

**Status:** draft

## Host / Admin Stories

### US-201 Manage admin access
As the owner, I want to manage who has admin access, so that I control who
can create quiz content.

**Acceptance criteria**
- [ ] Given the owner role, when they access admin management, then they
      can grant or revoke editor-level admin access for other accounts.
- [ ] Given an editor-level admin, then they can create and edit round and
      tile content but cannot manage other admins' access.

**Status:** draft

### US-202 Create a round
As an admin, I want to create a new round, so that I can publish a new set
of tiles for participants.

**Acceptance criteria**
- [ ] Given the admin area, when an admin creates a round, then they can
      set: a name, an optional genre tag, the tile count and how tiles are
      grouped into difficulty tiers, the round's duration, the wrong-guess
      time penalty (defaulting to +30 seconds), the answer-matching
      strictness (exact or forgiving), and the close behavior (reveal or
      lock) for unfinished tiles.
- [ ] Given a round is created but not yet published, then it is not
      visible to participants.

**Status:** draft

### US-203 Add a tile to a round
As an admin, I want to add a movie tile to a round, so that participants
have something to guess.

**Acceptance criteria**
- [ ] Given a round being edited, when an admin adds a tile, then they
      upload an audio clip and a cover image, enter the correct title,
      composer, and premiere year, assign a difficulty tier, and enter any
      number of additional accepted answer variants.
- [ ] Given a tile's accepted variants list, then a participant's guess
      matching the correct title or any listed variant (per the round's
      matching strictness) counts as correct.

*Note for admins:* clips are expected to be approx. 30–60 seconds (per
the brief). The upload form shows this as guidance.

**Status:** draft

### US-204 Publish a round
As an admin, I want to publish a round, so that participants can start
playing it.

**Acceptance criteria**
- [ ] Given a fully configured round, when an admin publishes it, then it
      becomes visible and playable to participants, starting its launch
      window.
- [ ] Given a published round whose launch window has elapsed, then it
      remains available for a participant to open for the first time,
      starting that participant's personal window (see Scoring & Timing
      Rules).
- [ ] Given any participant's window (launch or personal) ends, then their
      unfinished tiles are revealed or locked per the round's configured
      close behavior.

**Status:** draft

### US-205 Edit round or tile content
As an admin, I want to edit a round or tile after creation, so that I can
fix mistakes.

**Acceptance criteria**
- [ ] Given an existing round or tile, when an admin edits it (e.g. fixing
      a typo in an accepted answer), then the change applies immediately
      to all participants' future guesses.

**Status:** draft

## Non-Functional Requirements

### NFR-001 Answer secrecy
The participant's client must never receive anything that reveals a
tile's **answer** until that tile is solved by that participant (or
revealed to them by round completion or reveal-on-close). "Answer" means
the title, accepted variants, composer, premiere year, and original cover
image. Answer checking happens server-side. Admin screens are out of
scope.

**Acceptance criteria**
- [ ] Given an unsolved tile, then no participant-facing response (page
      HTML, client code bundle, API response, asset URL, or HTTP header)
      contains its title, any accepted variant, composer, year, or the
      original cover's file name or URL.
- [ ] Given an unsolved tile, then the cover the client receives is a
      server-produced blurred image or a placeholder, not the original
      image blurred in the browser.
- [ ] Given an unsolved tile, then the original cover can only be
      obtained through the response to a correct guess, or for a tile
      already solved or revealed for that participant.
- [ ] Given a tile's audio clip, then its URL and file name are opaque
      identifiers, and the delivered file carries no embedded metadata
      (e.g. ID3 title, album, artist, composer, comment, or cover art).
- [ ] Given a submitted guess, then the server decides whether it is
      correct; the client never receives the correct answer, the
      variants, or any hash or encoded form of them for comparison.
- [ ] Given a locked tile (lock-on-close), then the same rules apply as
      for an unsolved tile.

**Status:** draft

## Open Questions
Items that need input from the customer (Mogens, the host) or the product
owner before they're final. Items for the product owner are marked
**(PO decision)**; all others are for the customer.

- [ ] "First finisher" — does this mean the participant who is literally
      first (by real clock time) to complete the round, or the
      participant who first reaches the top of the adjusted-time
      leaderboard (which factors in wrong-guess penalties)? These can
      differ if someone finishes slightly later but with fewer wrong
      guesses.
- [ ] Is there ever a hard cutoff after which a round becomes completely
      unavailable to new participants, or can anyone start any round at
      any point in the future and get their own personal window?
- [ ] Can a round have more than one genre tag, or exactly one (or zero)?
      Note: the docs currently disagree — US-202 says "an optional genre
      tag" (zero or one), while the glossary's Round entry says "one or
      more genre tags". Align both once decided.
- [ ] How does the all-time leaderboard combine results across rounds?
      Summing adjusted completion times would rank participants who have
      completed more rounds lower, since every extra round adds time.
      Options include average time per completed round, points per
      placement in each round, or ranking first by rounds completed and
      then by total time.
- [ ] How do participants whose window ended before they finished appear
      on leaderboards? Excluded entirely, or listed below all finishers
      (e.g. by tiles solved, then time)? And does a round closed by reveal
      or lock count as "completed" for the US-108 completion message or
      the all-time leaderboard?
- [ ] Should the app support Danish as well as English, given the host and
      likely participants are Danish-speaking?
- [ ] Are there limits the host should not be able to exceed when
      configuring a round (max tile count, min/max wrong-guess penalty,
      min/max duration)?
- [ ] Can a participant change their nickname after signup, and must
      nicknames be unique?
- [ ] US-106 shows only aggregate stats after a correct guess, but the
      brief says Mogens liked seeing what others guessed. Should
      participants also see other participants' guesses? Confirm with
      Mogens.
- [ ] The competitive layer (leaderboards, wrong-guess penalties,
      launch/personal windows, first finisher, profile) comes from the
      product-owner interview, not the brief. Confirm with Mogens before
      building it.
- [ ] US-202/203/204: must the number of added tiles match the configured
      tile count before a round can be published? Define "fully
      configured" for US-204.
- [ ] US-205: when an accepted variant is added after participants have
      played, do earlier wrong guesses that now match keep their
      penalties?
- [ ] US-104: should tiles be numbered, as the brief describes ("a row of
      numbered tiles")?
- [ ] Should clip length be enforced at upload (reject clips outside a
      range, and with what tolerance), or stay as guidance only? The
      brief says "approx. 30-60 seconds".
- [ ] Password reset is not covered by any story. Should it be added, and
      how? **(PO decision)**
