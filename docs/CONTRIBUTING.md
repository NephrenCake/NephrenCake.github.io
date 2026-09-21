# Contributing to al-folio

Thank you for considering contributing to al-folio!

## Pull Requests

We welcome your pull requests (PRs).
For minor fixes (e.g., documentation improvements), feel free to submit a PR directly.
If you would like to implement a new feature or a bug, please make sure you (or someone else) has opened an appropriate issue first; in your PR, please mention the issue it addresses.

Note that since [#2048](https://github.com/alshedivat/al-folio/pull/2048) al-folio uses the [prettier formatter](https://prettier.io/) for its code, meaning all new submitted code must conform to its standard. If you don't have `prettier` installed for your setup and the `prettier` code check fails when submitting a PR, you can check the referred failed action in our repo. In that action there will be an artifact with an HTML diff showing the needed changes.

## Adding your site to the showcase

**Please do not open a pull request to add your site to the showcase list.** We have retired that process. Instead, post a request in the _Showcase_ category of [GitHub Discussions](https://github.com/alshedivat/al-folio/discussions) with a link to your site and the group it belongs in (Academics, Labs, Courses, or Conferences & workshops). Requests are reviewed and added to [`docs/SHOWCASE.md`](SHOWCASE.md) in batches, so it may take a little while before your entry appears.

## Repository Routing (v1.x)

`al-folio` is a starter in `v1.x`. Before opening a PR, route your change to the owning repo:

- `al-folio` (this repo): starter wiring (`Gemfile`, `_config.yml`), example/demo content, documentation, visual tests, cross-gem integration tests.
- `al-folio-core` and other `al-*` gem repos: component runtime behavior, layouts/includes/style primitives, feature logic, unit/component tests.
- If a feature does not fit an existing plugin, propose a new standalone plugin first, then implement there.

For the authoritative area-to-gem mapping, see [`BOUNDARIES.md`](BOUNDARIES.md). For how the starter and gems connect at runtime — including the failure modes that produce no error message — see [`ARCHITECTURE.md`](ARCHITECTURE.md).

## Plugin Naming Convention (v1.x)

We use a hybrid naming convention:

- Theme-coupled plugins: repo `al-folio-<feature>`, gem/plugin id `al_folio_<feature>`.
- Reusable plugins: repo `al-<feature>` or neutral name, gem/plugin id aligned with plugin namespace.
- Third-party non-`al-*` plugins are allowed in the ecosystem and can be featured.

## Featuring Community Plugins

You can publish and own your own plugin, then propose it for featuring in `al-folio`.

1. Open a **Plugin Feature Proposal** issue in this repo.
2. Share plugin metadata (repo URL, gem name, plugin id, compatibility, owner, demo path).
3. Open a PR to this starter updating:
   - [`_data/featured_plugins.yml`](../_data/featured_plugins.yml)
   - optional demo content page/post under `_pages/` or `_posts/`
4. If requesting **bundled** status (not only featured listing), include starter wiring updates in:
   - [Gemfile](../Gemfile)
   - [\_config.yml](../_config.yml)

Featuring and bundling are separate decisions:

- **Featured-only**: catalog/docs entry and demo.
- **Bundled**: also included in starter dependencies/plugin list by maintainers.

Plugin patch releases are published from their owning repositories. Update this starter only when a plugin release changes default wiring, dependency pins, documentation, examples, integration tests, visual baselines, or Docker/runtime release artifacts.

## Test Ownership

`al-folio` is a starter kit in `v1.x`. Keep tests aligned with runtime ownership:

- `al-folio`: visual regression + cross-gem integration + starter wiring contracts.
- Gem repos (`al-folio-core`, `al-folio-distill`, `al-*`): component correctness/unit tests and asset/runtime contract checks.

Do not add duplicate component-level correctness tests to this starter when the component is gem-owned. See [`BOUNDARIES.md`](BOUNDARIES.md).

## Local Validation

Before opening/updating a PR in `v1.x`, run:

```bash
bundle install
npm ci
npm run lint:prettier
npm run lint:style-contract
bundle exec jekyll build --baseurl /al-folio
```

The `--baseurl /al-folio` flag matters: the demo site is published as a project page, and building without it produces an unstyled site with broken links.

If your change touches plugin wiring or feature behavior, run the integration tests it affects. All seven are gated by `unit-tests.yml`:

```bash
bash test/integration_comments.sh
bash test/integration_plugin_toggles.sh
bash test/integration_distill.sh
bash test/integration_bootstrap_compat.sh
bash test/integration_upgrade_cli.sh
bash test/integration_css_minify.sh
bash test/integration_new_plugins.sh
```

If your change touches visual tests, install Playwright browsers once and run:

```bash
npx playwright install chromium webkit
npm run test:visual
```

## Issues

We use GitHub issues to track bugs and feature requests.
Before submitting an issue, please make sure:

1. You have read [the FAQ section](FAQ.md) of the README and your question is NOT addressed there.
2. You have done your best to ensure that your issue is NOT a duplicate of one of [the previous issues](https://github.com/alshedivat/al-folio/issues).
3. Your issue is either a bug (unexpected/undesirable behavior) or a feature request.
   If it is just a question, please ask it in the [Discussions](https://github.com/alshedivat/al-folio/discussions) forum.

When submitting an issue, please make sure to use the appropriate template.

## License

By contributing to al-folio, you agree that your contributions will be licensed
under the LICENSE file in the root directory of the source tree.
