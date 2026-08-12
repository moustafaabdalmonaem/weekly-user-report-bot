# Weekly User Report Bot (n8n)

An automated workflow built in [n8n](https://n8n.io) that fetches user data from an API on a schedule, cleans and transforms it, and delivers a formatted summary report straight to Telegram — no manual work required.

## What it does

Every **Monday at 9:00 AM**, the workflow:

1. **Triggers automatically** using a cron-based Schedule Trigger.
2. **Fetches data** from a REST API (`GET /users`).
3. **Cleans the data** — keeps only the fields that matter (`name`, `email`, `city`) and normalizes casing.
4. **Builds a report** — aggregates all records into a single, readable summary message with a timestamp and total count.
5. **Sends the report** to a Telegram chat automatically.

## Workflow structure

```
Schedule Trigger  →  HTTP Request  →  Edit Fields (Set)  →  Code (aggregate)  →  Telegram
   (WHEN)              (FETCH)           (CLEAN)              (FORMAT)          (DELIVER)
```

| Node | Purpose |
|---|---|
| **Every Monday 9AM** | Cron trigger (`0 9 * * 1`) — controls scheduling |
| **Fetch Users** | HTTP GET request to a public API |
| **Clean Fields** | Strips unnecessary fields, keeps only what's needed |
| **Build Report** | JavaScript Code node — merges all items into one summary string |
| **Send to Telegram** | Delivers the final message via the Telegram Bot API |

## Why this matters

This project demonstrates core workflow-automation concepts:
- Scheduled/cron-based triggers
- Working with REST APIs
- n8n's JSON item model (arrays of items, `$json` references)
- Data transformation with expressions and a Code node
- Sending notifications to a messaging platform

## Setup

1. Import `weekly-user-report-bot.json` into your n8n instance (**Workflows → Import from File**).
2. Open the **Send to Telegram** node and connect your own Telegram Bot credentials.
3. Replace the `chatId` value with your own Telegram chat ID.
4. Test the workflow manually, then toggle it **Active** to run it automatically every Monday.

## Requirements

- n8n (self-hosted or cloud)
- A Telegram bot token ([created via BotFather](https://core.telegram.org/bots#botfather))
- No coding experience required — the workflow is fully visual, with one small Code node for formatting

## Possible extensions

- Swap Telegram for Slack, Discord, or email
- Point the HTTP Request node at a real internal API instead of the demo endpoint
- Add error-handling / retry logic
- Change the schedule to daily, monthly, or any custom cron pattern
<img width="1280" height="635" alt="workflowing" src="https://github.com/user-attachments/assets/56a48287-5d61-43e9-b480-d89c529d971b" />



