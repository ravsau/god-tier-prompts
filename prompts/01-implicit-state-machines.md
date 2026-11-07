# 01. Find the implicit state machines

```
find all of the implicit state machines in my app
```

Ten words. Paste it into Claude Code, Codex, Cursor or any coding agent that can read your repo.

## Where it came from

Steve Ruiz ([@steveruizok](https://x.com/steveruizok)) [posted it on X](https://x.com/steveruizok/status/2116552016218710389) on Oct 31, 2026 with the words "good prompt". The post passed 1.1M views.

## Who vouched for it

People who credited the prompt and showed what it found:

- [Lars Trieloff](https://github.com/trieloff) (Adobe) [posted](https://x.com/trieloff/status/2116867892797165660): "'find all the implicit state machines in my app' is a fantastic prompt. Thanks for the suggestion, @steveruizok". His audit of Adobe's [helix-opspile](https://github.com/adobe/helix-opspile/issues/233) found that only one table has a real status column. The rest of the state lives in nullable timestamps, leases and in-memory flags. Its first known defect: a reply can post twice on Retry.
- [Luke Parker (@LukeParkerDev)](https://x.com/LukeParkerDev/status/2118036671513964648), who works on opencode: "Try it!! Merged 15 opencode desktop PRs so far and about 250 more implicit state machines are migrating too". His PRs on [anomalyco/opencode](https://github.com/anomalyco/opencode/pull/61718) include a rule that lifecycle state must use explicit state machines. GitHub search finds 161 merged PRs by him in that repo that mention "state machine", opened since Oct 30, 2026 (GitHub search API, read 2026-11-07).
- [Trevin Chow (@trevin)](https://x.com/trevin/status/2118690987153186845), with a longer version of the prompt: "This is an amazing prompt that helps find a ton of bugs for me."
- [Garrett Petersen (@GarrettPetersen)](https://x.com/GarrettPetersen): "Major refactor as a result of this. Also adding 'no implicit state machines' to my agent skills. Simply knowing the phrase 'implicit state machine' is the kind of thing that pays off in the age of vibe coding."
- [Yahia Bakour (@mynameisyahia)](https://x.com/mynameisyahia): "I genuinely hate how many bugs this found. Run it. Now."
- [Daniel Lockyer (@DanielLockyer)](https://x.com/DanielLockyer) posted a screenshot of his agent's summary: "I found about 70 implicit state machines. [...] spread across request handlers, Stripe web[...]"
- [Ben Kremer (@bkrem_)](https://x.com/bkrem_): "Confirming that this is a goated prompt, so much mileage out of a handful of words. (Opus 5.5 high)"

### Public refactors since the prompt went around

These PRs and issues do not name the prompt, but they do the exact audit it asks for. GitHub search finds 399 pull requests that mention "implicit state machine" from Oct 31 to Nov 7, 2026, against 74 in the 30 days before. (GitHub search API, read 2026-11-07.)

- [Georgios Konstantopoulos](https://github.com/gakonst) (Paradigm) opened PRs on [Foundry](https://github.com/foundry-rs/foundry/pull/18228) and [Alloy](https://github.com/alloy-rs/alloy/pull/4504): "Many lifecycles in Foundry were encoded implicitly, as bools or Options that are only valid in certain combinations, sentinel values, or flags kept in sync by hand." Each one becomes an enum, "so illegal combinations can no longer be represented".
- [Hyperlane](https://github.com/hyperlane-xyz/hyperlane-monorepo/pull/9971), by Paul Balaji: lifecycle state spread across flags, nullable resources, retry deadlines and queues could "lose ownership, publish stale state, resurrect stopped services [...] or replay already-confirmed mutations".
- [Flanksource Mission Control](https://github.com/flanksource/mission-control/issues/3678): a cancelled or timed-out playbook run could go back to scheduled when an in-flight action finished.
- [Darkroom Engineering's Claude settings](https://github.com/darkroomengineering/cc-settings/pull/298): they made it a rule, so Claude spots the pattern while writing, flags it in review, and can map every case in an app on request.
- [Hyperion](https://github.com/usehyperion/hyperion/pull/317): "refactor: remove implicit state machines", merged Nov 3, 2026.

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

Another long version from the replies, by [pooomj (@Dyikhyi56)](https://x.com/Dyikhyi56), that also asks for fixes:

```
Reverse-engineer my codebase: uncover hidden state machines, broken invariants, implicit contracts and bottlenecks. Stress-test failures, retries and concurrency. Prove what's broken, then find the smallest changes that eliminate entire classes of bugs and complexity.
```

## What to do with the results

You do not need a state machine library such as XState to fix most findings. For the top few:

1. Write the valid states and transitions down in one place, for example one enum and one `canTransition(from, to)` function.
2. Add a guard where the state changes, so an invalid move fails loudly.
3. Write a test for each transition, and one test for each invalid state the audit found.

Run the audit again after a few weeks of new features.

## Keep new ones out

The prompt finds implicit state machines after they exist. [Pps831](https://x.com/Pps831) asked for a matching rule so the agent does not create them, and Garrett Petersen added "no implicit state machines" to his agent skills. Put this in your repo's `CLAUDE.md` or `AGENTS.md`:

```
No implicit state machines. When something can change state over time (a
subscription, an upload, a job, an auth session), store it as one explicit
status field with a written list of allowed transitions, and check that list
at every place the state changes. Do not add a new boolean or timestamp that
silently creates a new state.
```
