# Decision Matrix

How to get from a situation to a pattern and an automation level. Read this before recommending.

---

## Part 1 — The eight axes

Score each axis. You will usually find that two of them are binding and the rest are context. Lead the diagnosis with the binding ones.

**1. Cost of error × reversibility** *(the ceiling-setter)*
Low cost, reversible → high autonomy is available. High cost, irreversible → the human stays in the decision, full stop.
The critical question is reversibility, not accuracy. A 99%-accurate irreversible action is worse than a 90%-accurate reversible one. Ask: "what does undo look like here?" If there's no answer, the automation ceiling is L2.

**2. Task structure**
Enumerable inputs and a finite outcome set → structured patterns (3, 6, 7, 11). Open-ended, unpredictable intent → conversational or canvas (1, 8).
Test: could you draw the form? If yes, the form is the baseline the AI pattern must beat.

**3. Frequency × volume**
Rare and high-stakes → guided flow or scenario advisor, heavy scaffolding, low autonomy (7, 10).
Frequent and low-stakes → inline, ambient, invisible (2, 5, 11).
High-volume and quality-bound → review queue (6). This is where most enterprise ROI actually lives.

**4. User expertise**
Expert users can evaluate suggestions instantly → copilot and canvas work well.
Novices cannot judge output quality → suggestions become silent authority. Novices need grounding, citations, and structure (7, 9), not open generation.
Ask specifically: can this user tell a good output from a plausible bad one, in the time they'll actually spend?

**5. Groundedness**
Is the answer in a corpus you control? → grounded Q&A (9), low hallucination surface.
Does it require synthesis beyond available data? → the pattern must expose uncertainty, and autonomy drops.

**6. Latency tolerance**
Sub-second need → inline, invisible, command (2, 3, 11).
Seconds are fine → chat, Q&A, canvas (1, 8, 9).
Minutes-to-hours acceptable → delegated agent, review queue, ambient (4, 5, 6). Async patterns unlock far more capability per interaction; check whether the realtime requirement is real or assumed.

**7. Auditability and regulation**
If a decision must be explainable to a regulator, a court, or an affected individual, invisible AI (11) and high autonomy are off the table without an explanation surface and a record. Determinism requirements push toward command (3) and guided flow (7) over free generation.

**8. Organizational readiness** *(the most-skipped axis)*
Does reviewer capacity exist? Does someone own this in production? Is there an escalation path with real humans behind it? Does the workforce see this as augmentation or replacement?
A pattern the organization cannot operate is the wrong pattern, regardless of its elegance. Downgrade the recommendation to what they can actually run, and name the readiness gap as the thing to fix.

---

## Part 2 — The automation ladder

Autonomy is a level, not a switch. Set it per moment in the journey, and make the ladder itself the roadmap: earn each step with evidence.

| Level | Name | Who acts | Human role | Typical fit |
|---|---|---|---|---|
| **L0** | Manual | Human | Does everything | Baseline to beat |
| **L1** | Suggest | Human | Sees an option, decides | Novel domain, low trust, high stakes |
| **L2** | Draft | AI produces, human finishes | Editor and author of record | High volume, human quality bar |
| **L3** | Execute on approval | AI acts after explicit confirmation | Approver per action | Consequential but routine |
| **L4** | Execute and notify | AI acts, human can undo | Monitor with undo | Reversible, high volume, proven accuracy |
| **L5** | Full autonomy | AI acts | Audits samples, owns the system | Low stakes, very high volume, or mature and measured |

**Rules that keep this honest**

- **Reversibility sets the ceiling.** No undo → maximum L3. This is not negotiable by accuracy improvements.
- **Start one level below where the data says you can.** Trust is asymmetric: earned slowly, lost in a single incident.
- **Promote by category, not globally.** "Invoices under X from known vendors move to L4" is a real decision. "The agent is now autonomous" is not.
- **Demotion must be as easy as promotion.** Define in advance the metric threshold that drops a category back a level, and who can pull it.
- **L4/L5 requires monitoring that L1-L3 doesn't.** If nobody is watching the aggregate, you have not reached L4 — you have reached unobserved L5.

---

## Part 3 — Axis profile → candidate patterns

Use as a starting shortlist, then pressure-test with the failure conditions in `pattern-library.md`.

| If the situation is… | Start with | Then consider |
|---|---|---|
| Open intent, expert user, no fixed output | 1 Conversational | 8 Canvas |
| User already authoring, high frequency | 2 Inline copilot | 8 Canvas |
| Rich feature set, navigation is the bottleneck | 3 NL command | 1 Conversational |
| Multi-step, tool-using, reversible, async | 4 Delegated agent | 6 Review queue |
| Continuous monitoring, no natural trigger | 5 Ambient | 11 Invisible |
| High volume, human quality bar, batchable | 6 Review queue | 11 Invisible + graduated autonomy |
| Structured outcome, variable path, compliance | 7 Guided flow | 1 Conversational as escape hatch |
| Substantial artifact, iterative production | 8 Canvas | 2 Inline copilot |
| Answer lives in documents, verification needed | 9 Grounded Q&A | 1 Conversational over the same corpus |
| Consequential human decision, many variables | 10 Scenario advisor | 9 Grounded Q&A |
| No human moment, very high volume, low stakes | 11 Invisible | 5 Ambient for oversight |

**Overrides that beat the table**

- Irreversible + high stakes → drop autonomy first, then pick the pattern. Never the other way around.
- No reviewer capacity → do not recommend 6 without also recommending how capacity gets created. Otherwise you have designed unmonitored autonomy.
- Stale or unowned corpus → 9 is not available yet. The first move is content ownership, not retrieval.
- Regulated decision affecting individuals → 11 requires an explanation surface bolted on, which usually means it becomes 6 or 10 in practice.
- The task is a form → say so. Recommending no AI at a given moment is a legitimate and often the strongest output of this skill.

---

## Part 4 — Pressure tests before finalizing

Run these four questions against the recommendation. If any answer is weak, revise before writing the report.

1. **The 20th percentile case.** Not the demo case — the messy, ambiguous, long-tail one. Does the pattern degrade gracefully or embarrassingly?
2. **The undo test.** Walk the worst plausible error end-to-end. Who notices, how fast, and what do they do? If the answer involves heroics, the autonomy level is too high.
3. **The Tuesday test.** It's an ordinary Tuesday, six months in, the launch team has moved on. Who owns this, who watches the metrics, and who fixes it? If nobody, it's an orphaned pattern.
4. **The beat-the-baseline test.** Compare against the boring alternative — a form, a saved search, a template, a better-written policy. If the AI pattern doesn't clearly win on the user's actual bottleneck, say so.
