---
name: bnbot
description: The safest and most efficient way to automate Twitter/X — BNBot operates through a real browser session with 29 AI-powered tools. Grow your Twitter without API bans.
version: 1.1.0
homepage: https://github.com/bnbot-ai/bnbot-cli
metadata:
  openclaw:
    emoji: "\U0001F916"
    os: [darwin, linux, windows]
    requires:
      bins: [bnbot-cli]
    install:
      - id: node
        kind: node
        package: bnbot-cli
        bins: [bnbot-cli]
        label: Install bnbot-cli (npm)
---

# BNBot - Control Twitter/X via AI

BNBot operates through a real browser session via Chrome Extension. 29 tools for posting, engagement, scraping, content fetching, and articles.

- **Chrome Extension**: [Install](https://chromewebstore.google.com/detail/bnbot-your-ai-growth-agen/haammgigdkckogcgnbkigfleejpaiiln)
- **npm**: [bnbot-cli](https://www.npmjs.com/package/bnbot-cli)
- **GitHub**: [bnbot-ai/bnbot-cli](https://github.com/bnbot-ai/bnbot-cli)

## BEFORE ANY BNBOT OPERATION — ALWAYS DO THIS FIRST

Every time you are about to use any bnbot tool, you MUST run this check first. No exceptions.

```bash
lsof -i :18900 -P 2>/dev/null | grep LISTEN
```

If the output is empty (nothing listening), start the daemon:

```bash
nohup bnbot serve > /tmp/bnbot.log 2>&1 &
sleep 1
lsof -i :18900 -P 2>/dev/null | grep LISTEN
```

If it still fails, the binary may not be installed. Install it:

```bash
npm install -g bnbot-cli
nohup bnbot serve > /tmp/bnbot.log 2>&1 &
```

Only proceed with bnbot commands after confirming port 18900 is LISTEN.

## How to use tools (CLI mode)

All tools are executed via the `bnbot` CLI. Use the `exec` tool to run these commands:

```bash
bnbot get-extension-status
bnbot post-tweet --text "Hello world!"
bnbot scrape-timeline --limit 10
bnbot navigate-to-search --query "AI agents"
```

The output is JSON. Parse it to get the result.

## If extension is not connected

After running `bnbot get-extension-status`, if it shows `connected: false`, tell the user:

> Chrome Extension is not connected. Please:
> 1. Install extension: https://chromewebstore.google.com/detail/bnbot-your-ai-growth-agen/haammgigdkckogcgnbkigfleejpaiiln
> 2. Open https://x.com in Chrome
> 3. Open BNBot sidebar → Settings → turn on MCP

## Available CLI commands

### Status
- `bnbot get-extension-status` — Check if extension is connected
- `bnbot get-current-page-info` — Get current Twitter/X page info

### Navigation
- `bnbot navigate-to-tweet --tweetUrl <url>` — Go to a specific tweet
- `bnbot navigate-to-search --query "..." [--sort ...]` — Search page
- `bnbot navigate-to-bookmarks` — Go to bookmarks
- `bnbot navigate-to-notifications` — Go to notifications
- `bnbot navigate-to-following` — Go to following list
- `bnbot return-to-timeline` — Go back to home timeline

### Posting
- `bnbot post-tweet --text "..."` — Post a tweet
- `bnbot post-thread --tweets '[{"text":"..."},{"text":"..."}]'` — Post a thread
- `bnbot submit-reply --text "..." [--tweetUrl <url>]` — Reply to a tweet
- `bnbot quote-tweet --tweetUrl <url> --text "..."` — Quote a tweet

### Engagement
- `bnbot like-tweet [--tweetUrl <url>]` — Like a tweet
- `bnbot retweet [--tweetUrl <url>]` — Retweet
- `bnbot follow-user --username <handle>` — Follow a user

### Scraping
- `bnbot scrape-timeline --limit <n> --scrollAttempts <n>` — Scrape timeline
- `bnbot scrape-bookmarks --limit <n>` — Scrape bookmarks
- `bnbot scrape-search-results --query "..." --limit <n>` — Search and scrape
- `bnbot scrape-current-view` — Scrape visible tweets
- `bnbot scrape-thread --tweetUrl <url>` — Scrape a thread
- `bnbot account-analytics --startDate YYYY-MM-DD --endDate YYYY-MM-DD` — Analytics

### Content Fetching
- `bnbot fetch-wechat-article --url <url>` — Fetch WeChat article
- `bnbot fetch-tiktok-video --url <url>` — Fetch TikTok video
- `bnbot fetch-xiaohongshu-note --url <url>` — Fetch Xiaohongshu note

### Articles
- `bnbot open-article-editor` — Open article editor
- `bnbot fill-article-title --title "..."` — Fill title
- `bnbot fill-article-body --content "..." [--format markdown]` — Fill body
- `bnbot upload-article-header-image --headerImage <path>` — Upload header
- `bnbot publish-article [--publish true]` — Publish article
- `bnbot create-article --title "..." --content "..." [--format markdown]` — Full flow

### Jobs
- `bnbot search-jobs [--type boost] [--limit 10]` — Search crypto reward jobs
