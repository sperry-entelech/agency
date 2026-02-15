# Entelech RevOps Practice: Cold Outreach Infrastructure

## Use Case Overview

**Service Category**: Revenue Operations — Outbound Infrastructure  
**Target Client**: B2B service companies ($500K-$5M revenue) with existing offer but no systematic outreach  
**Delivery Model**: Client-owned infrastructure, one-time build + optional management  
**Differentiator**: You own everything. No vendor lock-in. We build it in your environment.

---

## The Entelech Difference

### What Everyone Else Sells

| Generic Offer | What It Actually Means |
|---------------|------------------------|
| "AI-powered lead generation" | They rent you access to their Instantly account |
| "Pay per meeting" | They control the infrastructure, you depend on them |
| "Done for you outreach" | They own your sending domains, your lists, your data |
| "B2B middleman" | You're the middleman's client forever |

### What Entelech Builds

| Entelech Approach | What You Get |
|-------------------|--------------|
| Client-owned infrastructure | Your domains, your inboxes, your accounts — you own everything |
| Built on your operations | Targeting, messaging, and sequences tailored to your ICP, your offer, your voice |
| Transparent build | You see exactly what's set up, can modify it yourself |
| Knowledge transfer | You understand how it works, not dependent on us |
| Optional management | We can run it, or you can, or your VA can |
| Gateway to full agent | Outbound is where the relationship starts — expand to Lead Conversion, Sales Velocity, and Retention Agents when ready |

**The fundamental question**: Do you want to rent lead gen forever, or own the machine that produces it?

---

## Service Tiers

### Tier 1: Infrastructure Setup
**Price**: $500 one-time  
**Timeline**: 48-72 hours  
**Best for**: Clients who want to run their own outreach or have a VA manage it

**Deliverables**:
- 5 warmed sending domains (client owns)
- 5-10 sending inboxes configured (client owns)
- Email sequencer setup (Instantly, Smartlead, or client's choice)
- DNS records configured (SPF, DKIM, DMARC)
- Warm-up activated
- Basic CRM/tracking (Notion, Airtable, or client's existing)
- 30-min handoff Loom walkthrough

**Client Provides**:
- Target ICP description
- Core offer/message
- Payment for platform costs (~$150-300/month ongoing)

**What's NOT Included**:
- Lead list building
- Copywriting beyond basic template
- Ongoing management
- Campaign optimization

---

### Tier 2: Launch Package
**Price**: $1,500 one-time  
**Timeline**: 1 week  
**Best for**: Clients who want a working campaign, not just infrastructure

**Deliverables**:
Everything in Tier 1, plus:
- ICP research and targeting strategy
- Initial lead list (2,500-5,000 contacts)
- 3-email sequence written and loaded
- Campaign launched and monitored for first 2 weeks
- Reply handling framework documented
- Optimization recommendations after initial data

**Client Provides**:
- 30-min discovery call
- Approval on targeting and copy
- Access to their calendar for booking

---

### Tier 3: Managed Outreach
**Price**: $500/month or $200-400/meeting booked  
**Timeline**: Ongoing  
**Best for**: Clients who want hands-off lead flow

**Deliverables**:
Everything in Tier 2, plus:
- Ongoing campaign management
- Weekly list refreshes
- Copy testing and optimization
- Reply handling and qualification
- Meeting booking directly to client's calendar
- Weekly reporting

**Client Provides**:
- Monthly check-in (15-30 min)
- Feedback on lead quality
- Show up to meetings we book

---

## Pricing Psychology

### Why This Works

**Tier 1 ($500)** = Lower than hiring someone on Upwork, and they own it forever. No-brainer for anyone who's been quoted $2-3K by agencies.

**Tier 2 ($1,500)** = Still cheaper than one month of a bad SDR. Gets them actual results, not just "infrastructure."

**Tier 3 ($500/mo or per-meeting)** = Competes with SDR salary ($5-8K/mo) at fraction of cost. Per-meeting option = pure ROI, zero risk for them.

### Objection Handling

| Objection | Response |
|-----------|----------|
| "That's more than I expected" | "You're buying the infrastructure once. Agencies charge this monthly and you never own anything." |
| "Can't you just do it for less?" | "I could, but then I'd cut corners on warm-up or domains. You'd burn your sending reputation in 2 weeks." |
| "Why wouldn't I just use Apollo?" | "You could. But Apollo's sending is limited and their deliverability is suspect. This is dedicated infrastructure." |
| "What if it doesn't work?" | "If we can't get you replies in 30 days, I'll rebuild the campaign at no charge. But we need to agree on volume and targeting upfront." |

---

## Technical Stack (Client-Owned)

### Required Components

| Component | Recommended Tool | Monthly Cost | Who Owns It |
|-----------|------------------|--------------|-------------|
| Sending domains | Porkbun, Namecheap | ~$15/year each | Client |
| Sending inboxes | Google Workspace or Outlook | ~$6-12/inbox/mo | Client |
| Inbox management | Instantly, Smartlead | ~$97-150/mo | Client account |
| Warm-up | Built into Instantly/Smartlead | Included | Client |
| Lead data | Apollo, LinkedIn, custom | Variable | Client |
| Enrichment (optional) | Clay | ~$150/mo | Client |
| CRM | Notion, Airtable, HubSpot Free | Free-$50/mo | Client |

**Total client platform cost**: ~$150-350/month depending on scale

### Optional Enhancements (Path to Full Agent)

| Enhancement | Tool | When to Add |
|-------------|------|-------------|
| AI enrichment | Clay | When volume justifies cost, or targeting requires deep research |
| Multi-channel | LinkedIn automation | When email alone isn't enough |
| Agent orchestration | n8n + Claude API | When client needs CRM sync, intelligent routing, Slack notifications — the beginning of a bespoke agent |
| AI reply qualification | Claude API | When reply volume requires intelligent triage — the agent learns which replies are worth pursuing |
| Lead scoring agent | n8n + Supabase | When outbound generates enough data to build a learning lead scoring system |

---

## Delivery Process

### Phase 1: Discovery (Day 1)
- 30-min call or async Loom exchange
- Understand: ICP, offer, current lead sources, volume goals
- Confirm: Budget for platform costs, timeline expectations
- Deliverable: Scope confirmation, invoice sent

### Phase 2: Infrastructure Build (Days 2-3)
- Purchase domains (or guide client to purchase)
- Set up inboxes and DNS records
- Configure sequencer
- Activate warm-up
- Set up basic tracking

### Phase 3: Campaign Setup (Days 4-5) — Tier 2+
- Build initial lead list
- Write email sequence
- Load and schedule campaigns
- Test sends to verify deliverability

### Phase 4: Handoff (Day 5-7)
- Record Loom walkthrough
- Document everything in client's system
- Provide reply handling framework
- Schedule check-in for Day 14

### Phase 5: Optimization (Week 2-4) — Tier 2+
- Monitor early results
- Adjust copy, targeting, send times
- Document learnings
- Provide recommendations

---

## Positioning Within RevOps Practice

Cold outreach infrastructure is the **entry point** into the broader bespoke agent engagement:

```
┌─────────────────────────────────────────────────────────┐
│                    ENTELECH REVOPS                       │
├─────────────────────────────────────────────────────────┤
│                                                          │
│  ┌──────────────┐    ┌──────────────┐    ┌────────────┐ │
│  │   OUTBOUND   │───▶│   QUALIFY    │───▶│   CLOSE    │ │
│  │              │    │              │    │            │ │
│  │ Cold Email   │    │ Lead Capture │    │ CRM/Pipeline│ │
│  │ LinkedIn     │    │ Pre-call     │    │ Proposals   │ │
│  │ Cold Calling │    │ Scoring      │    │ Contracts   │ │
│  └──────────────┘    └──────────────┘    └────────────┘ │
│         │                   │                   │        │
│         ▼                   ▼                   ▼        │
│  ┌──────────────────────────────────────────────────────┐│
│  │                AGENT ORCHESTRATION LAYER             ││
│  │   n8n coordination, Claude intelligence, Supabase    ││
│  └──────────────────────────────────────────────────────┘│
│                                                          │
└─────────────────────────────────────────────────────────┘
```

**The land-and-expand path:**
Outbound infrastructure is where the relationship starts. Once the client sees meetings landing on their calendar, the natural next step is making the rest of their revenue operations work the same way:

- Outbound client getting replies → needs lead scoring and qualification → **Lead Conversion Agent**
- Outbound client booking meetings → needs faster proposals → **Sales Velocity Agent**
- Outbound client closing deals → needs onboarding that retains → **Client Retention Agent**
- Outbound client scaling → needs the full picture → **Full RevOps Agent**

**Land with outbound infrastructure ($500-$1,500), expand to bespoke agent engagement ($10K-$85K).**

---

## Case Study Template

### [Client Name] — [Industry]

**Situation**: [1-2 sentences on where they were]

**Solution**: [What we built - tier level, specific components]

**Results**: 
- Emails sent: X
- Reply rate: X%
- Meetings booked: X
- Pipeline value: $X
- Timeline: X days from start to first meeting

**Client owns**: [List everything they now control]

---

## Sales Conversation Framework

### Discovery Questions

1. "How are you currently getting in front of new prospects?"
2. "What's worked? What hasn't?"
3. "Have you tried cold email before? What happened?"
4. "If I could get you 20 qualified conversations a month, what would that be worth?"
5. "Do you have someone who could manage replies, or do you need that handled?"

### Positioning Statement

> "Most lead gen agencies rent you access to their system. You pay monthly forever, and if you stop paying, you have nothing. We build the infrastructure in your accounts — you own the domains, the inboxes, the data. We can manage it for you, or hand you the keys and you run it yourself. Either way, you're not dependent on us.
>
> And when outbound is working and you're ready to scale, we build bespoke agents on the rest of your operations — lead scoring, proposals, onboarding — so your whole revenue engine runs the same way: built on your business, owned by you."

### Close

> "Based on what you've told me, Tier [X] makes the most sense. That's [$X] to get [specific deliverables]. We can have you sending within [timeline]. Want to move forward?"

---

## Quick Reference: Is This Client a Fit?

### Green Flags
- ✅ B2B service company with clear offer
- ✅ Average deal size > $2,000
- ✅ Knows their ICP
- ✅ Has capacity to take sales calls
- ✅ Understands this is a system, not magic

### Yellow Flags
- ⚠️ Unclear offer or positioning
- ⚠️ Very small TAM (< 5,000 potential contacts)
- ⚠️ No one to handle replies
- ⚠️ Expects results without volume

### Red Flags
- 🚫 No budget for platform costs (~$150-300/mo)
- 🚫 Wants guaranteed results without defining success
- 🚫 B2C or very low-ticket offers
- 🚫 Has burned sending domains before and doesn't know why
- 🚫 Expects "AI" to do everything with no human involvement

---

## Implementation Checklist

### Pre-Sale
- [ ] Discovery call or async exchange completed
- [ ] ICP and offer understood
- [ ] Tier selected and scoped
- [ ] Invoice sent and paid

### Infrastructure (All Tiers)
- [ ] Domains purchased or transferred
- [ ] Inboxes created
- [ ] DNS records configured
- [ ] Sequencer account set up
- [ ] Warm-up activated
- [ ] CRM/tracking configured

### Campaign (Tier 2+)
- [ ] Lead list built
- [ ] Copy written and approved
- [ ] Campaign loaded
- [ ] Test sends verified
- [ ] Campaign launched

### Handoff
- [ ] Loom walkthrough recorded
- [ ] Documentation in client's system
- [ ] Reply framework provided
- [ ] Check-in scheduled

### Optimization (Tier 2+)
- [ ] Week 2 data reviewed
- [ ] Adjustments made
- [ ] Recommendations documented
- [ ] Case study drafted (if results warrant)

---

*Last updated: February 2026*
