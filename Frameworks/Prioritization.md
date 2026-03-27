# Prioritization: API Developer Experience Overhaul

> How I prioritized across three parallel workstreams (SOAP-to-REST migration, certification program, documentation overhaul) while keeping 100+ live OBT integrations and 20+ vendor integrations running without disruption.

---

## The Core Tension

This project wasn't a single initiative. It was three interconnected workstreams, each valuable on its own, but each competing for the same small team's time (2 PMs, ~10 devs):

1. **SOAP-to-REST migration** -- the biggest engineering effort, highest latency impact, but required partner coordination that slowed everything down
2. **Certification program** -- the biggest onboarding impact, but useless without documentation to back it up
3. **Documentation overhaul** -- the highest ROI per effort-hour, but lowest visibility and hardest to get team excited about

Meanwhile, the existing ecosystem work didn't stop. Vendor onboardings, OBT partner support, customer escalations, and daily operational issues all continued. This wasn't a greenfield project with a dedicated team. It was a modernization running in parallel with a full production workload.

---

## Framework: Effort-to-Unblock Ratio

The north-star metric for the year was conversion rate. But for this specific project, the operating metric was **time-to-go-live for new partners**: how fast can a new OBT or vendor go from first API call to production traffic?

Every feature decision was scored against: **how much does this reduce time-to-go-live, relative to the effort to build it?**

This naturally surfaced a counter-intuitive priority order: documentation first, not migration first.

---

## Sequencing: Why Documentation Came Before Migration

### What I'd expect most PMs to do

Most PMs would start with the SOAP-to-REST migration. It's the most visible, most technically impressive, and most resume-friendly initiative. It also has the clearest metric (80% latency reduction).

### What I actually did

I started with the documentation overhaul. Here's why:

| Initiative | Time-to-go-live impact | Effort | When it pays off |
|-----------|----------------------|--------|-----------------|
| **Documentation overhaul** | High -- directly reduces the back-and-forth that extends every integration by weeks | Medium -- collecting and organizing 5 years of tribal knowledge is work, but it's not engineering-heavy | Immediately. The next partner to start integrating benefits. |
| **Certification program** | High -- eliminates subjective "it works" debates and gives partners a self-service path to go live | Medium -- needs documentation as input (test scenarios map to documented workflows) | After documentation exists. Certification without docs is just a test suite with no study guide. |
| **SOAP-to-REST migration** | Medium on time-to-go-live (new partners can start on REST, but existing partners need migration time) / High on latency | High -- engineering-heavy, requires partner coordination, 6+ months of parallel support | Gradually. Each partner that migrates gets the benefit, but the full payoff takes 12+ months. |

Documentation unlocked certification. Certification unlocked faster onboarding. Faster onboarding freed engineering time from support. Freed engineering time accelerated the migration. The order mattered.

---

## Prioritization Within Each Workstream

### Documentation: What to Document First

The 5-year archive of support tickets and integration questions was massive. I couldn't document everything at once. I prioritized by frequency and severity:

| Documentation Area | Frequency of Questions | Severity When Undocumented | Decision |
|-------------------|----------------------|---------------------------|----------|
| **Workflow variations by market** | Very high -- asked on every integration | High -- misunderstanding market-specific flows causes integration failures | **Document first** |
| **Configuration hierarchy** (global, entity, sub-entity, role) | High -- partners don't understand how filtering works | Very high -- causes bugs in production when configuration isn't applied correctly | **Document first** |
| **Edge cases** (unrecognized vendor content, cross-selling filters, loyalty eligibility) | Medium-high -- comes up mid-integration | Medium -- delays go-live but doesn't break production | **Document second** |
| **OTA standard divergences** | Medium -- asked by OTA-fluent partners | Medium -- saves time for experienced partners but not critical for new ones | **Document second** |
| **Error codes and troubleshooting** | Medium | Low-medium -- partners eventually figure it out but waste time | **Document third** |
| **Rate and availability refresh logic** | Low -- only matters for high-volume partners | Low -- niche issue | **Defer** |

### Certification: Which Scenarios First

The certification program needed test scenarios that covered the most common integration paths before the edge cases.

| Scenario Category | Coverage | Effort to Build | Decision |
|------------------|----------|-----------------|----------|
| **Search and book workflow** (standard) | Covers 80%+ of OBT integrations | Medium | **Build first** -- the core happy path |
| **Cancel and modify workflows** | Covers 60%+ of integrations | Medium | **Build first** -- high failure rate when untested |
| **Multi-market workflow variations** | Covers 40% (partners in multiple markets) | High | **Build second** -- significant subset but more complex test design |
| **Configuration edge cases** (role-level filtering, vendor exclusions) | Covers 20% (only complex enterprise integrations) | High | **Build third** -- lower frequency, higher complexity |
| **Content sanitization checks** (vendor-side) | Vendor integrations only | Very high | **Defer to vendor-specific process** -- too variable to standardize |

### Migration: Which Partners First

For SOAP-to-REST, the question was which partners to migrate first, knowing that each migration required coordination with the partner's own development team.

| Partner Profile | Migration Urgency | Partner Readiness | Decision |
|----------------|-------------------|-------------------|----------|
| **New OBTs not yet integrated** | N/A -- start on REST directly | High (no migration needed) | **Default to REST** for all new integrations |
| **High-volume OBTs on SOAP** | High -- biggest latency impact, most user-facing | Varies -- large OBTs have annual dev cycles | **Prioritize** but respect their timelines. Offer parallel support. |
| **Medium-volume OBTs on SOAP** | Medium | Often more agile than large OBTs | **Migrate second** -- easier coordination, meaningful volume |
| **Low-volume OBTs on SOAP** | Low | Often resource-constrained | **Migrate last or maintain parallel** -- low ROI on active migration effort |
| **Vendor integrations (GDS, chains)** | Medium-high (content latency matters) | Low -- GDS systems move slowly | **Offer REST option, don't force timeline** -- some needed 6+ months of parallel |

---

## The Bigger Prioritization: This Project vs. Daily Operations

The team was handling ongoing work alongside this modernization:

- Monthly calls with every major OBT partner
- Weekly/biweekly calls with strategic customers
- Vendor onboarding pipeline (new hotel chains, GDS migrations)
- Customer escalations (configuration issues, content problems)
- New feature requests from account managers

### How I Managed the Split

**Ring-fenced time, not ring-fenced people.**
I couldn't dedicate team members exclusively to the DX overhaul. Instead, I ring-fenced a percentage of each sprint for modernization work. Operational issues always had priority (you can't let production break), but modernization had a guaranteed floor of capacity every sprint.

**Treated support ticket reduction as a leading metric.**
Every documentation improvement that reduced support ticket volume freed engineering time for the next sprint. I tracked this explicitly: "Last month, we answered 15 questions about configuration hierarchy. This month, after publishing the configuration guide, we answered 3." That freed time became migration capacity.

**Used the certification program to reduce onboarding overhead.**
Before certification, every new OBT integration required 1-on-1 handholding from an engineer. After certification, partners could self-test. Each partner that went through certification independently was an engineer freed for migration work.

---

## Prioritization Under Pressure: The OBT Partner Dynamic

The hardest prioritization decisions came from partner dynamics:

**Partners who refused to migrate from SOAP:**
Some long-established OBT partners had built their entire integration on SOAP and had no appetite for migration. Forcing them would damage the relationship. I maintained parallel SOAP support for these partners while making REST the default for everything new. The cost of parallel support was bounded and decreasing (as other partners migrated, the SOAP infrastructure served fewer and fewer).

**Partners in different markets with different workflow expectations:**
Even the same OBT operating in multiple markets could have different workflow requirements per market. The documentation and certification program had to handle this without creating a combinatorial explosion of test scenarios. I solved this by documenting the market-specific variations as addenda to the core workflows, not as separate workflows entirely.

**Vendors with content quality problems:**
Vendor onboarding took longer than OBT onboarding because of content sanitization: checking whether hotel content arrived cleanly, with correct formatting, consistent data, and no broken fields. This couldn't be fully automated or certified the same way. I kept vendor onboarding as a partially manual process with sanitization checklists, rather than trying to force it into the same certification framework.

---

## What I'd Do Differently

1. **Quantify the support cost earlier.** I knew support was consuming engineering time, but I didn't have clean hourly data until partway through. Starting with a 2-week time-tracking exercise ("how many hours per week do we spend answering partner integration questions?") would have made the documentation ROI case airtight from day one.

2. **Build the self-service testing environment before the certification criteria.** We defined what "pass" meant before partners could test themselves. In practice, partners wanted to experiment before studying the rules. A sandbox environment available earlier would have accelerated adoption.

3. **Create a partner migration dashboard.** Tracking which partners were on SOAP vs. REST, who was mid-migration, and who had no plans to migrate would have helped in conversations with leadership about when to sunset SOAP support. Without it, the "when do we turn off SOAP?" question was always harder to answer than it should have been.

---

*All company names, client names, and partner names have been anonymized. Metrics and decision frameworks are accurate as applied.*
