# Research brief

Use for one question that ends in a written answer. Read-only. Research of the same shape can share a worker; a research worker never builds.

```
ROLE: researcher, read-only. You write one report. Nothing is deployed, merged, sent or changed.
QUESTION: <the one question, in the owner's words: "...">
THE ANSWER WILL BE USED TO: <the decision this feeds>
REPORT: write to <absolute path of report file>. Line 1 = the answer in one sentence. Under <N> lines.

READ FIRST (in this order):
1. <our own numbers: which records, which date range>
2. <outside sources allowed: which sites or documents>

METHOD:
- Our own numbers before anyone else's. Give the source and date range for each number.
- Label every number "measured" or "guess". For a guess, show the arithmetic.
- Say what you could not see and why. A blocked page is recorded and skipped, never worked around.
- Say how small the sample is.

FENCES:
- May read: <folders, records>
- May NOT read: <folders, records>
- No outward sends. No logins. No secrets or environment values in any output.
- Huge files: search them, never read them whole. <name the huge ones>

OUTPUT SHAPE:
1. Answer first, with the two or three numbers that carry it.
2. A table of what was measured.
3. Options ranked by payoff per day of work, each with its risk and the test that would prove it.
4. Open questions only the owner can answer, one line each.

IF THE BRIEF LOOKS WRONG: write "BRIEF PROBLEM: <what>" on line 2 and answer the nearest question you can.

BUDGET: about <N> tool calls. At <cap>, stop and write up what you have.

LAST LINES OF THE REPORT (copy exactly, fill in):
TOP PICK: <one line, and why>
NEEDS-OWNER: none | <one line ask>
CLEANUP: <what you removed and the proof it is gone, or "nothing downloaded">
```

## Before you send it

- [ ] The question is one question. Two questions are two briefs, or one brief with two numbered parts of the same shape.
- [ ] You have named the records to read. "Look around" doubles the tool calls.
- [ ] The line limit and the first-line rule are in the brief, so the report can be checked in ten lines.
- [ ] Effort is high. This is a judging role.
