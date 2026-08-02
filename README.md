# AI Interaction Pattern Advisor

A Claude Skill that answers the question most AI projects skip: **not "can we build it," but "how should this show up in the experience, and at what level of autonomy?"**

Most failed enterprise AI work is not a model problem. It is a **pattern problem**: the right capability delivered through the wrong interaction, at the wrong level of automation, inside a journey nobody redesigned.

This skill turns Claude into a senior Service Designer / AI Transformation advisor. It interrogates the brief, picks the interaction pattern (or composition of patterns), sets autonomy per moment, and outputs a decision document that a product lead and a risk officer can both read in five minutes.

---

## Who this is for

| Audience | What they get out of it |
|---|---|
| **Service & Product Designers** | A rigorous way to argue for or against an AI feature, with the failure modes named before the build starts |
| **AI Transformation & Innovation leads** | A repeatable method for turning "we should use AI" into a scoped, governable, measurable intervention |
| **Product Managers & Owners** | A pattern choice and an automation level they can defend to a sponsor, plus a falsifiable pilot design |
| **Enterprise Architects & AI/ML leads** | The experience and organizational constraints that should shape the architecture, surfaced before commitment |
| **Operations & Service leaders** | Honest reviewer-capacity arithmetic and role-change implications, not a vendor's efficiency slide |
| **Risk, Compliance & Governance** | Risk tiering, explainability requirements, appeals routes, and audit needs stated at design time |
| **Consultants & Agencies** | A structured deliverable for AI opportunity assessments and journey redesign engagements |
| **Founders & startup teams** | A check against the default reflex of shipping a chat box on top of an existing product |

If you are choosing between a chatbot, a copilot, an agent, or no AI at all — you are the audience.

---

## What it gives you

- **Stops the default chatbot reflex.** Names when a form, a saved search, or a better-written policy beats the AI feature. "Build no AI here" is a legitimate — and often the strongest — output.
- **Challenges the brief instead of decorating it.** Most teams arrive with the solution already chosen. The skill evaluates that choice honestly rather than styling it.
- **Finds the binding constraint first.** If 9 of your 11 days are waiting rather than working, a faster agent moves the smaller half of the problem. One well-aimed question surfaces this; no framework does.
- **Sets autonomy per moment, not per product.** L4 on document handling and an L3 ceiling on the decision is a design position. "The agent will be autonomous" is not.
- **Makes reversibility the ceiling, not accuracy.** A 99%-accurate irreversible action is worse than a 90%-accurate reversible one. The skill enforces this.
- **Carries the organizational cost into the recommendation.** Roles that change, work that appears, ownership that must be named, reviewer hours that must actually exist.
- **Does the reviewer-capacity arithmetic out loud** — the single most common unexamined assumption in enterprise AI, and the one that quietly converts human-in-the-loop into rubber-stamping.
- **Names the counter-metric.** The number that must *not* move while the primary improves, so a pilot can fail honestly instead of being declared a success.
- **Designs a falsifiable pilot** with a baseline, a hypothesis, and a kill condition agreed before the data exists.
- **Gives you shared language.** Naming an anti-pattern — *chatbot tax*, *AI sprinkle*, *human-in-the-loop as alibi*, *orphaned pattern* — moves a stakeholder conversation faster than a deck.
- **Speaks your language.** Ask in English, get English. Ask in Persian, get Persian, headings included.

---

## The eleven patterns

| # | Pattern | One-line fit test |
|---|---|---|
| 1 | **Conversational assistant** | The task space is open-ended and the user can't be given a finite set of controls |
| 2 | **Inline copilot** | The user is already producing something and AI accelerates the next stroke |
| 3 | **Natural-language command** | The user knows the goal, the system knows the actions, the gap is syntax |
| 4 | **Delegated agent** | Multi-step, tool-using work the user is willing to stop watching |
| 5 | **Ambient intelligence** | Nobody would think to ask, but the answer matters when it happens |
| 6 | **Review queue (draft-and-approve)** | Volume is high, the quality bar is human, and batching is acceptable |
| 7 | **Guided adaptive flow** | Structured outcome, but the path depends on the answers |
| 8 | **Generative canvas** | The artifact is the interface; direct manipulation plus generation |
| 9 | **Grounded Q&A with citations** | The answer exists in a corpus and the user must be able to verify it |
| 10 | **Scenario / what-if advisor** | A human decides, and needs the shape of the option space |
| 11 | **Invisible AI in the pipeline** | No human moment exists; AI classifies, routes, or scores upstream |

Real services usually need a **composition of two or three patterns across the journey**, not one. Each reference entry covers where the pattern fits, **where it fails**, what the UI must provide, what the organization must provide, and what to measure.

## The automation ladder

Autonomy is a level, not a switch — set per moment in the journey, and earned with evidence.

| Level | Name | Who acts | Human role |
|---|---|---|---|
| **L0** | Manual | Human | Does everything — the baseline to beat |
| **L1** | Suggest | Human | Sees an option, decides |
| **L2** | Draft | AI produces, human finishes | Editor and author of record |
| **L3** | Execute on approval | AI acts after confirmation | Approver per action |
| **L4** | Execute and notify | AI acts, human can undo | Monitor with undo |
| **L5** | Full autonomy | AI acts | Audits samples, owns the system |

**No undo → maximum L3.** Not negotiable by accuracy improvements.

---

## How it works

**1. Clarify** — two to four questions aimed at the variables that actually change the answer: the real job, cost of error and reversibility, frequency and volume, who the user is and what happens to their role.

**2. Diagnose** — score the situation on eight decision axes, find the binding constraint, segment the volume, and shortlist candidate patterns.

**3. Report** — a fixed structure: job to be done → diagnosis → recommended pattern and automation level → runner-up with a switch threshold → **what you should not build** → interaction blueprint → trust and control mechanics → organizational implications → metrics with a counter-metric → a falsifiable first pilot.

---

## Example

A mid-size motor insurer arrives with the brief already decided:

> *"We want an AI agent to handle claims end-to-end. Our handlers are drowning — average claim takes 11 days. Leadership has approved budget for an agentic solution."*

**The question that changed everything:** *where do the 11 days actually go?*
Answer: roughly **2 days of handler work and 9 days of waiting** on documents, garages, and third-party insurers. The requested solution targets the smaller half of the problem.

**Volume turned out to be segmented**, not homogeneous — 55% simple and uncontested, 25% missing a document, 20% genuinely complex. One pattern across all three is the core error in the brief.

**The recommendation was a composition, with autonomy set per moment:**

| Moment | Pattern | Level |
|---|---|---|
| Intake / FNOL | Guided adaptive flow | L2 |
| Document handling | Invisible AI | L4 |
| Chasing & status | Ambient intelligence | L4 |
| Assessment | Review queue | L2 |
| Decision & payout | Review queue | **L3 ceiling — permanent** |
| Customer questions | Grounded Q&A | L2 |

**What it advised against:** the end-to-end agent. It targets 2 days of an 11-day problem; the decision moment is weakly reversible and regulated, so full autonomy there is a legal exposure rather than a design tradeoff; and a single agent tuned for the average claim fails the 20% complex tail, where cost and complaint risk concentrate.

**The highest-value pattern was the one nobody asked for** — ambient chasing of stalled claims. The wins are usually in the waiting, not in the working.

**The organizational section carried arithmetic, not principles:** ~1,400 claims/month × 45% needing review × ~6 minutes ≈ **63 reviewer-hours/month**. Across 38 handlers, capacity exists — *allocation* doesn't. If review time isn't carved out of the role, it gets absorbed into the gaps and quality falls silently.

**The counter-metric was named and made load-bearing:** complaint and appeal rate must stay flat. Cycle time can always be improved by deciding faster and worse.

📖 **[Read the full worked example →](references/worked-example.md)**

---

## Anti-patterns it will name

- **Chatbot tax** — a conversation imposed on a task that had a perfectly good form
- **AI sprinkle** — a feature bolted onto an unchanged journey, so nothing improves
- **Human-in-the-loop as alibi** — a reviewer with no time, no context, and no authority to disagree
- **Autonomy without reversibility** — L4/L5 on actions that can't be undone
- **Ungrounded confidence** — fluent answers over a corpus that doesn't support them
- **Demo-to-production gap** — works at n=10 curated cases, collapses on the long tail
- **Orphaned pattern** — nobody owns it after launch, so drift and cost accumulate unwatched
- **Invisible AI where accountability is required** — a legal problem, not only a design one

---

## Installation

**Claude.ai / Claude Desktop**

1. Download or clone this repo
2. Zip the contents so `SKILL.md` sits at the root of a folder named `ai-interaction-pattern-advisor`, and rename the archive to `ai-interaction-pattern-advisor.skill`
3. Upload it in Claude and click **Save skill**

```bash
git clone https://github.com/irSodeh/AI-Interaction-Pattern-Advisor.git
cd AI-Interaction-Pattern-Advisor
mkdir -p /tmp/ai-interaction-pattern-advisor
cp -r SKILL.md references /tmp/ai-interaction-pattern-advisor/
cd /tmp && zip -r ai-interaction-pattern-advisor.skill ai-interaction-pattern-advisor
```

**Claude Code / Cowork** — place the folder in your skills directory:

```bash
git clone https://github.com/irSodeh/AI-Interaction-Pattern-Advisor.git \
  ~/.claude/skills/ai-interaction-pattern-advisor
```

## Usage

Just describe the situation. The skill triggers on its own:

- *"Should this be a chatbot or a copilot?"*
- *"Where does AI fit in our claims process?"*
- *"How much autonomy should this agent have?"*
- *"Our chatbot isn't working — what should we do instead?"*
- *"We want to add AI to onboarding. Design the experience."*
- Or invoke it directly with `/pattern`

Adapt the depth to the ask: a quick pattern question gets a tight answer with the reasoning visible; a real service redesign gets the full report.

---

## Repository structure

```
.
├── SKILL.md                          # Workflow, report template, anti-patterns, posture
├── references/
│   ├── pattern-library.md            # The 11 patterns — fit, failure, UI, org, metrics
│   ├── decision-matrix.md            # 8 decision axes, L0–L5 ladder, axis→pattern mapping
│   ├── org-and-governance.md         # Risk tiering, ownership, reviewer capacity, metrics tree, pilot design
│   └── worked-example.md             # Full enterprise run, with notes on why it works
├── README.md
└── LICENSE
```

Built on Claude's [Agent Skills](https://docs.claude.com/en/docs/agents-and-tools/agent-skills/overview) progressive-disclosure model — the reference files load only when the skill needs them.

---

## Scope and limits

This skill is about the **interaction design and organizational fit** of AI in a service.

It is **not** a model selection guide, not a prompt engineering guide, and **not legal advice**. Where a question turns on regulation, it flags the exposure and the questions to bring to legal or risk — it does not rule on them. Jurisdictions differ and the rules move.

The pattern taxonomy is opinionated. It is meant to be argued with.

---

## Contributing

Issues and pull requests welcome — particularly:

- **New worked examples** from other domains (public sector, healthcare, HR, logistics, education)
- **Failure conditions** you've hit in production that the pattern library misses
- **Metrics** that proved to be leading indicators of a pattern going wrong
- Refinements to the decision axes or the automation ladder

Field evidence is more valuable here than theory. If a recommendation from this skill was wrong in practice, that's the most useful issue you can open.

---

License
MIT — see [LICENSE](LICENSE).

Creator:
---
Sodeh Abadi (Service & Product Designer Lead, AI-Native Products, Agentic Experience Designer, AI transformation.)
---
url: - https://linktr.ee/irSodeh
