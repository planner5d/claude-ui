# Planner 5D

![Planner 5D logo](.claude-plugin/icon.png)

A plugin for Claude, published by UAB Planner5D. Import measured 2D floor plans into editable Planner 5D projects from Claude. Check dimensions and openings against your drawing, and browse your Spaces, projects and documents with your linked Planner 5D account.

Connect to Planner 5D in Claude, then attach a floor plan you have permission to use.

Try “Check my floor plan against the 5 m wall.” Creating a new editable project from a floor-plan image is free with a linked account. Space-specific imports and other tools retain their usual permissions and allowances.

See the [Planner 5D privacy policy](https://planner5d.com/pages/privacy) and [support center](https://support.planner5d.com/en/).

## Install and connect

Once Planner 5D is available in Claude's global plugin marketplace:

1. Open **Customize → Plugins → Discover** in Claude. In Cowork, open the
   **Cowork** tab first, then **Customize**.
2. Search for **Planner 5D**, select the plugin and click **Add**.
3. Connect your Planner 5D account when prompted and complete the sign-in flow.
4. Start a conversation, attach a measured floor-plan drawing and ask:
   “Check my floor plan against the 5 m wall.”

See [Claude's plugin installation guide](https://support.claude.com/en/articles/13837440-use-plugins-in-claude)
for more details.

The plugin uses the hosted MCP connector at
`https://copilot.planner5d.com/claude/mcp`; authentication runs through the
Planner 5D sign-in flow. No API key, local server or dependency installation is
required. Claude's hosted OAuth callback is
`https://claude.ai/api/mcp/auth_callback`.

## Data and permissions

The connector sends the floor-plan images you choose to upload to Planner 5D
for recognition. It reads account, Space, project and document data through
your linked account. Other account actions run only with the permissions
granted to that account. Review the action before approving changes or paid
operations in Claude. The plugin contains no local server or background hooks.

## Included workflow

The `check-floor-plan` skill guides measured floor-plan recognition, follows the
original job to its saved project link, and asks you to verify dimensions and
openings in Planner 5D. You can also browse your accessible Spaces, projects and
documents. Your account permissions and allowances apply. This connector does
not provide native room editing or AI image generation.

## Example prompts

- "Import this floor-plan image into a new editable project using the free
  standalone import, then give me the saved project link."
- "List my Spaces, then show the projects in the Space I choose."
- "Show the documents in the Space I choose."

For a sample drawing and the upload requirements, open the
[floor-plan import help](https://copilot.planner5d.com/claude/help/).

## Troubleshooting

- If Claude asks you to reconnect, reconnect your Planner 5D account before
  retrying. Account permissions still control which Spaces and resources appear.
- If Claude cannot access the original chat attachment, use the built-in upload
  panel with the original PNG, JPEG or WebP file, up to 8 MiB.
- If recognition is still processing, check the original job's progress. Keep
  the original request and job IDs when recovering an interrupted import.
- Reopen the saved project and compare its dimensions and openings with the
  drawing. Recognition can differ from the source; use the Planner 5D editor to
  make corrections.

## Repository contents

- `.claude-plugin/plugin.json`: plugin identity, listing metadata and privacy link.
- The bundled Planner 5D icon shown above is used for the directory listing.
- `.mcp.json`: hosted MCP connection configuration, generated during export.
- `skills/check-floor-plan/SKILL.md`: the measured floor-plan workflow.

Planner 5D operates the remote connector. This repository contains the public
plugin bundle; deployment credentials and backend services are maintained
separately.

## Validation

With Node.js 24 installed, run these commands from this plugin directory:

```sh
npm install --global @anthropic-ai/claude-code@2.1.322
claude plugin validate . --strict
```

This uses
[Claude Code's plugin validator](https://code.claude.com/docs/en/plugins/cli-reference#plugin-validate)
and fails on errors or warnings.

[GitHub Actions](.github/workflows/validate-plugin.yml) runs the same check on
branch pushes, tags, pull requests and manual runs with Claude Code 2.1.322.
Update the pinned version in both places together. No API key or Planner 5D
sign-in is needed. This checks the manifest, local MCP configuration and skill
files; it does not test the remote MCP service, OAuth or recognition results.

For a local interactive test before directory approval, start Claude Code with:

```sh
claude --plugin-dir .
```
## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for bug reports, pull requests, validation
and the release checklist. For account, billing or private project questions,
contact [Planner 5D support](https://support.planner5d.com/en/).

## License

Licensed under the [Apache License, Version 2.0](LICENSE.txt).

Copyright (c) 2026 UAB Planner5D. See [NOTICE.txt](NOTICE.txt) for attribution.

## Trademarks

The Planner 5D name and logo are trademarks of UAB Planner5D. Apache-2.0 does
not grant trademark rights beyond those in section 6 of the license. See
[TRADEMARKS.md](TRADEMARKS.md) for branding and fork guidance.

Claude and Anthropic are trademarks of Anthropic, PBC. Their names identify the
supported platform; this plugin is not developed, sponsored or endorsed by
Anthropic.
