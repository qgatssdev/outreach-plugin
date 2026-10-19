---
description: Gets a new person set up on Outreach and keeps them moving: profile, mailbox, contacts and first drafts, in that order. Use when the person says get started, set me up, set up outreach, what do I do next, help me use this, or when they seem new to it.
---

# Get started

Walk the person through setup one step at a time, doing as much as possible for them here in Claude Code. Assume they are not technical: plain words, one thing at a time, and never ask them to edit a file or run a command.

Call `get_status` first. Its `setup` says what is done. Skip finished steps, and pick up at the first one that isn't.

## 1. Profile

Their real roles, numbers and stories. It is the only source of claims in their emails. Follow the `outreach:profile` skill: ask for their CV (they can drag the PDF into this chat or give its location), fill the profile in from it, check every number with them, and save it.

## 2. Mailbox

Their emails are sent from their own Gmail. This step happens on the website, not here, because it needs a Gmail app password, which should not be pasted into a chat. Tell them:

- open the website's **Mailboxes** page (the same site they created their token on);
- use a second Gmail account, not their main one;
- follow the three steps shown there, which take about two minutes.

Ask them to say when it is done, then check `get_status` again.

## 3. Contacts

Ask for their list as a CSV file (an export from Apollo, Prospeo or a spreadsheet saved as CSV). Read the file and pass its whole text to `import_contacts`, then tell them in a sentence what was added and what was skipped.

If some contacts have no email, `find_emails` looks them up through their own Prospeo account. If it says Prospeo is not connected, tell them to paste their Prospeo API key on the website's **Contacts** page (a free account at prospeo.io gives about 100 lookups a month), then try again.

## 4. Drafts

Offer to draft the first few contacts now, following the `outreach:draft` skill. Afterwards remind them that every draft waits on the website's **Drafts** page for them to read and approve, and nothing is sent before they do. Once approved, emails go out by themselves on the recipient's weekday morning, with two follow-ups, and stop when someone replies.

## Coming back later

On later visits, `get_status` shows what needs them: drafts to approve, replies to answer in Gmail, contacts left to draft. Suggest the single most useful next step.
