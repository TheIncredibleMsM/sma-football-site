# San Marcos Academy Six-Man Football — game-night site

**Live at [smabears.pages.dev](https://smabears.pages.dev)**

A single self-contained HTML page for spectators at San Marcos Academy six-man
football games. Scan the QR code at the stadium and you can learn the rules,
look up who wears number 13, check the schedule, or find out what just happened
on the field.

Built for someone standing in the stands on a phone with poor signal and a few
seconds to find an answer.

## What's in it

- **Six-Man in 60 Seconds** — the rules that make this game different from
  11-man, verified against the Texas six-man variations used in TAPPS play
- **Meet the Players** — all 24 Bears, searchable by jersey number or name
- **Meet the Coaches** — the seven staff behind the team
- **Schedule** — all twelve fixtures with the season record
- **What Just Happened?** — plain-language answers to what you just saw
- **Football Glossary** — no prior knowledge assumed
- **Butter Braids Fundraiser** — the junior class prom fundraiser (closes
  14 October 2026, then hides itself)

## Design constraints

- **One file, zero network requests.** Everything — styles, scripts, the team
  logo — is inlined, so the page works on weak cellular service at the stadium.
  About 37 KB gzipped.
- **Light mode by default**, because it degrades better in direct sunlight. Dark
  mode follows the phone's own setting.
- **Accessible from the start.** WCAG AA contrast in both themes, 56px tap
  targets, keyboard navigation, screen-reader labels, and no information carried
  by colour alone.
- **The page adapts to its data.** Filters and sections appear only when there is
  something to show, so the site is never half-broken while information is still
  arriving.

## Editing

Everything you need to change lives in the **DATA BLOCK** near the top of the
`<script>` tag at the bottom of `index.html`:

| What | Where |
|---|---|
| Team info, contact, season | `TEAM` |
| Fundraiser link, deadline, delivery area | `FUNDRAISER` |
| Players, numbers, grades, bios | `ROSTER` |
| Coaching staff and bios | `COACHES` |
| Fixtures, times, results | `SCHEDULE` |
| Glossary terms | `GLOSSARY` |

Colours all live in CSS variables at the top of the `<style>` block — nothing
below hard-codes a hex, so changing a brand colour updates both themes at once.

Add a score to a fixture and its card becomes a result. Fill in a coach's `bio`
and the paragraph appears. Set `FUNDRAISER.active` to `false` and the whole
fundraiser section disappears.

## Deploying

The site is hosted on Cloudflare Pages as a direct-upload project.

1. Zip `index.html` on its own, or use the folder
2. **Workers & Pages → smabears → Deployments → Create deployment**
3. Drag it in, then **Save and Deploy**

Live in under a minute at the same address, so the printed QR signs never need
reprinting. Cloudflare keeps every deployment, so a bad upload can be rolled
back instantly from the Deployments tab.

## Viewing locally

Open `index.html` in a browser, or run `python3 -m http.server` from this folder.

## Signage

`QR-sign.pdf` (kept outside this repo) is the printable stadium sign. It is drawn
as vectors, so it can be scaled to poster size without going soft. To regenerate
it against a different address, see `make_sign.py` and `qr.py`.

## History

See [CHANGELOG.md](CHANGELOG.md) for how this was built, including a note on why
the commit history starts where it does.
