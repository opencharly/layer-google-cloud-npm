# AGENTS.md — layer-google-cloud-npm

Standalone candy repo for the `google-cloud-npm` layer — the Firebase CLI
(`firebase-tools`) installed globally via npm under `~/.npm-global`. The candy
lives in `charly.yml` at the repo root and projects the `google-cloud-npm` skill
entity (`family: coder`).

Canonical files:

- `charly.yml` — the `google-cloud-npm:` candy entity and the
  `google-cloud-npm-skill:` skill entity.
- `package.json` — pins `firebase-tools`.
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — user overview only; never agent guidance.

## Load these skills first (R0)

- `/charly-coder:google-cloud-npm` — the owning skill: the npm install story,
  the `~/.npm-global` layout, and the `require:` deps. Load before editing or
  troubleshooting the layer.
- `/charly-image:layer` — the candy authoring reference (`charly.yml` schema,
  `plan:` step verbs incl. `check:`, per-distro `distro:` arms, package
  sections). Load before editing any entity field or plan step.

## Build / validate / test

- The merge gate is the **org-wide** `charly/pr-validator` (required check
  `validate / validate`, defined in `opencharly/.github`); this repo has **no
  per-repo candy gate** and ships only `.github/workflows/tag-on-merge.yml`.
- The candy's `plan:` `check:` steps are the functional evidence: the
  `~/.npm-global/bin/firebase` and `firebase-tools/package.json` file checks,
  and the `firebase --version` stdout match.
- The `require:` deps pin `layer-google-cloud`, `layer-nodejs`, and
  `layer-gemini`; the gemini requirement is what keeps a pinned
  `@google/gemini-cli` from being overwritten.

## Modify this repo

- Edit the `google-cloud-npm:` candy entity in `charly.yml` and the
  `package.json` pin together; keep the matching `google-cloud-npm-skill:`
  entity in step.
- A version bump is the `package.json` version plus any check that asserts it.

## Landing

- PR-only. Every change lands through a pull request; the org-required
  `charly/pr-validator` validates the diff and body and arms native auto-merge
  on PASS. Direct pushes to `main` are blocked.
- History lives in `CHANGELOG/` (written by `tag-on-merge` at merge time); the
  PR body IS the changelog.
- The authoritative rulebook is the umbrella `AGENTS.md` in
  `opencharly/opencharly` and `charly/AGENTS.md` in the charly repo. Do not
  restate its rules here.
