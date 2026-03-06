---
name: feishu-bot-setup
description: Create and configure a Feishu (Lark) app/bot for OpenClaw agents, including batch-importing scopes JSON, enabling IM bot capabilities, adding the bot to chats, and collecting App ID/App Secret/Verification Token/Encrypt Key for OpenClaw configuration. Use when a user asks how to create a new Feishu bot/app, fix missing permissions, or set up Feishu channel integration for OpenClaw.
---

# Feishu bot/app setup for OpenClaw

## Checklist (do in order)

1) **Create app** in Feishu Open Platform
- Create a new “自建应用 / Custom App”.
- Note **App ID** and **App Secret**.

2) **Enable bot features** (IM)
- Enable the bot/IM capability (messages, group chats, etc.).

3) **Import scopes (permissions)**
- Use “批量导入权限 / Batch import scopes”.
- Paste the baseline JSON from:
  - `references/scopes-baseline.json`

4) **Apply / publish**
- Submit for approval if your tenant requires it.
- Ensure the app is **released/available** to be installed in the tenant.

5) **Event subscription (if needed by your runtime)**
- Configure Event Subscription / Webhook endpoint.
- Record:
  - **Verification Token**
  - **Encrypt Key** (if encryption is enabled)
- Ensure the endpoint can receive Feishu callbacks from Feishu IP allowlist (tenant security).

6) **Install the app / add bot to chat**
- Add the bot to a group chat (or start a 1:1 chat).
- If the bot cannot see members or messages, re-check:
  - bot has been added to the chat
  - relevant `im:*` scopes were approved
  - the app is published/installed in the tenant

7) **Wire into OpenClaw**
Collect these values for OpenClaw config (names may vary by integration, keep the raw values):
- App ID
- App Secret
- Verification Token
- Encrypt Key

## Troubleshooting heuristics

- **Bot doesn’t receive group messages**
  - Confirm it is actually added to that group.
  - Confirm scopes: `im:message.group_msg`, `im:chat`, `im:chat.members:bot_access`.

- **Bot can send but cannot read**
  - Confirm read scopes: `im:message:readonly` and the specific p2p/group read scopes.

- **Docs/wiki access fails**
  - Confirm `docs:document.content:read`, `docx:document:readonly`, `wiki:wiki:readonly`.

- **Scope import accepted but features still missing**
  - Scopes often require admin approval and/or app re-publish.
  - Re-check tenant approval state.

## Notes

- Treat `references/scopes-baseline.json` as the default baseline for *new* Feishu apps used by OpenClaw.
- Add or remove scopes based on the exact features you need; keep changes minimal and document why.
