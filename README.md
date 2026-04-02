# Developer Kickstart: Workers' Compensation Capstone

This repository is the capstone project for the Developer Kickstart curriculum at Cloud Code Academy. You will design and build a Salesforce solution that tracks workers' compensation claims for an HR team—from data model and CSV import through Apex, triggers, and record pages—while applying what you learned across the program.

## Goals of the Practice

Throughout this project, you will practice:

- Modeling standard and custom objects and relationships that fit real-world workers' comp scenarios (including many-to-many links between employees and claims).
- Importing the provided CSV data in `data/` with the Data Import Wizard or Data Loader—not manual entry.
- Implementing bulk-safe Apex and triggers for risk levels, claim duration, rollups, status rules, and high-value flags, as specified by your instructor.
- Delivering record pages and collaboration practices (GitHub, team workflow) that reflect how you would ship in a real org.

Your instructor will share the full requirements, timeline, presentation expectations, and rubric.

## Setup

### Setup Checklist

1. Create or configure a Trailhead playground or Developer Edition org for this project.
2. Install [Visual Studio Code](https://code.visualstudio.com/).
3. Install **Salesforce Extension Pack** in VS Code (search Extensions for “Salesforce Extension Pack”).
4. Authorize your org: **Cmd/Ctrl + Shift + P** → `SFDX: Authorize an Org` → complete login in the browser.
5. Deploy from your machine using the command palette or **SFDX: Deploy Source to Org** on folders or files.

## Getting Started

1. Open `force-app/main/default/` and deploy the metadata to your org (right-click the folder → **SFDX: Deploy Source to Org**).
2. Review the CSV files in `data/` and align your schema before importing.
3. Build to your instructor’s requirements, deploy iteratively, and keep metadata in this repository.
4. Run Apex tests from VS Code if you add tests (**SFDX: Run Apex Tests**).
5. Push your work to GitHub and submit the repository link where your cohort asks (for example, the Slack submission form).

## Resources

If you get stuck, these may help:

- [Apex Developer Guide](https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/)
- [Salesforce Stack Exchange](https://salesforce.stackexchange.com/)
- [Visual Studio Code Documentation](https://code.visualstudio.com/docs)
- [Salesforce Extensions for Visual Studio Code](https://developer.salesforce.com/tools/vscode)

Good luck with your capstone.
