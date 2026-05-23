# Build Core Skills to Thrive as an AI-Era Developer
**Source:** Google I/O 2026 | Speakers: Nicole Forsgren & Andrew Macvean (Google Developer Intelligence Team)

---

## The Core Question
How do software engineers continue to thrive in the AI-native era?

**Key reality check:**
- 3/4 of all code at Google is now written by AI
- AI adoption can increase *individual* productivity while *decreasing* team-level benefits (DORA research)
- Engineers using AI the most are spending *more* time coding, ideating, and collaborating — not less
- Coding was never the bottleneck. The whole product lifecycle is.

---

## The Expanded T-Shaped Engineer

The classic T-shape (broad knowledge + deep specialization) now has new layers:

```
[ AI Use ] ←—— [ Core Engineering ] ——→ [ Adjacent Engineering ]
                                                ↕
                                    [ Adjacent Non-Engineering ]
                                      (Business & User Context)
                        |
                     [Deep
                  Specialization]
```

**New horizontal layer (non-negotiable):** Effective AI use — understanding AI constraints, evaluating outputs, steering AI in task-specific contexts.

**New wings:**
- **Adjacent Engineering:** Security, privacy, compliance, deployment infra, reliability
- **Adjacent Non-Engineering:** Business context, user needs, product thinking

> Without depth + breadth, AI just makes you do the wrong things faster.

---

## 5 Patterns of High-Performing AI-Native Engineers

### 1. Operating at Higher Altitudes
Think deeply about *why* you're building, not just *what* or *how*. This was always expected of senior engineers — now it's expected of everyone.

**Action:** Before writing a spec or prompt, articulate the business/user problem in one sentence. If you can't, don't start.

### 2. Shifting Left on Intent
Traditionally: shift testing/security earlier. Now: shift *intent* earlier.

Agents need context upfront — trade-offs, constraints, goals, success criteria. The source of truth is moving from code → structured intent documents.

**Action:** Write specification files before coding sessions. Treat specs like code (version control, reviews). This is product thinking made explicit.

### 3. Designing Environments, Not Just Writing Code
Top engineers aren't vibe-coding. They're setting guardrails, creating systems so agents + humans can work toward shared goals.

**Action:** Define agent role profiles with behavioral attributes, domain knowledge, and specific recipes. Set up style guide conventions with checks to detect agent drift.

### 4. Demanding Verified, High-Quality Output
Delegation ≠ abdication. The bar must stay high.

"Delegate tasks, not judgment."

**Action:** Set up structured feedback loops — user feedback, performance data, observability traces — to measure adherence to intent.

### 5. Maintaining a Scientific Mindset
Things move too fast to get it right the first time. The goal is to learn fast and iterate.

**Action:** Every week, experiment with one new approach. Codify what you learn back into your agent rules/specs. Intent + feedback loops = real scientific mindset.

---

## Practical Implementation Steps

### Core Software Engineering Skills

**1. Re-implementation as a learning tool**
- Don't accept the AI's first draft
- Prompt: "Tear down this solution and re-implement it from scratch. Document why you approached it differently and what you learned."
- Use this to check assumptions, surface missing context, and compare approaches

**2. Alien code walkthroughs**
- Have engineers explain code or system architectures they did NOT write
- Builds shared mental models
- Use whiteboards — analog is making a comeback for a reason
- Code is no longer the primary deliverable; shared system understanding is

**3. Codify team practices into agent skill/rule files**
- Write structured agent role profiles (behavioral rules, stylistic conventions, domain knowledge)
- Maintain these files like code: version control + observability
- Ask yourself: "What does good agent behavior look like here?" — forces you to stay sharp

---

### GenAI / Agent Orchestration Skills

**1. Upskill on evals (top priority)**
- Verification is now the bottleneck, not code generation
- Evals require the full T: AI knowledge + engineering depth + user/business context
- Evals are a critical artifact for shared team knowledge and capturing intent
- They define "what good looks like"

**2. Agent journaling / forced reflection**
- At end of each day/session, have your agent generate a reflection:
  - Where did it get stuck in the system?
  - Where were instructions confusing?
  - Where did it feel productive?
- Use this to improve instructions, agent skills, and tool usability

**3. Build teams of agents (not just one agent)**
- Recommended sweet spot: 3–5 agents
- Example 3-agent architecture (from Google's TensorFlow migration):
  - **Planner agent** → generates verifiable migration steps
  - **Orchestrator agent** → groups those steps
  - **Coder agent** → executes them
- Feed domain-specific playbooks per agent (e.g., YouTube-specific practices for YouTube migrations)

**4. Spec-driven development**
- Write specs before execution: goals, constraints, rationale, success criteria
- Specs + agent roles = source of truth for *what* and *why*
- Run review agents against your specs to stress-test requirements *before* writing code
- When everyone can prototype at lightspeed, specs prevent exploration from becoming chaos

**5. Establish human baselines**
- Measure verification overhead per task type
- Run experiments to find tasks where agent success probability is highest
- Preserve human attention for tasks agents can't yet perform and where taste matters

---

### Adjacent Engineering Skills (Security, Infra, Reliability)

**1. Blame-free postmortems**
- Make it a habit to document, read, and discuss outages/incidents
- Triangulate: postmortem docs + agent self-reflections + observability traces
- Reveals where edge cases are exposed and where system instructions are unclear

**2. Use AI to stress-test, not just to build**
- Set up red team / adversarial review agents
- Have agents explain *how they would exploit the system*
- Documents attack surfaces; forces you to engage with exploit mechanisms
- Trains both you and your agents to spot vulnerabilities

**3. Whiteboard-first architecture**
- Manually trace pipelines before a line of code is written
- Builds mental models (e.g., enterprise compliance, data flow)
- Challenges initial assumptions and gives agents better context going into execution

**4. Invest in observability**
- If features move 10x faster, you need 10x better monitoring
- Build/use unified data agents with access to: code, error logs, performance data, stack traces
- Goal: empower engineers (especially earlier-career) to understand complex distributed systems
- Use AI to *understand* systems, not just build them

**5. Tiered risk environments**
- Different apps have different risk profiles — don't treat everything like prod
- Move from prototype → production in incremental, iterative steps
- Each tier: tighter risk, faster feedback, contained blast radius

---

### Adjacent Non-Engineering Skills (Business & User Context)

**1. Become a value translator**
- Take user + business needs → turn into precise requirements
- Before optimizing: ask "for whom, and under what conditions?"
- Example: "Improve performance" → find the specific user segment → guide AI to optimize the critical paths that affect *that* scenario

**2. Don't let AI summarize all your user feedback**
- Dumping feedback logs into an LLM loses signal
- Do high-touch user feedback sessions
- Hearing actual joy or frustration builds empathy and makes the *why* real

**3. Protect your specs fiercely**
- Most cognitive energy → debating goals, business logic, edge-case constraints
- Clear articulation early = team alignment on *why* + richer context for agents
- Treat specs like code: version control, reviews, stress-testing with review agents

---

## For Engineering Leaders: 3 Immediate Shifts

### 1. Redefine how you measure productivity
- Stop measuring: pull requests, throughput, lines of code accepted
- Start measuring: outcomes, business needs met, quality + speed balanced
- If you measure only speed, devs won't rigorously verify AI output → system instability skyrockets
- Use a balanced portfolio of metrics

### 2. Protect productive struggle
- Carve out dedicated time (during work hours) for learning tools and understanding systems
- Encourage manual architectural walkthroughs
- Encourage experimentation with new tools/approaches
- Without this space, teams drown in cognitive debt

### 3. Foster radical psychological safety
- Agentic workflows will fail — that's expected
- If culture punishes failure, engineers default to old, safe ways of working
- Celebrate intelligent failure
- Run blameless postmortems so the whole team learns from systemic mistakes

> "A bad system will beat a good person every time." — Deming

---

## Key Mental Model Shifts

| Old Mental Model | New Mental Model |
|---|---|
| I write code | I design systems and environments |
| AI assists me | I orchestrate teams of agents |
| Code is the deliverable | Intent + verified outcomes are the deliverable |
| Shift left on testing | Shift left on *intent* |
| Single agent / chatbot | Balanced multi-agent teams |
| Measure throughput | Measure outcomes |
| Senior devs think about why | Everyone thinks about why |

---

## One-Line Takeaways

- **Shift left** (on intent, not just testing)
- **Shift up** (operate at higher altitudes — why, not just what/how)
- **Design systems** (environments, guardrails, agent teams) — not just code
- **Delegate tasks, not judgment**
- The software engineering role is not vanishing — it's becoming more important