# AES Portfolio Command Center — static GitHub Pages demo

An **unofficial Westinghouse Engineered Solutions concept portfolio** for a Project Controls Manager interview or portfolio demonstration. Not affiliated with or endorsed by Westinghouse Electric Company. All project names, personnel, milestones, budgets, risks, and capacity data are **fictional**.

## Features

- Executive dashboard showing portfolio budget, EVM forecast, CPI, SPI, project health and illustration-only trends.
- Project register with search, status filter, drill-down, add/remove sample projects.
- Cost and earned-value analysis with transparent calculation assumptions.
- Weekly resource demand/capacity planning and bottleneck identification.
- Risk / integrated change register (demonstration read-only dataset).
- Generated executive briefing that can be copied or downloaded as text.
- **Local deterministic assistant** that answers common portfolio questions from current browser data. No model, API key, cloud service, or server is required.
- Import/export JSON for demo scenarios; browser `localStorage` persistence; responsive layout.

## Deploy to GitHub Pages

1. Create an empty GitHub repository (for example, `aes-portfolio-command-center`).
2. Upload the files from this folder to the repository root, including `.github/workflows/pages.yml`.
3. Under repository **Settings → Pages → Build and deployment**, select **GitHub Actions** as the source.
4. Push to the `main` branch. The workflow publishes the static files. Your site URL will be `https://YOUR-USERNAME.github.io/YOUR-REPO/`.

Alternatively serve locally by opening `index.html` in a modern browser. For a development server: `python -m http.server 8080` then open `http://localhost:8080`.

## How the assistant works

The chatbot lives in `app.js` (`respond()`), using local keyword intents and live calculations over the demo dataset. It is **not** a generative AI model or a connection to Westinghouse systems. It does not send prompts off-device. To use a hosted LLM later, deploy an authenticated server-side service and send approved, permission-checked requests through that backend; **never** expose API keys in GitHub Pages browser JavaScript.

## Data model

`projects` objects: `id`, `name`, `program`, `owner`, `bac`, `progress`, `planned`, `ac`, `finish`, `status`.
`resources` objects: `team`, `capacity`, `demand` (illustrative weekly hours).
`risks` objects: `id`, `project`, `title`, `severity`, `owner`, `mitigation`, `type`.

Demo EVM: `EV = BAC × progress%`, `PV = BAC × planned%`, `CPI = EV/AC`, `SPI = EV/PV`, `EAC = AC + (BAC − EV)/CPI`. This EAC assumes current CPI continues; it is not appropriate for every project. The chart labeled “illustrative monthly series” is fabricated from the current snapshot and must not be interpreted as historical records.

## Safety and production considerations

This site is **not production-ready for internal confidential data**. GitHub Pages is publicly accessible unless additional access controls are arranged. Browser localStorage is not secure multi-user storage, authentication, authorization, or an audit trail. Do not upload sensitive project data, proprietary design information, nuclear facility data, customer contracts, employee records, or controlled/export-restricted information. For a production deployment, use corporate SSO/RBAC, an approved application hosting platform, audited server-side database, encrypted data, access-controlled data integrations (e.g. P6 / ERP / Power BI), formal change approvals, data lineage, and a governed AI gateway with monitoring and human-in-the-loop controls. Avoid sharing actual nuclear-related sensitive information with unauthorized AI services.

## Files

- `index.html` — layout, navigation, form, assistant shell
- `styles.css` — responsive dark dashboard design
- `app.js` — state, sample data, EVM, views, assistant, import/export
- `.github/workflows/pages.yml` — automated GitHub Pages deployment

Licensed under MIT for this sample code only; trademarks remain with their respective owners.
