# How to connect Invoice Simple to Claude Code, ChatGPT and any AI agent

**Yes, Claude, ChatGPT and other AI agents can work in your Invoice Simple account.** Invoice Simple has no publicly documented official app in ChatGPT or connector in Claude. Cotlet.dev connects your own signed-in Invoice Simple account to any AI agent, so you describe the job in plain words and the AI writes the estimate or invoice for you.

## What you can ask

> Create an invoice for Mark Davis: 6 hours of drywall repair at $65 an hour plus $140 in materials, due in 14 days.

> Write an estimate for Linda Chen for a full bathroom repaint, $1,200 labor and $310 paint, valid for 30 days.

> Turn yesterday's estimate for the Patel kitchen job into an invoice and send it to them.

> Which invoices are still unpaid after 30 days? List the client, amount and due date.

> Duplicate last month's lawn care invoice for Green Street Apartments, change the date to today and send it.

## Connect in 2 minutes

Get your API key at https://cotlet.dev/app and export it as `COTLET_API_KEY`.

### Claude Code

```bash
claude mcp add --transport http cotlet https://cotlet.dev/mcp/v1 --header "Authorization: Bearer $COTLET_API_KEY"
```

### ChatGPT

Settings → Apps → add connector URL `https://cotlet.dev/mcp/v1`, then sign in with Cotlet.dev. No API key needed.

### Cursor

Copy `.cursor/mcp.json` from this repo into your project:

```json
{
  "mcpServers": {
    "cotlet": {
      "url": "https://cotlet.dev/mcp/v1",
      "headers": {
        "Authorization": "Bearer ${COTLET_API_KEY}"
      }
    }
  }
}
```

## Run it locally (stdio)

This repo is a real MCP server. It speaks MCP over stdio, lists its Invoice Simple tools without any key, and forwards every tool call to the hosted Cotlet.dev server. The hosted URL above stays the recommended way. Use this when your client only starts local servers.

```json
{"mcpServers":{"invoice-simple":{"command":"uvx","args":["invoice-simple-mcp"],"env":{"COTLET_API_KEY":"your-key"}}}}
```

Or with Docker:

```bash
docker build -t invoice-simple-mcp .
docker run -i --rm -e COTLET_API_KEY invoice-simple-mcp
```

Tools: `invoice_simple_guide`, `invoice_simple_status`, `invoice_simple_open`, `invoice_simple_read`, `invoice_simple_click`, `invoice_simple_type`, `invoice_simple_close`. Without `COTLET_API_KEY` a tool call answers: "Set COTLET_API_KEY. Get a key at https://cotlet.dev/app".

## Command line

Python 3.10+, nothing else to install. From PyPI:

```bash
pip install invoice-simple-mcp        # or run it once: uvx invoice-simple-mcp connect
invoice-simple-mcp connect
```

Or straight from this repo:

```bash
export COTLET_API_KEY="your-key"
python3 invoice_simple_agent.py connect   # ready config for Claude Code, Cursor, ChatGPT
python3 invoice_simple_agent.py status    # is Invoice Simple ready in your Cotlet.dev account
python3 invoice_simple_agent.py guide     # Invoice Simple screens and sign-in link
python3 invoice_simple_agent.py read      # open Invoice Simple, read the page, close the browser
python3 invoice_simple_agent.py tools     # list Cotlet.dev tools
python3 invoice_simple_agent.py serve     # start the stdio MCP server (same as no argument)
```

## Questions from Invoice Simple users

**Does Invoice Simple have an API?**

Invoice Simple publishes no public API, API keys or developer documentation. Cotlet.dev works in your own signed-in Invoice Simple account instead, so your AI agent can create, send and chase invoices and estimates.

**How do I connect Invoice Simple to ChatGPT?**

Add Cotlet.dev as an app in ChatGPT (Settings → Apps, connector URL `https://cotlet.dev/mcp/v1`), sign in to Invoice Simple once in your Cotlet.dev Cloud Browser, and ask ChatGPT in plain words. No code and no Invoice Simple API key.

**Is there a way to use Claude with Invoice Simple?**

Yes. In Claude Code run the one-line `claude mcp add` command above; in the Claude app add `https://cotlet.dev/mcp/v1` as a custom connector. Claude then works in your own Invoice Simple account.

**Is there an Invoice Simple MCP server?**

Invoice Simple has no official MCP server and no official app in ChatGPT or Claude (checked November 2026). Cotlet.dev is a hosted Invoice Simple MCP server that works in your own account, with Claude, ChatGPT, Cursor, Codex, n8n, Make and Zapier.

**Is there an official Invoice Simple app in ChatGPT?**

As of November 2026 there is no publicly documented official Invoice Simple app in ChatGPT or connector in Claude. Invoice Simple's AI page gives information for assistants, not an integration. Cotlet.dev connects your own Invoice Simple account to ChatGPT today.

## Find it on

- [Invoice Simple on Cotlet.dev](https://cotlet.dev/integrations/invoice-simple-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=invoice-simple&utm_content=find)
- [PyPI package invoice-simple-mcp](https://pypi.org/project/invoice-simple-mcp/)
- [Step-by-step guide (PDF) on Internet Archive](https://archive.org/details/cotlet-connect-invoice-simple-to-ai-agents-guide)

## Also works with

- [Mangomint MCP](https://github.com/cotlet-connect/mangomint-mcp)
- [Wanderlog MCP](https://github.com/cotlet-connect/wanderlog-mcp)
- [SmugMug MCP](https://github.com/cotlet-connect/smugmug-mcp)
- [Garmin Connect MCP](https://github.com/cotlet-connect/garmin-mcp)
- [Housecall Pro MCP](https://github.com/cotlet-connect/housecall-pro-mcp)
- [Medium MCP](https://github.com/cotlet-connect/medium-mcp)
- [Crexi MCP](https://github.com/cotlet-connect/crexi-mcp)
- [DistroKid MCP](https://github.com/cotlet-connect/distrokid-mcp)
- [LinkedIn MCP](https://github.com/cotlet-connect/linkedin-mcp)
- [EstimateOne MCP](https://github.com/cotlet-connect/estimateone-mcp)
- [Google Search Console MCP](https://github.com/cotlet-connect/google-search-console-mcp)
- [Lichess MCP](https://github.com/cotlet-connect/lichess-mcp)
- [Strava MCP](https://github.com/cotlet-connect/strava-mcp)
- [StreamElements MCP](https://github.com/cotlet-connect/streamelements-mcp)
- [Meetup MCP](https://github.com/cotlet-connect/meetup-mcp)
- [AccuRanker MCP](https://github.com/cotlet-connect/accuranker-mcp)
- [GetYourGuide MCP](https://github.com/cotlet-connect/getyourguide-mcp)
- [Idealista MCP](https://github.com/cotlet-connect/idealista-mcp)
- [Riverside MCP](https://github.com/cotlet-connect/riverside-mcp)
- [Udemy MCP](https://github.com/cotlet-connect/udemy-mcp)
- [Faire MCP](https://github.com/cotlet-connect/faire-mcp)
- [Buildertrend MCP](https://github.com/cotlet-connect/buildertrend-mcp)
- [Fresha MCP](https://github.com/cotlet-connect/fresha-mcp)
- [Booksy MCP](https://github.com/cotlet-connect/booksy-mcp)
- [BookingKoala MCP](https://github.com/cotlet-connect/bookingkoala-mcp)
- [Milanote MCP](https://github.com/cotlet-connect/milanote-mcp)
- [Partiful MCP](https://github.com/cotlet-connect/partiful-mcp)
- [Contractor Foreman MCP](https://github.com/cotlet-connect/contractor-foreman-mcp)
- [Pixieset MCP](https://github.com/cotlet-connect/pixieset-mcp)
- [GlossGenius MCP](https://github.com/cotlet-connect/glossgenius-mcp)
- [ZenMaid MCP](https://github.com/cotlet-connect/zenmaid-mcp)
- [FieldEdge MCP](https://github.com/cotlet-connect/fieldedge-mcp)
- [Phorest MCP](https://github.com/cotlet-connect/phorest-mcp)
- [DINGG MCP](https://github.com/cotlet-connect/dingg-mcp)
- [PhotoShelter MCP](https://github.com/cotlet-connect/photoshelter-mcp)
- [RazorSync MCP](https://github.com/cotlet-connect/razorsync-mcp)
- [ShootProof MCP](https://github.com/cotlet-connect/shootproof-mcp)
- [Invoice2go MCP](https://github.com/cotlet-connect/invoice2go-mcp)
- [Appointy MCP](https://github.com/cotlet-connect/appointy-mcp)
- [Contractor+ MCP](https://github.com/cotlet-connect/contractor-plus-mcp)
- [All apps connected through Cotlet.dev](https://github.com/cotlet-connect)

---

More: https://cotlet.dev/integrations/invoice-simple-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=invoice-simple

Start free: https://cotlet.dev/signup?app=invoice-simple&utm_source=github&utm_medium=readme&utm_campaign=invoice-simple
