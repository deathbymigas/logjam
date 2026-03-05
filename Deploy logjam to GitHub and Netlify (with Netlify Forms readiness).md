# Problem statement
Publish the local Astro project to the existing GitHub repository `deathbymigas/logjam`, then deploy it through Netlify with Git-based continuous deploys and working Netlify Forms support.
## Current state overview
* Local repo is on branch `master` with one existing commit and additional uncommitted/untracked project changes; no Git remote is configured yet.
* The project is Astro v5 with standard scripts (`npm run build` -> `astro build`) and default static configuration (`astro.config.mjs`).
* The form implementation already includes Netlify-compatible HTML form markers (`name`, `method="POST"`, `data-netlify="true"`, hidden `form-name`) and uses `action="/confirmation"` for a custom success route.
* GitHub repository `deathbymigas/logjam` exists, is currently empty, and has default branch `main`.
* Current docs confirm: static Astro deploys to Netlify without extra adapter config; Netlify UI import from GitHub sets up continuous deployment; Netlify Forms require enabled form detection and deploy-time HTML parsing.
## Proposed changes
### 1) Align and publish the repository to GitHub
Standardize on `main` as the local primary branch (to match the remote default), commit the current working tree, add `origin` for `https://github.com/deathbymigas/logjam.git`, and push `main` upstream.
### 2) Link the GitHub repo to Netlify with explicit build settings
Create/import the site in Netlify from `deathbymigas/logjam`, authorize the Netlify GitHub App for repo access, and confirm build settings are `npm run build` (or `astro build`) with publish directory `dist`. Optionally commit a top-level `netlify.toml` to lock these settings in-repo.
### 3) Enable and validate Netlify Forms behavior
Confirm automatic form detection is enabled in Netlify, redeploy after enabling if required, then validate that the `contact` form is detected and submissions appear in Netlify Forms. Verify successful submission redirects to `/confirmation` in production.
## Validation and completion criteria
Deployment is complete when: GitHub `main` contains the project source, Netlify auto-deploys from that branch successfully, and at least one production form submission is captured under the `contact` form with redirect behavior working.
## Key references
* Local project: `package.json (5-10)`, `astro.config.mjs (1-4)`, `src/components/ContactForm.astro (7-17)`, `src/pages/confirmation.astro (1-16)`
* Astro Netlify deploy guide: [https://docs.astro.build/en/guides/deploy/netlify/](https://docs.astro.build/en/guides/deploy/netlify/)
* Netlify deploy-from-repo quickstart: [https://docs.netlify.com/start/quickstarts/deploy-from-repository/](https://docs.netlify.com/start/quickstarts/deploy-from-repository/)
* Netlify repository linking + GitHub App: [https://docs.netlify.com/build/git-workflows/repo-permissions-linking/](https://docs.netlify.com/build/git-workflows/repo-permissions-linking/)
* Netlify Forms setup: [https://docs.netlify.com/manage/forms/setup/](https://docs.netlify.com/manage/forms/setup/)
* GitHub local-code push workflow: [https://docs.github.com/en/migrations/importing-source-code/using-the-command-line-to-import-source-code/adding-locally-hosted-code-to-github](https://docs.github.com/en/migrations/importing-source-code/using-the-command-line-to-import-source-code/adding-locally-hosted-code-to-github)
