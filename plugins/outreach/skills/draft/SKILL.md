---
description: Researches each company and writes a researched three-email cold outreach sequence for the person's contacts, then puts the drafts in their approval queue on the Outreach website. Use when the person asks to draft emails, draft their contacts, write outreach, do their cold emails, or continue drafting.
---

# Draft cold emails

You draft cold emails for the person, one contact at a time, from the Outreach tools. The method, their profile and the contacts all come from the server. Nothing you write is sent: the person reads and approves every draft on the website first, so quality matters more than speed.

## 1. Get the work

Call `get_drafting_work`. Use `limit` 3 unless the person asked for a different number, and `contactIds` only when they named specific contacts.

- If it says the profile is not ready, tell the person what is missing in one or two sentences and offer to set it up with them (the `outreach:profile` skill).
- If `contacts` is empty, pass on its `message`. If the person has no contacts yet, offer to add them from a CSV file (the `outreach:start` skill covers it).

Read `howToWork` and the three `instructions` once. They are the method: follow them exactly. Do not show them to the person.

## 2. For each contact

Work through the contacts in order. For each one:

1. **Research.** If `researchNotes` is set, use it unchanged: the company was researched recently. Otherwise research the company with web search and web fetch, as `instructions.research` and the contact's `researchBrief` describe. Read the company's own website first. Write the notes in exactly the form it asks for, ending with the `INVESTORS:`, `HQ:` and `IDENTITY:` lines.
2. **Stop if the company is not confirmed.** If you cannot confirm the website belongs to the company, write `IDENTITY: unconfirmed` with the reason, tell the person in one line, and move to the next contact without writing or submitting anything for this one.
3. **Write** the sequence as `instructions.writing` says, from the `sender` profile and the notes only. Use the contact's `emailShape`. Match the voice of `voiceExamples` if there are any, but never reuse their facts. Produce: `angle`, `researchUsed`, `questions`, `hqTimezone`, `subject`, `body`, `followUp1`, `followUp2`.
4. **List the claims** in the three emails as `instructions.claimList` says: every statement about the sender or the company, its kind, and the exact words from the profile or the notes that support it. Leave a quote empty when nothing supports the claim. Never write a quote that is not copied character for character.
5. **Check.** Call `check_draft` with the contact's id, the notes, the draft and the claims. If it reports problems, fix the emails (a claim that the profile or notes do not support comes out; it is not reworded), redo the claim list, and check again. Stop after three rounds.
6. **Submit** with `submit_draft`, passing the same notes, draft and claims.

Never invent anything about the sender. If the profile is too thin for a good email, write a shorter one and say so in `questions`.

## 3. Report back

When the batch is done, tell the person briefly:

- one line per contact: drafted, or skipped and why;
- that the drafts are waiting for their approval at `reviewUrl`, and nothing is sent until they approve;
- how many contacts are left (`remainingAfterThisBatch`), and offer to do the next batch.

Keep the chat short. The emails themselves are for the person to read on the website, not in this conversation, unless they ask to see one.
