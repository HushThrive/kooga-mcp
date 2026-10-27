# Kooga's tools

Every tool a connection with read and write access is offered (67), grouped by the agent whose work it is. The connected server's own list and schemas are authoritative: a read-only connection gets the reads only, and the two tools that read customer messages appear only once the workspace turns them on. Inputs, outputs and examples for each are at https://kooga.io/docs/integrations/mcp-tools.

Every tool that reads or changes a workspace takes `workspaceId` (from `listWorkspaces`). **Read** tools only look things up. **Change** tools run at once inside Kooga. **Change, asks you first** tools ask the person first (anything that leaves Kooga, and a few changes that cannot be taken back) and take a `confirmToken` only after a yes.

## Connection

| Tool | Kind | What it does |
| --- | --- | --- |
| `readConnection` | Read | Who this connection acts as and what it may do: a stable id for the Kooga person (never an email address), the app, read only or read and write, and how many workspaces it reaches. |
| `listWorkspaces` | Read | List the Kooga workspaces this connection reaches, with the id to pass as workspaceId. |

## Maestro: your store, knowledge and team

| Tool | Kind | What it does |
| --- | --- | --- |
| `readStoreOverview` | Read | Orders, gross and net revenue, refunds, units and average order value over the last `days` (30 by default), with the change against the period before in `deltas` (null when there is nothing to compare). |
| `readTopProducts` | Read | The products that earned the most over the last `days`, best first, up to `limit` (10 by default, 50 at most): each with its title, orders, units and revenue. |
| `readProducts` | Read | The products on sale in the store, as Kooga last synced them: search words in the title, brand or category, keep only what is discounted or in stock, and sort by discount, price or stock. |
| `readSalesTrend` | Read | Daily revenue or order count over a period - for 'revenue trend', 'are sales going up', 'orders per day'. |
| `readCustomerStats` | Read | New versus returning customers for a period, plus top locations. |
| `readSalesChannels` | Read | Orders, revenue and units per connected channel - for 'which channel sells more', 'Shopify vs WooCommerce'. |
| `searchDocuments` | Read | Search the workspace's indexed documents for relevant content. |
| `readDocument` | Read | Read a full document from the knowledge base by its storage key, when a search result is not enough. |
| `listDocuments` | Read | The workspace's uploaded documents and folders. |
| `readCustomerInbox` | Read | Leads, handoff requests and unanswered questions the storefront agent collected. |
| `readCustomerFeedback` | Read | Thumbs-up and thumbs-down ratings shoppers left on the agent's answers. |
| `readWaitingItems` | Read | Everything waiting for the merchant right now, from every agent, in the order it matters: proposals to approve, questions only they can answer, and things to go and do. |
| `readRecentRuns` | Read | The recent runs of every agent: when each last worked, the note it left for the merchant, and how many things it proposed or did. |
| `readStatus` | Read | How one proposal or one piece of queued work stands now: waiting for approval, being carried out, done, failed (and why), dismissed or expired. |
| `readOptions` | Read | The exact values this workspace uses for one kind of thing, as stored: its segments (with ids), contact sources and statuses, the topics its tracked prompts are filed under, its tracked prompts, its competitors, its keywords. |

## SEO agent

| Tool | Kind | What it does |
| --- | --- | --- |
| `readDecaying` | Read | Published articles whose search clicks are falling, worst first. |
| `readIdeas` | Read | Content ideas that have been briefed but not yet written - most of them handed over by the GEO agent when it found a topic the brand is absent from. |
| `readOpportunities` | Read | Keywords ranking just off page one, pages earning impressions but few clicks, and articles losing traffic - from Search Console. |
| `readRankings` | Read | Google positions for the keywords the merchant tracks: `latest` is the newest weekly check and `previous` the one before (null means not in the top 20), `url` is the page that ranks and `pieceId` the Kooga article published there (null for any other page), `competitors` is where each tracked competitor stands on the same search, and `odds` says whether page one is within reach for a site this strong (within_reach, stretch, long_shot). |
| `readBacklinks` | Read | The newest backlink check: the site's domain rating (0 to 100) and the one at the check before, links gained and lost since, the same rating for each tracked competitor, and `linkGap`, the sites that link to a competitor and not to this site. |
| `generateArticle` | Change | Research and draft a new SEO article on a topic. |
| `refreshArticle` | Change | Rewrite only the sections of an article that have gone stale, using what people searched for when it was shown. |
| `readListings` | Read | Products whose listing is weak, best sellers first: no meta tags, a description too short to sell, images without alt text, a title over the store's limit, or copy already written in Kooga and not on the store yet. |
| `updateListing` | Change, asks you first | Writes a new title, description, search title and description, or image alt text to the product on your store. |
| `publishArticle` | Change, asks you first | Put a written article live on the connected site (Shopify or WordPress), or update the live post when it was published before. |
| `trackKeyword` | Change | Track where the store ranks on Google for a search, worded as people type it, in the store's language. |
| `researchKeywords` | Read | Search data for keywords: either look up the exact phrases given in `keywords`, or leave them out to get phrases people really search on Google around a `seed` topic (left out too, around this business), chosen to fit it. |
| `readSiteHealth` | Read | What Kooga's crawl of the site found, from the newest audit: its `score` (0 to 100, higher is healthier), how many pages it checked, the site-wide checks (robots.txt, sitemap, llms.txt, whether AI crawlers may read the site, which structured data the pages carry), and every kind of issue with what it means, how many pages have it and a few of them, worst first. |

## GEO agent

| Tool | Kind | What it does |
| --- | --- | --- |
| `readScorecard` | Read | How often AI engines mention this brand, per engine and over time: `series` has a point per engine and per day, week or month (`interval`). |
| `readPerceptions` | Read | The claims engines actually make, and whether they are correct. |
| `readAnswers` | Read | The answers AI engines gave to the tracked prompts, as Kooga kept them from each check: one per prompt, engine and day (the first that named the brand, else the first), newest first. |
| `readTopics` | Read | Which buyer topics AI answer engines mention this brand on, and which it is absent from. |
| `readCompetitors` | Read | Which brands AI answer engines name on the same prompts, and their share of voice against this brand. |
| `readSources` | Read | The domains and pages AI answer engines cite when answering these prompts, and how many of them are the brand’s own. |
| `readShelf` | Read | The product cards ChatGPT shows under its answers to the tracked prompts: the store's share of them, which stores fill the rest, and the prompts whose cards leave the store out. |
| `proposeProbe` | Change, asks you first | Run a fresh AI visibility check across every tracked prompt, for when the current data is too old to act on. |
| `briefContentGap` | Change | Write a draft article on a topic the brand is invisible on, from the evidence that shows it. |
| `addPrompt` | Change | Add a question to the ones AI Visibility asks the engines on every check, worded as a buyer would ask it, in the language buyers use: 'best handmade mugs in Romania'. |
| `addCompetitor` | Change | Add a competitor to the ones AI Visibility counts in every answer: its name, its site, and other names the engines use for it. |

## Email agent

| Tool | Kind | What it does |
| --- | --- | --- |
| `readSegments` | Read | The workspace's email segments and how many subscribers each had when last counted. |
| `readDeliverability` | Read | Sending health over the last 30 days: emails sent, bounce, complaint and unsubscribe rates by day and in total, the rates at which sending is reviewed or paused, and why emails were held back. |
| `readPerformance` | Read | The email list and how it is holding up: contacts by status, how many are active, joined and lost this week, the last 30 days of sending (bounce, complaint and unsubscribe rates, and a reputation score), and the mailbox providers the list is on. |
| `readCampaigns` | Read | The workspace's campaigns, newest first: each with its broadcastId, name, status, subject, when it was sent or is due, and for a sent one how many it went to, opened and clicked, its open and click rates, the A/B subject test's winner, and which campaign it was a resend of. |
| `readCampaign` | Read | One campaign as it is saved: its name, status, subject and the one it tests, preview line, audience, the brief it was written from, and its body, block by block, in the shape updateCampaign's `blocks` takes. |
| `previewSend` | Read | Work out exactly how many contacts a campaign to this segment would actually reach right now, and why the rest would not - suppressed, unsubscribed, mailed too recently, or over today's limit. |
| `draftCampaign` | Change | Write a campaign for a segment and leave it as a DRAFT for review. |
| `updateCampaign` | Change | Change a campaign that has not gone out (a draft or a scheduled one): its name, subject, the second subject it tests (null stops the test), the preview line, the audience, or its body. |
| `deleteCampaign` | Change, asks you first | Delete a campaign that has not gone out: a draft, or a scheduled one, whose send is called off with it. |
| `uploadImage` | Change | Keep an image for email: give a public https link to it (a product or collection photo, a recipe photo, a logo) and get back its address in Kooga, for a layout's image block or for the logo (updateEmailBrand). |
| `updateEmailBrand` | Change | Change what every email from this workspace carries: the logo a header block draws (a PNG, JPG or GIF address; uploadImage keeps one), the footer's own line (in place of "Sent by" and the store's name; the unsubscribe link always follows), the postal address in the footer, and up to five social links. |
| `enableFlow` | Change, asks you first | Switch on an automated email flow. |
| `readFlows` | Read | Every automated email flow: whether it is on, whether it needs a store and this workspace has one, its emails in order (how long each waits, whether it is written for each shopper when it sends, its subject and brief, what stops it), and what the flow sent, and how many opened and clicked, in the last 30 days. |
| `draftFlow` | Change | Write the emails of one automated flow and save them with the flow off, replacing the steps it had: up to eight emails, each with how long it waits (the first after the flow starts, the rest after the email before), a brief, an optional subject, and what stops the sequence before it (they bought, or opened or clicked the email before). |
| `updateFlowStep` | Change | Change one email of an automated flow that is off, by its place in the flow (readFlows lists them): how long it waits, its brief, its subject, whether it is written for each shopper when it sends or written now, what stops it, or whether it is sent at all. |
| `scheduleCampaign` | Change, asks you first | Send a drafted campaign to its audience now, or at a time (sendAt, ISO 8601 with a time zone, in the future). |
| `sendTestCampaign` | Change, asks you first | Send one test copy of a campaign, as it is saved now, to up to five addresses the person names, from the workspace's verified domain; the subject starts with [Test]. |
| `resendCampaign` | Change, asks you first | Send a campaign that went out again, as a new campaign, to the subscribers who did not open it, under a new subject when one is given (a different angle does better than the same words). |
| `findContacts` | Read | The workspace's email contacts, newest first, found by part of a name or address, by consent status or by where they came from. |
| `readContact` | Read | One contact in full, by the contactId findContacts gives: address, name, consent status and how they came to be subscribed, where they came from, what they asked the store's assistant when they came from a conversation, and their orders (count, spend, the latest ten). |
| `createSegment` | Change | Save a segment: subscribers that match rules. |
| `updateContact` | Change | Change a contact's name, city or country, by the contactId findContacts gives. |
| `unsubscribeContacts` | Change, asks you first | Unsubscribe up to 100 contacts, by the contactIds findContacts gives: they get no more campaigns or automated emails from this workspace, and each change is kept in their consent history. |

## Tasks and undo

| Tool | Kind | What it does |
| --- | --- | --- |
| `approveItem` | Change, asks you first | Approve one task waiting on Tasks: Kooga carries out what it proposes, as if the person pressed Approve in Kooga. |
| `dismissItem` | Change | Decline one task waiting on Tasks, with a reason when the person gave one: not_now, not_relevant or already_done. |
| `undoAction` | Change, asks you first | Put back what a change replaced (a product listing, a published article), when the change kept it and nothing has changed it since. |
