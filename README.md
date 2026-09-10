# Ansight for Cursor

Give Cursor runtime evidence from your mobile app using [Ansight CLI](https://www.ansight.ai).
Inspect logs, screenshots, visual trees, network activity, and app state; interact with a connected development build; and author repeatable tests and tasks.

Maintained by Ansight. This package is prepared for marketplace review; it is not yet a published or Cursor-approved listing.

## Requirements

- Cursor with plugin support and a local workspace on the machine running Ansight.
- A current Ansight CLI installation, available as `ansight` in Cursor’s terminal.
- For live app workflows, a development or QA build with the Ansight SDK enabled and connected to the resident host.
- Device and framework dependencies reported by `ansight doctor --json`.
- Python 3 only when using the automation-readiness scoring helper.

The plugin version tracks packaging independently of the CLI. The bundled workflows follow the current public skills; use `ansight version --json`, `ansight update check --json`, and installed command help to check compatibility. No hard minimum CLI version has been established by a compatibility test matrix yet. A running host may be older than the installed executable.

## Install for local testing

In Cursor, open **Customize → Plugins → Add → From Local Repository** and select this directory. The included marketplace manifest lets Cursor import this single plugin. Confirm the plugin details and install it.

Alternatively, use Cursor’s local discovery directory:

Copy this directory, including `.cursor-plugin`, to `~/.cursor/plugins/local/ansight`.
On macOS or Linux, you can instead run this from the plugin directory:

```sh
mkdir -p ~/.cursor/plugins/local
ln -s "$PWD" ~/.cursor/plugins/local/ansight
```

If that destination already exists, inspect it before replacing anything. On Windows, copy this directory to `$HOME\.cursor\plugins\local\ansight`.

Reload Cursor using **Developer: Reload Window**, then open **Customize** and confirm that Ansight and its skills appear. Teams and Enterprise administrators may need to enable **Allow Local Plugin Imports**. A marketplace installation with the same name takes precedence over a local plugin.

See [Cursor’s local plugin instructions](https://cursor.com/docs/plugins#test-plugins-locally).

## Start using it

Open your app repository in Cursor and try:

- “Use Ansight to check my CLI setup and show the connected apps.”
- “Use Ansight to investigate errors in this app’s latest recorded session.”
- “Use Ansight to open the settings screen and verify that the heading is visible.”
- “Use Ansight to create a repeatable test for this flow.”

You can also invoke `/ansight-cli-setup`, `/ansight-investigate-session`, or another [bundled skill](SKILLS.md) directly. Cursor selects relevant skills from their descriptions. The inspection router is for ambiguous requests; explicit tasks go directly to the specialist.

If Ansight is missing, use the [official installation instructions](https://www.ansight.ai/skills/ansight-install.md). Installing this plugin does not install the CLI, start a host, change your app’s SDK integration, or configure MCP. It adds no hooks or always-on rules.

## Local execution and data

Commands run through Cursor’s terminal and the existing Ansight host. Remote workspaces and cloud agents do not automatically reach a host on your laptop. Keep the workspace, CLI, and target host on the same machine for local inspection.

This package contains instructions and a Python scoring helper; it has no independent telemetry or hosted backend. Evidence returned to Cursor becomes part of the agent’s context and is subject to Cursor’s configured model and data handling. See Ansight’s [data and privacy documentation](https://www.ansight.ai/docs/workspace/data-privacy-and-analysis) for CLI capture and processing behavior. The skills preserve exact session selection, existing host state, and authorization boundaries for state-changing operations.

## Maintenance

The skill files, supporting resources, icon, catalog, and `sources.json` are generated from Ansight’s public skill sources. `sources.json` records source and packaged SHA-256 hashes. Make workflow changes in the source skills, then regenerate in the Ansight source repository:

```sh
node scripts/plugins/build-cursor-plugin.mjs
node scripts/plugins/build-cursor-plugin.mjs --check
node --test scripts/plugins/build-cursor-plugin.test.mjs
```

Packaging adds local skill references and Cursor invocation syntax. Public source URLs remain available for app documentation; OpenAI-only skill UI metadata is excluded. No runtime dependency download is needed to load the plugin.

## Support

Use [Ansight](https://www.ansight.ai) and the [CLI documentation](https://www.ansight.ai/docs/cli). Include the plugin version, CLI version, host version, and the failing command when reporting a problem; omit credentials and private session evidence.

## License

The skills and scoring helper in this plugin are [MIT licensed](LICENSE). Ansight CLI, SDKs, services, and trademarks remain subject to their separate terms. The logo identifies Ansight and does not grant trademark rights.
