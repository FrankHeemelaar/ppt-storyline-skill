# ppt-storyline

A Claude Code skill that turns a brief into a consultancy-style PowerPoint with a
real storyline (SCR: governing thought + action titles), rendered by a shared deck
engine. It writes the story first, gets outline sign-off, then renders.

## Bring your own guidelines

The skill applies two guides to everything it builds:

- **Communication** (prose/voice): `communication-guidelines.md` (template) +
  `communication-guidelines.local.md` (your personal version).
- **Slide design** (visual/structure): `slide-design-principles.md` (template) +
  `slide-design-principles.local.md` (your personal version).

For each, the skill reads the `.local` file first and falls back to the template.
The `.local` files are git-ignored, so your personal versions are never published.
Keep the templates to general, widely-known principles so they are safe to share.

**Setup for your own voice:**

1. Copy whichever template you want to personalise:
   `cp communication-guidelines.md communication-guidelines.local.md`
   `cp slide-design-principles.md slide-design-principles.local.md`
2. Edit the `.local` file(s) with your own rules (or point them at an existing
   playbook). Keep anything taken from a copyrighted source in your own words in the
   `.local` file; the published templates stay general.
3. Done. The skill now follows your guides, and they stay out of git.

If you do not create a `.local` file, the skill just uses the template defaults.

## Dependencies

Rendering uses a separate AH deck engine (`cli.js <deck.json> <out.pptx>`). Point
the skill at your own renderer or spec format if you do not have that engine; the
storyline method (SCR + action titles) is engine-agnostic.
