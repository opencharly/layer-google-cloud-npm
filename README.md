# google-cloud-npm

The Firebase CLI — `firebase` on `PATH` for Google Cloud Node.js tooling.

`google-cloud-npm` installs the Firebase CLI globally via npm. It depends on
`google-cloud` + `nodejs` and ships a `package.json` pinning `firebase-tools`,
which the build installs globally under `NPM_CONFIG_PREFIX` (`~/.npm-global`).
The result is verifiable: the `firebase` binary lands in `~/.npm-global/bin`, the
`firebase-tools` package is unpacked under `~/.npm-global/lib/node_modules`, and
`firebase --version` exits cleanly and prints a semantic version. The Gemini CLI
is provided by the `gemini` candy — this candy requires it rather than
re-installing gemini at an unpinned version, so a composing box that also
composes `gemini` never has its pinned version overwritten by a `*` install.

## What it provides

| Property | Value |
|---|---|
| Layer / candy | `google-cloud-npm` |
| Requires | `layer-google-cloud`, `layer-nodejs`, `layer-gemini` |
| Binary | `~/.npm-global/bin/firebase` |
| Service / port | none |

## How to use it

Compose the layer by pinning this repo in a box's `candy:` list:

```yaml
my-firebase-box:
  candy:
    base: fedora
    candy:
      - '@github.com/opencharly/layer-google-cloud-npm:v2026.243.0515'
```

Then, inside the built image:

```bash
firebase --version       # semantic version
firebase deploy          # once authenticated
```

## Layout

- `charly.yml` — the `google-cloud-npm:` candy entity: the `require:` deps and
  the `check:` steps.
- `package.json` — pins `firebase-tools`.
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — this user overview.

## Related

- Family skill: `/charly-coder:google-cloud-npm`
- `/charly-coder:google-cloud` — the Google Cloud SDK dependency
- `/charly-coder:nodejs` — the Node.js runtime dependency
- `/charly-coder:gemini` — the Gemini CLI (pinned `@google/gemini-cli`)
- [`opencharly/charly`](https://github.com/opencharly/charly) — the charly CLI and image builder
- [`opencharly/opencharly`](https://github.com/opencharly/opencharly) — the umbrella
