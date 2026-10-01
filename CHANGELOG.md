# Changelog

A record of how this site was built. Grouped by phase rather than by commit,
because most of this work predates the repository being used properly — see the
note at the end.

---

## Phase 1 — First build (early August 2026)

- Single self-contained `index.html`. No external requests of any kind, so the
  page loads on weak cellular service in the stands.
- Five sections: game-night homepage, Six-Man in 60 Seconds, searchable roster,
  schedule, and a "What Just Happened?" guide with a football glossary.
- **Six-man rules verified against primary sources**, not written from memory.
  San Marcos Academy plays in TAPPS, which uses the Texas six-man variations
  (NCAA rules with UIL exceptions). Checked: 15 yards for a first down, the
  clean-exchange rule, 4-point field goals, the inverted PAT values (kick = 2,
  run/pass = 1), 10-minute quarters, and the 45-point mercy rule.
- Accessibility built in from the start rather than retrofitted: WCAG AA contrast
  throughout, 56px minimum tap targets, keyboard navigation, screen-reader
  labels, no information conveyed by colour alone.

## Phase 2 — Real content

- Full 2026–27 schedule entered from the official sheet. Every fixture verified
  to fall on a Friday.
- Roster populated from the coaching staff's list.
- The roster page was built to **reconfigure itself around whatever data
  exists**: the jersey-number search, the grade filter and the position filter
  each appear only once there is something to put in them. This meant the page
  was never broken while information was still arriving.

## Phase 3 — Dark mode and visual work

- Dark mode via `prefers-color-scheme`, so the site follows the phone's own
  setting — light at an afternoon game, dark at a Friday night kickoff.
- Palette chosen around **halation**: light text on dark backgrounds blooms for
  readers with astigmatism, worst at night with dilated pupils. Dark mode uses
  near-black and off-white rather than `#000`/`#fff`, which would have scored
  better on paper and read worse in practice.
- All colour moved into CSS variables; nothing below the `:root` block hard-codes
  a hex, so both themes change from one place.
- **Fixed a real accessibility defect:** card borders sat at 1.5:1 contrast and
  would have vanished in daylight. Solved for a border that keeps the purple tint
  while clearing the 3:1 non-text threshold in both themes.
- The official SMA Bears logo was extracted from the schedule sheet, had its
  white background flood-filled from the edges (preserving the white claws and
  teeth inside the artwork), and was inlined as a ~15 KB WebP so it costs no
  network request and sits correctly on both themes.

## Phase 4 — Publishing

- Deployed to Cloudflare Pages at `smabears.pages.dev`.
- **QR sign built from scratch.** No QR library was available and the package
  index was unreachable, so the encoder was written against ISO/IEC 18004 and
  verified by decoding its own output. It took three real bugs to get right; the
  last was a Reed–Solomon generator polynomial coming out in reverse order, which
  corrupted every symbol while still looking like a valid QR code.
- The sign is vector, so it stays sharp at any print size, and the finished PDF
  is verified by rendering it back to an image and scanning it.

## Phase 5 — Revisions from the coaching staff

- Removed the "next game" panel, the directions links, and the add-to-calendar
  buttons.
- Added a **Meet the Coaches** page with seven staff and bio slots.
- **Positions removed entirely** at the coaching staff's request — not hidden,
  but deleted along with the filter and the data fields. The roster note now
  explains the absence: nearly every Bear plays offense, defense and special
  teams in the same game.
- Roster rebuilt to 24 players with official game jersey numbers. Several
  surnames were corrected in the process (Southword → Southworth, Gilliad →
  Gilliland, Armstrong → Arrington).
- Nicknames display as `Lukin "Cash" Gilliland`, and the search matches either
  name.
- **Two students asked that their legal first names not appear.** These were
  removed from the data itself rather than hidden in the display, because a web
  page's source is public and a hidden name is still readable by exactly the
  people they were concerned about.
- Kickoff times set; past fixtures now show as PLAYED automatically once their
  date passes.

## Phase 6 — In-season

- Results recorded as win/loss without published scores, at the school's
  preference. Schedule page shows the season record, counting regular-season
  games only.
- Homecoming and Senior Night corrected — they had been the wrong way round.
- **Butter Braids fundraiser section** for the junior class, with the
  pay-it-forward explanation, a hand-delivery area warning placed above the order
  button rather than below it, and an automatic close on the deadline so a dead
  order link can never sit on the site.
- The fundraiser link originally supplied was the organiser's **admin dashboard**,
  which authenticated with no login via a token in the URL and exposed seller and
  order management. It was not published. The correct public storefront link was
  located and verified instead.

---

## A note on this repository's history

The commit history does **not** contain the intermediate versions of this site.
Only one snapshot was committed during the build, and the working versions
between then and now were overwritten rather than saved. Those file states no
longer exist and have not been reconstructed — inventing commits for them would
make this history a work of fiction rather than a record.

What is here instead: the August snapshot, the current state, and this changelog
describing what happened in between.

From this point on, each change should be committed as it is made, so the history
is real going forward.

### One thing to keep in mind

Git history is permanent. Anything committed stays recoverable even after it is
deleted from the current file. Two students have already asked for their legal
names to be removed from this site — if that happens again after a name has been
committed, deleting it from `index.html` will **not** remove it from the
repository's history. Worth a thought before each commit, given this file
contains the names and grade levels of minors.
