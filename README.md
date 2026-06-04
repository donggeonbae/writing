# writing

LaTeX-based academic paper writing for the donggeonbae research system.

Use this repository to develop venue-specific LaTeX manuscripts, outlines, drafts, revisions, citations, strict review loops, response letters, and submission-ready materials.

## Related Repositories

- `donggeonbae/research`: shared source material and reusable research notes.
- `donggeonbae/review`: paper reviews and critique.
- `donggeonbae/figure`: paper figure generation and visual assets.
- `donggeonbae/writing`: LaTeX manuscript drafting and submission preparation.

## Suggested Workflow

1. Start with research notes from `donggeonbae/research`.
2. Prefer reviewed evidence from `donggeonbae/review`.
3. Create and export figures through `donggeonbae/figure`.
4. Draft claims, sections, and manuscripts in `donggeonbae/writing`.
5. Link claims back to reviews, source notes, and figure specs.
6. Mark unresolved citation, template, or evidence gaps explicitly.

## Suggested Folders

- `manuscripts/`
- `bibliography/`
- `outlines/`
- `sections/`
- `figures/`
- `tables/`
- `responses/`
- `reviews/`
- `docs/`
- `templates/`
- `scripts/`


## HTML Archive Framework

This repository includes the encrypted static HTML archive framework adapted from `Lukael/research`.

Typical report flow:

```powershell
$env:REPORT_PASSWORD="<local secret>"
node scripts/build-markdown-report.js --slug example-report --input path\to\report.md --title "Example Report"
```

The command creates `projects/<slug>/index.html` and, when `REPORT_PASSWORD` is set, `projects/<slug>/report.enc`. The transient plaintext HTML is written under `build/` and should not be committed.

