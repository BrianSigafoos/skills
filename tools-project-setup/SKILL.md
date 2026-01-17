---
name: tools-project-setup
description: Set up new Brian Sigafoos tools projects to match the established CLI or static web patterns, including repo layout, docs hosting, CI and release workflows, install scripts, formatting config, and AGENTS guidance. Use when scaffolding or aligning a tool repo and when adding the tool to the https://github.com/BrianSigafoos/tools index (README and docs).
---

# Tools Project Setup

## Overview

Create or align tools repos by copying the established patterns from fast-format-x, git-new-branch, debt-calc, and ppp-pricing. Decide whether the tool is a Rust CLI or a static web tool, then apply the matching checklist and update the tools index with a placeholder entry.

## Decide the tool type

- **CLI tool (Rust + marketing site)**: See fast-format-x and git-new-branch. Use when shipping a binary with install.sh and a GitHub Pages landing page.
- **Web tool (static site)**: See debt-calc and ppp-pricing. Use when the product is a browser app deployed from docs/.

## Common baseline (all tools)

- Add MIT `LICENSE` with the current year and Brian Sigafoos.
- Add `.fast-format-x.yaml` and run `ffx` for formatting.
- Add `README.md` with a short product summary, quick start, and development notes.
- Add `AGENTS.md` with project overview, dev commands, formatting, and testing notes.
- Use `docs/` for the hosted site and set `docs/CNAME` to `<tool-slug>.bfoos.net`.
- The hosted site supports dark mode with a user toggle and defaults to system color scheme unless toggled.
- Place the dark mode toggle in the top-right corner by default unless the layout demands otherwise.
- The hosted site footer links to `https://briansigafoos.com`, `https://github.com/BrianSigafoos/<repo>`, and `https://tools.bfoos.net`.
- The hosted site is mobile responsive.
- Keep the repo name, domain, and CLI alias consistent with the tool slug.
- Use `https://github.com/BrianSigafoos/<repo>` for GitHub links.

## CLI tool pattern (Rust + installer + marketing site)

Follow the fast-format-x or git-new-branch repo layout and update names, URLs, and binaries.

- **Core files**
  - `Cargo.toml`, `Cargo.lock`, `src/`, and `tests/` as needed.
  - `.fast-format-x.yaml` with rustfmt and prettier (copy from fast-format-x or git-new-branch).
  - `AGENTS.md` with Rust dev commands, ffx formatting, and Rust code principles.
  - `README.md` with install, usage, development, and release sections.
  - `LICENSE` (MIT).

- **Installers**
  - `install.sh` at repo root and a byte-for-byte copy at `docs/install.sh`.
  - Update `REPO`, `BINARY_NAME`, output banner, and download URL.
  - Keep `docs/install.sh` in sync with `install.sh` (CI checks this).

- **GitHub Actions**
  - `ci.yml` with test, lint, build, and install.sh sync checks (copy and rename from existing CLI tool).
  - `release.yml` to build platform binaries and publish GitHub Releases.
  - Update artifact names and binary names in `release.yml`.
  - Add `release.toml` for cargo-release with tag format `vX.Y.Z`.

- **Docs site**
  - Create `docs/index.html`, `docs/style.css`, and assets by copying from an existing CLI tool.
  - Set `docs/CNAME` to `<tool-slug>.bfoos.net`.
  - Update copy, links, and CLI alias on the landing page.

- **Search and replace checklist**
  - Replace prior repo names and binary names in `README.md`, `install.sh`, `docs/install.sh`, `docs/index.html`, and workflows.
  - Update GitHub URLs to `https://github.com/BrianSigafoos/<repo>`.
  - Keep the short domain consistent with the tool slug.

## Web tool pattern (static site + Pages)

Follow the debt-calc or ppp-pricing repo layout and update the site content.

- **Core files**
  - `docs/index.html`, `docs/styles.css`, and `docs/app.js` (or similar).
  - `docs/data/` for static JSON data when needed.
  - `.fast-format-x.yaml` using prettier (and standard for JS if needed).
  - `README.md` with quick start, Pages deploy note, and file map.
  - `AGENTS.md` with dev commands, formatting, and project conventions.
  - `LICENSE` (MIT).

- **GitHub Actions**
  - `docs/` deploys via `pages.yml` (copy from debt-calc or ppp-pricing).
  - Set `docs/CNAME` to `<tool-slug>.bfoos.net`.

- **Optional helpers**
  - Add `Makefile` targets for `serve`, `refresh`, or `test` when needed.
  - Add `scripts/` for data refresh jobs and document any required env vars.

## Update the tools index with a placeholder entry

Add a placeholder entry to the tools index so the new project is discoverable before launch.

- **Update README list**
  - Edit `../tools/README.md` under CLI or Web Tools.
  - Use a placeholder name and description until the final copy is ready.
  - Example:
    ```markdown
    - [tool-name](https://tool-name.bfoos.net) (`tool`) - Coming soon.
    ```

- **Update docs index**
  - Edit `../tools/docs/index.html` and add a new `project-card`.
  - Use a `project-cli` badge for CLIs or `project-cli project-web` for web tools.
  - Use placeholder tagline and description until launch.
  - Keep CLI cards grouped above web cards, matching the existing layout.

## Final checks

- Run `ffx` and verify the Pages site locally (`python3 -m http.server --directory docs` or the project Makefile).
- Confirm `install.sh` and `docs/install.sh` are identical for CLI tools.
- Ensure the tools index entry is present in `../tools/README.md` and `../tools/docs/index.html`.
