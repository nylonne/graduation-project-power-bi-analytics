# Technical Architecture

> **Team-owned deliverable:** The architecture, report content, and supporting materials are maintained collectively by the Graduation Project group. Major changes should be reviewed and communicated to the team.

## System overview

The application is a Microsoft Power BI Desktop report stored as a single `.pbix` artifact. It combines the semantic model, Power Query transformations, DAX measures, report layout, static assets, and report configuration. Power BI Desktop is the authoring and local execution environment; Power BI Service is optional and is only needed for approved publishing, sharing, or scheduled refresh.

```text
Approved data sources
        │
        ▼
Power Query (connect, clean, shape)
        │
        ▼
Semantic model (tables, relationships, measures)
        │
        ▼
Report pages, slicers, and visuals
        │
        ▼
Power BI Desktop / approved Power BI Service workspace
```

## Report composition

The current report contains 35 pages:

- Landing Page
- Summary - Global Summary and Summary - Collection By Date Summary
- Four views each (overview, cash, bank, and bank-wise) for Skyline, Rihana, Degla Landmark, Lake Front 6, Degla Palms, Crysta Plaza, One Kattameya, and Zahra

The `.pbix` package also includes embedded static image resources and an HTML-content custom visual. Treat the report as a binary release artifact: make a backup before edits and avoid changing its internal package files manually.

## Repository responsibilities

| Location | Purpose | Version-control guidance |
| --- | --- | --- |
| `reports/` | Approved `.pbix` report releases | Track intentional versions; avoid simultaneous edits. |
| `data/raw/` | Original source files | Do not commit confidential, personal, or large source data. |
| `data/processed/` | Reproducible prepared data | Commit only non-sensitive, documented outputs. |
| `assets/images/` | Report and documentation images | Use descriptive names and record source/licensing. |
| `exports/` | Generated PDFs, images, and extracts | Treat as disposable outputs unless a release requires one. |
| `scripts/` | Repeatable import, preparation, or validation helpers | Document dependencies and inputs beside each script. |

## Key decisions

1. **Keep the PBIX intact.** The report remains a single Power BI artifact because moving the file does not alter its embedded data model, measures, or visual definitions.
2. **Separate inputs from outputs.** Raw data, prepared data, visual assets, and exports have distinct homes to prevent accidental source-data edits and clutter.
3. **Use a canonical report directory.** `reports/Graduation Project.pbix` is the agreed location after the active Power BI session releases the file lock.
4. **Do not store secrets in the repository.** Connection credentials, service tokens, and personal data must be configured through Power BI settings or approved secure storage, never committed to Git.
5. **Coordinate binary edits.** A PBIX cannot be safely merged like source code. One collaborator should edit the report at a time, then communicate the saved version to the group.
6. **Preserve collective credit.** Report pages, exports, presentations, and documentation must acknowledge the Graduation Project group and the individual members who contributed.

## Implementation and maintenance

Use Power Query for source connection and shaping, relationships for model behavior, and DAX for reusable business measures. Keep measure names clear, avoid duplicated logic across visuals, and validate totals after every model or refresh change. Before publishing, test page navigation, slicers, cross-filtering, tooltip content, number formats, and empty states.

For major development, save timestamped report copies in a restricted backup location or use Power BI Project (`.pbip`) where the team has agreed on that workflow. Do not convert or split this report unilaterally: a project conversion can change collaboration practices and needs a team decision.
