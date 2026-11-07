# Contributing

The collection grows through receipts, not through votes or follower counts.

## What makes a prompt god tier

The brief for this repo came from [Bootoshi](https://x.com/KingBootoshi):

> we need a collection of God tier prompts like this
>
> not skills I DON'T CARE ABOUT YOUR SKILLS
>
> i want a single sentence of vectors so juicy each verb, noun, and adjective act like flavorful curry bombs BURSTING with information that a simple prompt ends up being VERY impactful

In practice, a prompt must pass these checks:

1. **One sentence.** No skill file, no setup, no multi-step template. If it needs a document to work, it is a skill, not a prompt for this repo.
2. **Every word does work.** Remove any word and the result gets worse. Filler like "you are an expert" or "make no mistakes" fails this check.
3. **At least one loaded term.** It uses a precise term the model already knows well, which pulls in a whole body of knowledge. In prompt 01, "implicit state machines" tells the agent what to look for, where it hides, and what bugs it causes, all in three words.
4. **It finds or changes something real.** It produces a result you can check in your own code, not advice.

## How a prompt gets in

1. **Suggest it.** Open a "Suggest a prompt" issue, or a draft PR that adds the prompt's page to `prompts/`. Either one gets the `candidate` label. Open candidates are the waiting list. Give a 👍 to the ones you want in.
2. **Collect receipts.** People who run it comment on the candidate issue or PR with a public link to what it found.
3. **Promote it.** When a candidate has receipts from at least 3 different people (not the author), it goes into `prompts/` with those receipts on its page. For an issue, open a PR that closes the issue. For a candidate PR, add the receipts and merge it.

## What counts as a receipt

A public link that someone else can open and check:

- a pull request or issue that fixes or lists what the prompt found,
- a post with a screenshot of the agent's output,
- a commit that cites the prompt.

Likes, views, and "great prompt" replies are not receipts. A well-known name does not replace a receipt. When a known engineer or project does post a receipt, it goes first on the page, because readers trust those the most.

## Vouching for a prompt that is already in

Use the "Vouch for a prompt" issue. Good receipts get added to the prompt's page.
