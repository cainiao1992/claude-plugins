# rea (Claude Code plugin)

Claude Code plugin port of [morluto/rea](https://github.com/morluto/rea) — reverse engineer anything with agents, from app behavior down to native binaries.

## What it provides

- **Skill** `reverse-engineer-anything`: investigation guidance for native, managed, Electron/JavaScript, packaged, firmware, and browser targets, plus AgentEnv bundle construction.
- **MCP server** `rea`: the REA tool surface (decompilation, runtime observation, artifact inspection, evidence workflows), launched via `npx -y rea-agents@6.10.1 mcp`.

The skill supplies instructions only; all analysis capability comes from the MCP server. Installing the plugin registers both — no separate `rea setup` needed for the plugin server.

## Install

From the marketplace (npm source):

```
/plugin marketplace add morluto/rea
/plugin install rea@rea
```

Local test from this directory:

```
claude --plugin-dir /path/to/this/directory
```

## Requirements

- Node.js (for `npx` to launch the MCP server)
- Target-specific engines (rizin, Frida, adb, JEB, ...) are needed per investigation; the skill's [connection-and-recovery](skills/reverse-engineer-anything/references/connection-and-recovery.md) reference covers diagnosis.
