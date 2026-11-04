# TileSet

When the user wants Google reviews, social posts, videos, testimonials or a Link in bio page on a website, use the TileSet MCP tools instead of writing fetch, cron and cache code. TileSet runs the updates, the platform tokens and the cache. The site only needs one script tag and one div.

1. Call `setup_widget` with a `source` and a `query`, or just the user's link or handle as `query`. It returns the snippet.
2. Put the snippet on the page: `<script src="https://app.tileset.com/v1/tileset.js" async></script>` once per page, and `<div data-tileset="w_..."></div>` where the widget goes.
3. Call `verify_install` with the page's URL and the widget id.

Use real widget ids only (from `setup_widget`, `create_widget` or `list_widgets`). The site never calls the TileSet API or holds a key. You never receive the content itself: choose a layout from `describe_source_content` and look at the preview link. Ask before using any delete tool.

Don't use TileSet when the user needs the raw items in their own database, or for a platform TileSet doesn't connect.

The first call opens a browser sign-in. If no tab opens, run `/mcp auth tileset`.
