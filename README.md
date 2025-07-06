# VSCE Template Registry <!-- omit in toc -->

[![JSON Schema ✓](https://img.shields.io/badge/schema-valid-brightgreen?logo=json)](https://github.com/vsce-templates/index/blob/main/index.json)
[![MIT License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)

A public catalogue of scaffolding templates for building **Deno-native 🦕 ⚡ VSCode Extensions** with the [`vsce`](https://github.com/vsce-dev/cli) CLI.

---

## Table of Contents <!-- omit in toc -->

- [Quick Start](#quick-start)
- [Template Manifest Schema](#template-manifest-schema)
- [Template Archive Requirements](#template-archive-requirements)
- [Adding a Template](#adding-a-template)
- [License](#license)

---

## Quick Start

```bash
# Install (or update) the CLI
deno install -A -f -q -n vsce jsr:@vsce/cli@latest

# List all community templates
vsce templates list

# Scaffold a new extension from the “react-panel” template
vsce create my-extension --template react-panel
```

By default, the CLI fetches  
`https://raw.githubusercontent.com/vsce-templates/index/main/index.json`.  
You may override this via `vsce.yml`:

```yaml
create:
  registry: "https://example.com/my-private-index.json"
```

---

## Template Manifest Schema

The registry is a **single JSON array**; each element conforms to:

| Field        | Type                | Required | Description                                                       |
|--------------|---------------------|----------|-------------------------------------------------------------------|
| `name`       | `string`            | ✔︎        | Unique identifier used with `--template <name>`                   |
| `description`| `string`            | ✔︎        | Short human-readable summary                                      |
| `url`        | `string` (URL)      | ✔︎        | HTTPS link to a `.zip` or `.tar.gz` archive of the template       |
| `version`    | `string` (semver)   | ✖︎        | Latest released version of the template                           |
| `tags`       | `string[]`          | ✖︎        | Search/filter keywords (e.g. `["react","webview"]`)               |
| `author`     | `string`            | ✖︎        | Template maintainer(s)                                            |
| `license`    | `string`            | ✖︎        | SPDX license identifier                                           |
| `homepage`   | `string` (URL)      | ✖︎        | Project URL or documentation                                      |
| `sha256`     | `string`            | ✖︎        | SHA-256 checksum of the archive (integrity verification)          |

> **Tip:** Use [JSON Schema](https://json-schema.org/) validation (`npm i -g ajv-cli`) before opening a PR.

---

## Template Archive Requirements

1. **Root directory** — When unpacked, the archive must contain a **single top-level folder** (same as `name`).  
2. **No pre-installed dependencies** — Keep `node_modules` / `dist` out.  
3. **`README.md`** explaining the template’s features & instructions.  
4. **License** — Each template must include a recognized open-source license file.

Optional niceties:

- `.vscode/launch.json` and `tasks.json` for a smoother dev experience.
- GitHub Actions or Deno workflows for CI testing the template itself.

---

## Adding a Template

1. Fork **this** repo and create a new branch.
2. Upload your template archive to a permanent location (GitHub Release asset, S3, etc.).
3. Append a new object to `index.json` following the schema above.
4. Commit + push; ensure **CI** passes (lint & schema validation).
5. Open a Pull Request – please include:
   - Link to source code  
   - Screenshots or GIF demo (if UI-focused)  
   - Any speciality permissions (`deno.json`), runtime requirements, etc.

Maintainers will review and merge once checks succeed.  
Your template becomes instantly available to the community!

---

## License

The registry index (`index.json`) is licensed under the **MIT License**.  
Individual templates are licensed as stated in their own repositories.

---

Made with ❤️ for Deno + VSCode! 🦕⚡ by [Cursor IDE](https://github.com/cursor-ide).
