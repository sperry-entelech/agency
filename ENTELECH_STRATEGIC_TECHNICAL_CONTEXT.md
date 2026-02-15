# Entelech: Strategic & Technical Context Document
*Comprehensive reference for sales conversations, technical scoping, partnerships, and positioning.*
*Last updated: February 2026*

---

## 1. PLATFORM ARCHITECTURE

### The Entelech Platform (entelech-platform repo)

A production-grade internal operations hub built on Next.js 14, TypeScript, Tailwind CSS, and Supabase. This is the command center that ties together all business systems — project tracking, lead generation, email analytics, AI tooling, and temporal intelligence.

**Core Architecture:**
- **Frontend:** Next.js 14 App Router with React 18, Tailwind CSS, Radix UI components (shadcn/ui), Lucide icons
- **Database:** Supabase (PostgreSQL) for auth, context versioning, outbound analytics, and logging
- **AI Layer:** Anthropic SDK (Claude) for agent orchestration, proposal generation, and context formatting
- **External Services:** Skills Factory API, Context Version Control API (Cloudflare Workers), Google Sheets integration, GitHub API

**Platform Pages & Capabilities (16 pages):**

| Page | Status | What It Does |
|------|--------|-------------|
| Dashboard | Functional (some hardcoded stats) | Central hub — engagement stats, quick actions, integration status |
| Audit | Fully functional | 3-tier lead gen form (Basic/Standard/Comprehensive), all free, feeds campaigns |
| Campaigns | Fully built | Performance tracking — impressions, clicks, conversions by project |
| Clients | Basic CRUD | Client management with mock data, links to engagement creation |
| Context | Advanced, auth-gated | Full temporal intelligence — context commits, history, Claude-formatted export |
| Engagements | Demo/mockup | Simulated 30-minute agent engagement flow |
| Outbound | Fully functional | Email campaign analytics — delivery, opens, clicks, replies, bounces by channel |
| Outbound Admin | Fully functional | Data entry for email stats, SQL setup guide, performance indicators |
| Projects | Fully built | Registry of 13 projects across 16 categories with filtering and search |
| Skills | Live integration | Skills Factory library — search, download, install commands |
| Systems | Fully built | 16 business system categories mapped to agency documentation |
| Tools | Partial | Proposal Generator (active), SOW Generator (active), Contract Generator (coming soon) |
| Logs | Fully functional | Real-time activity monitor with filters, export, auto-refresh every 5s |
| Integrations | Functional | Google Sheets config, platform logging active, n8n stub |
| Cursor Prompts | Functional | Skills-based prompt generation for Cursor IDE |
| Documentation | Links hub | Points to agency system map and documentation categories |

**Command Palette:** Cmd+K keyboard-navigable search across all platform sections — a polished UX detail that signals production quality.

### Agent Orchestrator (lib/services/agent-orchestrator.ts)

The centerpiece AI system: a 3-agent pipeline that executes full consulting engagements in ~30 minutes.

**Pipeline:**
1. **Master Coordinator Agent** (~8s) — Parses discovery input, identifies priorities, selects approach
2. **Solution Design Agent** (~12s) — Generates technical architecture, implementation plan, resource estimates
3. **Client Enablement Agent** (~8s) — Creates business-focused deliverables, training materials, handoff docs

Each agent returns structured output: analysis, recommendations, confidence score, and processing time. The orchestrator chains them sequentially, passing context forward. Built on `claude-3-5-sonnet-20241022` via the Anthropic SDK.

**In practice:** This system generates $35K-$50K enterprise proposals from a single discovery call. The TransMedics case study validated: 700+ lines of production-ready code, 7 comprehensive business documents, 100% technical specification accuracy.

### Context Version Control (lib/services/context-version-control.ts)

A git-like temporal intelligence system for business context, running on Cloudflare Workers.

**How it works:** Business context (client data, market insights, operational metrics) gets versioned through typed commits. Each commit has a hash, timestamp, author, message, and typed field changes (text, number, json, array, boolean, date). Sources include manual entry, API integrations (Twitter, CRM, webhooks), and Claude conversations.

**Key functions:**
- `createCommit()` — Version a context change with typed fields
- `getCurrentContext()` — Get the latest state of all context
- `getClaudeContext()` — Export context formatted for Claude injection (markdown, JSON, or YAML)
- `getContextAtDate()` — Time-travel to any historical context state
- `getFieldHistory()` — Track how a specific field evolved over time

**Why this matters:** This solves the "stale context" problem in AI-assisted consulting. When you're managing multiple client engagements, the system ensures Claude always has current, versioned business context — not last month's assumptions.

### Skills Factory (lib/services/skills-factory.ts)

A content analysis and skill generation pipeline. Analyzes content (copywriting, process, technical) and generates reusable Claude skills with metadata, tagging, and ZIP download. Skills are searchable, publishable to GitHub, and installable in development environments.

### Project Registry (lib/data/projects.ts)

Tracks 13 projects across the `sperry-entelech` GitHub org: entelech-platform, skills-factory, entelech-website, audit-request-form, cold-email-infrastructure, member-engagement-platform, agency-system-map, hilb-demo, tnt-groundspan-pricing, tnt-holiday-website, tnt-tacky-lights, proposal-generator, mtt-solver. Categorized across 16 business system categories (marketing, sales, service-delivery, multi-agent, client-success, backend-infrastructure, ai-intelligence, etc.).

---

## 2. SERVICE DELIVERY FRAMEWORK

### The 6-Phase Systematic Delivery Framework

Every engagement follows a documented, repeatable process:

**Phase 1: Discovery & Operational Mapping (Week 1)**
- 2-week comprehensive discovery: stakeholder interviews, process deep-dives, technology assessment
- Map ALL workflows — not just the pain point the client called about (Moza principle: holistic mapping)
- Tribal knowledge capture: the things the best people know that aren't written down
- Deliverable: Detailed operational map with agent architecture recommendations

**Phase 2: Architecture & Design (Week 2)**
- Bespoke agent architecture designed for client's specific operations
- Modern stack decision matrix applied: React frontend, Supabase + n8n/FastAPI backend
- Client approves architecture before any building starts
- Deliverable: Solution design with technical specifications

**Phase 3: Agent Development (Weeks 2-3)**
- AI-assisted development (3-5x faster than traditional)
- Development meta: GPT-5 TDD planning → Lovable rapid prototyping → Cursor production code
- Integration with client's existing tools and software stack
- Deliverable: Functional agent ready for testing

**Phase 4: Deployment & Feedback Activation (Weeks 3-4)**
- Staged rollout with human oversight
- Feedback loop activation: team teaches the agent what's right and wrong
- Edge case handling and error correction begin
- Deliverable: Live agent with active feedback loops

**Phase 5: Quality Assurance & Governance (Weeks 4-5)**
- 6-layer testing: Unit → Integration → System → UAT → Performance → Security
- Quality gates: 99.5% uptime, <2s response times, 100% deployment success
- Human-in-the-loop governance, audit trails, error correction protocols
- Deliverable: Validated agent with governance controls

**Phase 6: Documentation & Handoff (Weeks 5-8)**
- Results measurement against baseline
- Agent accuracy progression tracking (70% → 85% → 95%+)
- Complete documentation, training materials, and improvement protocols
- Deliverable: Client owns and operates independently

### The 48-Hour Implementation Track

For smaller engagements (outbound infrastructure, single-workflow agents), a compressed timeline exists:

- **Hours 1-16:** Intelligence integration — Azure, PostgreSQL, AI models, n8n platform setup
- **Hours 17-32:** Architecture deployment — integrations, workflows, dashboards
- **Hours 33-48:** Optimization & launch — testing, training, go-live
- **Quality gates** at Hour 16 (component), Hour 32 (integration), Hour 48 (production)

### Multi-Agent Proposal System

The crown jewel of delivery speed: generates complete $35K-$50K enterprise proposals in 30 minutes.

**4 Specialized AI Agents:**
1. **Master Coordinator** (5-10 min) — Parses discovery, selects templates, coordinates agents
2. **Technical Implementation** (10-15 min) — Generates production-ready infrastructure specs
3. **Documentation Agent** (10-15 min) — Creates business-focused handoff materials
4. **Discovery Parser** — Structures raw client information into agent-consumable format

**Validated output (TransMedics):** 700+ lines production-ready code, 7 business documents, 100% spec accuracy, 70% cost reduction ($18,432 annual savings).

### Client Success Framework (44 files documented)

**Onboarding Arc:**
- Day 1: Welcome celebration, portal access, CSM introduction
- Week 1: Optimization call, performance review, training delivery
- Month 1: Success report with ROI dashboard and cost savings breakdown
- Month 3: Strategic review, expansion discussion

**Performance Tracking (by package tier):**
- Essential ($2,500): 5 core KPIs — uptime, time saved, user adoption, error reduction
- Professional ($5K-7.5K): 10 metrics — adds integration uptime, cross-department impact
- Enterprise ($10K-15K): 15+ metrics — adds revenue impact, strategic transformation

**Alert System:** Green (optimal) → Yellow (10-20% below target) → Red (critical)

**Referral Program:**
- Bronze (1 referral): $500 credit, priority support
- Silver (3 referrals): $1,500 credit, custom development
- Gold (5+ referrals): $3,000+ credit, strategic partnership

**Success Targets:** Week 1 (75% utilization, 8/10 comfort), Month 1 (90% adoption, 9/10 satisfaction), Month 3 (95% optimization, 8/10 referral likelihood).

---

## 3. TECHNICAL STACK & CAPABILITIES

### Production Stack

| Layer | Technology | Purpose |
|-------|-----------|---------|
| Frontend | Next.js 14, React 18, TypeScript, Tailwind CSS | App shell, SSR, component system |
| UI Components | Radix UI (shadcn/ui), Lucide icons | Accessible, composable UI primitives |
| Database | Supabase (PostgreSQL) | Auth, data persistence, real-time subscriptions |
| AI | Anthropic SDK (Claude), GPT-5 Thinking | Agent orchestration, proposal generation, planning |
| Agent Orchestration | n8n, FastAPI, CrewAI | Workflow coordination, complex logic, multi-agent |
| Infrastructure | Vercel (hosting), Cloudflare Workers (edge compute) | Deployment, edge functions |
| Prototyping | Lovable | Rapid UI prototyping before Cursor production code |
| Development | Cursor IDE | AI-assisted production development |
| Payments | Whop | Client payment processing |
| Analytics | PostHog, Mixpanel | Product analytics, event tracking |
| Integration | Google Sheets API, GitHub API | Data logging, repo discovery |

### What's Actually Built vs Stub

**Production-ready systems:**
- Audit request form (3-tier lead generation, campaign-connected)
- Outbound email analytics dashboard (real Supabase data, admin panel)
- Context Version Control (temporal intelligence with Claude export)
- Project Registry (13 projects, 16 categories, full filtering)
- Skills Factory integration (search, download, install)
- Campaign performance tracking
- Real-time logging system with export
- Command palette (Cmd+K navigation)
- Agent Orchestrator pipeline (3-agent, validated with TransMedics)

**Demo/minimal:**
- Dashboard engagement stats (hardcoded numbers)
- Engagement execution flow (simulated with setTimeout)
- Client management (basic CRUD, 2 mock clients)
- Contract Generator (coming soon stub)
- n8n integration (placeholder only)

### Development Methodology (2025 Meta)

The documented development workflow follows:
1. **GPT-5 Thinking** — TDD-style planning, architecture decisions
2. **Lovable** — Rapid prototyping, UI scaffolding
3. **Cursor** — Production code development with AI assistance

Revenue scaling through template maturity:
- Months 1-3: 100% custom work ($10K-25K per engagement)
- Months 4-6: 50% templated ($25K-50K, faster delivery)
- Months 7+: 80% templated ($50K+ with RevShare options)

---

## 4. SALES & OUTBOUND SYSTEMS

### The Land-and-Expand Model

**Entry Point: Cold Outreach Infrastructure ($500-$1,500)**
A productized, fixed-price offer that gets prospects into the ecosystem fast:
- **Tier 1 ($500):** Domain, warmup, 1 mailbox, 500 prospects, 3 templates — 48-72 hour delivery
- **Tier 2 ($1,500):** 3 domains, 9 mailboxes, 2,500 prospects, smart sequences, CRM handoff — 5-7 day delivery
- **Managed ($500/mo):** Ongoing prospect sourcing, A/B testing, deliverability monitoring, monthly reporting

**Expansion Path:** Outbound infrastructure → leads start flowing → prospect needs help converting them → Lead Conversion Agent ($10K-$25K) → Sales Velocity Agent → Client Retention Agent → Full RevOps Agent ($45K-$85K).

### Sales Intelligence Assets (35 files)

**Prospect Packages (5 detailed):**
Each contains: company profile, decision makers, pain points, technology gaps, ROI calculations ($200K-$900K+ annual benefit), package recommendation, payback period (typically 1-5 days), implementation focus, next action steps.

Companies profiled: VMW Express ($10M revenue, 75 employees), Fleetmaster Express, Riverside Logistics, Ceres Transport, Pete Burr Machine.

**ROI Calculator (transportation-specific):**
- Enterprise ($20M+): $2.3M annual benefit, 15,244% ROI, 2.4-day payback
- Professional ($2M-20M): $2.6M annual benefit, 34,499% ROI, 1.1-day payback
- Foundation ($100K-2M): $208K annual benefit, 8,320% ROI, 4.4-day payback

**Proposal Templates:** Foundation, Professional, Enterprise, and RevOps Consulting variants — all updated with bespoke agent language and the value-based, risk-free engagement model.

**Objection Handling:** Price objections, timing concerns, risk mitigation, "can't we just use ChatGPT ourselves?" response frameworks.

### Email & Marketing Systems

**Cold Prospect Sequence (7 emails, Day 1-20):**
- Progression: Problem awareness → Perfectionism trap → Speed advantage → Learning agents → Cost of delay → Competitive urgency → Final push
- Conversion target: 8-12% to demo booking
- Behavioral scoring: Opens (+2), Clicks (+5), Content visits (+10), ROI calculator (+15), Calendar (+20)
- Segmentation: High (50+), Medium (25-49), Low (1-24), No engagement

**LinkedIn Authority Posts (5 pieces):**
Including the agent-thesis post: "95% of 'AI Agents' Are Actually Just Workflows" — breaks down the workflow vs agent distinction for a business audience.

**Outbound Analytics Dashboard (live in platform):**
Tracks 4 email channels with monthly stats: sent, delivered, opened, clicked, replied, bounced, complaints. Historical data spanning Sept-Dec 2025 (e.g., Channel 1: 15K-35K emails/month). Full admin panel for data entry.

**Content Library:**
- Blog articles (authority piece on $100K automation inflection point, 2,400 words)
- ROI calculation frameworks with industry-specific calculators
- Competitive comparison matrices (vs Traditional Consultants, vs DIY, vs Lead Gen Agencies)
- Sales battle cards with agent vs workflow differentiation

---

## 5. STRATEGIC POSITIONING

### The Core Thesis

**Entelech builds bespoke AI agents on client operations.** Not templates. Not generic SaaS. Systems built on tribal knowledge, edge cases, and specific software stacks — that get better every week through human feedback.

This is distinct from what 95% of the market sells:

| | Competitors | Entelech |
|---|-----------|---------|
| **What they build** | Workflows (define what AND how) | Agents (define what, AI figures out how) |
| **How it's built** | Templates configured for your business | Bespoke on YOUR operations, YOUR data |
| **After deployment** | Static — works the same on day 1 and day 100 | Learns — 70% accuracy → 99%+ in 4 weeks |
| **Who owns it** | Vendor lock-in, licensing fees | Client owns everything, no restrictions |
| **Governance** | "Trust the AI" | Human-in-the-loop, audit trails, error correction |

### The Five Principles (adapted from enterprise AI agent frameworks)

1. **Don't automate one thing at a time.** Map ALL workflows. Build agents that handle multiple functions holistically.
2. **Your agent is built on YOUR operations.** Tribal knowledge, edge cases, specific stack. Generic SaaS can't capture this.
3. **Good agents get better every week.** 70% accuracy to 99%+ in 4 weeks through human feedback and error correction.
4. **Governance isn't optional.** Human-in-the-loop from day one. "The best agents are built by people who literally do not trust them."
5. **You own everything.** Agent runs on your infrastructure, integrates with your stack, works independently of us.

### Service Tiers

| Tier | Price | Timeline | What You Get |
|------|-------|----------|-------------|
| Outbound Infrastructure | $500-$1,500 | 48 hrs - 7 days | Client-owned sending setup, prospects, templates |
| Managed Outbound | $500/mo | Ongoing | Prospect sourcing, A/B testing, deliverability |
| Lead Conversion Agent | $10K-$25K | 2-3 weeks | Scoring, routing, follow-up, learning system |
| Sales Velocity Agent | $10K-$25K | 2-4 weeks | Proposal gen, adaptive follow-up, pipeline optimization |
| Client Retention Agent | $10K-$25K | 2-4 weeks | Onboarding, engagement, churn prevention |
| Full RevOps Agent | $45K-$85K | 4-8 weeks | All of the above as one coordinated intelligence |

**Business model:** Outbound is fixed-price, client-owned. Agent engagements are value-based, risk-free — clients pay only when they see measurable results. No IP restrictions across any tier.

### The Echelon Vision (Long-term)

Every consulting engagement generates proven agent frameworks. Echelon is the future product play: a self-service platform where businesses deploy these proven frameworks directly. The path: **custom agent → proven framework → self-deployable product** (custom → productized → scaled).

### Current Status (February 2026)

**Pre-revenue.** Infrastructure built, delivery framework documented, systems ready to deploy. A few deals in conversation, no closed clients yet.

**What exists:**
- 200+ files of documented operational systems
- Multi-agent proposal generation (validated: 30-minute turnaround)
- 6-phase delivery framework with SOPs, quality gates, handoff procedures
- Bespoke agent development methodology documented and ready to deploy
- Cold outreach infrastructure — productized 3-tier offering, documented and ready to sell
- Platform with live lead gen, outbound analytics, project tracking, temporal intelligence
- TNT Limousine marketing work as proof-of-concept
- 5 detailed prospect packages with ROI calculations
- Complete client success framework (onboarding, tracking, referrals)

---

## 6. IMMEDIATE APPLICABILITY

### For Sales Conversations

**When a prospect asks "What do you actually do?"**
"We build bespoke AI agents on your operations. Not chatbots, not Zapier chains. A system that understands your business — your lead process, your proposal workflow, your onboarding — and handles it as one coordinated intelligence. The agent learns from your team's feedback and gets better every week. You own everything we build."

**When they say "We already have automations":**
"Most 'automations' are workflows — they do exactly what they're told, the same way, forever. An agent figures out HOW to accomplish the goal. When a lead comes in that doesn't match your normal pattern, a workflow breaks. An agent adapts. And it gets smarter every time."

**When they ask about risk:**
"You pay nothing upfront. We build it, deploy it, prove it works. If you don't see clear, measurable value — you pay nothing. You keep everything we built. We can start with outbound infrastructure for $500 — you'll have meetings on the calendar in a week."

**Objection — "Can't we just use ChatGPT/Claude ourselves?"**
Point to: tribal knowledge capture, multi-workflow coordination, feedback loops, governance. ChatGPT is a tool; an agent is a system built on YOUR operations that improves weekly.

### For Technical Scoping

**What we can deploy immediately:**
- Cold outreach infrastructure (48-72 hours for Tier 1)
- Lead scoring and routing agents (2-3 weeks)
- AI-powered proposal generation (validated 30-minute pipeline)
- Client onboarding automation (2-4 weeks)
- Email campaign analytics dashboard (existing platform feature)
- Context version control for client data (existing platform feature)

**Stack we deploy on:**
React/Next.js frontend, Supabase backend, n8n for workflow orchestration, Claude for agent intelligence, Vercel for hosting. Everything cloud-native, client-ownable.

### For Partnership Discussions

**What a partner gets access to:**
- 200+ files of documented systems (not vaporware — real SOPs, templates, frameworks)
- Multi-agent proposal system that generates $35K-$50K proposals in 30 minutes
- Productized entry-point offer ($500 outbound) that opens doors
- Complete client success playbook (onboarding → tracking → referrals → expansion)
- Platform with live analytics, project tracking, and AI tooling

**The gap that needs filling:**
Sales execution. The systems are built, the methodology is documented, the platform is functional. What's missing is consistent pipeline generation and closing.

---

## GAPS, QUICK WINS, OUTDATED INFO & MISSING PIECES

### Gaps

1. **No closed client data.** All ROI projections are based on industry benchmarks, not Entelech client results. The TransMedics case study validates the proposal system, but there's no post-deployment success story yet.
2. **Dashboard stats are hardcoded.** The platform dashboard shows "3 active engagements" and "$45K value delivered" — these are mock numbers, not live data. Needs real Supabase integration.
3. **Engagement execution is simulated.** The platform's engagement flow uses `setTimeout` to fake the 30-minute process. The actual agent orchestrator works (validated), but it's not wired into the platform UI for real execution.
4. **Client management is minimal.** Basic CRUD with 2 mock clients. No real CRM functionality yet.
5. **n8n integration is a stub.** Referenced throughout documentation as core orchestration layer but not connected in the platform.
6. **Contract Generator doesn't exist yet.** Listed as "coming soon" in the Tools page.

### Quick Wins

1. **Wire the agent orchestrator to the engagement UI.** The backend works. The frontend is a mockup. Connecting them gives a live demo of the 30-minute proposal system.
2. **Replace hardcoded dashboard stats with Supabase queries.** The database schema exists. Just needs real data flow.
3. **Deploy the outbound infrastructure offer.** Fully documented, productized, and priced. Ready to sell today.
4. **Use the audit form as a lead magnet.** It's fully functional and campaign-connected. Drive traffic to it.
5. **Export the context document (this file) as injectable Claude context.** Use it in every sales conversation, proposal generation, and partner discussion.

### Outdated Info

1. **COMPANY_INFO file references** may still contain some "2025" language in corners despite the February 2026 update.
2. **Package pricing in client-success** ($2,500/$5K-7.5K/$10K-15K tiers) doesn't align with the current agent pricing model ($10K-$85K value-based). These appear to be from an earlier productized-package model that preceded the bespoke-agent positioning.
3. **Transportation-focused prospect packages** (VMW Express, Fleetmaster, etc.) reflect an earlier vertical focus. Current positioning is broader (growth-stage B2B, $500K-$5M).
4. **Technology references** to "GPT-5 Thinking" and "Claude Sonnet 4.1" in operations docs may need version updates as models evolve.

### Missing Pieces

1. **No case study template** for when the first client closes. Need a framework ready to capture results from day one.
2. **No pricing calculator** that dynamically scopes agent engagements based on discovery inputs. The ROI calculator exists for transportation but not for general B2B.
3. **No client-facing portal.** The platform is internal-only. Clients can't log in to see their agent's performance, feedback loops, or improvement metrics.
4. **No automated lead qualification.** The audit form captures leads but doesn't score or route them — ironic for a company selling lead conversion agents.
5. **No demo environment.** When a prospect wants to see the agent in action, there's no sandbox or recorded demo. The engagement simulation is internal only.

---

*This document contains the complete strategic and technical context of Entelech as of February 2026. It should be injected into any Claude conversation involving sales, scoping, partnerships, or positioning to ensure consistent, accurate, and comprehensive responses.*

*Source repositories: `entelech-platform` (Next.js 14 operations hub) and `agency` (200+ files of business documentation).*
