# 01. Find the implicit state machines

```
find all of the implicit state machines in my app
```

Ten words. Paste it into Claude Code, Codex, Cursor or any coding agent that can read your repo.

## Where it came from

Steve Ruiz ([@steveruizok](https://x.com/steveruizok)) posted it on X on Oct 31, 2026 with the words "good prompt". The post passed 1.1M views. People who ran it on their own code replied:

- Yahia Bakour: "I genuinely hate how many bugs this found. Run it. Now."
- Daniel Lockyer posted a screenshot of his agent's summary: "I found about 70 implicit state machines. [...] spread across request handlers, Stripe web[...]"
- Ben Kremer: "Confirming that this is a goated prompt, so much mileage out of a handful of words. (Opus 5.5 high)"

## What it means

A state machine is two things: the states something can be in, and the rules for moving from one state to the next.

Your app is full of them. A user is logged out, logging in, logged in, or expired. A payment is pending, paid, failed, or refunded. An agent task is queued, running, waiting for a tool, done, or failed.

The state machine is **implicit** when nobody wrote it down. There is no `status` enum with a list of allowed moves. Instead, the state lives in a mix of booleans, timestamps, nullable columns and `if` checks, spread across many files.

Here is a subscription that looks like normal code:

```js
if (subscription.status === "active") {
  allowAccess();
}

if (subscription.cancelledAt) {
  showCancellationBanner();
}

if (subscription.trialEndsAt < Date.now()) {
  showUpgradePrompt();
}
```

Under those three checks there is a full state machine: trial, active, past due, cancelled, expired. Nothing in the code says which moves between them are allowed, so the code allows moves nobody planned.

## The bugs it finds

When the states are implicit, the app can reach combinations that should never exist:

- A cancelled user still has access, because `status` says active and `cancelledAt` is set at the same time.
- A failed payment starts a new free trial.
- A webhook that arrives late moves an account back to an older state.
- Two requests at the same time each apply a different transition.

Linters and unit tests rarely catch these, because each `if` is correct when you read it alone. The bug is in how the pieces combine.

## Why it matters more with AI-written code

Coding agents are good at adding one feature at a time. After a few weeks of that, the app has business logic that nobody designed as a whole. Each feature added one flag or one timestamp. This prompt asks the agent to rebuild the model of how your app actually behaves, instead of reviewing the code line by line.

## A longer version

The short prompt works well. If you want a report you can act on, use this:

```
Audit this codebase for implicit state machines.

Find workflows where states and transitions are encoded indirectly through
booleans, enums, timestamps, status fields, conditionals, or async events.

For each workflow:
1. List the states and the valid transitions.
2. Point to the relevant files and lines.
3. List invalid or contradictory states the current code allows.
4. Look for race conditions, missing transitions, and inconsistent state handling.
5. Rank the findings by real bug risk.
6. Say whether an explicit state machine would help, or whether simple conditionals are enough.

Do not modify code. Put concrete issues before theoretical ones.
```

## What to do with the results

You do not need a state machine library such as XState to fix most findings. For the top few:

1. Write the valid states and transitions down in one place, for example one enum and one `canTransition(from, to)` function.
2. Add a guard where the state changes, so an invalid move fails loudly.
3. Write a test for each transition, and one test for each invalid state the audit found.

Run the audit again after a few weeks of new features.
