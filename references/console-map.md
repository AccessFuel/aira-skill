# AccessFuel console map

Based on the customer docs at `https://app.accessfuel.com/docs`. Read only the
section relevant to the request and use the console's own names.

## Paths (all under `https://app.accessfuel.com/console/<workspaceSlug>`)

| Console name | Path | Notes |
| --- | --- | --- |
| Ask AIRA | `/aira` | New chat. Use `agent` and `prompt` as described in SKILL.md; new chats only. |
| Audiences | `/segments` | Sidebar says Audiences; the URL keeps the legacy `segments` path. |
| Personas | `/personas` | Grid of persona cards; Create persona top right. |
| Marketing Studio | `/studio` | Campaigns list, Queue, Board, Calendar. |
| Brand DNA | `/brand-dna` | Under Marketing Studio in the sidebar. |
| Playbooks | `/playbooks` | Saved prompt templates. |
| Skills | `/skills` | Uploaded skill packs. |
| Agents | `/agents` | Built-in department agents plus custom agents. |
| Insights | `/insights` | Insights and recommendations (Aira Plus, owners/admins). |
| Library | `/library` | Documents and saved artifacts. |
| Docs | `https://app.accessfuel.com/docs/...` | Requires sign-in. |

## Audiences (segments)

Docs: `/docs/audiences/segments`

- An audience groups customers by shared behavior. Every customer gets an
  RFM score (Recency, Frequency, Monetary, each 1 = best to 5) and lands in
  an audience by RFM pattern.
- 12 default audiences ship with every workspace: Champions, Loyal Customers,
  Big Spenders, Potential Loyalists, New Customers, Promising, Need Attention,
  Can't Lose Them, At Risk, About to Sleep, Hibernating, Lost. Each carries a
  strategic objective (Maximize LTV, Retain, Acquire, Reactivate, Monitor) and
  a recommended campaign type such as "VIP/Loyalty" or "Win-back".
- **Custom audiences are created with AIRA in natural language.** Examples
  from the docs: "Create an audience of customers who spent more than $500 in
  the last 90 days", "Build an audience of customers from Canada who ordered
  more than 3 times". AIRA checks the criteria against the data and
  shows the expected match count before saving. Custom audiences are
  dynamic and recalculate on demand.
- Detail page: count and share of customer base, total revenue, AOV, top
  products, campaign type, RFM patterns, tabs Customers / Map / Geography,
  Segment Criteria (a plain-language summary of membership rules), Update Audience,
  Actions → export CSV (Standard, Google Ads, Facebook, Klaviyo).
- Before creating: check existing audiences, including the defaults. Reuse one
  only after verifying its criteria match the requested thresholds and period.
- A preview estimate and a saved/live count are different observations. Record
  their labels, timestamps and freshness instead of presenting them as one count.

## Personas

Docs: `/docs/audiences/personas`

- A persona is a named archetype built on one or more audiences: name
  (alliterative, e.g. "Jetsetter Jamie"), AI portrait, audience size, top
  products, revenue and AOV, source audiences, type badge Standard or Custom.
- Create: Personas → Create persona → name plus source audience(s); or from an
  audience detail page → Generate persona from this audience. AIRA reads the
  members, generates the portrait, infers traits.
- Refresh persona re-reads the current audience; the portrait stays unless
  regenerated.
- Generation has durable queued, generating, completed and failed states. Use
  the final saved persona ID and its saved audience relationship. Retry failed
  work only; do not duplicate queued or generating requests.
- Use in chat with `@<Persona name>`. Persona = voice; audience = the list.
  A campaign brief uses both.
- The docs distinguish measured facts (size, revenue, top products) from AI
  inference (traits, tone). Keep that distinction in reports.
- Average order value is revenue/orders; average lifetime spend is
  revenue/customers. Keep both labels explicit.

## Marketing Studio and campaigns

Source: `/docs/changelog`, entries 0.19.18 and 0.19.26.

- Marketing Studio holds campaigns, content review, scheduling and publishing
  progress: Campaigns list → campaign brief and schedule → Queue, Board
  (Drafting, Review, Scheduled, Published, Needs attention), Calendar.
- Campaigns can target personas and audiences and use several social and
  email channels; every scheduled post stays linked to its campaign.
- **Ask AIRA to create or update a campaign** and it prepares distinct drafts
  for LinkedIn, Instagram, X, Facebook or email, then shows what it created and
  why. Every draft goes to Marketing Studio for review. Ask AIRA to keep all drafts
  unscheduled, apply saved Brand DNA, and mark missing product details with
  placeholders. Verify the resulting state before reporting completion.
- Resolve selected personas and audiences by saved ID in the current workspace.
  Confirm their saved relationship, and preserve existing draft IDs during
  campaign updates or retries.
- Docs examples: "Create a three-post launch campaign for LinkedIn and
  Instagram next week." / "Update the summer campaign for email and show me
  the drafts to review."
- An accepted Insights recommendation can be turned into a campaign.

## Brand DNA

Docs: `/docs/brand-media/brand-dna`

- Four steps from a website URL: Brand Assets (logo, colors, fonts), Brand
  Foundation (mission, vision, values), Brand Personality (audience, Jungian
  archetype, Aaker dimensions), Brand Voice & Tone (four sliders, language
  patterns, tone by channel and scenario).
- Once saved it flows into every AIRA chat, playbooks, personas, Library
  documents and generated imagery. If Brand DNA is missing, disclose the gap
  and ask AIRA to label provisional brand choices.

## AIRA

Docs: `/docs/aira`, `/docs/aira/first-conversation`, `/docs/aira/tips`

- For this skill, use **AIRA** (`agent=general`) for lookups and most work,
  **Marketing** (`agent=marketing`) for campaign drafts, and **Workflow**
  (`agent=planner`) for reviewable multi-step plans and diagnoses.
  Other department and custom agents are available through the workspace picker.
- Toolbar toggles: Web search, Data access (on by default), model picker.
- Input triggers: `/` runs a playbook; `@` mentions a file, persona, skill or
  agent. Mention once per chat; it stays loaded.
- Good prompts are specific about data, time window, goal and output shape.
  Docs example: "I am planning a retention campaign and need to identify
  at-risk customers who have not purchased in 60 days but had high order
  values previously."
- Artifacts (tables, charts, reports) appear in a side panel and can be saved
  to the Library.

## Playbooks

Docs: `/docs/aira/playbooks`

- Saved prompt templates with `{{variables}}` and optional
  `{{?var}}...{{/var}}` sections; variable types Text, Text Area, Dropdown,
  Persona, Image Model. Per-playbook settings can pin the agent, model, web
  search and an auto-attached skill.
- Official playbooks in every workspace: YouTube Influencer Finder, Customer
  Analysis Report, Email Campaign Draft, Product Launch Announcement,
  Competitive Analysis, Social Media Calendar. Custom playbooks are
  workspace-shared.
- In chat: `/` then the name. The expanded prompt is editable before sending.

## Skills

Docs: `/docs/aira/skills`

- A skill is a `.zip` or `.skill` under 10 MB with `SKILL.md` (YAML `name`
  and `description`) plus reference files. Official skills are read-only and
  in every workspace; custom skills are workspace-scoped and can be disabled.
- Activate in chat with `@skill-name`; attach to a playbook to auto-load.

## Connected apps

Docs: `/docs/account/connected-apps`

- Settings → Connected Apps. Organization apps are connected once by an admin
  for the whole team; Personal apps are connected by each member. Admins choose
  which tools AIRA may use per app. If an app the user needs is not connected,
  point them to Settings → Connected Apps or ask an admin.

## Insights and recommendations

Docs: `/docs/analytics/insights`

- Scheduled or manual sweeps produce a short list of insights and prioritized
  recommendations (Aira Plus, visible to owners and admins). Each
  recommendation can be accepted, adjusted or dismissed; an accepted one can
  become a campaign (see `/docs/changelog`, entry 0.19.18). Sweeps cost roughly
  500 to 1500 credits; use the current displayed estimate when discussing cost.
