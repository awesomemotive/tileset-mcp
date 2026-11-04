<p align="center"><img src="assets/icon-512.png" alt="TileSet" width="96" height="96"></p>

# TileSet MCP server

[TileSet](https://tileset.com) puts live social feeds, reviews and testimonials on any website with one script tag and one div. This repository is the public home of its MCP server, so you can add TileSet to your AI agent and let it set up widgets for you. Smash Balloon makes TileSet.

The server is hosted. There's nothing to install or run:

```
https://app.tileset.com/mcp
```

The first time your agent calls it, a browser tab opens. You sign in with Google or by email and approve, and that's the whole setup. There's no key to create or paste.

## Add it to your agent

| Client | How |
|---|---|
| Claude Code | `claude mcp add tileset --scope user --transport http https://app.tileset.com/mcp`, or install the plugin from this repo: `/plugin marketplace add awesomemotive/tileset-mcp`, then `/plugin install tileset@tileset` |
| Claude (web and desktop) | Settings, Connectors, add a custom connector with the URL above |
| ChatGPT | Settings, Connectors (turn on developer mode first if your plan needs it), then a new connector with the URL above and OAuth |
| Codex | `codex mcp add tileset --url https://app.tileset.com/mcp` |
| Cursor | Add `{ "mcpServers": { "tileset": { "url": "https://app.tileset.com/mcp" } } }` to `~/.cursor/mcp.json` or `.cursor/mcp.json` |
| VS Code | Add `{ "servers": { "tileset": { "type": "http", "url": "https://app.tileset.com/mcp" } } }` to `.vscode/mcp.json` |
| Gemini CLI | `gemini extensions install https://github.com/awesomemotive/tileset-mcp`, or `gemini mcp add --scope user --transport http tileset https://app.tileset.com/mcp`. Run `/mcp auth tileset` if no tab opens |
| Kiro | Powers, Add Custom Power, Import power from GitHub, then paste `https://github.com/awesomemotive/tileset-mcp` |
| Cline | Ask Cline to install TileSet from this repo. It follows [llms-install.md](llms-install.md) |
| Lovable | Chat connectors, add a custom MCP server with the URL above and choose OAuth |
| Anything else | `npx @tileset/cli setup` adds TileSet to Claude Code, or prints the setting to paste for Cursor, Windsurf and others |

Clients that can't do the browser sign-in can send an API key instead: create one under **Agents & API** in the [TileSet dashboard](https://app.tileset.com) and send it as `Authorization: Bearer <key>`.

Step-by-step guides for each client: [Connect an AI agent](https://tileset.com/docs/connect-an-agent/).

## Then ask for what you want

- "Add my Google reviews to the homepage, below the booking button."
- "Show my latest YouTube videos on the landing page."
- "Make me a Link in bio page with my shop link and my newest reviews."
- "Is my TileSet widget installed on example.com/about?"

The agent connects the source, builds the widget, gives you the snippet (or places it, if it can edit your site) and checks that it's live.

## What the agent can do

- **Set up:** `setup_widget` connects a source, creates a widget and returns the snippet in one step. `verify_install` checks a live page for the script and the widget. Plus `connect_source`, `create_widget`, `update_widget`, `get_embed_code`, `describe_widget_options` and the list tools.
- **Design without reading your content:** `describe_source_content` answers with counts (how many items, ratings, photos, text lengths), and every widget tool returns a preview link, so the agent picks a layout and looks at the result.
- **Link in bio pages:** create one, change its look and blocks, and read its views and clicks.
- **Testimonials:** add testimonials, which wait for your approval in the dashboard.
- **Updates and credits:** see the balance and how often each source updates, trigger an update, or set a monthly cap.

The full list, with every argument: [What an agent can do](https://tileset.com/docs/mcp-tools/).

## What the agent never sees

An agent sets up and runs your widgets, but it never reads your content. No tool returns a post or a review, or its words, names, pictures or links. It gets a TileSet key for your account's widgets and sources, never your platform passwords or tokens. You see your content in the dashboard, and your visitors see it in the widget.

## Why not just write the feed code?

You can, and for a feed you need in your own database, or one from a platform TileSet doesn't connect, you should. For a feed on a page, TileSet runs the parts a quick fetch script leaves out: the update schedule, the platform tokens, a last good copy kept for 30 days when a platform goes down, and a script under 10 KB that doesn't move your layout around. The honest comparison is here: [TileSet or build it yourself](https://tileset.com/docs/build-it-yourself/).

## Plans

The free plan has 60 credits a month and up to 3 live sources, with no card needed. Credits are only spent when a source updates, and page views are never counted. [Plans and credits](https://tileset.com/docs/plans-and-credits/).

## What's in this repo

There's no server code here, because the server is hosted. These are the files each client needs to find and install it:

| File | For |
|---|---|
| `.claude-plugin/plugin.json`, `.claude-plugin/marketplace.json`, `.mcp.json` | Claude Code plugin and marketplace |
| `skills/tileset/SKILL.md` | The TileSet skill, which tells an agent when and how to use the tools (Claude Code and Kiro) |
| `plugin.json`, `mcp.json` | Agent Plugins format (Kiro powers and other Agent Plugins clients) |
| `gemini-extension.json`, `GEMINI.md` | Gemini CLI extension |
| `llms-install.md` | Install steps for Cline and other agents that install from a README |
| `server.json` | The entry in the official MCP Registry (`com.tileset/tileset`) |
| `assets/` | Icons |

## Help, privacy and terms

- Docs: https://tileset.com/docs/
- Support: https://tileset.com/docs/help-and-support/ or support@tileset.com
- Privacy policy: https://tileset.com/privacy/
- Terms: https://tileset.com/terms/

## License

The files in this repository are MIT licensed. See [LICENSE](LICENSE). The TileSet service itself is covered by its [terms](https://tileset.com/terms/).
