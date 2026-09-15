# Route6 — Claude Code plugin

Give your AI agent its own place on the internet: a real public IPv6 address, a
`*.on.route6.me` hostname, port forwarding with a webhook URL, web fetch from its
own IP, and a private mesh with your other agents — 23 MCP tools, controlled by
the agent itself. Every tool is on every plan, including Free (no card).

## Install

In Claude Code:

```
/plugin marketplace add route6me/claude-plugin
/plugin install route6@route6
```

Then connect the MCP server. With the Route6 client running
(`curl -fsSL https://dl.route6.me/install.sh | sh && r6me up`, key from
https://route6.me):

```bash
claude mcp add --transport http route6 http://localhost:3000/mcp
```

Or without a client (outbound tools only — no port forwards, webhooks or mesh):

```bash
claude mcp add --transport http route6 https://gw.route6.me/mcp \
  --header "Authorization: Bearer $ROUTE6_API_KEY"
```

The plugin ships the skill that teaches Claude *when and how* to use the tools —
the webhook recipe, identity rotation and reputation checks, reaching teammates
over the mesh, and team coordination patterns — plus a
[parameter reference for every tool](skills/route6/references/tools.md), generated
from the tool schemas.

## What the tools cover

| Area | Tools |
|------|-------|
| Identity | `identity` (get / set_ipv6 / check_reputation), `hostname_register` |
| Inbound | `port_forward` (create / list / delete), `port_forward_secure`, `port_forward_tls` |
| Diagnostics | `net` (ping / traceroute / dns_resolve) |
| Web | `web_fetch`, `web_search`, `web_browse`, `scrape` |
| Mail | `smtp_allowlist` |
| Team | `team_status`, `team_ping`, `team_chat`, `team_whiteboard`, `team_capability`, `team_task`, `team_events`, `team_metrics`, `team_loop`, `team_project_task`, `team_roles` |
| Plan | `plan_upgrade` |

Plans differ in capacity (agents, egress, scraper credits). A few capabilities
need a paid plan — your own hostname, scraper top-ups, the Static IPv4 add-on,
outbound SMTP — and the tool says so when called.

More: [docs.route6.me](https://docs.route6.me) · [examples](https://github.com/route6me/examples) · [route6.me/pricing](https://route6.me/pricing)

## License

Plugin manifest and documentation: MIT. The Route6 service and client are proprietary.
