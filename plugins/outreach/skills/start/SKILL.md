---
allowed-tools: mcp__plugin_outreach_outreach__* WebSearch WebFetch Read
description: Gets a new person set up on Outreach and keeps them moving: profile, mailbox, contacts and first drafts, in that order. Use when the person says get started, set me up, set up outreach, what do I do next, help me use this, or when they seem new to it.
---

# Get started

Walk the person through setup one step at a time, doing as much as possible for them here in Claude Code. Assume they are not technical: plain words, one thing at a time, and never ask them to edit a file or run a command.

Call `get_status` first. Its `setup` says what is done. Skip finished steps, and pick up at the first one that isn't. Its `links` hold the website's pages: whenever you send them to the website, give the link rather than describing where to go.

## 1. Profile

Their real roles, numbers and stories. It is the only source of claims in their emails. Follow the `outreach:profile` skill: ask for their CV (they can drag the PDF into this chat or give its location), fill the profile in from it, check every number with them, and save it.

## 2. Mailbox

Their emails are sent from their own Gmail. This step happens on the website, not here, because it needs a Gmail app password, which should not be pasted into a chat. Tell them:

- open the website's **Mailboxes** page, and give them the link from `links.mailboxes` in `get_status`;
- use a second Gmail account, not their main one;
- follow the three steps shown there, which take about two minutes.

Ask them to say when it is done, then check `get_status` again. When it is connected, tell them the limit is per mailbox: each Gmail sends 20 a day in its first week and 30 after that, so connecting more spare Gmail accounts on the same page lets them send more each day. It is optional, and they can add one any time.

## 3. Contacts

Most people start from a list of recently funded companies on Crunchbase. Follow the `outreach:find-contacts` skill: it takes their Crunchbase list (an export, or rows pasted straight from the page), picks the companies that fit what they want, connects their Prospeo account here in the chat, finds the founders, and adds them with verified emails.

If they already have a list of people, as a Prospeo export or a spreadsheet saved as CSV, read the file and pass its whole text to `import_contacts`, then tell them in a sentence what was added and what was skipped. If some have no email, `find_emails` looks them up through Prospeo (connect it with `connect_prospeo` first, as the find-contacts skill describes).

## 4. Drafts

Offer to draft the first few contacts now, following the `outreach:draft` skill. Afterwards remind them that every draft waits on the website's **Drafts** page (`links.drafts`) for them to read and approve, and nothing is sent before they do. Once approved, emails go out by themselves on the recipient's weekday morning, with two follow-ups, and stop when someone replies.

## Coming back later

On later visits, `get_status` shows what needs them: drafts to approve, replies to answer in Gmail, contacts left to draft. Suggest the single most useful next step.
