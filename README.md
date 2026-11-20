# rea marketplace

A Claude Code plugin marketplace curating reverse-engineering and JavaScript-analysis plugins.

## Plugins

| Plugin | Version | What it does | License |
|--------|---------|--------------|---------|
| [rea](plugins/rea/) | 6.10.1 | Reverse engineer anything with agents, from app behavior down to native binaries (upstream: [morluto/rea](https://github.com/morluto/rea)) | MIT |
| [jshookmcp](plugins/jshookmcp/) | 0.4.8 | MCP server for AI-assisted JavaScript analysis and security analysis — browser automation, CDP debugging, network monitoring, JS hooks, code analysis (upstream: [vmoranv/jshookmcp](https://github.com/vmoranv/jshookmcp)) | AGPL-3.0-only |

## Install

```
/plugin marketplace add <this-repo>
/plugin install rea@rea
/plugin install jshookmcp@rea
```

Local test:

```
claude --plugin-dir /path/to/this/repo/plugins/rea
claude --plugin-dir /path/to/this/repo/plugins/jshookmcp
```

## Layout

```
.claude-plugin/marketplace.json   # marketplace manifest (multi-plugin list)
plugins/<name>/
├── .claude-plugin/plugin.json    # per-plugin manifest
└── skills/                       # bundled skills
```

Each plugin registers its MCP server via `npx` with a pinned package version, so analysis capability updates are decoupled from this marketplace's own releases.

## Notes per plugin

- **rea**: target-specific engines (rizin, Frida, adb, JEB, ...) are needed per investigation; see the skill's connection-and-recovery reference.
- **jshookmcp**: runs on Node.js ≥ 22. The registered server uses the lightweight profile (`MCP_TOOL_PROFILE=search`, `npm_config_omit=optional`), which skips optional ONNX/Z3/Binaryen/Camoufox/Playwright runtimes — remove `npm_config_omit` in `plugins/jshookmcp/.claude-plugin/plugin.json` if you need full-profile features. Telemetry is disabled by default (`JSHOOK_OBSERVABILITY_EXPORTER=none`); remove that env var to restore upstream-default metrics export.
