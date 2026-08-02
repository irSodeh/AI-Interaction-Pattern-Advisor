# Worked Example — Enterprise

A complete run of this skill against a realistic enterprise brief. Read it to calibrate depth, tone, and the level of specificity expected. Do not copy its conclusions — copy how it reasons.

The example is deliberately a case where the user arrives with the wrong solution already chosen, because that is the most common real situation.

---

## The brief as it arrived

> "We're a mid-size insurer, about 400 people. Motor claims. We want to put an AI agent in the claims process so it can handle claims end-to-end — customer files the claim, agent assesses it, pays out. Our handlers are drowning; average claim takes 11 days. Leadership has approved budget for an agentic solution. Can you design the AI experience?"

## Step 1 — What was asked, and why

Four questions, not more. Note that each one is aimed at a variable that changes the answer, not at general context-gathering.

1. **"Walk me through one claim end to end — where do the 11 days actually go? Is it handler work time, or is it waiting on documents, third parties, and repair quotes?"**
   *Why:* if the bottleneck is waiting, an agent that works faster changes nothing. This single question frequently invalidates the whole brief.

2. **"When a payout decision is wrong — too high, too low, or wrongly rejected — what happens? Who finds out, how fast, and can it be reversed?"**
   *Why:* reversibility sets the automation ceiling before any pattern is chosen.

3. **"Of your monthly claim volume, what share are low-value, single-vehicle, documented, no-injury, no-dispute? And what share are the messy ones?"**
   *Why:* the answer determines whether one pattern or a segmented set of patterns is right. Almost always the latter.

4. **"How many handlers do you have, what would their job be if AI drafted the assessment, and has anyone told them the plan?"**
   *Why:* reviewer capacity and role redesign decide whether the pattern survives month three.

**The answers that came back:** 11 days breaks into ~2 days of handler work and ~9 days of waiting on documents, garages, and third-party insurers. Wrong payouts are recoverable in principle but recovery is expensive and generates complaints; wrongful rejections carry regulatory exposure. Roughly 55% of volume is low-value, documented, uncontested; 20% is genuinely complex; 25% is in between, usually because a document is missing or unreadable. 38 handlers, no communication to the team yet, and leadership has not decided whether this is headcount reduction or capacity relief.

---

## Step 2 — The report

### The job to be done

Get a motor claim from first notice to a correct, explained decision faster — where "faster" for the customer means less waiting and fewer chase calls, and for the business means less handler time per claim without an increase in wrong decisions or complaints. The stated brief was an end-to-end agent; the evidence points elsewhere, and this report says why.

*Assumption stated:* leadership's intent on headcount is unresolved. That decision changes the change-management design substantially, and it should be made before pilot communication, not after.

### Diagnosis

- **The binding constraint is not handler speed.** 9 of 11 days are waiting. An agent that assesses in seconds moves 2 days, not 11. The largest available win is in the waiting: chasing documents, reading them the moment they arrive, and telling the customer where things stand without a phone call.
- **Reversibility is weak.** Payouts are recoverable but costly; rejections carry regulatory exposure and an appeals duty. That caps autonomy on the decision itself at L3, permanently, regardless of measured accuracy.
- **Volume is segmented, so autonomy must be too.** 55/25/20 is not one problem. Applying one pattern to all three segments is the core error in the original brief.
- **Reviewer capacity exists but is unbudgeted.** 38 handlers is real capacity; whether they are given review time is a decision nobody has made.
- **Regulatory tier is High** for the decision moment — a claim decision affects an individual's money, and they must be able to contest it.

### Recommended pattern

**A composition, not one pattern. Autonomy set per moment.**

| Moment | Pattern | Level | Rationale |
|---|---|---|---|
| Intake / FNOL | 7 Guided adaptive flow | L2 | Structured, compliance-bound output; path varies by incident type; captures the right documents on the first attempt, which is where waiting is created |
| Document handling | 11 Invisible AI | L4 | Classify, extract, check completeness. No human moment, reversible, high volume. This attacks the 9 days directly. |
| Chasing & status | 5 Ambient intelligence | L4 | Detects a stalled claim and acts — chases the garage, updates the customer proactively. The single highest-leverage change and the one nobody asked for. |
| Assessment | 6 Review queue | L2 | AI drafts the assessment with evidence and a reasoned figure; handler decides. High volume, human quality bar, batchable. |
| Decision & payout | 6 Review queue | **L3 ceiling** | Explicit human approval per decision. Not negotiable at the current reversibility and risk tier. |
| Customer questions | 9 Grounded Q&A | L2 | Policy wording and claim status, cited. Not open chat — the corpus is the policy. |

**The one place a delegated agent (4) belongs:** the simple segment's *document chase* — a bounded, reversible, multi-step task with a clear stop condition. Not the claim decision.

### Runner-up, and the switch condition

**Straight-through processing (11 Invisible, L5) for the simple segment.** Genuinely viable — many insurers run it — but only after evidence. The switch condition, stated as a threshold rather than a feeling: for the low-value uncontested segment, once the review queue shows ≥95% handler agreement with the drafted figure across ≥2,000 consecutive claims, with complaint rate flat and no disparity signal across customer segments, move that segment to L4 with sampled audit at 10%. Not before, and not for any other segment.

### What you should not build here

**An end-to-end agentic claims handler.** Three reasons, in order of severity:

1. It targets 2 days of an 11-day problem. The budget would be spent on the smaller half.
2. The decision moment is high-risk and weakly reversible. Full autonomy there is a regulatory problem, not a design tradeoff — and no accuracy number fixes it, because the exposure is in the inability to explain and contest.
3. A single agent across a segmented volume will be tuned for the average claim and fail the 20% complex tail, which is exactly where cost and complaint risk concentrate.

The honest reframing for leadership: the same budget, spent on waiting-time patterns and a review queue, produces a larger measurable result with a fraction of the risk exposure. That is a better story to tell the board than "we built an agent."

### Interaction blueprint (assessment moment)

| Moment | What the handler sees | What the system does | If it goes wrong |
|---|---|---|---|
| Entry | Queue ordered by confidence, lowest first; simple segment batched | Drafts assessment, attaches evidence, flags gaps | Missing document → item is held out of queue, chase triggered, not drafted on incomplete data |
| During | Draft figure with its components; each component links to the source document line | Retrieves policy terms, prior similar claims, repair benchmarks | Low confidence on a component → shown unfilled with a reason, never guessed |
| Output | Handler approves, edits, or rejects with a required reason | Records decision, provenance, and edit delta | Edit exceeds a threshold → routed to a second reviewer |
| Correction | Edit inline; reason codes feed a weekly quality review | Logs the delta by category | Repeated same-category edits → category is demoted a level automatically |
| Failure | Clear "assess manually" path with full documents attached | Falls back cleanly, no partial state | System unavailable → the manual path is the same path, so handlers stay fluent in it |

### Trust and control mechanics

1. **Component-level evidence, not a summary.** The handler must be able to see which line of which document produced each number. A total with a confidence score is not reviewable.
2. **Explicit unfilled fields.** Where the model is uncertain, the field is empty with a reason. Plausible guesses in an assessment are the specific failure mode that produces rubber-stamping.
3. **Reject with a reason code, mandatory.** This is the training signal and the quality audit trail in one.
4. **Customer-facing explanation generated from the same evidence** that the handler saw — so the explanation given at appeal matches the basis of the decision. This is the regulatory requirement doing double duty as a design constraint.
5. **Dwell-time monitoring on approvals**, surfaced to the ops owner weekly. Below a floor, the queue has stopped being oversight.

### Organizational implications

- **Roles:** handler work shifts from production to judgment and exception handling. New work appears and must be staffed: reason-code review, corpus and benchmark maintenance, queue monitoring. Roughly one FTE-equivalent of new work that nobody has budgeted. The 20% complex segment becomes the core of the senior handler role — which is a genuine upgrade, and should be communicated as one only if it's true.
- **Ownership:** four names needed. Experience owner (claims product), operational owner (claims ops — this is the one currently missing), content owner (policy wording and repair benchmarks), risk owner (compliance, with authority to demote a category).
- **Governance:** High tier at the decision moment. Required: logged decisions with evidence, an appeals route, disparity testing across customer segments, and model documentation. Data residency and the retention conflict between audit and minimization need a decision from someone outside the product team.
- **Reviewer capacity, explicitly:** at ~1,400 claims/month, 45% needing meaningful review at ~6 minutes each, that's ~63 hours/month — under one FTE, comfortably within 38 handlers. Capacity is not the constraint; *allocation* is. If review time is not carved out of the handler role, it will be absorbed into the gaps and quality will fall silently.
- **Degradation:** the manual path is preserved because it is the same path. Systematic error is detected via weekly agreement-rate review; the remediation path — identify affected claims, re-decide, notify — should be written before launch, not after the first incident.

### How you'll know it's working

| Layer | Metric | What good looks like |
|---|---|---|
| Interaction | Handler agreement with drafted figure | Rising, then stable above 90% by segment |
| Interaction | Approval dwell time | Above a floor. Falling toward zero is a warning, not a win. |
| Service | Cycle time, split into work time and waiting time | Waiting time falls first and falls most — that's the thesis |
| Service | Inbound status calls per claim | Down sharply; the ambient pattern's real proof |
| Trust | Complaint and appeal rate | Flat. **This is the counter-metric.** |
| Trust | Disparity in outcomes across customer segments | No drift |
| Business | Cost per claim; leakage (over- and under-payment) | Cost down without leakage moving |

**The counter-metric is load-bearing:** cycle time can be improved by deciding faster and worse. If appeals rise while cycle time falls, the pilot has failed, whatever the dashboard says.

### First move

An 8-week pilot on the **low-value uncontested segment only**, with two of the six patterns: invisible document handling (11) and ambient chasing (5), plus the review queue at L2 for assessment. No agent, no customer-facing chat.

- **Hypothesis:** cycle time on this segment falls from 11 days to under 6, driven mainly by waiting time, with handler agreement above 90% and complaint rate flat.
- **Baseline first:** four weeks of current-state measurement before anything ships. Most claims pilots cannot prove their result because nobody measured the before.
- **Kill condition, agreed in advance:** if handler agreement stays below 80% after four weeks of tuning, or if complaints rise at all, the assessment draft is pulled and the pilot continues on document handling and chasing alone — which would still be a real win.
- **Include the tail deliberately:** 20% of pilot volume drawn from the messy segment, not to automate it, but to see how the patterns degrade.
- **What this pilot does not test:** cost at full volume, behavior of the complex segment, and the second-order effect on handler skill over time.

---

## What to notice about this example

- The recommendation **contradicted the brief**, with reasoning the sponsor can take to their board. That is the skill working, not the skill being difficult.
- The **binding constraint came from a question, not a framework.** Ask where the time actually goes before recommending anything.
- **Autonomy was set per moment** — L4 on documents, L3 ceiling on decisions — rather than as a single product-level statement.
- The **organizational sections carry real arithmetic and real names**, not principles. "Reviewer capacity is important" is worthless; "63 hours/month, capacity exists, allocation doesn't" is actionable.
- The **counter-metric is named and made load-bearing**, so the pilot can fail honestly.
- The **highest-value pattern was one nobody asked for** — ambient chasing. Look for these; they are usually in the waiting, not in the working.
