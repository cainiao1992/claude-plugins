# jshookmcp (Claude Code plugin)

Claude Code plugin port of [vmoranv/jshookmcp](https://github.com/vmoranv/jshookmcp) — an MCP server for AI-assisted JavaScript analysis and security analysis: browser automation, CDP debugging, network monitoring, JS hooks, and code analysis.

## What it provides

- **MCP server** `jshook`: launched via `npx -y @jshookmcp/jshook@0.4.7` over stdio, with the lightweight profile (`MCP_TOOL_PROFILE=search`, `npm_config_omit=optional`) that skips optional ONNX, Z3, Binaryen, Camoufox, and Playwright packages. Remove `npm_config_omit` in `.claude-plugin/plugin.json` when those full-profile runtimes are required.
- **Skills** (6, from the upstream repo): getting-started, best-practices, configuration, telemetry, tool-selection, troubleshooting.

## Install

From this marketplace: `/plugin install jshookmcp@rea`

## Requirements

- Node.js ≥ 22 (`engines: ^22.22.2 || ^24.15.0 || >=26.0.0`)
- No install-time lifecycle scripts; native runtimes are optional and loaded on demand

## Telemetry

Outbound telemetry is **disabled** in this plugin via `JSHOOK_OBSERVABILITY_EXPORTER=none` in the server `env` (`.claude-plugin/plugin.json`) — zero network, zero overhead. Remove that env var to restore upstream-default metrics export. See the bundled `telemetry` skill for details.
