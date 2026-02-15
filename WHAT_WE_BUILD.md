# What We Build — Entelech

This document explains what Entelech actually delivers to clients. If you're considering a partnership, this is what you'd be selling, building, or supporting.

---

## The Consulting Engagement

Every client engagement follows the same basic arc:

### 1. Discovery & Audit (Week 1)
- Free consultation — we look at the client's current revenue operations
- Identify specific leaks: slow lead follow-up, long sales cycles, early client churn, manual bottlenecks
- Deliver actionable findings whether or not they hire us
- No cost, no obligation. This is how we earn trust.

### 2. Scope & Agreement
- Define what we're fixing and what success looks like
- Value-based pricing — investment tied to projected business impact, not hours
- Client pays only when they see results (risk-free model)
- No upfront payment, no IP restrictions, no long-term lock-in

### 3. Implementation (2-8 weeks depending on scope)
- Build the bespoke agent using our 6-phase delivery framework
- Regular client check-ins — no disappearing for weeks
- Quality gates at each phase before moving forward
- Client has visibility into progress throughout

### 4. Handoff & Optimization
- Complete documentation and training
- Client owns everything — code, data, systems, domains
- Ongoing support available but not required
- Performance monitoring to verify results match projections

---

## What We Actually Deliver

### The Bespoke Agent

Most "AI consultants" build workflows — they define what happens AND how, step by step. We build agents. You define the goal, and the system figures out the how.

This isn't a chatbot. It's not a Zapier chain. It's a system that understands your business operations and handles work across multiple functions — lead processing, proposals, onboarding, reporting — as one coordinated intelligence, not isolated automations.

### What an Agent Handles

A single bespoke agent manages multiple workflows holistically. Instead of building four separate automations, we build one system that understands how they connect:

- **Lead processing** — Scoring, routing, personalized follow-up, CRM updates. The agent learns which leads convert and adjusts scoring over time.
- **Proposal generation** — AI generates custom proposals from discovery notes, formats to your template, sends for review. 30 minutes instead of 5 hours.
- **Client onboarding** — Welcome sequences, kickoff scheduling, milestone tracking, proactive check-ins. Days, not weeks.
- **Operations coordination** — Pipeline visibility, follow-up sequences that adapt to prospect behavior, forecasting from actual data, early warning systems for churn risk.
- **Reporting** — Client success dashboards, delivered value tracking, revenue leak identification.

**What the client gets:** One system that runs their revenue operations, with each function informing the others. A lead that converts feeds data back into scoring. An onboarding pattern that reduces churn informs how proposals frame the engagement. The agent sees the full picture because it handles the full picture.

### How It's Built — On YOUR Operations

We don't start with templates. We start with your processes, your edge cases, your data, your software stack.

Every business has tribal knowledge — the things your best people know that aren't written down anywhere. The dispatch rules that only work because Sarah knows which drivers handle which routes. The proposal language that closes deals because Mike figured out the right framing three years ago. The onboarding steps that prevent churn because someone learned the hard way.

Generic AI SaaS can't capture this. A bespoke agent can — because it's built on how YOUR business actually operates.

### How It Improves

A good agent gets better every week. Here's how:

- **Human feedback loops** — When the agent makes a mistake, your team flags it. The agent learns.
- **Error correction** — Edge cases that trip up the agent on day one become handled cases by day five.
- **Accuracy progression** — 70% accuracy in week one → 85% in week two → 95%+ by week four → 99%+ by month two.
- **Continuous learning** — The agent adapts as your business evolves. New service? New market? The agent learns.

This is the fundamental difference between an agent and a workflow. Workflows are static — they do what they're told. Agents learn and improve.

### What You Own — Everything

- The agent runs on your infrastructure
- All code, data, and configurations belong to you
- The system integrates with your existing stack
- It works independently of us — if you fire us tomorrow, the agent keeps running
- No vendor lock-in, no licensing fees, no hostage-taking

---

## The Entry Point: Cold Outreach Infrastructure

Not every engagement starts with a full agent build. For many clients, the relationship starts with something concrete and immediate: **client-owned outbound infrastructure**.

### What This Is

We build cold email sending infrastructure in the client's own accounts — their domains, their inboxes, their data. Not rented. Owned.

Most lead gen agencies rent you access to their system. You pay monthly forever, and if you stop paying, you have nothing. We build the machine and hand you the keys.

### Three Tiers

- **Infrastructure Setup ($500)** — 5 warmed sending domains, configured inboxes, DNS records, sequencer setup, handoff walkthrough. Client runs it themselves or has a VA manage it. Delivered in 48-72 hours.
- **Launch Package ($1,500)** — Everything above plus ICP research, initial lead list (2,500-5,000 contacts), 3-email sequence written and loaded, campaign launched and monitored for 2 weeks. Delivered in 1 week.
- **Managed Outreach ($500/month or $200-400/meeting booked)** — Ongoing campaign management, weekly list refreshes, copy testing, reply handling, meeting booking. Hands-off lead flow.

### Why This Matters Strategically

Outbound infrastructure is the entry point to the full agent engagement. Once meetings are landing on the calendar, the client naturally asks: "Can you make the rest of our revenue operations work this well?"

- Getting replies → needs lead scoring and qualification → **Lead Conversion Agent**
- Booking meetings → needs faster proposals → **Sales Velocity Agent**
- Closing deals → needs onboarding that retains → **Client Retention Agent**
- Scaling → needs the full picture → **Full RevOps Agent**

**Land with outbound ($500-$1,500). Expand to bespoke agent ($10K-$85K).**

Details: `sales-intelligence/cold_outreach_use_case.md`

---

## How We Deliver: The 6-Phase Framework

Our delivery process is documented and repeatable. Every engagement follows these phases:

**Phase 1 — Discovery & Operational Mapping**
Map ALL workflows — not just the one they called about. Understand how the business actually operates, identify the problems, capture tribal knowledge, define success metrics. Output: comprehensive operational map and structured requirements document.

**Phase 2 — Architecture**
Design the agent. Choose tools, map how workflows connect, define integrations, plan governance and human-in-the-loop checkpoints. Output: technical blueprint the client approves before we build.

**Phase 3 — Agent Development**
Build the bespoke agent. AI-assisted development (Claude Code) means we build 3-5x faster than traditional agencies. The agent is built on the client's actual operations, not generic patterns.

**Phase 4 — Deployment & Feedback Activation**
Put it live. Staged rollout, not big-bang launches. Test in production conditions. Activate human feedback loops so the agent starts learning from real usage immediately.

**Phase 5 — Quality Assurance & Governance**
Validate the agent handles real-world conditions. Test edge cases, verify accuracy, confirm governance controls work. Human-in-the-loop oversight, audit trails, and error correction protocols are validated. This is where the agent begins its accuracy progression — 70% → 85% → 95%+ through structured feedback.

**Phase 6 — Documentation & Handoff**
Complete documentation, team training, knowledge transfer. The client owns the agent and can operate it without us. Feedback loops and improvement cycles are documented so the agent continues learning after handoff.

Each phase has defined deliverables, quality checkpoints, and client sign-off before proceeding. Nothing moves forward until the previous phase is solid.

---

## Technology Stack

We use modern, proven tools. Here's what matters to clients:

| Tool | What It Does | Why It Matters |
|------|-------------|----------------|
| **n8n / Make.com** | Visual workflow automation | Client can see and modify their automations without hiring developers |
| **Claude (Anthropic)** | AI capabilities | Powers intelligent features — proposal generation, lead scoring, content creation |
| **Supabase** | Database & backend | Enterprise-grade data storage. Client owns their data completely |
| **Vercel** | Hosting & deployment | Fast, reliable, scales automatically. No server management |
| **Python / React** | Custom code (when needed) | For anything automation platforms can't handle. Client owns all code |

**Key principle:** We use no-code tools where they make sense (faster, client can maintain) and custom code where they don't (complex logic, branded interfaces, unusual integrations). Best of both worlds.

**Ownership:** Clients own everything. Code, data, domains, automations. No vendor lock-in. If they want to hire another developer tomorrow, they can.

---

## Pricing Model

### Value-Based, Risk-Free
- **No upfront payment.** Engagement begins with a free audit.
- **Client pays only when they see measurable value.** Not when we finish building — when results are verified.
- **No IP restrictions.** Client owns everything outright.
- **No long-term contracts.** Engagement scope is defined and finite.

### Typical Ranges
*(Final investment determined after value delivery and mutual agreement)*

- **Outbound Infrastructure** (entry point — client-owned sending setup): $500-$1,500
- **Managed Outreach** (ongoing outbound management): $500/month or per-meeting
- **Single Agent** (lead conversion OR sales velocity OR retention): $10K-$25K
- **Two Agents Combined** (deeper integration): $25K-$45K
- **Full RevOps Agent** (comprehensive overhaul): $45K-$85K

### Why This Works
Most consultants charge upfront and hope the client is happy. We deliver first and charge on results. This is genuinely differentiated — almost no one in this space does it because it requires confidence in your delivery.

We can do it because the delivery framework is systematized. We know what we're building, how long it takes, and what results it produces. That removes the risk for both sides.

---

## Proof of Concept: TNT Limousine

TNT Limousine is the clearest example of what we can build and deliver:

- **Wine tour marketing system** — 24-winery guide with interactive maps, lead capture, conversion-optimized landing pages
- **Holiday campaign** — Tacky lights tour promotion with 61 locations, seasonal booking system
- **Lead generation tools** — Quote request forms, email capture, automated follow-up
- **Complete websites** — Static HTML/CSS/JS, professionally designed, mobile-responsive

TNT is an employer relationship, not a client engagement. But the work is real, the systems are live, and the results are measurable. It demonstrates the full arc: understand the business, design the solution, build it, deploy it, hand it off.

---

## The Echelon Connection

Every consulting engagement generates two things:

1. **Client results** — the immediate deliverable
2. **Proven agent frameworks** — validated agent architectures that work in a specific vertical

This is the progression: custom agent → proven framework → self-deployable product. Every bespoke agent we build for a consulting client generates patterns that can be generalized. Echelon is where those proven agent frameworks become accessible to businesses that don't need a full consulting engagement — they need a pre-built agent they can configure to their operations.

Today's consulting clients become tomorrow's Echelon beta users. Today's consulting partners have equity in both the practice and the platform.

---

## Summary for Partners

If you're evaluating a partnership, here's what you need to know about the product:

- **We sell business outcomes** (more leads, faster sales, lower churn), not technology
- **We build bespoke agents** — holistic systems that handle multiple workflows, not one-off automations
- **Agents learn and improve** — 70% → 99%+ accuracy through human feedback loops
- **The pricing model is genuinely different** — risk-free, value-based, no upfront cost
- **Clients own everything** — the agent, the code, the data. No lock-in, no hostage-taking
- **The infrastructure to deliver is built** — agent development methodology documented and ready to deploy

For partnership details, see `PARTNERSHIP_FRAMEWORK.md`.
For the big picture, see `PARTNER_OPPORTUNITY.md`.

---

*Questions about deliverables or technical capabilities? Contact Ethan: sperry@entelech.net*
