# Repository guidance

This is the Jekyll source for [figliadimaestra.it](https://figliadimaestra.it), a static
site built on the `minimal-mistakes-jekyll` theme (skin: `sunrise`), served via GitHub
Pages with a custom domain (`CNAME`). Content and UI copy are in Italian.

## Layout

- `_config.yml` — Jekyll and theme configuration.
- `_pages/` — standalone pages (about, contact, services).
- `_data/navigation.yml` — site navigation menu.
- `_includes/analytics-providers` — analytics snippets.
- `assets/` — images and static assets.
- `index.md` — homepage content.
- `_site/`, `.jekyll-cache/` — build output, git-ignored.

## Build & test

Ruby version is pinned in `.ruby-version` (3.2.2); dependencies are in `Gemfile`.

```bash
bundle install
bundle exec jekyll build
bundle exec htmlproofer ./_site --ignore-missing-alt --disable-external
```

CI (`.github/workflows/build.yml`) runs the same build and HTML validation on every push
to non-`gh-pages` branches.

## Conventions

- Pages are plain Markdown with Jekyll front matter; keep front matter fields consistent
  with existing pages in `_pages/`.
- Third-party GitHub Actions are pinned to full commit SHA with the version as a trailing
  comment (see `build.yml`); `.pre-commit-config.yaml`'s `gha-sha-convert` hook maintains
  this automatically — run `pre-commit run gha-sha-convert --all-files` after adding or
  updating a workflow action reference.
- Dependency updates are managed by Dependabot (`.github/dependabot.yml`), grouped per
  ecosystem so each run opens a single PR.
