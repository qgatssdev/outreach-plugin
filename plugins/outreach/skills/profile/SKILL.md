---
allowed-tools: mcp__plugin_outreach_outreach__* Read
description: Sets up or updates the person's Outreach profile, the record of their real roles, numbers and stories that every cold email draws on. Use when the person wants to set up their profile, add their CV, update their experience, or when drafting says the profile is not ready.
---

# Set up the profile

The profile is the only source of claims about the person in any email. A number in it may be sent to a stranger, so only what the person confirms goes in.

1. Call `get_profile` to see what is there and what is missing (`warnings`).
2. If the person has a CV, ask for it: a file path they can give you, or text they paste. Read it.
3. Fill in the profile from the CV and what they tell you:
   - `headline`: one line finishing "I'm <name>, …", such as "a full-stack engineer and product manager". Ask which title should come first.
   - `roles`: strongest first. Each achievement leads with its result and keeps every figure exactly as the CV states it.
   - `numbers`: each figure they could defend on a call, with what it measures.
   - `stories`: two or three in the shape "I chose X over Y and it led to Z". Ask for these; a CV rarely has them.
   - `portfolioUrl`, `signOff`, and `targetRole`. `locationLine` stays empty unless they want location mentioned, then it is said from the reader's side ("I'm within an hour of Madrid time"). `bannedPhrases` are phrases they never want used.
4. Never guess or round a figure. Leave out anything the CV does not say and the person has not confirmed.
5. Show the person a short summary of what you will save, especially every number, and ask them to confirm.
6. Save with `save_profile`, keeping anything they did not ask to change. Tell them what is still missing, if anything.
