# Pattern Library

Eleven AI interaction patterns. For each: what it is, when it fits, when it fails, what the UI must provide, what the organization must provide, and the metric that tells you it's working.

Read the fit/fail sections before recommending. The failure conditions are more diagnostic than the fit conditions — most bad pattern choices are visible in the failure list, not the fit list.

**Contents**
1. Conversational assistant
2. Inline copilot
3. Natural-language command
4. Delegated agent
5. Ambient intelligence
6. Review queue (draft-and-approve)
7. Guided adaptive flow
8. Generative canvas
9. Grounded Q&A with citations
10. Scenario / what-if advisor
11. Invisible AI in the pipeline
+ Composition notes

---

## 1. Conversational assistant

**What it is.** An open text surface. The user states intent in natural language; the system responds and holds context across turns.

**Fits when**
- The task space is genuinely open-ended — you cannot enumerate the controls
- Users arrive with wildly varied, unpredictable intents
- The user's problem is ill-formed and needs to be shaped through dialogue
- Expressing the request in words is genuinely faster than navigating a UI

**Fails when**
- The task is structured and finite. A four-field form beats a conversation every time. This is the most common misapplication in enterprise work.
- Users don't know what the system can do — an empty box with no affordances produces "what can you do?" and then abandonment
- The output needs to be precise, comparable, or auditable
- Latency is high and the user is mid-task

**UI must provide.** Visible scope statement (what it can and can't do), starter intents or examples, graceful "I don't know" rather than invention, context transparency (what it remembers), and an exit to a human or a structured path.

**Org must provide.** Content and knowledge ownership, an escalation path with real capacity behind it, conversation review sampling, and a policy on what the assistant may commit the organization to.

**Watch.** Abandonment after first turn, escalation rate, repeat-question rate.

---

## 2. Inline copilot

**What it is.** Suggestions surfaced inside the user's existing work surface — ghost text, next-action suggestion, inline rewrite, code completion.

**Fits when**
- The user is already producing an artifact and the AI accelerates the next increment
- The user has the expertise to judge the suggestion instantly
- Suggestions are cheap to accept and cheaper to ignore
- High frequency, low stakes per instance

**Fails when**
- The user lacks the expertise to evaluate the suggestion — then it becomes silent authority, not assistance
- Suggestions interrupt flow or steal keystrokes
- The artifact is high-stakes and a wrong suggestion propagates invisibly

**UI must provide.** Zero-cost dismissal, clear visual distinction between AI-generated and human-authored content, single-keystroke accept, and no modal interruption.

**Org must provide.** A position on authorship and accountability for AI-influenced output, and — where it matters — provenance retained in the record.

**Watch.** Acceptance rate, edit distance after acceptance (high acceptance with heavy editing means the suggestion is a starting point, not a completion — different value story), dismissal fatigue.

---

## 3. Natural-language command

**What it is.** The user expresses a goal in words; the system maps it to a deterministic operation and executes it. The AI does interpretation, not judgment.

**Fits when**
- The system has many capabilities buried in menus and navigation is the bottleneck
- The action set is finite and deterministic
- The user knows what they want but not where it lives
- You want AI's flexibility without AI's unpredictability in the outcome

**Fails when**
- The mapping is ambiguous and misfires are expensive
- The user needs to discover capabilities rather than recall them
- The action is irreversible and there's no confirmation step

**UI must provide.** Show the interpreted action before executing ("I'll do X to Y — confirm"), a fallback to normal navigation, and undo.

**Org must provide.** A maintained action registry; when new capabilities ship, the language mapping ships with them.

**Watch.** Misinterpretation rate, confirmation-rejection rate, share of actions initiated by command vs navigation.

---

## 4. Delegated agent

**What it is.** The user hands over a multi-step goal. The agent plans, uses tools, and works over an extended horizon, checking in at defined points.

**Fits when**
- The task is genuinely multi-step and tool-using
- The user's time is better spent elsewhere while it runs
- Steps are individually verifiable, and the work is reversible or sandboxed
- The cost of a wasted run is bounded

**Fails when**
- Actions are irreversible and consequential — this is the hard ceiling
- The user can't verify the work afterward (verification is harder than doing it)
- The environment is unstable and failure modes are unbounded
- There's no meaningful checkpoint design, so it's autonomy by default

**UI must provide.** A visible plan before execution, progress that shows what's being done and why, an interrupt that actually stops work, checkpoint approvals at consequential steps, and a full trace afterward. The trace is the product as much as the result is.

**Org must provide.** Scoped credentials and least-privilege tool access, a spend/action budget per run, audit logging, an owner for agent behavior in production, and an incident path for when an agent does something wrong at scale.

**Watch.** Completion rate without intervention, intervention points per run, cost per completed task, and — most important — the rate of confidently-wrong completions.

---

## 5. Ambient intelligence

**What it is.** AI running continuously in the background, surfacing something only when it matters: anomaly alerts, digests, proactive flags, auto-enrichment.

**Fits when**
- The user wouldn't know to ask, but the answer matters when it occurs
- Monitoring is continuous and human attention is not
- The signal-to-noise ratio can be tuned high enough to preserve trust

**Fails when**
- Precision is low. Alert fatigue kills the pattern permanently — recovering trust after a noisy launch is far harder than launching late.
- There's no clear action attached to the signal
- It creates surveillance dynamics over employees or customers. Treat this as a design red line, not a tuning parameter.

**UI must provide.** Every alert paired with a recommended action, tunable sensitivity in the user's hands, a reason for the flag, and an easy "this wasn't useful" that actually changes behavior.

**Org must provide.** Ownership of the alert stream, a response SLA (an unactioned alert stream is worse than none), and a workforce-monitoring policy where employees are involved.

**Watch.** Precision (dismissal rate), action-taken rate, time-to-detection, and the trend in dismissal over time.

---

## 6. Review queue (draft-and-approve)

**What it is.** AI produces at volume; humans approve, edit, or reject in a batched queue. The workhorse pattern of enterprise AI, and the most under-designed.

**Fits when**
- Volume is high and per-item human production is the bottleneck
- The quality bar requires human judgment but not human authorship
- Batching is acceptable — no realtime constraint
- Reviewing is meaningfully faster than producing

**Fails when**
- Reviewing takes as long as producing. Then you've added a step, not removed one — check this with a stopwatch before committing.
- Reviewer capacity doesn't exist. The queue silently becomes autonomy.
- Reviewers have no authority or no context to disagree — rubber-stamping.
- Items are heterogeneous enough that reviewers can't build rhythm.

**UI must provide.** Diff-first presentation (what the AI changed or asserted, not a wall of text), confidence-based ordering so scarce attention goes where it's needed, keyboard-fast approve/reject, a required reason on reject that feeds training, and batch actions for the confident tail.

**Org must provide.** Honest reviewer capacity math (see `org-and-governance.md`), a role definition for the reviewer that isn't just "their old job plus this", and a graduated autonomy plan — the queue should shrink as confidence is earned, by category, with evidence.

**Watch.** Reviewer agreement rate, dwell time per item (near-zero dwell is rubber-stamping), edit rate by category, and queue depth trend.

---

## 7. Guided adaptive flow

**What it is.** A structured, stepwise flow where AI determines the path, the next question, or the branching — an intelligent wizard. Structured output, adaptive route.

**Fits when**
- The outcome must be structured and complete (an application, an assessment, an intake)
- The path genuinely varies by respondent and static branching would be unmanageable
- Users need scaffolding — they don't know what matters
- Compliance requires that specific things were asked and answered

**Fails when**
- A static form would do. Adaptive complexity has real maintenance cost.
- The branching logic can't be explained or audited
- Users need to see the whole shape upfront to prepare

**UI must provide.** Progress that stays honest even when the path is dynamic, back-navigation without losing answers, a way to see and edit everything before submission, and reasons for unusual questions.

**Org must provide.** Ownership of the question logic including its fairness properties, and — where regulated — an auditable record of why each path was taken.

**Watch.** Completion rate, drop-off by step, downstream data quality, and disparity in path assignment across groups.

---

## 8. Generative canvas

**What it is.** A working surface where direct manipulation and generation coexist: documents, designs, diagrams, spreadsheets, code workspaces. The artifact is the interface.

**Fits when**
- The output is a substantial artifact the user will iterate on
- Both fine manual control and broad generative moves are needed
- The user's intent emerges through making rather than specifying

**Fails when**
- The output is small or one-shot — chat or inline is lighter
- Generation overwrites manual work unpredictably. This is the trust-killer for this pattern.
- Version history is absent

**UI must provide.** Scoped generation (act on selection, not everything), reliable versioning and undo across generative steps, clear provenance of which regions are generated, and preservation of manual edits through subsequent generations.

**Org must provide.** Storage and version policy, IP and licensing position on generated content, and template/design-system governance so output stays on-brand.

**Watch.** Iterations to acceptable output, share of final artifact retained from generation, undo frequency immediately after generation.

---

## 9. Grounded Q&A with citations

**What it is.** Questions answered from a defined corpus, with citations back to source. Enterprise knowledge access.

**Fits when**
- The answer exists in documents and finding it is the bottleneck
- The user must be able to verify — regulated, technical, or high-consequence contexts
- The corpus is maintained and has an owner

**Fails when**
- The corpus is stale, contradictory, or has no owner. The pattern will faithfully surface the contradictions and be blamed for them.
- The question requires judgment or synthesis beyond what the documents contain
- Access permissions aren't respected per-user — a retrieval system that ignores document permissions is a data breach waiting to happen

**UI must provide.** Citations at the claim level, not a source list at the bottom; visible corpus scope and freshness; an explicit "not in the corpus" answer; and one click to the source in context.

**Org must provide.** Corpus ownership and a freshness SLA, permission inheritance from the source systems, a content lifecycle (who retires outdated documents), and feedback routing from wrong answers back to content owners.

**Watch.** Citation click-through (low can mean high trust or blind trust — disambiguate with sampling), answer-not-found rate, and time-to-answer versus the prior baseline.

---

## 10. Scenario / what-if advisor

**What it is.** AI models options and consequences; the human decides. Decision support, explicitly not decision-making.

**Fits when**
- The decision is consequential and must remain human
- Multiple variables interact in ways that are hard to hold in the head
- The value is in seeing the shape of the option space, not in getting an answer

**Fails when**
- The model's assumptions are hidden. Then it's an oracle with a chart, and the human is deciding on false precision.
- Users read the modeled scenarios as predictions
- The decision is actually routine and this is ceremony

**UI must provide.** Editable assumptions surfaced as first-class controls, uncertainty ranges rather than point estimates, side-by-side comparison, and sensitivity — which variable actually moves the outcome.

**Org must provide.** Model documentation and assumption review, a stated position that accountability stays with the human decision-maker, and a record of what was modeled at the time of decision.

**Watch.** Whether assumptions get edited (if never, users aren't engaging, they're accepting), decision reversal rate, and post-hoc calibration of the modeled ranges.

---

## 11. Invisible AI in the pipeline

**What it is.** Classification, routing, scoring, extraction, or prioritization inside the system, with no direct user-facing moment.

**Fits when**
- The task has no natural human moment and no human would add value
- Volume is very high and per-item stakes are low
- Errors are caught downstream or are cheaply reversible
- Speed and consistency matter more than nuance

**Fails when**
- The decision affects a person's rights, money, access, or opportunity with no explanation surface. Increasingly a legal problem in regulated jurisdictions, not merely an ethical one.
- Errors compound silently downstream
- Nobody monitors drift, because there's no user to complain

**UI must provide.** Nothing to the end user — but an operator surface is mandatory: distributions, drift, override logs, and sampled review.

**Org must provide.** Monitoring ownership, a drift and recalibration schedule, an appeals or correction route where individuals are affected, and documentation adequate for audit.

**Watch.** Distribution drift, downstream correction rate, and disparity metrics across affected groups.

---

## Composition notes

Real services rarely need one pattern. Common, well-behaved compositions:

- **Support/service journey** — invisible triage (11) → grounded Q&A for self-serve (9) → review queue for agent-drafted replies (6) → delegated agent (4) only for narrow reversible actions like address changes or refunds under a threshold
- **Knowledge work** — grounded Q&A (9) for retrieval → generative canvas (8) for production → inline copilot (2) for refinement
- **Operations and back office** — invisible extraction (11) → review queue (6) with graduated autonomy → ambient anomaly detection (5) over the whole flow
- **Intake and onboarding** — guided adaptive flow (7) for the structured path → conversational assistant (1) as an escape hatch for the confused → invisible scoring (11) for routing
- **Analysis and planning** — grounded Q&A (9) → scenario advisor (10) → generative canvas (8) for the resulting artifact

Two rules for compositions:
1. **One pattern owns each moment.** Overlapping patterns at the same moment confuse users and diffuse ownership.
2. **Autonomy is set per moment, not per product.** The same service can be L1 at the decision point and L4 at the routing step. Blanket autonomy statements are a sign nobody has thought about it.
