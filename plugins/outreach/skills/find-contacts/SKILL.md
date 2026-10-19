---
allowed-tools: mcp__plugin_outreach_outreach__* WebSearch WebFetch Read
description: Turns a list of recently funded companies, usually copied or exported from Crunchbase, into contacts for Outreach. Picks the companies that fit what the person is looking for, finds the founders there through their own Prospeo account, and adds them with verified emails. Use when the person shares or pastes a Crunchbase list or any list of companies, asks to find companies or people to email, wants more contacts, or needs to connect Prospeo.
---

# Find companies and the people to email

The person brings a list of companies, usually from Crunchbase. You pick the ones worth emailing, find the right person at each through their Prospeo account, and add them as contacts. Assume they are not technical: plain words, short messages, one question at a time.

Call `get_status` and `get_profile` first. `get_status` gives the website's `links`; whenever you send them to the website, give the link.

## 1. What they are looking for

Read `companyPreferences` in the profile. If it is empty, ask in one message what kind of company they want: the field (fintech, developer tools, health), the stage (pre-seed to Series B), the size, where (a country, or remote), and anything to avoid. Save their answer in their own words as `companyPreferences` with `save_profile`, keeping the rest of the profile exactly as it is. If it is already set, say it back in one line and ask if it still holds.

## 2. The list

Ask for their list. Either works:

- an export from Crunchbase, saved as CSV: they can drag the file into this chat or say where it is saved;
- the rows copied straight from a Crunchbase search page and pasted here. Messy pasted text is fine.

Read it and pull out each company: name, website, last round (type, amount and date), industries, headquarters and description. Do not ask them to tidy it. A company with no website can't be searched: if there are only a few, find the website with a quick web search; otherwise leave them out and say how many.

## 3. Pick the companies

Judge each company against their preferences, using what the list says:

- **Fit first.** Score higher when what the company builds resembles their past work in the profile's roles. Fit matters more than size.
- **Timing.** Hiring usually starts one to three months after a round. Best: Seed or Series A announced 2 to 8 weeks ago, Pre-Seed 2 weeks to 4 months ago. Rounds older than about six months are weak; Series C and later are usually too big.
- **Leave out** deep tech, bio and hardware unless they asked for it, and anything they said to avoid.

Look a company up on the web only when the list leaves its fit genuinely unclear, and only for a handful. Then show the shortlist as a short table (company, round and date, a few words on why it fits) with one line on how many were left out and the main reasons. Ask them to confirm or strike any before you spend Prospeo credits.

## 4. Connect Prospeo

Skip this if `find_people` works. If it says Prospeo is not connected, explain that Prospeo finds the founders and their verified emails, from their own account, and that a free account comes with credits every month. Ask them to:

1. sign up at https://prospeo.io;
2. open https://app.prospeo.io/api and copy their API key;
3. paste it here.

Pass it to `connect_prospeo`. Tell them it is stored encrypted and how many credits the account has. Never repeat the key back.

## 5. Find the people

Before searching, say what it costs: about 1 credit for every 25 people searched, then 1 credit for each email found.

Call `find_people` once with every confirmed company's website (up to 100 a call). Ask for the next page only if `totalPages` is more than 1 and companies you need are missing. Pick one person per company, two at most:

- The one who would hire them. At a small startup that is the CEO or a founder. For an engineering or product role, a CTO or technical co-founder is as good.
- Skip titles like "Founding Designer" or "Founding Account Executive": early employees, not founders. Also skip "Owner" or "Founder" entries that are plainly another business, people marked `alreadyAContact`, and every company `onDoNotContactList`.
- Prefer people with `hasVerifiedEmail: true`. Leave out those without one: no email would be found for them.

## 6. Add them

Build a CSV with the columns Name, Title, Company, Website, LinkedIn, Timezone, Stage, Last Round, Tier and Notes, one row per person:

- **Stage** is the round type (Seed, Series A); **Last Round** is its amount and date, like `$4M (2026-08-12)`.
- **Timezone** comes from the person's result.
- **Tier** is `A?`.
- **Notes** says in one line why the company fits, for the research that comes later.

Quote any field that contains a comma. Pass the CSV to `import_contacts` with a filename like `Crunchbase picks 2026-10-19`, then call `find_emails` to look up their emails in the background.

Tell them in two or three lines how many people were added, at which companies, and that emails are being found now. Then offer to start drafting (the `outreach:draft` skill) once the emails are in: `get_status` shows how many still need one.
