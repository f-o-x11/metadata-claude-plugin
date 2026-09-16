# Metadata for Claude Code and Cowork

Use your connected Metadata account to understand advertising performance, plan B2B audiences, prepare brand-aware ad concepts, and review campaign launch readiness.

This plugin bundles four skills and the remote [Metadata MCP](https://mcp-server.metadata.io/mcp) connection. An existing Metadata account with MCP access is required. Available data, channels, and actions depend on your account's permissions, subscriptions, and connected integrations. Metadata's service terms and any usage charges apply separately from this plugin's MIT license.

## Workflows

| Skill | Example request |
|---|---|
| `performance-review` | Compare the last 30 complete days with the preceding 30 days. Explain changes in spend, leads, and qualified pipeline without changing campaigns. |
| `audience-planning` | Estimate a US and Canada LinkedIn audience of senior software marketing leaders. Show the actual criteria and reach warnings without saving it. |
| `brand-creative` | Create an editable square LinkedIn concept for our brand using the saved brand kit, headline "Make every campaign count," and CTA "Learn more." Return a preview without saving or publishing. |
| `campaign-readiness` | Inspect my draft campaigns and explain what is missing before launch. Do not change budgets, campaign status, or integrations. |

## Install in Claude Code

Add this repository as a marketplace, then install the plugin:

```text
/plugin marketplace add f-o-x11/metadata-claude-plugin
/plugin install metadata@metadata-plugins
```

Run `/reload-plugins` or restart Claude Code after installation. Open `/mcp`, select the plugin's Metadata connection, and complete Metadata's OAuth sign-in in your browser. Use your intended workspace. Never paste passwords or access tokens into chat.

Invoke a workflow directly, or describe the task naturally:

```text
/metadata:performance-review Compare my last two complete months.
/metadata:audience-planning Preview a US LinkedIn audience of software marketing directors.
/metadata:brand-creative Create an editable square concept using my brand kit.
/metadata:campaign-readiness Check my named draft campaign without launching it.
```

## Install in Cowork

For a local installation, download the plugin ZIP from this repository's [Releases](https://github.com/f-o-x11/metadata-claude-plugin/releases) and use Claude's plugin upload flow. If your organization manages plugins centrally, ask its owner to upload the ZIP or add this marketplace through Organization settings > Plugins. Marketplace availability and permissions depend on your Claude plan and organization settings.

After enabling the plugin, connect Metadata using the normal OAuth flow and describe one of the workflows above. The plugin's public-directory review is separate from direct installation.

## Account access and actions

Each workflow starts by checking the authenticated Metadata account. If it is not the intended workspace, reconnect before reading other account data or making changes. The plugin does not contain an account, credentials, demo data, or a fixed customer identifier.

The MCP server provides both read and write tools. A reporting, audience-preview, or readiness request does not authorize campaign changes or spending. Creative generation can consume the account's generation allowance; generated previews are not automatically published. The creative skill explicitly disables library upload for preview-only requests and does not archive an existing asset without authorization.

An explicit request to create or update an audience is handled using the current tool schema and real returned IDs. Campaign launch and budget changes require a clear user request identifying the campaign, channels, budget, and schedule, plus any host-required confirmation. A successful configuration check does not override expired dates, disconnected channels, or token errors.

The skills report empty results, unavailable estimates, integration failures, and uncertain write outcomes as such. They do not invent metrics or treat zero estimates as guaranteed market size. No scheduled jobs, local executables, installation scripts, or automatic campaign actions are included.

## Troubleshooting

- **Metadata tools unavailable:** check that the plugin is enabled, reload it, and use `/mcp` in Claude Code or the connection controls in Cowork to authenticate.
- **Wrong account:** stop and reconnect to the intended workspace. Do not use account switching to inspect another customer's data.
- **Integration refresh error:** reconnect the affected advertising channel in Metadata if you have permission. A connector can authenticate successfully while an advertising-channel token is expired.
- **Missing metrics or zero audience estimate:** inspect the reporting dates, filters, actual tool response, and relevant integration state before drawing conclusions.
- **Credit or entitlement error:** report the failed operation and manage the account through Metadata's normal interface. The plugin does not sell credits in chat.

## Development

Validate both manifests and load the plugin locally:

```sh
claude plugin validate .
claude plugin validate .claude-plugin/plugin.json
claude --plugin-dir .
```

Use an authorized isolated workspace for testing. Check account identity first, exercise read and preview workflows, and avoid launches or live spend merely to test an installation.

## Links

- [Metadata](https://metadata.io)
- [Developer documentation](https://metadata.io/developers/)
- [Support](https://help.metadata.io)
- [Privacy policy](https://metadata.io/privacy-policy)

The MIT license covers the files in this repository. It does not grant access to Metadata's hosted service or rights to Metadata trademarks.
