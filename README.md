# Agent Fleet Hard Rules

Hard rules for a lead agent that hands work to worker agents, on any model: how to write the brief, when to spawn, when not to, and how to check the result without paying for it twice.

Every rule comes from a measured case in one real week of agent-fleet work (about 4,600 spawn attempts, about 3,000 finished worker reports, 10 billion billed tokens). Nothing here is theory. Where the sample is small, we say so.

These rules began as a playbook for one model, Fable. We now apply them to every agent we run, whatever the model. Each number below still names the model it was measured on.

## The short version

A strong worker does what the brief says, exactly, and tells you when the brief is wrong. That is the whole rule set in one line. A loose brief used to get quietly patched over by the worker. Now it gets built as written, or stopped and flagged. So the lead's brief is the thing to fix, for every agent.

## The 15 rules

Each rule has a test you can run on a brief or a transcript.

### Writing the brief

**1. Goal, done-test and report path go in the first five lines. Keep the brief near 2,000 characters.**
Why: our Fable briefs had a median of 1,969 characters and none was refused for a missing section; the week before, 356 briefs were refused at launch for shape.
Test: can a stranger say what "done" means after reading five lines?

**2. Paste command lines from a run that worked. Never write them from memory. Say what each value is (file path, commit id, text).**
Why: a "land this branch" brief passed the review result as words where the tool wanted the path of the result file. The tool refused. The worker ran the brief's command exactly, did not guess a fix, and reported the right form. One spawn and 251,000 tokens bought nothing.
Test: every flag value in the brief exists on disk or resolves as a commit.

**3. Every requirement names where it came from: the owner's words or the ticket line. End the list with "Do not add anything else."**
Why: a brief carried one requirement the lead had made up. Fable built it, and flagged that it reversed an earlier deliberate decision. The branch was thrown away: 1.66 million tokens, 46 tool calls.
Test: delete any requirement with no source. Does the owner miss it?

**4. Mark each fact "checked at (time)" or "not checked".**
Why: a review brief said the pre-checks were green when one was red, and a build brief had the calendar week off by one. Both workers found out the slow way.
Test: no bare claims about the state of a branch, a test or a date.

**5. Put the house shell rules in the agent definition, up front. A refusal half-way through a job is the most expensive way to teach a rule.**
Why: our own guards refused 12.7% of all worker tool calls in the Sonnet week and 4.3% under Fable; 29 of 30 Fable workers still hit at least one. Each refusal is a wasted round trip.
Test: count guard refusals per worker. Target is under one.

**6. Paste the exact closing lines the report must end with.**
Why: 4.2% of Sonnet workers (125 of 2,984) had to be woken again only to add one required line. Fable workers: 0 of 24.
Test: zero re-wakes whose only output is "report now has the line".

**7. Say what to do when the brief looks wrong: stop that step, do not improvise, write the problem on line 2 of the report.**
Why: half of Fable reports (12 of 24) raised something for the lead to decide, against 21% for Sonnet. That is the feature. Give it a fixed place to land.
Test: every brief has an "if the brief looks wrong" line.

### Spawning

**8. Check the preconditions before you spawn: is the piece free, is there a green pre-check for this exact commit, is there review budget left.**
Why: 8 of 9 refused Fable launches were this. Each refused launch costs one full lead-agent call (median 153,000 tokens of context) and a turn.
Test: launch refusals for "already owned" or "not ready" are zero.

**9. Do not spawn for a one-command job. Script it or do it in the lead.**
Why: the cheapest spawn we measured cost 251,000 tokens for 9 tool calls. A lead call costs about 153,000.
Test: no worker finishes in under 10 tool calls.

**10. Batch read-and-prove work of the same shape into one worker. Never batch unrelated builds.**
Why: one Fable worker went through 94 open tickets and closed 11 on checked proof for 4.7 million tokens, about 0.4 million per close. The fleet average the week before was about 20 million per close.
Test: same-shape checks share a worker; each build has exactly one.

**11. One builder owns one piece until it is ready for review. Cap builder spawns per piece, then stop and decide.**
Why: 156 of 406 pieces took six or more spawns; one took 29. Most of the cost of a piece is the handing back and forth.
Test: spawns per closed piece. Ours was 6.7. Lower is better.

**12. First line of the brief says read-only or builder. Read-only workers end with "nothing deployed, merged, sent or changed".**
Why: read-only work is safe to batch and cheap to check; a builder is neither. Mixed briefs are where unasked changes came from.
Test: the role line is present and the tools given match it.

### Cost and checking

**13. High effort only for roles that judge: reviewer, judge, research, root-cause. Medium for builders and mechanical work.**
Why: high-effort Fable workers had a median of 5.3 million tokens and 15 minutes; medium-effort ones 1.7 million and 6 minutes. This is not a clean test, since the roles differ, but it is the biggest cost dial we found.
Test: no builder or mechanical role runs at high effort without a written reason.

**14. Give every role a tool-call cap: a nudge, then a hard stop with "report what you have".**
Why: each extra tool call cost about 42,000 billed tokens under Fable (94,000 under Sonnet), because the whole conversation is re-read each time. One uncapped sweep used 189 calls.
Test: the 90th-percentile tool count per role sits under its cap.

**15. Check a report with its first ten lines plus one thing that cannot be faked: the file exists, the commit is on the branch, the result file's first line.**
Why: 97.9% of launched workers delivered a report, so the report is usually there. What matters is whether its one key claim is true, and that is one cheap look, not a re-read.
Test: the lead spends under five tool calls per report.

## What we measured

| Measure | Sonnet workers, 7 days | Fable workers, first day |
|---|---|---|
| Spawn attempts | 4,273 | 55 |
| Refused at launch | 28.7% (about 19% without a harness glitch) | 16.4% |
| Refused for brief shape | 356 | 0 |
| Finished workers measured | 2,984 | 30 |
| Billed tokens per worker, median | 2.29 million | 4.11 million |
| Reviewer: tokens / minutes / tool calls | 3.03 million / 9.6 / 51 | 5.76 million / 22.7 / 78 |
| Review pass rate | 64% of 687 | 44% of 9 |
| Review failures later upheld | not measured | 5 of 5 |
| Tool calls refused by our own guards | 12.7% | 4.3% |
| Reports that flag a decision for the lead | 21% | 50% |
| Re-wakes only to fix the report | 4.2% | 0 of 24 |
| Tool calls per model call | 1.16 | 1.8 |

Plain reading: a Fable reviewer costs about 1.9 times the tokens and 2.4 times the minutes of a Sonnet reviewer, fails more work, and was right every time we could check. It does not go off-brief (0 unasked actions in 24 reports read by hand). Four of 30 Fable runs lost time to a mistake in the lead's brief.

## Limits of this data

- The Fable sample is one day and 30 finished workers, 9 of them reviewers. Treat every Fable number as early.
- Fable reviewers were mostly judging work built by Sonnet. We have no pass rate yet for work Fable built.
- There is no like-for-like builder comparison: the first Fable builder jobs were small.
- There is no clean high-versus-medium effort test.
- "Billed tokens" counts every token on every call, including cached re-reads.

## Templates

- `templates/brief-builder.md`
- `templates/brief-gate.md`
- `templates/brief-research.md`

Fill in the angle brackets. Delete nothing; a line you cannot fill is a line you have not checked.

## Updates

- A second file, `RULES.md`, will be added when the tested guard set lands: the same hard rules, each paired with the automatic check that enforces it. It is not published yet.

## License

MIT. See `LICENSE`.
