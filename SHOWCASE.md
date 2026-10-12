# Showcase brief

> **Status:** planning only — nothing described here is built or approved.
> **Written:** 2026-10-11, from a session that reviewed the live site, the six app repos, and a peer's portfolio site.
> **For:** a future Claude Code session in this repo. Read `CLAUDE.md` and `ROADMAP.md` first; this brief does not override them.

## 1. Goal

Kyle wants kaihuber.dev to do more than list links: to **showcase the work Kyle and AI (KAI) are doing**, in a way that is interesting and inspiring to other people who build things with AI. It is not a job funnel and not a traffic play (`CLAUDE.md`: a page the owner is proud of and can show off).

**Working assumption about the audience** (confirm in §9): people who build, or are curious about building, real software with AI assistants — hobbyists, indie builders, engineers and product people wondering what is realistic. Success is a visitor thinking "I could do that" or "I'd steal that practice", and Kyle being glad to send the link to a friend.

## 2. How to work from this document

- Nothing here is approved scope. Ask the §9 questions first, then propose **one slice at a time** (§6), each as its own small PR. Kyle merges PRs personally, and `main` deploys immediately.
- Facts below were gathered on 2026-10-11 from public repos and live sites. Re-verify anything before it goes on the page; repos move.
- Stay inside the guardrails in §7. If a slice needs a backend, a build step, or a second page, stop and flag it rather than adding it.

## 3. Where the site is now

- One static page: `index.html` (~7 KB), `style.css` (~3 KB), `favicon.svg`, `images/kyle.jpg`. No JS, no framework, no build step.
- Layout: a 640 px column — hero (photo, name, tagline), then one tile per app. Tagline: "Kyle and AI (aka KAI) build small things that solve small problems and put them on the internet."
- Style tokens in `style.css`: light `#fff` / dark `#0f0f0f` via `prefers-color-scheme`, accent `#2563eb` / `#60a5fa`, system font stack. A tile is `<li><a class="app">` with a 24×24 stroke-style inline SVG icon — copy an existing `<li>`.
- Six tiles: Cash Out, 7929, Date Kyle, Mountaintop, Run with Kai, Bee Solver (table in `CLAUDE.md`).
- Hosting: GitHub Pages from `main` root, apex via A records, `CNAME` file. `_config.yml` excludes internal docs from the published site; this file is listed there. Any further internal doc must be added too.
- **The gap:** tiles say *what* each app is. Nothing says *why it exists, how it was made, what went wrong, or what it proves.* That is where the interesting material is (§5).

## 4. What a peer's site is worth borrowing

Source: coreyscherrer.com, reviewed 2026-10-11 (page text, a phone-width screenshot, DOM inspection, and one architecture page; desktop visual polish was not seen directly). It is a job-search portfolio — résumé, career timeline, contact form — so its goal differs from this site's. The transferable ideas:

1. **Show the machine, not just the output.** Two interactive panels sit above the fold: a knowledge-graph explorer (thousands of nodes, with counts shown) and a live service-health "rack" with up/down status. Visible proof of work reads as more credible than a claim.
2. **A repeatable story shape per project:** problem → what was done → outcome. Each portfolio item has its own deep-dive page, and the architecture pages share a template: one-paragraph pitch, a request-flow diagram with every hop named, numbered "moving parts" with tech tags, a section on safety gates (a human approve/deny step before any side-effecting action), a short "why this is more than a chatbot" list, and a link to the next node.
3. **A one-line point of view** on the human/AI split — in effect, the agents build and the person operates.
4. **Honest signals:** a down service is shown as down, and one skill is self-rated novice.
5. **Cost treated as a first-class fact:** every LLM call is logged with its dollar cost, framed as "no surprises on the invoice".
6. **Small personal projects mixed in** with the heavy systems (a trip planner, a neighbourhood map), which keeps it human.
7. **"Click to explore" interactions** instead of walls of text.

What it is built on, so it is not mistaken for a template to copy: a self-hosted dynamic platform (Flask/gunicorn, Postgres, Redis, nginx), a Bootstrap-style template plus D3, AOS and typed.js, a very long page (~13,500 px), dark theme with cyan accents. kaihuber.dev is deliberately the opposite — static, ~10 KB, no JS. That contrast is itself a position worth stating on the page (§6, D).

**Do not borrow:** skill meters, stat counters, a career timeline, a contact form, résumé framing, a chat widget (needs a backend and an API key), the visual identity or wording, or anything that publishes internal hostnames, ports or service names.

## 5. Kyle's raw material

What is actually interesting, per app. All six repos are public under `github.com/kyhuber/`.

| App (repo) | Built how | The story worth telling | Evidence to link |
|---|---|---|---|
| Cash Out (`Cash-Out`) | Next.js/TypeScript PWA; Supabase (Postgres + row-level security); Vercel; a small API layer holds the Anthropic key; voice via OS dictation | Built after a coworker found an employer had not paid out tips — caught only by checking a pay stub. Log a shift by talking or typing a sentence and an LLM parses it into structured data. Engineering lesson: OS keyboard dictation, because the browser Web Speech API is unreliable on iOS Safari. | `README.md` ("Why this exists"), `Cash_Out_PRD.md` |
| 7929 (`7929`) | Next.js 15, Tailwind 4, shadcn/ui, Supabase; includes an MCP server per its README | Home maintenance by *interval*, not calendar date — nothing is ever "missed", only overdue by N days. Single user. A house exposed to an AI through MCP (verify `mcp/` before claiming it). | `7929-prd.md`, `mcp/` |
| Date Kyle (`date-kyle`) | Plain HTML/JS, no build, GitHub Pages workflow | A dating profile in the form of a startup pitch deck, in four languages, built to be edited and published from an iPhone. | `README.md` |
| Mountaintop (`mountaintop`) | Dependency-free ES modules, no build step, `node:test` | The Huber brothers' card game. With no human playtesters available, scoring was chosen from a deterministic 160,000-game simulation; a hidden-card "blind bid" round has regression tests; `KAI.md` keeps a dated log of validated assumptions and lessons learned (including a merge that looked clean and was not). | `KAI.md`, `analysis/scoring-report.md`, `test/` |
| Run with Kai (`run-with-kai`) | Static site; HealthKit exports feed `data.js`; a Claude skill does the analysis | An AI training analyst **with hard rules**: no estimated values, history is never regenerated, and pain that changes stride means stop and report. The generic skill is committed; the personal one with health history stays private. Public but `noindex`, shared with running friends. | `CLAUDE.md`, `skills/run-training-analysis/SKILL.md` |
| Bee Solver (`bee-solver-claude`, plus `bee-solver`, `-llama`, `-gemini`) | Static JS plus word lists | Four repos exist. `bee-solver`, `-llama` and `-gemini` are same-evening attempts on 2024-08-18/19 (commit messages: "llama is confused", "Still not working…"). `-claude` was reworked later (cleaned dictionaries, a popular-words list, hexagon UI via a `claude/`-branch PR merged 2026-02-20). | commit histories |

**Cross-cutting patterns — this is the inspiring part, and it is transferable:**

- Every repo carries its AI working agreement in-repo: `CLAUDE.md`, `AGENTS.md`, `KAI.md`, a PRD, and a `TODO` addressed to the human.
- Guardrails are written as hard rules, not preferences (the Run with Kai safety rule; "no estimation"; "stay unlisted"; no secrets in this repo).
- Decisions are validated, not asserted: simulations, a regression test per bug, lessons-learned logs.
- Constraint as a design principle: no build step, zero runtime dependencies, editable from a phone.
- The AI maintains the human's to-do list (`Kyle_To_Do.md`, `TODO.md`).
- Small problems, real people: a coworker's missing tips, a brothers' card game, a house, running friends.

## 6. Candidate directions

Legend: ✅ fits Phase 1 as written · ⚠ needs Kyle to widen scope in `CLAUDE.md` first · ⛔ Phase 2+ or a separate app.

| ID | Idea | Scope |
|---|---|---|
| **A** | **Tile stories.** Under each one-liner, add *why I built it* plus small tags (host · stack · source), and an optional `<details>` "How it's built" of 3–4 lines (problem → what I did → what I learned). Stays one page, no JS. | ✅ |
| **B** | **"How KAI works."** A short section distilling the practices in §5 into 5–6 principles, each linking to the real file as a receipt. Probably the most transferable thing for the audience. | ✅ |
| **C** | **"Bee Solver, four ways."** Same task, several AIs, side by side. Needs a fair test first (below). | ✅ as a section · ⚠ as its own page |
| **D** | **Receipts strip.** Measured facts: page weight, "no build, no JS", last-shipped date per app (entered by hand), repo count. This is where the static-vs-heavy contrast from §4 is stated. Auto-fetching "last commit" from the GitHub API in the visitor's browser is possible but is a runtime API call, rate-limited to 60/hour/IP unauthenticated. | ✅ static · ⚠ live |
| **E** | **Per-app deep dives** using the §4 template. Only after A shows which stories deserve depth. | ⚠ (new pages) |
| **F** | **Live status for the six apps.** Client-side `fetch(url, { mode: 'no-cors' })` is reachability only. Public URLs only. Low value for six apps. | ⚠ |
| **G** | **Public project inventory.** Overlaps Phase 2's "inventory" in `ROADMAP.md`. Keep any public view a curated subset, separate from the internal hub. | ⛔ |
| **H** | **Ask-KAI chat.** Needs a backend, an API key, rate limits, a cost cap and prompt-injection handling. If ever built, a separate subdomain app like the others — never in this repo. | ⛔ |

**Fair-test notes for C**

- It is not apples-to-apples: the llama and gemini repos are one-evening 2024 attempts, while `-claude` has had rounds of iteration since. Say so on the page.
- Do not attribute the original `bee-solver` to a model until Kyle confirms — its README says nothing.
- Method sketch: fixed rules (confirm: NYT Spelling Bee — centre letter required, 4+ letters, pangrams), a fixed set of past puzzles with known answer lists, and for each version record whether it runs at all, precision/recall against the answers, time, code size, and commits-to-working. Run it headless; publish the numbers next to the commit logs.
- The three 2024 repos already serve from GitHub Pages (`kyhuber.github.io/<repo>/`), so link rather than copy.

**Recommended order:** A → B → C → D, one PR each. They are the cheapest, in scope, and highest signal. Revisit E once A has shown what is worth deepening. Leave F–H parked.

## 7. Guardrails

Hold in every slice.

- **Repo rules (`CLAUDE.md`):** plain HTML/CSS, no framework, no build step, no secrets or env vars, static only. New internal docs go in `_config.yml`'s exclude list. Contact stays "GitHub link only" unless Kyle changes that.
- **Phase 2 stays parked.** Do not let the knowledge-hub vision shape this work.
- **Privacy — this repo and site are public:**
  - 7929's README states a full street address in a public repo. Do not repeat it on the site, and ask Kyle before adding source links for 7929 or calling out the house.
  - Run with Kai shows personal health metrics and is `noindex` in its own repo. Keep it that way, and do not surface heart-rate or HRV data on the landing page.
  - Date Kyle is a personal dating profile. Ask before expanding on it beyond its tile.
  - Do not name people from the repos (family, running friends) without asking.
  - Never publish internal hostnames, ports, or service names in any status or architecture view.
- **Honesty:** describe what the apps do today; label experiments and failures plainly; do not claim "built by AI" beyond what each repo shows; numbers must be measured, with dates; confirm model attribution.
- **Do not imitate coreyscherrer.com's look or wording.** Borrow structure only; credit the inspiration only if Kyle wants.
- **Quality:** works with JS off; check at 360 px and 390 px; keyboard accessible; light and dark; respects `prefers-reduced-motion`.

## 8. Voice

Existing tone is plain and low-key: "small things that solve small problems". The Bee Solver page is playful ("Kyle & Claude Solve the Bee!"). Keep the site understated, with personality coming from the specifics (a coworker's tips, 160,000 simulated games, an iPhone-editable dating deck) rather than from adjectives. Confirm in §9.

## 9. Open questions for Kyle (ask first)

1. Who exactly is the audience, and what should they do or feel afterwards — try building something, follow along, get in touch?
2. How much of the AI process should be visible: working-agreement files only, or prompts, transcripts and failures too?
3. Which apps are showcase-worthy and which are just listed? (Date Kyle and Run with Kai are personal.)
4. Is "one static page" a hard rule, or may the site grow pages like `/built/<app>/`? Is a client-side fetch to the GitHub API or the subdomains acceptable?
5. Bee Solver: which model produced the original `bee-solver`, and where should a comparison live — a section here, or its own repo or subdomain?
6. Should tiles link to source repos? (See the 7929 note in §7.)
7. Tone: understated, or playful like the Bee Solver page?

## 10. Provenance and known unknowns

- Gathered 2026-10-11 from: this repo; the READMEs, `CLAUDE.md`/`KAI.md`, file listings and commit logs of the six public repos via the GitHub API; the live bee-solver page; coreyscherrer.com.
- Not verified: how the peer site looks on desktop (only phone width plus DOM inspection); what is inside 7929's `mcp/`; whether the llama and gemini solvers still work; who built the original `bee-solver`; Cash Out's current live state.
