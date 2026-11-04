# Installing the TileSet MCP server

TileSet is a hosted, remote MCP server. There is nothing to download, build or run.

- URL: `https://app.tileset.com/mcp`
- Transport: streamable HTTP
- Auth: OAuth 2.1 with dynamic client registration. The first call returns 401 with the protected-resource metadata, and the user signs in with Google or by email in the browser and approves.

## Steps

1. Add the server to the MCP settings under the name `tileset`, with the URL above and streamable HTTP as the transport. For a client that uses an `mcpServers` map:

   ```json
   {
     "mcpServers": {
       "tileset": {
         "type": "streamableHttp",
         "url": "https://app.tileset.com/mcp"
       }
     }
   }
   ```

   With the Cline CLI, the same thing in one line: `cline mcp add tileset https://app.tileset.com/mcp --transport http --yes`

2. Connect. If the client supports OAuth, a browser tab opens for the user to sign in and approve. In the Cline CLI, `cline mcp` has an Authorize OAuth action if no tab opens.
3. If the client can't do the browser sign-in, ask the user to create an API key under **Agents & API** in the TileSet dashboard (https://app.tileset.com). Add it as a header, and keep it out of any file that's committed or shared:

   ```json
   {
     "mcpServers": {
       "tileset": {
         "type": "streamableHttp",
         "url": "https://app.tileset.com/mcp",
         "headers": { "Authorization": "Bearer <the user's API key>" }
       }
     }
   }
   ```

4. Check it works by calling the `list_widgets` tool. A new account answers with an empty list.

Then follow the user's request, starting with `setup_widget`. See the README for what the tools do.
