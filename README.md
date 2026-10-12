# Instoryview Agent Skill

[![npm CLI](https://img.shields.io/npm/v/instoryview?label=CLI)](https://www.npmjs.com/package/instoryview)

**An Agent Skill that lets Claude Code, Codex, Cursor and other compatible AI assistants answer questions about the Instagram accounts you track with [Instoryview](https://instoryview.com).** Ask in plain language; the assistant reads your retained follower and following snapshots and detected changes through Instoryview's CLI or MCP tools, and explains what the data does and does not show.

## Example prompts

- "Which Instagram accounts am I tracking?"
- "Show alice's last available followers."
- "What changes did Instoryview detect for alice in the last seven days?"
- "Who stopped following alice since October 1?"
- "Query bob's public followers online, at most 2 credits."

## Install

```bash
npx skills add instoryview/skill
```

This installs the Skill into the assistants found on your machine. With the [Instoryview CLI](https://github.com/instoryview/cli) you can install the same Skill without GitHub: `instoryview skill install` (`--target claude` for `~/.claude/skills`, `--project` for one project).

## Connect your account

The Skill contains no credentials and installs no software. Give the assistant access one of two ways:

1. **Remote MCP (OAuth):** add `https://instoryview.com/mcp` as a connector and sign in on Instoryview's own authorization page.
2. **CLI:** `npm install --global instoryview`, then `instoryview auth login` (macOS Keychain) or set `INSTORYVIEW_API_KEY`.

Never paste an API Key into a chat.

## What the assistant can do

| You ask about | MCP tool | CLI command |
|---|---|---|
| Tracked accounts | `list_tracking` | `instoryview tracking list --json` |
| Account profile and totals | `get_account` | `instoryview account USERNAME --json` |
| Existing followers | `list_followers` | `instoryview followers USERNAME --json` |
| Existing following | `list_following` | `instoryview following USERNAME --json` |
| Detected changes | `get_account_changes` | `instoryview changes USERNAME --json` |
| Online lookup of a public account | `query_public_account` | `instoryview followers USERNAME --live --max-credits N --json` |

## Built-in safeguards

- **Existing data first.** Reads use data Instoryview already holds and never start a scan.
- **Explicit budgets.** An online lookup runs only after you name the target, the data type and a maximum number of credits. It returns one page and never starts continuous tracking.
- **Honest data.** The assistant reports the data's observation time, coverage and warnings. "Detected at" is not the exact time someone followed or unfollowed, a partial list is not the whole Instagram list, and no detected change is not proof of no activity.
- **Data is not instructions.** Names and bios returned by the API are treated as data only.

## FAQ

**Does it work with ChatGPT?** Use the [ChatGPT / Codex plugin preview](https://github.com/instoryview/chatgpt-plugin) or add the MCP server above as a custom connector.

**Does it need my Instagram password?** No. It uses only your Instoryview account.

**Is it free?** The Skill is free. Reading your stored data does not spend credits; online lookups spend credits within the limit you set. See [pricing](https://instoryview.com/pricing).

## Links

[Skill docs](https://instoryview.com/docs/skill) · [Open API](https://instoryview.com/docs/reference) · [CLI](https://github.com/instoryview/cli) · [Instagram follower tracker](https://instoryview.com) · support@instoryview.com
