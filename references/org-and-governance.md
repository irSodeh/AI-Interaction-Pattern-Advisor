# Organizational Layer and Governance

The part that decides whether the pattern survives contact with the organization. Read this when writing the organizational, metrics, and pilot sections of the report — and always when the context is enterprise.

---

## 1. Risk tiering

Tier the use case before arguing about autonomy. The tier sets what evidence and oversight is required, not whether the project is allowed.

| Tier | Description | What it demands |
|---|---|---|
| **Minimal** | Internal productivity, reversible, no effect on individuals | Light monitoring, sampled review |
| **Limited** | Customer-facing but advisory; person can disregard the output | Disclosure that it's AI, escalation path, quality sampling |
| **High** | Affects access, money, employment, health, legal standing, or opportunity | Human decision retained, explanation surface, appeals route, bias testing, documentation, logged decisions |
| **Prohibited-adjacent** | Manipulative, covertly monitoring, or inferring sensitive attributes without basis | Redesign the use case; this is not a governance problem to be managed |

Jurisdictions differ and the rules move. Flag the tier and the questions to bring to legal or risk. Do not rule on legality — name the exposure precisely enough that the right person can.

Two questions that decide the tier faster than any framework: *does an individual experience a consequence from this output?* and *can they contest it?*

---

## 2. Who owns what

Every recommended pattern needs these four named. Unnamed roles are the most reliable predictor of quiet failure.

- **Experience owner** — the pattern's design, its scope statement, and its evolution
- **Operational owner** — day-to-day performance: cost, latency, queue depth, escalations. This is the role most often missing.
- **Content/data owner** — corpus freshness, permissions, retirement of stale sources. Non-negotiable for patterns 9 and 11.
- **Risk owner** — tiering, audit trail, incident response, the authority to pull the pattern back a level

If the same person holds all four in a large organization, note it as a risk, not a virtue.

---

## 3. Reviewer capacity math

Before recommending a review queue (pattern 6) or any human-in-the-loop design, do this arithmetic explicitly in the report. It is the single most common unexamined assumption in enterprise AI.

```
items/day × minutes/review ÷ 60 = reviewer-hours/day needed
reviewer-hours available = FTEs × productive hours × share of role allocated to review
```

Productive review hours are roughly 5–6 per FTE-day, not 8, and review is fatiguing — quality falls measurably in long unbroken sessions.

If demand exceeds supply, only four honest options exist. Name which one is being chosen:
1. Reduce volume entering review (confidence thresholds, sampling by category)
2. Reduce time per review (diff-first UI, ordering, batch actions)
3. Increase capacity (hire, reallocate, and say whose work stops)
4. Raise autonomy for proven categories, with evidence

The dishonest fifth option — leaving the queue underserved — is what actually happens by default, and it converts governance into rubber-stamping. Say this plainly.

---

## 4. Role redesign and change management

An AI pattern moves work. Name where it moves, in the report.

- **What disappears** — the tasks the pattern absorbs. Be honest; euphemism destroys trust with the people affected.
- **What appears** — reviewing, exception handling, prompt and policy tuning, monitoring, corpus maintenance. This work is real and usually unbudgeted.
- **What changes character** — production becomes judgment; volume work becomes exception work. This is a genuine skills shift, not a small adjustment, and it suits some people far better than others.
- **What the affected group needs** — early involvement, a truthful account of headcount intent, training on the new work, and a voice in the escalation design. Involving reviewers in designing the review UI is the cheapest trust investment available.

Adoption failure is nearly always a change-management failure wearing a UX costume. When the user's problem is "people aren't using it," check role clarity, incentives, and trust before redesigning the interface.

---

## 5. Metrics tree

Build the measurement plan top-down so every interaction metric ladders to something the sponsor funded.

```
Business outcome        cost-to-serve, revenue, cycle time, risk exposure
        ↑
Service outcome         resolution rate, throughput, quality, satisfaction
        ↑
Interaction outcome     acceptance, edit distance, override, abandonment
        ↑
System health           latency, cost/interaction, drift, availability
```

**Trust metrics deserve their own line.** They are leading indicators and they degrade before the business metrics do:
- Reviewer agreement rate — falling means the model or the corpus is drifting
- Dwell time on approvals — near-zero means rubber-stamping
- Override rate — near-zero can mean excellent, or blind acceptance. Disambiguate by sampling overrides that *should* have happened.
- Complaint and appeal volume from affected individuals

**Always name a counter-metric** — the number that must not move while the primary improves. Deflection up with resolution down. Throughput up with error rate up. Speed up with appeals up. Without a counter-metric, any pattern can be declared a success.

---

## 6. Degradation and failure design

Every recommendation must answer: what does the service do when the AI is unavailable, wrong, or untrusted?

- **Unavailable** — is there a non-AI path, and does the staff still know how to run it? Six months after launch, often not. Say who keeps it exercised.
- **Wrong at scale** — how is a systematic error detected, how far does it propagate before detection, and what is the remediation and notification path?
- **Untrusted** — if users stop believing it, does the service still function or does it collapse? Patterns where the human path has been dismantled are fragile in a way that doesn't show up until it matters.

The organizations that recover well from AI incidents are the ones that designed the fallback before they needed it.

---

## 7. Pilot design

The recommendation ends in a pilot, not a program. A good pilot is designed to be *falsifiable*.

- **Narrowest slice that still produces the real signal** — one category, one team, one segment. Narrow enough to ship in weeks.
- **A stated hypothesis about the pattern** — "review-and-approve at L2 cuts handling time by a third without raising the error rate" is testable. "Improve efficiency with AI" is not.
- **A pre-agreed kill or downgrade condition** — what result would make you abandon this pattern? Agree it before the data exists, when it's still cheap to be honest.
- **Baseline captured first.** Most pilots fail to prove anything because nobody measured the before.
- **Include the long tail deliberately.** Curated pilots produce results that don't survive general release.
- **Name what the pilot does not test** — scale, cost at volume, the second-order behavior change. Being explicit here prevents over-reading a good result.

---

## 8. Enterprise constraints worth surfacing early

Ask about these when they're load-bearing; a pattern that violates them is dead on arrival regardless of design quality.

- **Data residency and cross-border processing** — often determines the deployment shape before anything else
- **Permission inheritance** — retrieval that ignores source-system permissions is a data incident, not a bug
- **Retention and logging** — audit needs conflict with minimization; someone must decide, and it's rarely the product team
- **Vendor and model dependency** — what happens when the model version changes underneath a tuned pattern
- **Procurement and approval timelines** — these often set the real project timeline; design the pilot to fit inside them
- **Works councils, unions, or employee representation** — where workforce monitoring or role change is involved, engagement is required early, not at launch
