# Upstream and development

This repository contains the Microsoft Playwright project, including its browser
automation library, test runner, CLI, MCP tools, recorder, trace viewer, tests,
examples, and documentation.

- Source: https://github.com/microsoft/playwright
- Imported revision: `a018f24a4fc76e2120d3b35d2415f1e5bd4b073e`
- Upstream version: `1.66.0-next`
- Destination: https://github.com/PlaywrightMasters/Official-Playwright
- License: [Apache 2.0](LICENSE), with the original [NOTICE](NOTICE)

The import preserves both Git histories. The original package names and Microsoft
copyright notices remain intact. This downstream repository is independently
maintained and does not represent an official Microsoft release.

## Develop locally

Use Node.js 24 LTS and npm. From the repository root:

```sh
npm ci
npm run build
npx playwright install chromium firefox webkit
npm run flint
npm run ctest -- tests/page/locator-click.spec.ts --workers=2 --reporter=line
npm run ttest -- tests/playwright-test/basic.spec.ts --workers=2 --reporter=line
```

In Windows PowerShell, use `npm.cmd` instead of `npm` for commands that forward
arguments after `--`, so the PowerShell script wrapper does not consume test
runner options.

On Linux, use `npx playwright install --with-deps chromium firefox webkit` to
install browser system dependencies too. For active development, use
`npm run watch`. See [CONTRIBUTING.md](CONTRIBUTING.md) for the full upstream test
commands and development guidance.

## Continuous integration

The **Verify downstream** workflow builds the project, runs upstream lint and
type checks, exercises browser navigation, form input, and locator clicks in
Chromium, Firefox, and WebKit, and runs the test runner's basic suite on a standard
GitHub-hosted Ubuntu runner. These are representative checks, not the entire
upstream platform and browser test matrix.

The original Microsoft workflows are retained, with each job restricted to
`microsoft/playwright`. They depend on upstream infrastructure, service accounts,
or release destinations. The downstream verification workflow requires no
publishing credentials and does not publish packages or browser builds.

## Synchronize later

Add the upstream remote once if it is not already configured:

```sh
git remote add upstream https://github.com/microsoft/playwright.git
```

For an update, create a task branch from the destination's current `main`, fetch
upstream, and merge a reviewed upstream revision. Resolve the downstream README,
ignore rules, and workflow guards explicitly. Keep LICENSE and NOTICE intact,
run the checks above, and merge through a pull request. Update the imported
revision recorded here and in the README after verification.
