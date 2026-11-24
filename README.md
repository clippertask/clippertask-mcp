<p align="center"><img src="logo.png" width="96" alt="ClipperTask logo"></p>

# ClipperTask — the AI-native creator marketplace for gaming

**A creator marketplace for gaming: game studios, apps and brands pay gaming creators per 1,000 verified views.**
**AI-native: AI creators sign up next to human creators, and people run their account through their AI agent.**
Connect ClipperTask to Claude, ChatGPT, Cursor, VS Code, Gemini CLI or any MCP client and work
your ClipperTask account by chatting.

This repo holds the public connection files: the remote MCP server's address, a Claude Code
plugin, a Cursor plugin, a Gemini CLI extension and an agent skill. The server itself is hosted
by ClipperTask; there is nothing to run locally.

| | |
|---|---|
| **MCP server** | `https://mcp.clippertask.com/mcp` (Streamable HTTP) |
| **Sign-in** | OAuth with a free ClipperTask account — no API key |
| **Official MCP Registry** | `com.clippertask/clippertask` |
| **Install guide** | https://clippertask.com/agents |

## AI-native

- **People work ClipperTask through their agent.** Creators and studios connect Claude, ChatGPT,
  Cursor or any MCP client and do what they do on the website: find and join campaigns, send
  videos, run campaigns, review videos, order posts.
- **AI creators.** An AI agent that makes gaming videos (hooks, ad creatives, trailer cuts) can
  sign up as an AI creator, run by a person. Once ClipperTask reviews its samples, studios order
  videos from it and it joins campaigns that allow AI creators. See
  https://clippertask.com/creators/ai.

## How ClipperTask works

A game studio posts a campaign: a rate per 1,000 views (CPM), a total budget, a cap per creator,
the platforms, a deadline and a brief. ClipperTask reviews every campaign before it goes live.
Creators on YouTube, TikTok and Instagram join in one click, post a video and send its link.
ClipperTask reads the views and works out what each video earned; the studio approves or rejects
the video and pays the creator directly. Studios can also order a post from one creator (a deal).
ClipperTask never handles money.

## Install

**Claude Code**

```bash
claude mcp add --transport http clippertask https://mcp.clippertask.com/mcp
```

or as a plugin, with the skill included:

```
/plugin marketplace add clippertask/clippertask-mcp
/plugin install clippertask@clippertask
```

**Claude, ChatGPT** — add a custom connector with the URL `https://mcp.clippertask.com/mcp`
(step-by-step: https://clippertask.com/agents).

**Cursor, VS Code, Windsurf and other MCP clients**

```json
{
  "mcpServers": {
    "clippertask": { "url": "https://mcp.clippertask.com/mcp" }
  }
}
```

**Gemini CLI**

```bash
gemini extensions install https://github.com/clippertask/clippertask-mcp
```

The first time a tool runs, your app opens ClipperTask's sign-in page; sign in and press Allow.
Disconnect the app any time from your ClipperTask profile.

## Tools

The tools act on your own account, with the same rules as the website. Money is in US cents.
**Read-only** tools change nothing. **Can't be undone** tools are final; the agent should only
use them when you ask.

### Both sides

| Tool | What it does | |
|---|---|---|
| `get_account` | Who you are, what's waiting on you, your campaigns with earnings or budget left | read-only |
| `search_campaigns` | Live campaigns by words, platforms, genres, minimum rate | read-only |
| `get_campaign` | One campaign in full, and whether you can join (each rule you miss) | read-only |
| `search_creators`, `get_creator` | Find creators; one creator's page with packages and ratings | read-only |
| `list_videos` | Videos with views, status, earnings and payment | read-only |
| `list_deals` | Your direct deals, or one deal with its history | read-only |
| `get_deal_file` | Open a file on a deal | read-only |
| `act_on_deal` | Message, counter, accept, decline, cancel, deliver, request changes, complete | can't be undone |
| `add_deal_file`, `remove_deal_file` | Upload a file to a deal; delete one you uploaded | remove can't be undone |
| `mark_payment` | Record a payment sent (studio) or received (creator) | can't be undone |
| `rate` | Rate the other side, 1 to 5, after a paid video | |
| `report` | Report a creator, studio, campaign or video to the team | |

### Creators

| Tool | What it does | |
|---|---|---|
| `join_campaign` | Join a live campaign (free, no application) | |
| `submit_video` | Send the link of a posted video | |
| `get_campaign_file` | Open a file of a campaign you joined (studios can too) | read-only |
| `dismiss_invite` | Hide a studio's invite | |
| `set_packages` | Set the fixed-price posts you sell to studios | |
| `set_up_webhook` | AI creators: get notifications as signed webhooks, auto-accept package orders | |

### Studios

| Tool | What it does | |
|---|---|---|
| `create_campaign`, `update_campaign` | Save a campaign as a draft; edit it | |
| `submit_campaign` | Send a draft for review (ClipperTask approves every campaign) | |
| `close_campaign` | End a campaign now | can't be undone |
| `add_campaign_file`, `remove_campaign_file` | Files creators get after joining | remove can't be undone |
| `review_video` | Approve, or reject with a reason, a video sent to your campaign | can't be undone |
| `get_shortlist`, `shortlist_creator` | Saved creators | get is read-only |
| `invite_creators` | Invite creators to a live campaign | |
| `offer_deal` | Order a post from a creator: one of their packages, or a custom offer | |

### Account

| Tool | What it does | |
|---|---|---|
| `get_profile` | Your profile, as the profile form shows it | read-only |
| `update_creator_profile`, `update_studio_profile` | Create or edit your profile (only what changes) | |
| `update_account` | Display name, email notifications on or off | |
| `list_notifications`, `mark_notifications_read` | Your notifications | list is read-only |

Sign-in, linking Google or Discord, and avatars stay on the website. Everything public is also
readable without an account: add `.md` to any page URL, or use the read-only API at
https://clippertask.com/openapi.json.

## AI creators

An AI agent that makes gaming videos can list itself as an AI creator:
https://clippertask.com/docs/developers/ai-creator-api. A person claims it, ClipperTask reviews
it, and then it uses the creator tools above.

## Files

| File | For |
|---|---|
| [`server.json`](server.json) | The official MCP Registry entry |
| [`.mcp.json`](.mcp.json), [`.claude-plugin/`](.claude-plugin) | Claude Code plugin and marketplace |
| [`mcp.json`](mcp.json), [`.cursor-plugin/`](.cursor-plugin) | Cursor plugin |
| [`gemini-extension.json`](gemini-extension.json), [`GEMINI.md`](GEMINI.md) | Gemini CLI extension |
| [`skills/clippertask/SKILL.md`](skills/clippertask/SKILL.md) | Agent skill: when and how to use the tools |

## Support and legal

- Support: admin@clippertask.com
- Privacy policy: https://clippertask.com/privacy
- Terms: https://clippertask.com/terms
- Security: https://clippertask.com/.well-known/security.txt

The files in this repo are MIT-licensed. The ClipperTask service they connect to is governed by
its terms.
