# API Developer Experience Overhaul

> Cutting integration onboarding from months to weeks through SOAP-to-REST migration, a certification program, and documentation that pre-answered 5 years of support tickets.

## Context

**Company type**: European B2B hotel content aggregator (TravelTech)
**My role**: Product Manager, Search and Book Ecosystem
**Team**: Ecosystem team (2 PMs, ~10 devs)
**Timeline**: 2023-2024

---

## The Problem

The company had been running integrations for 20+ years. Over that time, the API landscape had accumulated layers of technical debt:

**Legacy SOAP APIs were still in production.** Many partner integrations were built on SOAP endpoints that predated the company's modern REST architecture. These were slower, harder to debug, and a pain for new developers to work with.

**Onboarding a new partner took 2-6 months.** A new online booking tool (OBT) integration involved extensive back-and-forth: clarifying API behavior, explaining edge cases, debugging misunderstandings, and resolving workflow mismatches. For vendor integrations (hotel chains, GDS systems), it was even longer due to content sanitization requirements.

**The documentation was technical but incomplete.** API specs existed, but they only covered the "happy path." The same questions kept coming up in every integration, and the answers lived in the heads of senior engineers and support tickets, not in any document a partner could reference.

Over 100 OBT integrations and 20+ vendor integrations were live. Every hour spent on support for a legacy integration was an hour not spent on new partnerships or product improvements.

---

## What I Did

### 1. SOAP-to-REST Migration

The legacy SOAP endpoints were a bottleneck for everything: performance, developer onboarding, and maintenance cost.

I led the migration to RESTful APIs. This wasn't just a protocol swap. It involved:

- **Mapping every active SOAP endpoint** to understand which partners depended on what
- **Designing the REST equivalents** with the engineering team, ensuring backward compatibility during the transition period
- **Coordinating migration timelines with partners**: we couldn't just turn off SOAP. Each partner needed a migration window, and some of the largest partners had their own development cycles that we had to work around
- **Versioning strategy**: implementing proper API versioning so future changes wouldn't break existing integrations (something the SOAP architecture never had cleanly)

**Result**: 80% reduction in API latency. Partners that migrated reported faster integration cycles and fewer support issues.

### 2. API Certification Program

The real onboarding bottleneck wasn't the API itself. It was the ambiguity around expected behavior, edge cases, and workflow variations.

I designed a certification program that formalized the integration process:

- **Standardized test workflows**: Partners could validate their integration against predefined scenarios (search, book, cancel, modify, edge cases) before going live
- **Clear pass/fail criteria**: No more "it works on our end" debates. Either the integration passed certification, or it didn't, with specific failure reasons documented
- **Self-service testing environment**: Partners could run certification tests independently, reducing dependency on our team for every test cycle

### 3. Documentation Overhaul

This was the highest-impact, lowest-glamour part of the project.

I led an effort to collect every recurring question, ticket, and support interaction from the past 5 years of integration work. We categorized them and built documentation that wasn't just an API reference, but a comprehensive integration guide:

- **Functional documentation alongside technical specs**: Not just "this endpoint returns X" but "here's why a booking workflow in market A differs from market B, and here's what your system needs to handle"
- **OTA standard context**: Explaining how our APIs mapped to OTA (Open Travel Alliance) standards, and where we diverged, so partners familiar with the standard could onboard faster
- **Edge case library**: Documented every known edge case with examples: what happens when a vendor sends content we don't recognize, how cross-selling content is filtered per customer configuration, how loyalty program eligibility is validated

---

## The Complexity: Multi-Layer Configuration

One of the hardest documentation challenges was the configuration hierarchy. Each customer organization could have rules at multiple levels:

- **Global level**: "No content from vendor X across all entities"
- **Entity level**: "Germany entity uses different rules than US entity"
- **Sub-entity level**: Different OBTs for different departments within the same entity
- **Role level**: VIPs see 5-star options, contractors have hard price caps

We had to make sure the API documentation, the certification tests, and the self-service configuration tools all reflected this hierarchy clearly. A partner integrating with us needed to understand not just the API contract, but how customer-specific rules would affect the responses they received.

---

## Outcomes

- **80% reduction in API latency** from SOAP-to-REST migration
- **Onboarding timeline reduced from months to weeks** for new OBT integrations
- **Support ticket volume dropped significantly** after documentation overhaul (partners could self-serve answers to questions that previously required engineering time)
- **35% increase in user adoption** through improved integration experience and market research across DACH and Europe
- **Certification program became the standard** for all new partner onboardings

---

## What I Learned

1. **Developer experience is product management.** An API is only as good as the experience of integrating with it. Latency, documentation, testing tools, and onboarding flow are all product surfaces that need the same rigor as any user-facing feature.

2. **Your support tickets are your backlog.** The 5-year archive of integration questions was the single best source of product requirements. Every recurring question was a documentation gap. Every recurring bug was a design flaw.

3. **Migrations need empathy for the partner's timeline.** We couldn't force partners to migrate from SOAP to REST on our schedule. The migration plan had to account for their development capacity, their release cycles, and their appetite for change. Some partners needed 6 months of parallel support.

4. **Certification programs reduce relationship overhead.** Before certification, every integration involved subjective back-and-forth about whether something "worked." After certification, it was binary: pass or fail, with clear remediation steps. This made relationships healthier, not more transactional.

---

*All company names, client names, and partner names have been anonymized. Metrics and technical details are accurate as described.*
