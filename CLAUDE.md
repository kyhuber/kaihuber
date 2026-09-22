# CLAUDE.md

Context for Claude Code in this repository. This file is loaded automatically every session — keep it lean and current. Longer-term thinking belongs in `ROADMAP.md`, not here.

## What this repo is

The source for a static landing page hosted at the root of `kaihuber.dev`. The page's only job right now is to link out to three other apps that already live on subdomains of the same domain.

This repo is also the seed of a longer-term project — see `ROADMAP.md`. Don't build toward that vision yet. It isn't in scope until Phase 2.

## Current phase: Phase 1 — Landing page

**In scope:**
- A single static page (HTML + CSS, no framework, no build step) introducing the domain
- Links out to each of the three subdomain apps below
- Basic responsive layout — this will be viewed on phones

**Out of scope for now:** databases, auth, APIs, build tooling, anything listed under Phase 2 in `ROADMAP.md`. If a task seems to need any of those, stop and flag it rather than adding it.

## The apps this page links to

| App | Host | Subdomain | One-line description |
|---|---|---|---|
| `Cash Out` | `Vercel` | `cashout.kaihuber.dev` | `Used to track information about work shifts, including hours worked and tips, to forecast paycheck amounts` |
| `7929` | `Vercel` | `https://7929.kaihuber.dev/` | `Web app built on a database used to track tasks that need to be done around my house` |
| `Date Kyle` | `GitHub Pages` | `https://date.kaihuber.dev/` | `Fun site that showcases pictures of me and details about me in the interest of attracting a partner.` |

DNS for all three subdomains is already live and working. This repo doesn't touch that setup — it only needs to be deployed and pointed at the root/apex domain, which uses an A record (or the host's ALIAS/ANAME equivalent) rather than a CNAME, since apex domains can't use CNAME.

## Hosting for this repo

GitHub Pages, serving the apex domain via a `CNAME` file at the repo root. Requires an A record (not ALIAS/ANAME) at the registrar pointing the apex to GitHub Pages' IPs, plus Pages enabled in the repo settings (Settings → Pages → source: deploy from the `main` branch, root).

## Conventions

- Plain HTML/CSS. Don't introduce a framework unless a concrete need shows up — this is a link page, not an app.
- Match the git + VS Code workflow already used for the other three apps.
- No secrets, API keys, or env vars belong in this repo at this phase — it's static and will likely be public.

## Longer-term vision

See `ROADMAP.md`. Don't let it influence Phase 1 work.