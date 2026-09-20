# Setup and Development Guide

> **Group project workflow:** Every contributor shares responsibility for protecting the report, documenting changes, and recognizing the work of the full Graduation Project group.

## Prerequisites

- Microsoft Power BI Desktop (current supported version)
- Access to every required data source and its approved credentials
- Permission to use any embedded data, logos, images, and custom visuals
- Optional: Git for documentation, scripts, and controlled report versioning

## Initial setup

1. Clone or copy the project folder.
2. Check that the repository contains the three root documentation files and the `reports`, `data`, `assets`, `exports`, and `scripts` directories.
3. Open `reports/Graduation Project.pbix` in Power BI Desktop.
4. If this transition is not yet complete, open the root-level `Graduation Project.pbix` instead. Close Power BI Desktop, then move it to `reports/Graduation Project.pbix` before the next work session.
5. In Power BI Desktop, open **File > Options and settings > Data source settings** and supply or update credentials locally. Never commit credentials.
6. Refresh the report only after checking that the inputs are correct and allowed for use.

## Configuration

Document every data source in this file or in `docs/` as the team confirms it:

| Item | What to record |
| --- | --- |
| Source | File, database, API, or folder name—not credentials |
| Owner | Team member or approved system owner |
| Refresh method | Manual, gateway, or service schedule |
| Privacy level | Required Power BI privacy setting |
| Expected grain | For example: one row per sale, payment, or date |

Do not include passwords, API keys, access tokens, or exported sensitive data in the repository.

The supplied raw workbooks and the report logo are recorded in [docs/DATA_SOURCES.md](docs/DATA_SOURCES.md). Keep raw files in `data/raw/` and do not bypass the ignore rule unless the group explicitly approves the exact files for distribution.

## Development workflow

1. Announce that you are editing the report before opening it.
2. Create a backup copy or save a clearly named working version before structural changes.
3. Make the change in Power BI Desktop.
4. Validate key totals, filters, navigation, and affected pages.
5. Save the report, close it, and let the next collaborator know it is available.
6. Record material changes in the pull request, commit message, or team change log.
7. Keep the contributor list in `README.md` current so each participant receives appropriate credit.

## Quality checks

Before handing off or publishing, verify that:

- the report opens without repair prompts;
- all expected pages render and page navigation works;
- slicers and cross-filter interactions return sensible values;
- a representative total agrees with the approved source under the same filters;
- visuals have readable titles, labels, formats, and empty states;
- refresh results are current and no credentials or restricted data are exposed.

## Publishing

Publishing and sharing are separate decisions. Publish only to the agreed workspace, verify the audience and permissions, then reopen the published report to test its filters and visuals. Do not use a public "Publish to web" link unless the group has explicit authorization for public distribution.
