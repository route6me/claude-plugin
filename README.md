# Route6 — Claude Code plugin

Give your AI agent its own internet identity: a real public IPv6, a DNS hostname, port forwarding, web fetch from a stable IP, and (Team plan) a private mesh with other agents — 27 MCP tools, controlled by the agent itself. Free tier, no card.

## Install

In Claude Code:

```
/plugin marketplace add route6me/claude-plugin
/plugin install route6@route6
```

Then connect the MCP server (free API key from https://route6.me):

```bash
claude mcp add --transport http route6 https://gw.route6.me/mcp \
  --header "Authorization: Bearer $ROUTE6_API_KEY"
```

The plugin ships the skill that teaches Claude *when and how* to use the tools — identity rotation on blocks, the hostname + port-forward + TLS webhook recipe, team coordination patterns — plus the full [27-tool parameter reference](skills/route6/references/tools.md).

## What the tools cover

| Area | Tools |
|------|-------|
| Identity (free) | `identity_get`, `identity_set_ipv6`, `identity_check_reputation` |
| Diagnostics (free) | `net_ping`, `net_traceroute`, `net_dns_resolve` |
| Web (free basic) | `web_fetch`; paid: `web_search`, `web_browse`, `scrape` |
| Inbound (Agent plan) | `hostname_register`, `port_forward_create/list/delete/tls` |
| Team (Team plan) | mesh status/ping, chat, whiteboard, capabilities, task queue, project tasks, roles |

More: [docs.route6.me](https://docs.route6.me) · [examples](https://github.com/route6me/examples) · [route6.me/pricing](https://route6.me/pricing)

## License

Plugin manifest and documentation: MIT. The Route6 service, clients, and container are proprietary.
