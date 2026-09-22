# Roadmap

## Where this is headed

Beyond the landing page, this repository is meant to eventually become a central hub sitting across a wider set of personal projects — a place to spot efficiencies between them and apply consistent security practices, instead of each project inventing its own conventions from scratch.

This is intentionally vague right now. Phase 1 doesn't depend on any of it, and none of it should leak into that work until it's actually being built. Treat this file as a parking lot for ideas, not a spec.

## Phase 1 — Landing page (current)

Static page at the root domain linking to the three existing subdomain apps. Scope and details live in `CLAUDE.md`.

## Phase 2 — Knowledge hub (future, not started)

Rough ideas to develop once Phase 1 ships, roughly in the order they'd probably get tackled:

- An inventory of related projects in one place — repo, host, stack, current status
- A shared conventions doc: naming, deploy process, env var / secrets handling
- A lightweight security checklist applied consistently across projects — dependency updates, exposed API surface, auth patterns, what's public vs. private
- Whatever else surfaces once there's more than one project to actually compare against each other

## Projects to eventually fold in

*(Left blank on purpose — add these yourself as each project comes into scope, rather than having this pre-populated. Worth deciding, project by project, which ones are fine to reference in what may end up being a public repo, and which — client work, anything with credentials or personal data — should stay out of it entirely, or get referenced only by name with the details kept elsewhere.)*

## Non-goals for now

- Don't scaffold Phase 2 infrastructure while Phase 1 is still unbuilt.
- Don't add dependencies or tooling the landing page itself doesn't need, just because the eventual hub might use them.
- Don't assume every project belongs in the hub — some may be better left standalone.
