# Deepbits Codex Marketplace

This is a Codex marketplace version of the Deepbits Dr. Binary security plugin.
It installs one plugin, `drbinary-chat-plugin`, which connects Codex to the remote
Dr. Binary MCP server and adds security-focused skills for binary analysis,
Windows system investigation, browser hijack checks, registry review, network
inspection, suspicious file scans, and Android/AOSP kernel CVE research.

## Structure

```text
.agents/plugins/marketplace.json
plugins/drbinary-chat-plugin/
  .codex-plugin/plugin.json
  .mcp.json
  skills/
    analyze-binary/
    binary-analysis/
    check-browser-hijack/
    check-network/
    cyber-security-analyst/
    find-cves/
    kernel-cve-analysis/
    scan-registry/
    scan-suspicious-files/
    scan-system/
```

## MCP Server

The plugin uses the remote Dr. Binary MCP server:

```json
{
  "mcpServers": {
    "drbinary": {
      "type": "http",
      "url": "https://mcp.deepbits.com/mcp"
    }
  }
}
```

There is no local MCP server to build or run. Authentication happens through the
remote server when Codex connects to `drbinary`.

## Included Skills

- `binary-analysis`: Upload and analyze suspicious binaries with remote Rizin,
  Ghidra, sandbox, and artifact inspection tools.
- `kernel-cve-analysis`: Query the Android/AOSP kernel CVE database by CVE,
  version, date, branch, or exploitability.
- `cyber-security-analyst`: Run structured Windows security investigations and
  produce evidence-based remediation reports.
- `analyze-binary`: Command-style workflow for local suspicious file analysis.
- `find-cves`: Command-style CVE query routing.
- `scan-system`, `scan-registry`, `scan-suspicious-files`,
  `check-browser-hijack`, `check-network`: Windows security scanning workflows.

## Install

From Codex, add this marketplace root and install the plugin:

```bash
codex plugin marketplace add https://github.com/DeepBitsTechnology/codex-plugins.git
codex plugin install drbinary-chat-plugin@deepbits
```

## Notes

Some remote analysis steps can run for several minutes. If a workflow times out,
increase Codex's tool timeout in your config:

```toml
tool_timeout_sec = 600
```

This sets the tool timeout to 10 minutes. The remote `run_sandbox` tool also accepts
its own `timeout` parameter, up to 600 seconds.
