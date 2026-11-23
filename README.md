# Invoice Simple API integration and MCP server: connect Invoice Simple to ChatGPT, Claude and any AI agent

Invoice Simple API integration and MCP server, unofficial, by Cotlet. Your AI works in your own signed-in Invoice Simple account: estimates, invoices, clients, payments, expenses and receipts, on the same screens your login opens. No developer and no Invoice Simple API key needed. Cotlet is independent and is not affiliated with Invoice Simple.

**Does Invoice Simple have an API or an MCP server?** Invoice Simple has no public API and no Zapier or Make app (checked 23 Nov 2026). Its pricing page, help center and its own page for AI assistants name no API and no QuickBooks integration. It takes card payments through Stripe and PayPal, and its only AI feature is an AI Receptionist phone add-on. Invoice Simple has no MCP server and no ChatGPT or Claude app.

## What contractors and freelancers ask their AI to do in Invoice Simple

| Job | Ask your AI | Make it repeat |
|---|---|---|
| Estimate from a voice note | "Make an estimate for the Patel deck repair from this voice note: 12 hours, two boxes of screws, stain. Show me before you save." | When a job comes in |
| Estimate to invoice, with extras | "Turn the accepted Patel estimate into an invoice and add the two extra items I did on site." | When a job ends |
| Overdue invoices | "List overdue invoices, total them per client and draft a polite reminder for each. Send nothing yet." | Weekly |
| Who has not paid and this month's income | "Which clients have not paid, and what did I invoice and collect this month?" | Weekly |
| Quarter for your accountant | "Export this quarter's invoices, payments and expenses with receipt photos into one folder for my accountant." | Quarterly |
| Expenses by tax category | "Sort this year's expenses into tax categories and list the receipts that are missing." | Before tax time |
| Statement for one client | "Find every invoice for Harbor Cafe and make one statement with what is paid and what is open." | When a client asks |
| Income in a spreadsheet | "Put each paid invoice in my Google Sheet with client, amount and date." | Your own endpoint, called from Google Sheets |
| Monthly invoices for repeat clients | "Make this month's invoices for my five repeat clients from last month's, with the new dates." | Monthly |
| Moving to another app | "Export all my clients, invoices and expenses to CSV so I can import them into Xero." | Once |

Your AI asks you before it sends, books or changes anything. Payments stay in your hands: Cotlet refuses payments.

## Your own Invoice Simple API, built with Cotlet

Invoice Simple gives you no API and no Zapier app. With Cotlet you build your own: your AI does the job once in your Cloud Browser, you save it as an endpoint, and you call it from Google Sheets, QuickBooks, Xero, Zapier, Make, n8n, your own code.

Examples you can build in a few minutes (none of them exists until you build it):

| Endpoint you build | What it returns or does |
|---|---|
| `unpaid-invoices` | invoice, client, amount and days overdue, oldest first |
| `income-for-period` | invoiced and collected totals for a period, by client |
| `expenses-for-period` | expenses with category, amount and receipt link |
| `client-statement` | every invoice for one client with paid and open amounts |
| `open-estimates` | estimates waiting on a client, with total and days since sent |
| `draft-invoice` | saves a draft invoice from the lines you send; nothing is sent (writes only after you allow it) |

Call it with your Cotlet API key, JSON in and JSON out:

```bash
curl -X POST https://cotlet.dev/api/v1/custom/unpaid-invoices \
  -H "Authorization: Bearer $COTLET_API_KEY" -H "Content-Type: application/json" -d '{}'
```

Limits: one call runs up to 90 seconds, writes wait for your consent, payments are blocked. Start here: https://cotlet.dev/app/custom-api/new?app=invoice-simple

## Connect in 2 minutes

Sign up at https://cotlet.dev, sign in to Invoice Simple once in your Cloud Browser, then add Cotlet to your AI.

### Claude

Settings → Connectors → Add custom connector, paste `https://cotlet.dev/mcp/v1` and sign in with Cotlet.dev.

### ChatGPT

Open Plugins in ChatGPT, choose Create as a plugin, paste `https://cotlet.dev/mcp/v1` and sign in with Cotlet.dev. No API key needed.

### Claude Code

```bash
claude mcp add --transport http cotlet https://cotlet.dev/mcp/v1 --header "Authorization: Bearer $COTLET_API_KEY"
```

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

Or with Docker:

```bash
docker build -t invoice-simple-mcp .
docker run -i --rm -e COTLET_API_KEY invoice-simple-mcp
```

Tools: `invoice_simple_guide`, `invoice_simple_status`, `invoice_simple_open`, `invoice_simple_read`, `invoice_simple_click`, `invoice_simple_type`, `invoice_simple_close`. Without `COTLET_API_KEY` a tool call answers: "Set COTLET_API_KEY. Get a key at https://cotlet.dev/app".

## Command line

Python 3.10+, nothing else to install.

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
**Does Invoice Simple have an API or a Zapier app?**

No. Invoice Simple has no public API and no Zapier or Make app (checked 23 Nov 2026). With Cotlet you build your own endpoints in your signed-in Invoice Simple account and call them from Google Sheets, Zapier, Make or n8n.

**How do I get Invoice Simple into QuickBooks or to my accountant?**

Invoice Simple names no QuickBooks integration. Your AI exports the quarter's invoices, payments and expenses with receipt photos into one folder, ready for your accountant or a QuickBooks or Xero import.

**Can ChatGPT or Claude make an Invoice Simple estimate from a voice note?**

Yes. Your AI turns the voice note or notes into estimate lines and saves a draft in your account. You check it before it goes to the client.

**Can an AI agent chase overdue Invoice Simple invoices?**

Yes. It lists overdue invoices per client and drafts a reminder for each. Nothing goes out until you say yes.

**Can AI sort my Invoice Simple expenses for taxes?**

Yes. It sorts the year's expenses into tax categories and lists the receipts that are missing.

**How do I export everything from Invoice Simple before I leave?**

Your AI exports your clients, invoices and expenses from the screens your login opens into CSV files that Xero, Wave or Zoho can import.

**Is there an Invoice Simple MCP server or ChatGPT app?**

No. Invoice Simple's AI Receptionist answers your phone. Cotlet is an unofficial MCP server for the ChatGPT and Claude apps and any MCP client.

## Find it on

- [Invoice Simple MCP server on Cotlet.dev](https://cotlet.dev/integrations/invoice-simple-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=invoice-simple&utm_content=find)
- [Invoice Simple API with Cotlet](https://cotlet.dev/integrations/api/invoice-simple?utm_source=github&utm_medium=readme&utm_campaign=invoice-simple&utm_content=find)
- [Does Invoice Simple have an API or MCP server?](https://cotlet.dev/api-mcp-status/invoice-simple?utm_source=github&utm_medium=readme&utm_campaign=invoice-simple&utm_content=find)

## More invoicing and trades apps on Cotlet

- [Joist MCP](https://github.com/cotlet-connect/joist-mcp)
- [Tradify MCP](https://github.com/cotlet-connect/tradify-mcp)
- [Invoice2go MCP](https://github.com/cotlet-connect/invoice2go-mcp)
- [MYOB MCP](https://github.com/cotlet-connect/myob-mcp)
- [Housecall Pro MCP](https://github.com/cotlet-connect/housecall-pro-mcp)
- [ZenMaid MCP](https://github.com/cotlet-connect/zenmaid-mcp)
