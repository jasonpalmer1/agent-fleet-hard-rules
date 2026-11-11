# Gate (review) brief

Use for one independent review of one exact change. A strong reviewer is strict and slow (measured on Fable): plan for about 20 to 30 minutes and about twice the tokens of a lighter model. In our data its failures were right every time we could check, so send it only work that has already passed its own pre-checks.

```
ROLE: reviewer, read-only. You may run tests in your own copy. You may NOT edit the change, push, merge or deploy.
GOAL: decide whether this exact change is safe to ship.
REPORT: write to <absolute path of verdict file>. Line 1 = PASS | PASS WITH NOTES | FAIL PRODUCT | FAIL TEST-ONLY.

THE CHANGE: <repository>, base <commit id>, tip <commit id>, change fingerprint <hash>.
Review this change only. If the tip has moved, stop and say so.

WHAT IT IS MEANT TO DO: "<the owner's words or ticket line>"
MUST BLOCK: <what the change must refuse>
MUST STILL ALLOW: <what must keep working>

EVIDENCE FROM THE REAL WORLD (not just the code): <where the real usage data, logs or screenshots are>
Check the change against this evidence first. A fix aimed at the wrong place fails even if the code is clean.

PRE-CHECK STATE:
- checked by the lead at <time>: <which checks are green, with the record path>
- not checked: <which checks nobody has run on this tip>
Do not trust this section. Re-run the cheapest check yourself and say if it disagrees.

ROUND: this is review round <n> of <limit>. Earlier findings: <path, or "none">.
On a re-review, confirm each earlier finding is fixed before looking for new ones.

HOW TO FAIL IT: every finding has a file, a line, a way to reproduce it, and a size (blocks shipping | note only).
"FAIL TEST-ONLY" means the product is right and only the tests are wrong or missing.

SAFETY: never run a command you are testing against real files; never print secrets or environment values.

IF THE BRIEF LOOKS WRONG: write "BRIEF PROBLEM: <what>" on line 2 and review what you can.

BUDGET: about <N> tool calls. At <cap>, stop and give the verdict you can support.

LAST LINES OF THE REPORT (copy exactly, fill in):
VERDICT: <same word as line 1>
REVIEWED: base <commit id> tip <commit id> fingerprint <hash>
CLEANUP: <what you removed and the proof it is gone>
```

## Before you send it

- [ ] There is a green pre-check record for this exact tip.
- [ ] No other reviewer is already on this change.
- [ ] Review rounds used are under the limit. At the limit, a judge decides cut or continue; do not send another reviewer.
- [ ] The brief points at real-world evidence, not only at the code.
- [ ] Effort is high. This is a judging role.

## After it reports

Read line 1 and the "blocks shipping" findings. Pass the verdict FILE PATH to the next tool, never the verdict words.
