# Kooga MCP server

Work in your Kooga marketing from Claude, ChatGPT, Cursor or any MCP client: ask how sales, Google rankings, AI visibility and email moved, and have it write articles, draft campaigns and answer what is waiting for you. Anything that leaves Kooga asks you first.

[![Add to Cursor](https://cursor.com/deeplink/mcp-install-dark.svg)](https://cursor.com/install-mcp?name=Kooga&config=eyJ1cmwiOiJodHRwczovL21jcC5rb29nYS5pby9tY3AifQ%3D%3D)
[![Install in VS Code](https://img.shields.io/badge/VS_Code-Install_Kooga-0098FF?logo=visualstudiocode&logoColor=white)](https://vscode.dev/redirect/mcp/install?name=kooga&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fmcp.kooga.io%2Fmcp%22%7D)

| | |
|---|---|
| Server | `https://mcp.kooga.io/mcp` |
| Transport | Streamable HTTP |
| Sign-in | OAuth 2.1 (dynamic client registration, PKCE), or an access token |
| Registry name | `io.kooga/kooga` |
| Every tool | [kooga.io/docs/integrations/mcp-tools](https://kooga.io/docs/integrations/mcp-tools) |

Kooga hosts the server, so there is nothing here to install or run. This repository holds its listing (`server.json` for the [MCP Registry](https://registry.modelcontextprotocol.io), `lhm.plugin.json` for LobeHub) and these instructions.

## What it does

Kooga is the AI marketing platform for businesses: four agents (SEO, GEO, Chat and Email) run your content, AI visibility, storefront chat and email. Connected to an assistant, it lets you:

- **Read your store.** Sales, best sellers, the product catalogue, customer cohorts and sales by channel.
- **Work on Google search.** Articles losing traffic, search opportunities, tracked keyword positions, backlinks, site health and keyword research; write, refresh and publish articles, and fix weak product listings.
- **See how AI assistants talk about you.** How often ChatGPT, Gemini, Perplexity and Claude name you, by topic and country, who they name instead, what they cite and what they actually answered; track prompts and competitors, and write the article that closes a gap.
- **Run email.** Audiences, contacts and consent, sending health and results; draft, change, test, schedule and resend campaigns, draft and turn on flows, create segments, and set the logo and footer.
- **Answer your agents.** Read what is waiting on Tasks and what the agents did; approve or dismiss a task, and undo a change.

One connection can reach several workspaces, which suits agencies. When you connect, you choose which, and whether it may only read or also make changes.

It also offers four ready-made prompts (Account audit, Monday review, Fix my weakest topic, Competitor radar) and a glossary of Kooga's terms as the resource `kooga://glossary`.

## Connect

You need a Kooga account, as owner or admin of the workspaces you connect. When your assistant asks you to sign in, Kooga opens: tick the workspaces it may reach, choose **Read only** or **Read and change**, then **Allow**.

### Claude (web and desktop)

Open **Settings**, then **Connectors**, choose **Add custom connector**, name it Kooga and paste `https://mcp.kooga.io/mcp`. Choose **Connect**, then turn Kooga on from the tools menu in a conversation.

### Claude Code

```bash
claude mcp add --transport http kooga https://mcp.kooga.io/mcp
```

Then type `/mcp` and choose Kooga to sign in.

### ChatGPT

Turn on developer mode in ChatGPT's settings (paid plans; on Business or Enterprise your admin allows it), then add a connector with the address `https://mcp.kooga.io/mcp` and OAuth as its sign-in.

### Cursor

Use the **Add to Cursor** button above, or add this to `~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "kooga": { "url": "https://mcp.kooga.io/mcp" }
  }
}
```

### VS Code

Use the **Install in VS Code** button above, or run:

```bash
code --add-mcp '{"name":"kooga","type":"http","url":"https://mcp.kooga.io/mcp"}'
```

### Any other client

Add a remote MCP server with the address `https://mcp.kooga.io/mcp` (Streamable HTTP). To try it in MCP Inspector:

```bash
npx @modelcontextprotocol/inspector
```

### With an access token (n8n, Make, scripts)

For a tool that cannot open a sign-in page, make a token in Kooga at **Settings, Connected apps, Access tokens**. It starts with `kooga_pat_` and is shown once. Send it as a bearer token:

```bash
claude mcp add --transport http kooga https://mcp.kooga.io/mcp --header "Authorization: Bearer kooga_pat_..."
```

A token works as you, in the workspaces you ticked, with the same confirmations and limits. Treat it like a password.

## What it asks before doing

With **Read and change**, work that stays inside Kooga runs at once, as if you did it in Kooga: writing an article, drafting a campaign, creating a segment, tracking a keyword.

Anything that leaves Kooga asks you first, in Kooga's own words: publishing an article, sending, scheduling or resending a campaign, sending a test, turning on a flow, changing a product listing on your store, running a paid visibility check, unsubscribing contacts and deleting a campaign. Where your assistant can show a confirmation, it does; otherwise it asks in the chat. One yes does one thing.

Kooga moves no money, changes no plan and deletes no contacts.

## What you can ask

- "What changed in my store this week?"
- "Which articles are losing traffic, and which should I refresh first?"
- "How often do AI answers mention us next to our competitors?"
- "What is waiting for me in Kooga? Approve the article ideas, skip the rest."
- "Draft an abandoned-cart flow: a reminder after an hour, then one more the next day."
- "Compare March with February: orders, email results and AI visibility."

## Privacy

- **What reaches your assistant.** What it looks up for you (your store's figures, articles, contacts and, only if you turn them on for the connection, what shoppers wrote to your store's chat) goes to the company that runs the assistant, under that company's terms.
- **What Kooga keeps.** A record of each request: who asked, which app, which workspace, which tool and whether it worked. Never what it sent or what came back. You see the record at **Settings, Connected apps**, and each entry is deleted after 180 days.
- **Who can reach what.** The assistant signs in with a token issued for your account and never sees your password. Anyone who loses access to a workspace loses their assistant's access to it at the same moment, and you can disconnect an assistant at any time.
- **Text from outside.** What shoppers, other sites and AI engines wrote reaches the assistant marked as information, never as instructions.

The full policy is at [kooga.io/privacy-policy](https://kooga.io/privacy-policy).

## Support

- Docs: [kooga.io/docs/integrations/connect-an-assistant](https://kooga.io/docs/integrations/connect-an-assistant)
- Support: [support@kooga.io](mailto:support@kooga.io)
- Security reports: [security@kooga.io](mailto:security@kooga.io)

## Licence

The files in this repository are under the [MIT licence](LICENSE). Kooga itself is a hosted service under its [terms](https://kooga.io/terms-of-service).
