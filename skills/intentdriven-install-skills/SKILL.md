---
name: intentdriven-install-skills
domain: intentdriven
description: Use when installing or reinstalling the local IntentDriven plugin after changing its skills, references, registry, package metadata, manifests, or repository instructions.
depends-on: []
chains-to: null
suggests: []
user-invokable: true
---

# IntentDriven Install Skills

Install IntentDriven from its local checkout into every supported harness available on this machine.

## Boundary

- Use the owning repository as the installation source by default.
- Do not publish, push, install missing harnesses, or change another plugin.
- Treat an unavailable harness as a reported skip.
- Treat packaging, installation, and active-session reload as different claims.

## Workflow

### 1. Resolve and validate the checkout

Resolve the repository that contains this skill. Confirm that the package and plugin name is `intentdriven`.

Read these five versions:

```bash
jq -r '.version' package.json
jq -r '.version' .claude-plugin/plugin.json
jq -r '.plugins[0].version' .claude-plugin/marketplace.json
jq -r '.version' .codex-plugin/plugin.json
jq -r '.plugins[0].version' .omp-plugin/marketplace.json
```

All values must be the same nonempty version. Stop before installation on a mismatch.

Confirm each `skills/<name>/SKILL.md` has matching frontmatter `name` and a description that starts with `Use when`.

### 2. Detect harnesses

Check `command -v pi`, `command -v omp`, `command -v claude`, and `command -v codex` separately. A missing command is a skip.

Read current command help when the installed CLI differs from the examples. Do not invent flags.

### 3. Install from the local checkout

Set `root` to the resolved absolute repository path.

| Harness | Local install | Required evidence |
|---|---|---|
| Pi | From the intended workspace, run `pi install "$root" -l --approve`, then `pi list --approve`. | The local package entry names `root`. Report the workspace because the install is project-local. |
| OMP | Refresh only the `intentdriven` marketplace from `root`; run `omp plugin install intentdriven@intentdriven --force`, `omp plugin list --json`, and `omp plugin discover intentdriven`. | The intended version, local source, and expected skill inventory are visible. |
| Claude Code | Refresh only the `intentdriven` marketplace from `root`; run `claude plugin install intentdriven@intentdriven --scope user -y`, then `claude plugin list --json`. | The intended plugin ID, version, and local marketplace source are visible. |
| Codex | Refresh only the `intentdriven` marketplace from `root`; run `codex plugin add intentdriven@intentdriven --json`, then `codex plugin list --available --json`. | The intended plugin ID and version are enabled from the local marketplace. |

If the target workspace for Pi is not specified, use this checkout for local development and report that limited scope.

If refresh requires removal, remove only the `intentdriven` plugin or marketplace and reinstall it immediately. Never clear shared caches or remove unrelated plugins.

If a harness cannot run inside the active harness, report the exact blocker and the manual command with the resolved path.

### 4. Verify packaging and activation

Run available native packaging checks from the repository root:

```bash
claude plugin validate .
claude plugin validate .claude-plugin/plugin.json
omp plugin install ./ --dry-run --json
```

A dry run proves packaging only. Post-install listing or discovery proves installation. A new session or observed reload proves activation.

## Output contract

```text
Plugin: intentdriven
Checkout:
Version:
Pi: installed | skipped | blocked | not attempted; evidence and workspace
OMP: installed | skipped | blocked | not attempted; evidence
Claude Code: installed | skipped | blocked | not attempted; evidence
Codex: installed | skipped | blocked | not attempted; evidence
Activation: observed reload | restart needed | unverified
Checks:
```

## Verification gate

Do not report completion unless all five manifest versions agree and every harness has a separate status with observed evidence or an exact skip/blocker.
