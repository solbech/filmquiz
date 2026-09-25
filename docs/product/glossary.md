# Glossary

| Term | Definition |
|------|------------|
| Round | The core unit of quiz content: a named, host-created set of tiles. Has a configured duration, wrong-guess penalty, tile/difficulty structure, and close behavior. May optionally carry one or more genre tags. |
| Genre | An optional theme tag on a round (e.g. "Horror", "Action") used as an alternate way to browse rounds, alongside the plain chronological round listing. Not a separate content type from a round. |
| Tile | One movie to guess within a round: an audio clip, a cover image, a correct title/composer/year, and a list of accepted answer variants. |
| Difficulty tier | A label (e.g. Easy, Medium, Hard) grouping tiles within a round by intended difficulty. Purely descriptive — participants may pick tiles in any order regardless of tier. |
| Accepted answer variant | An alternative spelling/title an admin has explicitly marked as correct for a tile (e.g. "Die Hard" for "Die Hard With a Vengeance"), in addition to the official title. |
| Answer matching strictness | A per-round setting: "exact" (guess must match the title or a listed variant exactly, case-insensitive) or "forgiving" (also ignores things like punctuation, extra spaces, and leading articles). |
| Participant | A signed-up user who plays rounds and appears on leaderboards under their nickname. |
| Admin | A user who can create and edit round/tile content. See Owner and Editor. |
| Owner | An admin role that can also grant/revoke admin access for other accounts. |
| Editor | An admin role that can create/edit round and tile content but cannot manage other admins' access. |
| Host | The person(s) running the quiz for their audience — in this app, synonymous with an admin (Owner or Editor). |
| Launch window | The period starting the instant a round is published, of the round's configured duration. Participants who start the round during this window share the same start instant for ranking and "first finisher" purposes. |
| Personal window | For a participant who first opens a round after its launch window has elapsed, an individual countdown of the same configured duration, starting when they open it. |
| Wrong-guess penalty | A time penalty (default +30 seconds, host-configurable per round) added to a participant's adjusted completion time for each wrong guess they make anywhere in the round. |
| Adjusted completion time | A participant's real elapsed time from their applicable window's start to finishing the round's last tile, plus their total wrong-guess penalties. Used to rank leaderboards. |
| Leaderboard (round) | Ranking of participants who have completed a specific round, by adjusted completion time. |
| Leaderboard (all-time) | A single combined ranking aggregating participants' adjusted completion times across all rounds they've completed. |
| First finisher | Special, permanent recognition given to the participant who completes a round first (see open question on exact definition). Shown on their profile and that round's leaderboard even if later completion times beat theirs. |
| Reveal (on close) | A round close-behavior setting: when a participant's window ends, their unfinished tiles' answers are shown automatically. |
| Lock (on close) | A round close-behavior setting: when a participant's window ends, their unfinished tiles become unplayable without revealing the answer. |
| Profile | A participant's personal page showing their nickname, all-time leaderboard position, and earned "first finisher" badges. |
