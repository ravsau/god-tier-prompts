# God Tier Prompts

Short prompts for coding agents that do a lot of work for their size. One sentence, no skill file, no setup.

This started from a reply to Steve Ruiz's prompt on X, where Bootoshi wrote: "we need a collection of God tier prompts like this. not skills [...] i want a single sentence". This repo is that collection.

Each prompt has its own page with the prompt, where it came from, what it means in plain words, and a longer version for when you want a structured report.

## The prompts

| # | Prompt | What it finds |
|---|---|---|
| 01 | [`find all of the implicit state machines in my app`](prompts/01-implicit-state-machines.md) | Hidden states and transitions spread across flags, timestamps and `if` checks, and the bugs they cause |

## How to use them

1. Open your coding agent (Claude Code, Codex, Cursor or similar) in the root of your repo.
2. Paste the prompt as it is.
3. Read the report before you let the agent change anything.

## Add one

Open a pull request with a new file in `prompts/`. A prompt belongs here if it is one sentence and people who ran it can show what it found. Credit the person who first posted it.

## Credits

- Prompt 01: [Steve Ruiz](https://x.com/steveruizok), Oct 31, 2026.
- The idea for the collection: [Bootoshi](https://x.com/KingBootoshi).

Collected by Saurav Sharma ([CloudYeti](https://www.youtube.com/@cloudyeti)).

learn.cloudyeti.io

Book 1:1 consulting: cloudyeti.io/meet
