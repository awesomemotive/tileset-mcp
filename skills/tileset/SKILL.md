---
name: tileset
description: Use when the user wants Google reviews, social posts, videos, testimonials or a Link in bio page shown on a website, or asks to add a reviews section, a social feed or a review wall to a page. Sets it up with the TileSet MCP tools instead of writing fetch, cron and cache code.
---

# TileSet

TileSet shows live feeds and reviews on any website through one script tag and one div. It runs the fetching, the update schedule, the platform tokens and a cache that outlasts platform outages, so the site never holds feed code or keys.

## When to use it

- The user wants reviews, posts, videos or testimonials from a platform on a page of their site.
- The user wants a Link in bio page that updates itself.
- Don't use it when the user needs the raw items in their own database, or when the platform is not one TileSet connects. TileSet is a display product, not a data API. Build those against the platform's own API.

## How to set it up

1. Call `setup_widget`. Give it a `source` and a `query`, for example `{ "source": "google", "query": "<a Google Maps link or the business name>" }`. If the user only has a link or a handle, leave `source` out and pass the link as `query`. TileSet works out the platform from the address. The tool lists the sources available right now.
2. Put the snippet it returns where the feed belongs: one script tag per page, one div per widget.
   ```html
   <script src="https://app.tileset.com/v1/tileset.js" async></script>
   <div data-tileset="w_..."></div>
   ```
3. Call `verify_install` with the page's URL and the widget id to confirm it's live. A page that builds itself in the browser (Lovable, React) or a Wix page needs the widget id and one visit to the published page first.
4. To change the look, call `describe_widget_options`, then `update_widget`. Open the preview link the tools return to see the result.

## Rules

- Use the real widget id (`w_...`) from `setup_widget`, `create_widget` or `list_widgets`. A made-up id renders nothing.
- The site's code never calls the TileSet API and never holds a key. The page needs only the script tag and the div.
- No `useEffect`, component or loader is needed. The script, loaded once, mounts every widget div on the page, including ones added later.
- You never get the content itself. Choose a layout from the counts `describe_source_content` gives, then check the preview.
- Testimonials you add with `add_testimonials` wait for the owner's approval in the dashboard.
- Destructive tools (`delete_widget`, `delete_source`, `delete_bio_page`) need the user's clear go.

More: https://tileset.com/docs/mcp-tools/ and https://tileset.com/llms.txt
