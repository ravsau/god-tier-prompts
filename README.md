# God Tier Prompts

Short prompts for coding agents that do a lot of work for their size. One sentence, no skill file, no setup.

This started from a reply to [Steve Ruiz's prompt on X](https://x.com/steveruizok/status/2116552016218710389), where Bootoshi wrote: "we need a collection of God tier prompts like this. not skills [...] i want a single sentence". This repo is that collection.

## The bar

This list stays small on purpose. A prompt gets in only when it is goated and vouched:

1. It is one sentence, or close to it.
2. At least 3 different people (not the author) ran it on their own work and posted a public receipt: a PR, an issue, or a screenshot of what it found. Likes and "great prompt" replies do not count.
3. The page names who vouched for it, with links to the receipts.

It is fine if this list has fewer than five prompts for a long time. One prompt that people have tested is worth more than fifty that sound clever. Prompts that look promising but have no public results yet wait in [candidates.md](candidates.md).

## The prompts

| # | Prompt | What it finds | Vouched by |
|---|---|---|---|
| 01 | [`find all of the implicit state machines in my app`](prompts/01-implicit-state-machines.md) | Hidden states and transitions spread across flags, timestamps and `if` checks, and the bugs they cause | Lars Trieloff (Adobe), Garrett Petersen, Yahia Bakour, Daniel Lockyer, Ben Kremer, plus public refactors in Foundry, Alloy and Hyperlane ([receipts](prompts/01-implicit-state-machines.md#who-vouched-for-it)) |

## Lines for your coding agent's system prompt

The prompts above find problems after they exist. These lines go in your repo's `CLAUDE.md` or `AGENTS.md` so the agent does not create the problem in the first place.

```
No implicit state machines. When something can change state over time (a
subscription, an upload, a job, an auth session), store it as one explicit
status field with a written list of allowed transitions, and check that list
at every place the state changes. Do not add a new boolean or timestamp that
silently creates a new state.
```

Garrett Petersen [did a major refactor](prompts/01-implicit-state-machines.md#who-vouched-for-it) after running prompt 01 and added "no implicit state machines" to his agent skills.

## How to use them

1. Open your coding agent (Claude Code, Codex, Cursor or similar) in the root of your repo.
2. Paste the prompt as it is.
3. Read the report before you let the agent change anything.

## Add one

1. Open a ["Suggest a prompt"](../../issues/new?template=new-prompt.yml) issue with the prompt, who first posted it, and your own receipt. It becomes a candidate.
2. If you ran a prompt from here or from `candidates.md`, open a ["Vouch for a prompt"](../../issues/new?template=vouch.yml) issue with a link to the result.
3. When a candidate has 3 receipts from different people, open a PR to move it into `prompts/`.

Details in [CONTRIBUTING.md](CONTRIBUTING.md).

## Credits

- Prompt 01: [Steve Ruiz](https://x.com/steveruizok/status/2116552016218710389), Oct 31, 2026.
- The idea for the collection: [Bootoshi](https://x.com/KingBootoshi).

Collected by Saurav Sharma ([CloudYeti](https://www.youtube.com/@cloudyeti)).

learn.cloudyeti.io

Book 1:1 consulting: cloudyeti.io/meet
