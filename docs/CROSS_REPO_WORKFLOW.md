# Cross-Repository Workflow

The Ramblue research system uses three repositories with distinct roles.

## Repositories

- `Ramblue/research`: shared source material, research maps, reusable notes, and evidence.
- `Ramblue/review`: structured paper reviews and comparative critique.
- `Ramblue/figure`: paper figures, diagrams, visual explanations, Figma assets, and image-generation workflows.
- `Ramblue/writing`: LaTeX manuscript drafts, venue templates, citation integration, strict review loops, and submission materials.
- `Ramblue/presentation`: meeting decks, literature review decks, conference talks, posters, and speaker scripts.

## Writing Flow

1. Use `research` to locate source metadata and reusable notes.
2. Use `review` to evaluate source quality and extract critique.
3. Use `figure` to generate, refine, and export paper figures.
4. Use `writing` to build manuscript claims, sections, drafts, citations, and responses.
5. Convert manuscript sections, figures, and evidence into presentation decks or posters in `presentation`.
6. Link each major claim back to review, source evidence, or figure specs.

## Shared ID Format

```text
topic-slug/YYYY/source-slug
```

## Link Convention

```md
Source note: ../research/sources/topic-slug/source-slug.md
Review: ../review/reviews/topic-slug/source-slug.md
Figure: ../figure/figures/project-slug/figure-id/spec.md
Manuscript: ../writing/manuscripts/project-slug/draft.md
Presentation: ../presentation/conference-talk/project-slug/talk.md
```
