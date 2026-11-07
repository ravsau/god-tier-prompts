# Rules for agents and contributors in this repo

This repo is a short list of prompts that people have tested. Keep it short.

## Do not inflate the list

- A prompt goes into `prompts/` only when it is goated and vouched: at least 3 different people, other than the author, ran it on their own work and posted a public receipt (PR, issue, commit, or a screenshot of the output). Links to those posts go on the prompt's page under "Who vouched for it".
- Likes, views and "great prompt" replies are not a vouch. A vouch shows a result: bugs found, a refactor, a number.
- It is fine if the collection has fewer than five prompts. Do not add prompts to make the list look bigger. Do not write new prompts yourself and add them.
- Prompts with promise but no public results go into `candidates.md`. Move one to `prompts/` only after the vouches exist.
- Longer variants of an existing prompt go on that prompt's page, not into a new file.

## Intake

- New prompts arrive as "Suggest a prompt" issues (label `candidate`) and get a line in `candidates.md`.
- Receipts arrive as "Vouch for a prompt" issues (label `vouch`) or comments. Open each link and check that it shows a result before you add it to a page.
- A well-known name does not replace a receipt. When a known engineer or project posts a receipt, list it first.
- Prompts for general decisions or learning, not for a coding agent working on a repo, do not belong here.

## Each prompt page has

1. The prompt, exactly as first posted, in a code block.
2. Where it came from, with a link to the first post.
3. What it means, in plain words, with one small example.
4. Who vouched for it, with links and a short quote of what they found.
5. Optional: a longer version and what to do with the results.

## Writing

- Plain words for a global audience. Define any term the first time you use it.
- Quote people exactly. Mark cuts with `[...]`. Do not add results that the source does not show.
- No em dashes.
