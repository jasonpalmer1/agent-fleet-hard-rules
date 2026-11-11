# Builder brief

Use for one piece of code work, owned by one worker until it is ready for review. Keep the filled brief near 2,000 characters.

```
ROLE: builder. You may write code and push a branch. You may NOT merge, deploy or send anything.
GOAL: <one sentence: what is true when this is done>
DONE MEANS: <the one check that proves it, and who or what runs it>
REPORT: write to <absolute path of report file>. Line 1 = DONE | PARTIAL | NOT DONE, plus one sentence.

SOURCE: "<the owner's exact words, or the ticket line, that this work comes from>"

START FROM: a fresh copy of <repository> at commit <commit id> in <absolute work folder>.

DO (each line names its source):
1. <requirement>  [source: <owner's words | ticket line>]
2. <requirement>  [source: <...>]
Do not add anything else. If something looks missing, say so in the report. Do not build it.

FACTS, checked by the lead at <time>:
- <fact, and how it was checked>
FACTS, not checked:
- <fact the worker should confirm before relying on it>

COMMANDS (copied from a run that worked; run exactly as written, do not change flags):
  <command> <flag> <value>     # value is a: file path | commit id | plain text
If a command refuses, do NOT retry with different flags. Report the exact refusal.

TESTS YOU MUST RUN BEFORE REPORTING:
- Real data: <what real input to use>
- Small screen: <width to check, if anything is visible>
- Bad input: <the bad case that must not break>
- Must BLOCK: <what the change must refuse>
- Must still ALLOW: <what must keep working>

IF THE BRIEF LOOKS WRONG: stop that step, do not improvise. Write "BRIEF PROBLEM: <what, and the right form if you can see it>" on line 2 of the report.

HOUSE SHELL RULES: <paste yours, for example: absolute paths only; one command per call; no in-place stream edits>

BUDGET: about <N> tool calls. At <cap>, stop and report what you have.

LAST LINES OF THE REPORT (copy exactly, fill in):
BRANCH: <name>  TIP: <commit id>  BASE: <commit id>
CLEANUP: <what you removed and the proof it is gone>
NEEDS-OWNER: none | <one line ask>
```

## Before you send it

- [ ] The piece is free: no other worker holds it.
- [ ] Every path and commit id in the brief exists right now.
- [ ] Every requirement has a source. Anything without one is deleted.
- [ ] This is more than a one-command job. If not, script it.
- [ ] Effort is medium unless you can write down why not.
