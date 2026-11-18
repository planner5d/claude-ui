# Contributing to Planner 5D

This repository contains the Claude plugin manifest, hosted MCP connection
configuration, listing icon and floor-plan skill. The remote service and its
deployment are maintained separately.

## Report a problem

Open a GitHub issue with the steps to reproduce, expected and actual behavior,
Claude surface (web, desktop, Cowork or Claude Code), and plugin version. Include
a redacted screenshot when it helps. Use a small synthetic drawing for import
examples.

Do not post access tokens, OAuth codes, cookies, account details or private
floor plans. For account, billing or private project problems, contact
[Planner 5D support](https://support.planner5d.com/en/) instead. Report suspected
security vulnerabilities privately through support rather than a public issue.

## Propose a change

1. Create a branch from `main` and keep the change focused. Discuss substantial
   workflow or permission changes in an issue first.
2. Keep the manifest description and README consistent with the tools the hosted
   connector actually exposes. Update the owning documentation when behavior changes.
3. Preserve the production MCP URL, OAuth flow and account permissions unless
   the corresponding service change has been agreed with the maintainers.
4. Run the validation commands below. Include the result and any relevant manual
   checks in your pull request. UI changes should include a screenshot.

Only submit material you have the right to contribute. Include the license and
required attribution for any third-party material you add. Update
[NOTICE.txt](NOTICE.txt) when applicable; do not list dependencies that are not
bundled in this plugin.

## Branding and forks

Follow [TRADEMARKS.md](TRADEMARKS.md). Preserve copyright and attribution
notices when redistributing. Give an independently published fork its own
plugin name, display name, publisher identity and icon so users can identify
who maintains it. Do not reuse Planner 5D or Anthropic branding to imply
sponsorship or endorsement. These branding guidelines do not change the
copyright or patent permissions granted by Apache-2.0.

## Validate locally

Use Node.js 24 and the same Claude Code version as
[GitHub Actions](.github/workflows/validate-plugin.yml):

```sh
npm install --global @anthropic-ai/claude-code@2.1.322
claude plugin validate . --strict
```

No API key or Planner 5D sign-in is needed for validation. It checks local plugin
files; it does not prove that the hosted service, OAuth or recognition works.
For an interactive check, run `claude --plugin-dir .`, connect a test account
and use a synthetic plan. Confirm before creating projects or spending credits.

## Release checklist

- Run strict validation and require a successful GitHub Actions run.
- Check the manifest description, icon, documentation, support, privacy and terms links.
- Review the publisher identity, trademark notices and any bundled third-party
  attribution. Use only branding the publisher has the right to use.
- Verify sign-in and the floor-plan workflow against the production connector
  using an authorized test account. Check that the resulting project is saved
  and opens in Planner 5D.
- Update the plugin version when publishing an update; keep the README and
  validator version in sync with CI.
- Confirm that the submitted repository or archive is accessible to the directory
  reviewers. Approval and listing in Claude's directory are separate from a GitHub commit.
