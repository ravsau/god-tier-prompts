# Make it simpler and dumber

```
Please step back and think again. How can we make this SIMPLER and DUMBER while still achieving our goals?
```

Status: candidate. It moves into the list when 3 people, other than the author, post a public receipt.

## Where it came from

Simon Last, a co-founder of Notion, [posted it on X](https://x.com/simonlast/status/2033949482539487467) on Mar 17, 2026, in a list of his favorite prompt snippets for coding. He uses it "For iterating on a spec".

## What it means

Agents tend to add things: more layers, more options, more config. This prompt asks for the opposite and keeps the goal fixed.

- "SIMPLER" asks it to remove parts.
- "DUMBER" asks for the obvious, boring solution instead of a clever one.
- "while still achieving our goals" stops it from dropping a requirement to get there.

For example, a spec for notifications has a queue, a retry service and per-user rules. The simpler and dumber version might send the email inside the request and write failures to one table that someone checks each day.

## Who vouched for it

No receipts yet.
