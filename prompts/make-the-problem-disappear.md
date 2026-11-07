# Make the problem disappear

```
What higher-level abstraction would make this entire problem disappear?
```

Status: candidate. It moves into the list when 3 people, other than the author, post a public receipt.

## Where it came from

Wyrmfalls [posted it on X](https://x.com/Wyrmfalls/status/2118826627408830479) on Nov 6, 2026, as the last of five prompts in a reply to [Bootoshi's call](https://x.com/KingBootoshi/status/2118803776387928228) for god tier prompts. Bootoshi [replied](https://x.com/KingBootoshi/status/2118838510874714159): "last one is a banger TY".

## What it means

An abstraction is a layer that hides details behind a simpler interface: one type, one function, one module. "Higher-level" means it sits above the code that has the problem. "Make this entire problem disappear" asks for a design where the bug cannot happen, instead of a fix for one case.

For example, an app has a dozen bugs where a price shows in the wrong currency. Twelve fixes are twelve patches. A `Money` type that always carries its currency makes the whole class of bug impossible.

Related candidate: [issue #1](https://github.com/ravsau/god-tier-prompts/issues/1) asks the same question across a whole codebase.

## Who vouched for it

No receipts yet. Bootoshi's reply is praise, not a receipt.
