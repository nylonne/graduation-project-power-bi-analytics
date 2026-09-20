# Graduation Project – Power BI Sales & Collections Analytics

> **Group graduation project:** This dashboard was created collaboratively by the Graduation Project group. Its analysis, data modelling, design, implementation, validation, and presentation are shared team work.

An interactive Power BI dashboard for monitoring portfolio-level and project-level sales and collection performance. The report provides a landing page, global summaries, collection-by-date analysis, and dedicated overview, cash, bank, and bank-wise pages for Skyline, Rihana, Degla Landmark, Lake Front 6, Degla Palms, Crysta Plaza, One Kattameya, and Zahra.

**Repository name:** `graduation-project-power-bi-analytics`  
**Repository description:** Collaborative Power BI graduation project for portfolio sales and collections analytics.

## Repository layout

```text
.
├── reports/                 # Canonical home for the Power BI report
│   └── Graduation Project.pbix
├── data/
│   ├── raw/                 # Original input files; do not edit in place
│   └── processed/           # Reproducible cleaned or prepared data
├── assets/
│   └── images/              # Images used by report pages or documentation
├── exports/                 # Generated PDFs, presentations, and extracts
├── scripts/                 # Optional repeatable preparation/validation scripts
├── docs/                    # Supporting documentation that does not belong at root
├── README.md                # Overview and report usage
├── TECHNICAL.md             # Architecture and implementation notes
├── SETUP.md                 # Setup and collaboration instructions
└── LICENSE                  # MIT License
```

> Current transition note: `Graduation Project.pbix` is still at the repository root because it is open in Power BI Desktop and Windows has locked it. Once it is closed, move it to `reports/Graduation Project.pbix`; no report content or internal references will change.

## Use the report

1. Open the `.pbix` file in Microsoft Power BI Desktop.
2. Start on **Landing Page**, then use the page navigation to choose a global summary or a project.
3. Use slicers and filters to focus the visuals on the required date, project, or payment context.
4. Refresh only after confirming that the configured data sources are available and authorized.
5. Save a named version before substantial edits and publish only to the approved Power BI workspace.

See [SETUP.md](SETUP.md) for installation and collaborator workflow, and [TECHNICAL.md](TECHNICAL.md) for the report architecture.

## Group collaboration and credit

This is a joint graduation project, not the work of one individual. All participating group members are joint contributors to the dashboard, its data model, analysis, design, testing, and presentation. Add each member's name and agreed contribution below before final submission or publication; do not omit contributors whose work is incorporated in the report.

| Contributor | Contribution |
| --- | --- |
| Graduation Project group members | Joint authorship of the report and supporting work |
| _Add member name_ | _Add agreed contribution_ |
| _Add member name_ | _Add agreed contribution_ |

## License

This project is protected by the [Graduation Project Contributor-Only License](LICENSE), copyright 2026 Graduation Project Contributors. It may be used only by verified group contributors; it is not open source. Confirm that you have permission to share any embedded data, branding, images, or custom visuals before distributing the report.
