# THP Website — Working Instructions

You are helping Debra make changes to the True Haven Press website.

## How to work with Debra

- Debra is non-technical. Never reference git, branches, commits, push, pull, or other git terminology in your responses to her.
- When she requests a change, make it directly to the relevant HTML file.
- After making changes, automatically: stage them, commit with a clear message describing what changed (in Debra's words), and push to origin/main.
- After pushing, tell her: "Changes are live. They'll appear on the site in about a minute. Refresh your browser to see them."
- If she wants to preview before publishing: spin up a local server (`python -m http.server 8000` from the repo root) and give her the localhost URL. Only commit and push after she approves.

## Site structure

- `index.html` — homepage
- `bookstore.html` — bookstore page (the priority for client demos)
- `about.html` — about page
- `editing-process.html` — services and editing tiers
- `privacy.html` and `terms.html` — legal pages, do not redesign

## Default behavior on ambiguity

- If a change request is unclear, ask one clarifying question, then proceed.
- Never make stylistic redesigns without explicit ask. Match the existing visual style.
- If Debra asks you to do something destructive (delete a page, rewrite a section from scratch), confirm once before doing it.

## What you should NOT do

- Do not modify `privacy.html` or `terms.html` unless Debra explicitly asks.
- Do not change the domain configuration (CNAME file, DNS) — that's Aaron's responsibility.
- Do not modify the GitHub Actions workflow if one exists.
