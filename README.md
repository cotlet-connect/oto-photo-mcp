# oto.photo MCP server for ChatGPT and Claude

oto.photo publishes no public API or official MCP server, checked 15 November 2026. Cotlet.dev connects ChatGPT, Claude and other AI agents to your own signed-in oto.photo account.

Source: [oto.photo integration page](https://cotlet.dev/integrations/oto-photo-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=oto-photo).

## What can your AI agent do?

The live page describes 10 hosted tools, with 5 reads and 5 writes:

| Area | Read | Write |
| --- | --- | --- |
| Galleries | `view_client_galleries` | `share_client_gallery` |
| Bookings | `view_booking_calendar` | `manage_booking_calendar` |
| Clients | `view_client_list` | `update_client_list` |
| Certificates | `view_gift_certificates` | `create_gift_certificate` |
| Portfolio | `view_portfolio` | `update_portfolio` |

Four write tools ask for confirmation by default; you can change this per tool. Private client-list updates run immediately. Read tools run immediately.

Encrypted albums stay closed. Photo uploads, deletions, your oto.photo subscription and your Google account stay outside these tools. The tools return gallery links and certificate pages; sending them to clients stays with you.

## What can I ask?

> List the favourites my client picked in the autumn family album.

> Show my bookings for next week.

> Prepare a new session with the date, price and deposit I provide, and ask before saving.

> List clients with birthdays in the next month.

> Group the wedding albums in one folder and ask before creating the gallery link.

> Show my valid gift certificates.

## Connect ChatGPT and Claude

1. [Get access to oto.photo](https://cotlet.dev/signup?app=oto-photo).
2. Enable oto.photo in the console and sign in at `https://oto.photo/auth` in your Cotlet.dev Cloud Browser with your Google account.
3. In ChatGPT, add `https://cotlet.dev/mcp/v1/connect` in Settings > Apps & Connectors, with OAuth.
4. In Claude, add the same URL in Settings > Connectors > Add custom connector.

## Connect Codex and Claude Code

Create an API key in your Cotlet.dev console and set `COTLET_API_KEY` in your environment.

Codex:

```toml
[mcp_servers.cotlet]
url = "https://cotlet.dev/mcp/v1"
bearer_token_env_var = "COTLET_API_KEY"
```

Claude Code:

```bash
claude mcp add --transport http cotlet https://cotlet.dev/mcp/v1 --header "Authorization: Bearer $COTLET_API_KEY"
```

## Optional local MCP wrapper

Python 3.10+, standard library only. This repository provides seven generic browser helpers over the hosted Cotlet.dev tools: `oto_photo_guide`, `oto_photo_status`, `oto_photo_open`, `oto_photo_read`, `oto_photo_click`, `oto_photo_type`, `oto_photo_close`.

These helpers are separate from the 10 hosted business tools above. Listing helpers requires no key; calling them requires `COTLET_API_KEY`.

```bash
export COTLET_API_KEY="your-key"
python3 oto_photo_agent.py serve
```

For a local-only MCP client, use an absolute path:

```json
{"mcpServers":{"oto-photo":{"command":"python3","args":["/absolute/path/to/oto_photo_agent.py","serve"],"env":{"COTLET_API_KEY":"your-key"}}}}
```

Other commands: `connect`, `status`, `guide`, `read`, `tools`.
The `read` command opens the browser, reads the page and closes the browser session.

## Questions

**Does oto.photo have a public API or official MCP server?**

The Cotlet.dev integration page reports no public API, developer documentation, API keys, official MCP server or official ChatGPT or Claude connector, checked 15 November 2026.

**Can the agent upload photos or open encrypted albums?**

No. Uploads stay with you. Encrypted albums stay closed to the agent.

**Does the agent send messages to clients?**

No. It returns gallery links, certificate pages and birthday lists. You send them yourself.

**Is this official?**

No. Cotlet.dev is independent and is not affiliated with oto.photo.

## Access and control

Use your own oto.photo account. Disable oto.photo for agents, reset the browser or sign out of Google sessions in your Google account to revoke access. You complete Google sign-in and any two-step check yourself.
Cotlet.dev is independent and is not affiliated with oto.photo.
