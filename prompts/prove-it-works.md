# Prove it works

```
Prove to me this works
```

Status: candidate. It moves into the list when 3 people, other than the author, post a public receipt.

## Where it came from

Boris Cherny, who created Claude Code, [posted it on X](https://x.com/bcherny/status/2017742752566632544) on Jan 31, 2026, as tip 6 in a thread of tips from the Claude Code team: "Or, say "Prove to me this works" and have Claude diff behavior between main and your feature branch".

## What it means

"It works" is a claim. "Prove" asks for evidence. The agent has to run the code and show you the result: a diff of behavior between `main` and your branch, a test that failed before and passes now, or the real output of a command. If it cannot prove it, you find out before the merge, not after.

For example, the agent fixes a date bug and says "Fixed." You reply "Prove to me this works." It runs the old and the new code on the same inputs and shows you which outputs changed.

## Who vouched for it

- [SergeForge](https://x.com/SergeForge/status/2113294630003388632), Oct 22, 2026: "i finally put two of these to the test. "prove it works" caught bugs in 3/3 runs."
