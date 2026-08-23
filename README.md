# San Marcos Academy Six-Man Football — game-night site

A single self-contained HTML page for spectators: the rules of six-man football,
the roster, the next game, and what just happened on the field. No external
requests, so it still loads on weak cell service in the stands. Light mode by
default because it reads better in direct sunlight; dark mode follows the phone's
own setting.

**Status: work in progress.** Everything marked `### PLACEHOLDER ###` needs real,
school-approved information before this goes live.

## Editing

Open `index.html` and edit only the DATA BLOCK near the top of the `<script>` tag
at the bottom of the file. Colors all live in CSS variables at the top of the
`<style>` block — nothing below hard-codes a hex.

## Viewing locally

Open `index.html` in a browser, or `python3 -m http.server` from this folder.
