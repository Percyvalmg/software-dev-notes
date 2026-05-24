# The Evolution of the Developer Craft
**Source:** Google I/O 2026 | Speakers: Richard Seroter (moderator), Addy Osmani, Aja Hammerly, Ciera Jaspan

---

## What Seniority Means in the AI Era

Seniority used to mean you could write code others couldn't. Now it means you can understand code others can't — and bring strong engineering fundamentals to every decision.

**What hasn't changed:**
- Breaking big problems into smaller parts
- Trade-off analysis (security vs. performance, build vs. buy, etc.)
- Solving challenging problems in ways that work for the business
- Mentorship and investment in junior engineers

**What's shifting:**
- Seniority mindset now needs to exist at every level — even new grads need to think like senior engineers
- Hiring for: comfort with AI, curiosity about new tools, demonstrated habits for staying current
- Senior engineers can't just spawn agents and leave the rest of the team to figure it out — mentorship is more important, not less

---

## Who Builds What Is Getting Blurry

One week on Ciera's cross-functional team (engineers, UX researchers, data scientists), everyone explored AI tools. Outcome: the software engineers spent the week writing design docs and fixing documentation. The UX researchers were writing code.

The pattern that emerged: **everyone is doing the junior version of someone else's job, and the senior version of their own.**

People with broad curiosity — a bit of UX, a bit of product, a bit of coding — are thriving because AI lets them combine those skills in new ways.

---

## Skills to Build Now

### Architecture over syntax
The big one. Knowing how to frame problems for agents, structure multi-agent systems, and make sound trade-offs has moved down the stack — everyone is now dealing with architecture decisions.

Key questions to get comfortable with:
- What should be its own agent vs. bundled into one?
- How should agents talk to each other?
- One agent for a day vs. 10 agents for an hour — what makes sense?

### Documentation quality
Bringing agents onto a team is like doubling your headcount with all-junior staff. If your documentation was thin before, it's a real problem now. Every design decision, process nuance, and context artifact that lived in someone's head needs to exist somewhere an agent (or new team member) can find it.

### Avoiding cognitive debt and cognitive surrender
- **Cognitive debt:** Your understanding of how to solve problems erodes because you keep deferring to AI.
- **Cognitive surrender:** You stop thinking altogether and just accept whatever the LLM produces.

Counter-move: when working with an agent, take time to understand what it generated and why it made the decisions it made. Don't just merge and move on.

### Spec clarity — knowing what "done" means
Moving from writing code to writing intentions that become code requires being precise about the end state. "Done" for an experienced engineer includes: functional correctness, performance, accessibility, UX quality, security. If your spec doesn't cover those dimensions, you're leaving them to the LLM's interpretation.

---

## De-skilling: What to Let Go Of

**Syntax.** You don't need to memorize it. Read the language, understand its strengths and tradeoffs, and generate the code. Aja touches five languages in a typical week — she knows Go's concepts and tradeoffs but doesn't bother with its syntax.

**Friction points.** Any part of your workflow that causes friction and adds no value — including IDE setup rituals, boilerplate, repetitive formatting — is a candidate to hand off. Whenever you find a friction point, try to get AI to handle it.

**Stack religion.** Five years ago, people had strong tribal allegiances to frameworks and libraries. That matters a lot less when an agent can handle the implementation details.

---

## How to Work Effectively with Agents

**Treat agents as adversarial mentors.**
After each session, ask: "What did we miss? What didn't I understand about this? What's not right here?" Tell it not to be nice. Aja does this before every push. It feels uncomfortable at first. Quality improves significantly.

**Build a reinforced learning loop.**
Configure your agent to capture learnings at the end of each session — either automatically codify them into a markdown/config file, or prompt yourself to articulate what you didn't know the day before. Mistakes from yesterday shouldn't repeat tomorrow.

**Teach the agent to update its own memory.**
Every time the agent makes a mistake, have it figure out why and update its configuration file. It feels slower upfront; it compounds positively over time.

**Manage the orchestration tax.**
Running 20 agents doesn't mean 20x your cognitive bandwidth — your bandwidth is still finite. Strategy: define isolated, deferrable tasks for background agents, and reserve your attention for the work that actually needs it (the complex, ambiguous, high-stakes pieces).

**Define isolated tasks clearly before deferring.**
When spinning up background agents, be explicit about scope. Vague delegation creates sprawl that's hard to review.

---

## Staying Current Without Burning Out

**Aja's model:** Work-in-progress meetings — a recurring team session where people share half-baked experiments and new techniques. Also: just ask "how'd you do that?" when you see a colleague do something interesting.

**Ciera's model:** One new tool per month. Go deep, find your personal best practices, then either keep it in rotation or drop it fast. Don't try to keep up with everything.

**Addy's model:** An innovation budget — a fixed, intentional amount of time for experimenting with new tools. Be picky about what you try so you have enough time to actually assess it. Look for tools that are doing something genuinely different, not just converging on the same UX patterns as everyone else.

**Shared principle:** Learn tools that actually connect to a problem you're currently solving. Tools disconnected from real work are hard to stay motivated about.

**Reality check on social media:** What's being hyped on X is often aimed at solo founders and one-person startups. It may not apply to your team or enterprise context at all. Use it as a leading indicator, not a prescription.

---

## Practical Implementation Steps

### Habits to start now
- **End-of-session adversarial review:** Before closing a session, ask your agent what you missed, what's weak, what could bite you later.
- **Learning capture:** Configure your agent to codify session learnings into a persistent file. Review it; feed it back in.
- **Block experimentation time:** Request 2 hours/week per person for hands-on tool experiments. Call it science fair, work-in-progress, whatever. Make it real time, not theoretical.
- **Automate one painful task this week:** Think of something you do repeatedly that brings you no joy. Try to eliminate or shrink it with whatever tools were just launched.

### For engineering managers
- Protect time for experimentation during work hours — not as homework.
- Run work-in-progress or show-and-tell sessions where people share experiments.
- Invest explicitly in junior engineer mentorship. Velocity pressure is real, but the juniors of today are the seniors of tomorrow.
- Set expectations: seniority now includes showing others how to work, not just producing output.

---

## Key Quotes

> "Seniority used to mean that you could write code and solve problems that other people couldn't. And now it means that you understand code that other people can't necessarily understand." — Addy Osmani

> "We are all doing the junior level of everyone else's job and then the senior level of our own job." — Ciera Jaspan

> "I treat any of the AIs I'm interacting with as an adversarial mentor. Tell me what I missed. Tell me what I don't understand. Don't be nice." — Aja Hammerly

> "Remind yourselves that there is a difference between feeling busy and actually being productive. You can run 20 agents and feel really, really busy. That doesn't mean you're actually getting productive work done." — Addy Osmani

---

## One-Line Takeaways

- Seniority = judgment and system understanding, not syntax mastery
- The junior version of everyone's job is now accessible to everyone — the senior version of your own job matters more than ever
- Cognitive surrender is the real risk: don't just accept AI output, understand it
- Spec clarity is the new code quality: if you can't define done, you can't delegate well
- Architecture decisions have moved down the stack — everyone needs to be able to reason about them
- Build the adversarial mentor habit: actively ask what you missed, before every push
- One new tool per month, learned deeply, beats chasing every new release
- Feeling busy is not the same as being productive
