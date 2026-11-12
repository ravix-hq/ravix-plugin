# Ravix plugin for Cursor

[Ravix](https://ravix.sh) runs coding agents in persistent cloud sandboxes called
tracks. Each track has its own machine, its own branch, and its own pull request.

This plugin connects Cursor to the Ravix MCP server at `https://app.ravix.sh/mcp`.
Your Cursor agent can then list your Ravix projects, open tracks, send prompts,
and wait for the results.

## Contents

| Path | Purpose |
|---|---|
| `.cursor-plugin/plugin.json` | The plugin manifest. |
| `mcp.json` | The `ravix` remote MCP server (HTTP). |
| `skills/ravix/SKILL.md` | The core flow for the agent. |
| `assets/logo.png` | The Ravix logo. |

## Install

1. In Cursor, open the plugin catalog and search for **Ravix**.
2. Install the `ravix` plugin.

## Sign in

The server uses OAuth. You do not set an API key or a variable.

1. After you install the plugin, Cursor shows that the `ravix` MCP server needs
   sign-in. Select **Connect**.
2. A browser window opens at `app.ravix.sh`. Sign in with GitHub if necessary.
3. Approve the access that Cursor asks for.
4. Go back to Cursor. The `ravix` tools are now available.

To remove access, disconnect the server in Cursor.

## Tools

The main tools:

| Tool | What it does |
|---|---|
| `list_projects` | Lists the projects you can access. Filter with `repo` or `query`. |
| `launch_task` | Opens a track and queues its first prompt. |
| `create_track` | Opens a track without a prompt. |
| `send_prompt` | Queues a prompt on an existing track. |
| `wait_task` | Waits up to 50 seconds for a task to change. |
| `get_task` | Reads the state, reply, and outcome of one task. |
| `close_track` | Closes a track. **Irreversible**: the machine and unpushed work are destroyed. |

The server also has tools for tracks, plans, previews, environments, and
workspaces. Cursor shows the full list after you sign in.

## Example

> Use Ravix to fix the failing login test in acme/web, then tell me when the
> pull request is ready.

The agent calls `list_projects`, then `launch_task`, then `wait_task` until the
task is done. It gives you the track link.

## Support

Open an issue in this repository, or go to [ravix.sh](https://ravix.sh).

## License

MIT. See [LICENSE](LICENSE).
