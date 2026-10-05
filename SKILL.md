---
name: ppt-storyline
description: Build any PowerPoint / slide deck / presentation (ppt, pptx, deck, slides, presentatie). This is the default skill whenever the user wants to make, draft or ask for a deck from a topic, decision, or raw notes. Produces a consultancy-style storyline (SCR / governing thought + action titles) rendered in the locked AH RACI-look, and always applies the user's own communication guidelines.
---

# PPT storyline (consultancy)

Write the story first, render it second. This skill drafts an SCR narrative with action
titles, gets sign-off on the outline, then renders it via the shared AH deck engine.

Working dir for every command: `C:\Projects\_shared\ah-deck-engine` (bash: `/c/Projects/_shared/ah-deck-engine`).
The house style (colours, Inter, blue top bar, tables) is locked in the engine. Do not restyle in the spec.

## How it works

0. **Load the guidelines first.** Before drafting anything, read two guides, each
   with the same resolution order (first that exists wins, `.local` overrides template):
   - **Communication** (prose/voice): `communication-guidelines.local.md`, then
     `communication-guidelines.md`. Governs every action title, body, exec summary
     and callout you write. If it names an external source of truth (a playbook
     file), read that too.
   - **Slide design** (visual/structure): `slide-design-principles.local.md`, then
     `slide-design-principles.md`. Governs archetype choice, layout, what to cut,
     hierarchy, charts and whitespace.
   The `.local` files are the user's personal guides and are git-ignored; the
   templates ship as fallbacks. Apply both guides throughout the outline and the spec.
1. **Get the brief.** Ask only for what is missing: topic, audience (senior mgmt vs team),
   the one decision or message, any raw input to draw from, rough slide count. If the user
   already gave enough, skip the questions and proceed.
2. **Draft the storyline as an action-title outline first.** Structure it SCR:
   governing thought, then Situation, Complication, Resolution. Write one action title per
   slide and pick an archetype for each. Do not write full slide bodies yet.
3. **Horizontal-logic self-check.** Read only the titles, top to bottom. If they do not tell
   the whole story on their own, rewrite them before showing the user.
4. **Get sign-off (two-phase, safe default).** Show the numbered outline: `title — archetype`
   per slide. Only after the user confirms do you write the deck-spec and render. This
   mirrors a dry-run-first discipline: never render before the outline is approved.
5. **Write the deck-spec and render.** Fill in the bodies, write
   `<topic>-deck.json`, then run `node cli.js <topic>-deck.json <out.pptx>`. Save the deck
   next to the source material or in the relevant project, not in the engine folder.
6. **Report back.** Give the `.pptx` path and the final title outline.

## SCR method

- **Governing thought:** the single sentence the audience must remember. Everything supports it.
- **Situation → Complication → Resolution:** shared context, then the tension that forces a
  decision, then your answer. Open with an `executiveSummary` slide carrying the governing thought.
- **Action titles:** every content-slide title is an assertion (the so-what), not a label.
  "Promo planning is fragmented across five tools" beats "Current state". Quantify where you
  can, one idea per title.
- **The ask:** close on a `callout` (variant `decision`) that states what you want approved.

## Deck-spec and archetypes

Full field reference: `schema.md` in the engine folder. Twelve archetypes:

- `cover`, `sectionDivider` — full-bleed blue open and section breaks.
- `executiveSummary` — governing thought + 3 supporting points.
- `agenda` — numbered list.
- `bullets` — header + bullets, optional callout.
- `cards` — 2 to 4 header-bar cards (evidence, options).
- `callout` — one BLUF banner; variant `info` / `decision` / `question` / `proof`.
- `twoColumn` — two panels (before/after, us/them).
- `table` — manual table, `light` (default) or `dark` zebra.
- `processFlow` — horizontal steps + arrows.
- `kpiTiles` — big-number tiles.
- `imageCaption` — screenshot or wireframe with caption.

## Rules

- House style lives in the engine, never hardcode colours or fonts in the spec.
- Real content, no lorem ipsum. Conclusion first, action titles are assertions.
- All prose follows the loaded communication guidelines (step 0). Language and
  spelling are whatever that guide specifies.
- Two-phase approval is mandatory: outline sign-off before rendering.
- Bespoke diagrams (heatmap, RACI matrix, org diagram) are v2, not in this skill yet.
