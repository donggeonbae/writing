# AGENTS.md

## Purpose

This repository is for LaTeX-based academic paper writing. Use it to develop manuscript outlines, drafts, revisions, citation-backed arguments, venue-specific templates, strict review loops, and submission-ready materials.

Related repositories:

- `Ramblue/research`: shared research materials, source maps, reading queues, datasets, and reusable notes.
- `Ramblue/review`: structured paper reviews, evidence extraction, critique, and strict manuscript review.
- `Ramblue/figure`: paper figures, diagrams, visual explanations, Figma assets, and image-generation workflows.
- `Ramblue/writing`: LaTeX manuscript drafting, venue templates, citation integration, strict review loops, and submission preparation.
- `Ramblue/presentation`: meeting decks, literature review decks, conference talks, posters, and speaker scripts.

## Repository Role

Use this repository for:

- LaTeX manuscript projects
- venue and journal template setup
- section outlines and drafts
- abstract, introduction, related work, method, result, discussion, and limitation writing
- citation planning and BibTeX/BibLaTeX maintenance
- strict internal paper review loops
- response-to-reviewer drafts
- submission checklists
- final figure placement, captions, and cross-references

Do not use this repository as the main place for raw source collection, detailed paper critique, figure asset generation, or presentation production. Put those in `Ramblue/research`, `Ramblue/review`, `Ramblue/figure`, and `Ramblue/presentation`.

## Project Orientation

Before writing or revising:

1. Identify the target manuscript, venue or journal, audience, and current draft state.
2. Search for the official venue or journal template when the target venue is known.
3. Check `Ramblue/research` for source notes and `Ramblue/review` for reviewed evidence.
4. Check `Ramblue/figure` for figure specs, assets, captions, and export status.
5. Confirm whether the task is ideation, outlining, drafting, editing, citation integration, strict review, or submission preparation.
6. Keep claims traceable to evidence.

## Recommended Structure

- `manuscripts/`: LaTeX manuscript projects, grouped by project slug.
- `templates/`: Venue or journal templates, plus local manuscript templates.
- `bibliography/`: Shared `.bib` files, citation notes, and citation audits.
- `outlines/`: Standalone outlines and argument maps.
- `sections/`: Reusable or independently drafted sections.
- `figures/`: Final exported figure files copied or linked from `Ramblue/figure`.
- `tables/`: Table plans and source-backed tabular evidence.
- `reviews/`: Strict internal review reports for manuscripts.
- `responses/`: Response letters and reviewer rebuttal drafts.
- `docs/`: Cross-repository workflow and repository documentation.
- `scripts/`: Build, lint, export, and citation-check scripts.

Update this structure if the repository develops a more specific convention.

## Venue Template Rules

When a manuscript targets a specific conference or journal:

- Use web search to find the official current template, author kit, formatting instructions, and submission checklist.
- Prefer official venue, society, publisher, or journal pages over mirrors.
- Record the exact template source URL and access date.
- Do not silently adapt an old template for a new submission year.
- Keep template files separate from manuscript content where practical.
- Preserve required style files, class files, bibliography style files, and build instructions.

## LaTeX Rules

- Prefer LaTeX as the default manuscript format.
- Keep source files modular when the manuscript becomes large.
- Use stable labels for sections, figures, tables, equations, and algorithms.
- Keep bibliography entries consistent and deduplicated.
- Do not manually fake citation output.
- Avoid hardcoded layout hacks unless required by the venue template.
- Build the PDF after meaningful LaTeX changes when tooling is available.

## Evidence and Citation Rules

- Every substantive factual, methodological, or comparative claim should be supported by a source note, review, citation, internal result, or figure spec.
- Prefer reviewed evidence from `Ramblue/review` before using raw notes from `Ramblue/research`.
- Mark placeholders clearly with `TODO`, `CITATION NEEDED`, `VERIFY`, or `SOURCE NEEDED`.
- Do not fabricate citations, page numbers, venues, results, author claims, or reviewer comments.
- Separate manuscript text from planning notes.

## Figure Integration Rules

- Generate and iterate figure assets in `Ramblue/figure`.
- Store final manuscript-ready exports under this repository only when needed for LaTeX build stability.
- Every figure should have a source spec, intended claim, caption draft, and export format.
- Check that figure labels, captions, and manuscript references match.
- Do not use generated images for factual scientific evidence unless clearly labeled and appropriate.

## Strict Review Loop

Use `Ramblue/review` as the strict paper-review agent for manuscript drafts.

For internal reviews, ask for:

- novelty assessment
- claim-evidence alignment
- methodological weakness
- related-work gaps
- citation gaps
- overclaiming and unsupported language
- figure and table clarity
- venue fit
- likely reviewer objections

Do not smooth over serious weaknesses. Preserve hard critique and convert it into revision tasks.

## Cross-Repository Interaction

Use stable IDs to connect manuscript claims with reviews, source notes, and figure specs.

Recommended ID format:

```text
project-slug/topic-slug/YYYY/source-or-figure-slug
```

Prefer relative links when repositories are checked out under the same parent directory:

```md
Source note: ../research/sources/topic-slug/source-slug.md
Supporting review: ../review/reviews/topic-slug/source-slug.md
Figure spec: ../figure/figures/project-slug/figure-id/spec.md
Presentation: ../presentation/conference-talk/project-slug/talk.md
```

When drafting a claim from a review, preserve the review's uncertainty level. Do not upgrade tentative evidence into a strong manuscript claim.

## Writing Style

- Use precise academic prose.
- Prefer clarity over ornamental language.
- Keep topic sentences useful.
- Make transitions show logical movement, not just sequence.
- Use active voice when it improves clarity.
- Avoid overstating generality, causality, or novelty.
- Keep terminology consistent across the manuscript.

## Quality Checklist

Before finishing writing work, verify:

- the manuscript goal, audience, and venue are clear
- the official template status is recorded when relevant
- key claims have evidence links or citation placeholders
- citations are real and traceable
- figure specs and exported files are linked when relevant
- terminology is consistent
- limitations are acknowledged where appropriate
- unresolved issues are marked explicitly

## Agent Behavior

When acting as an AI writing agent:

- Improve argument structure before polishing sentences.
- Preserve the author's intended contribution.
- Search for official venue templates when needed.
- Use strict review feedback rather than softening it.
- Do not invent evidence, citations, templates, or submission rules.
- Report what changed, what evidence supports it, and what still needs verification.
