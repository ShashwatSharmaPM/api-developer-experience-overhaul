# Stakeholder Map: API Developer Experience Overhaul

> This project's stakeholders weren't just internal teams. They were 100+ OBT partners, 20+ vendors, and dozens of enterprise customers, each with their own development cycles, technical preferences, and tolerance for change. The product was the API. The users were other companies' engineering teams.

---

## Why This Project Had Unusual Stakeholder Complexity

Most developer experience projects serve developers inside your own company or developers building on your public platform. This one served **partner engineering teams at other companies** who had their own priorities, their own release schedules, and their own opinions about how APIs should work.

That meant:
- I couldn't mandate migration timelines. Partners migrated when their dev teams had capacity.
- Documentation had to serve wildly different technical audiences: some partners were OTA-fluent travel tech specialists; others were generalist engineering teams building their first travel integration.
- The certification program had to feel helpful, not gatekeeping. If partners experienced it as bureaucracy, they'd push back through their account managers.
- Every change to the API, even improvements, required change management across 100+ live integrations.

---

## Stakeholder Map

### OBT Partners (100+ Online Booking Tools)

**What they cared about**: Stable APIs, clear documentation, fast issue resolution, not being forced to change things that already work.

**Their concern with this project**: "We've built our integration on SOAP over the last 5 years. It works. Why should we spend engineering time migrating to REST? What's in it for us?"

**How I managed them**:
- Never forced migration timelines. Made REST the default for all new integrations, and offered SOAP partners a migration path with parallel support for as long as they needed (some required 6+ months).
- Led the migration pitch with partner benefits, not our benefits: "REST is 80% faster. Your users experience lower latency. Your debugging is easier. Your next integration change will take days, not weeks."
- For each major OBT, I had at least one call per month (existing cadence) to understand what they were working on, flag upcoming changes on our side, and advertise new capabilities. This relationship continuity meant the migration and certification conversations happened inside existing trust, not as cold announcements.
- The certification program was positioned as a service: "This gives your team a self-service way to validate your integration without waiting for our engineers. You can test on your schedule." Not: "You must pass certification to go live."

**What they needed from me**: No breaking changes to existing integrations, clear documentation they could hand to their own developers, self-service testing capability, and respect for their own timelines.

**Alignment mechanism**: Monthly partner calls, migration timeline co-created per partner, self-service certification environment, dual-layer documentation.

---

### Vendor Partners (20+ Hotel Chains, GDS Systems, Aggregators)

**What they cared about**: Getting their hotel content distributed to as many OBTs as possible through us, content being displayed correctly, minimal integration maintenance.

**Their concern with this project**: "Our integration already works. We publish our content via OTA standards. If you change your APIs, we don't want to change ours. Also, content sanitization takes too long. Speed that up."

**How I managed them**:
- Vendor integrations were inherently different from OBT integrations. OBTs consumed our content (we controlled the output format). Vendors pushed content to us (we had to handle whatever format they sent). This meant vendor-side DX was less about API design and more about content quality and mapping.
- Documented OTA standard alignment and divergences explicitly. Vendors who followed OTA standards could see immediately where their existing integration matched our expectations and where adjustments were needed. This alone saved weeks per vendor onboarding.
- Did not force vendors into the same certification framework as OBTs. Vendor onboarding included a content sanitization phase (checking content quality, field consistency, data formatting) that was too variable to standardize into binary pass/fail. Instead, created sanitization checklists specific to vendor type (GDS vs. direct chain vs. aggregator).
- Highlighted the direct-connect value proposition: one major hotel chain moved from GDS to a direct connection with us because it eliminated GDS fees. These transitions required careful coordination but the vendor was motivated by cost savings.

**What they needed from me**: OTA alignment documentation, clear content sanitization expectations, minimal changes to their existing publishing workflow.

**Alignment mechanism**: Vendor onboarding checklists, OTA mapping documentation, direct coordination during content sanitization phase.

---

### Enterprise Customers (Organizations Booking Through OBTs)

**What they cared about**: Hotels showing up correctly, configuration rules being applied properly, bookings working reliably.

**Their concern with this project**: Most customers didn't know or care about the API layer. Their concern surfaced indirectly: "Why is hotel X not showing up?" or "Why are my contractors seeing 5-star hotels when the policy caps them at 3-star?"

**How I managed them**:
- Customers interacted with the API indirectly through OBTs. Their experience of the DX overhaul was: integrations work faster, fewer bugs in configuration application, and new OBTs onboard more quickly (expanding their booking options).
- The configuration hierarchy documentation (global, entity, sub-entity, role-level rules) was primarily for partner engineers, but it also served the implementation team who configured these rules for customers. Better docs meant fewer configuration errors, which meant fewer customer complaints.
- Account managers were briefed on the DX overhaul so they could explain to customers why things were improving: "We've simplified our integration process, which means your new OBT will be ready faster" or "We've fixed the configuration documentation, which is why the filtering issues you reported are resolved."

**What they needed from me**: Working integrations. Correct configuration. Faster access to new OBT options. They didn't need to know about the API layer.

**Alignment mechanism**: Indirect, via account managers and the implementation team. Customer-facing impact communicated through existing relationship channels.

---

### Account Managers

**What they cared about**: Customer satisfaction, retention, being able to answer customer questions about integration timelines, not being surprised by partner-facing changes.

**Their concern with this project**: "If you're changing the APIs, will that break anything for my customers? And when a customer asks when their new OBT integration will be ready, what do I tell them now vs. before?"

**How I managed them**:
- Briefed account managers on what the DX overhaul meant for their customer conversations. The key message: "Integrations will be faster. Your customers will get access to new OBTs sooner. Existing integrations won't break."
- Gave them updated onboarding timelines they could share with customers. Before: "2-6 months." After: "2-2.5 months for standard workflows."
- When individual partners were mid-migration (SOAP to REST), I flagged it to the relevant account managers so they could set customer expectations: "Your OBT partner is updating their integration with us. You might see a brief testing window. Everything will be faster afterward."
- Account managers were also a valuable input channel. They heard customer complaints about specific OBT integrations ("booking in market X is slow," "cancel workflow doesn't work the way we expect"). These complaints often traced back to integration issues that the documentation or certification program could address.

**What they needed from me**: Updated timelines, advance notice of partner changes, and talking points for customer conversations.

**Alignment mechanism**: Briefings before partner-facing changes, updated onboarding timeline guidance, escalation path for integration-related customer complaints.

---

### Engineering Team (~10 Developers)

**What they cared about**: Reducing support burden, working on interesting technical problems, not maintaining two protocol versions forever.

**Their concern with this project**: "SOAP-to-REST migration is the right thing to do, but we're already stretched thin with partner support and operational issues. When do we actually get time to build this?"

**How I managed them**:
- Ring-fenced modernization capacity in every sprint rather than asking for a dedicated block of time. This meant the team always made progress on the DX overhaul without stopping operational work.
- Positioned the documentation overhaul as support burden reduction. Every doc improvement that reduced incoming questions was time the team got back. I tracked this explicitly: fewer configuration questions this month meant more migration capacity next month.
- The certification program was designed to free engineering time from onboarding handholding. Before certification, an engineer had to be on call for every new partner's integration process. After certification, partners self-tested. Each partner that went through certification independently was an engineer freed for other work.
- Gave the team ownership of the REST API design decisions. I defined what the REST APIs needed to achieve (which workflows to support, what backward compatibility constraints to maintain, what the versioning strategy should look like from a partner perspective). Engineering owned the implementation architecture.
- The SOAP sunset question ("when do we stop supporting SOAP?") was a source of anxiety. I set the expectation clearly: SOAP stays until the last high-value partner migrates, but we stop investing in SOAP improvements. New features go to REST only. This gave the team a clear direction without the pressure of an arbitrary cutoff date.

**What they needed from me**: Protected time for modernization work, fewer support interruptions (via better docs and certification), ownership of technical architecture decisions, and a clear SOAP sunset policy.

**Alignment mechanism**: Sprint-level modernization capacity, support ticket tracking as a leading metric, collaborative REST API design sessions, clear SOAP deprecation policy.

---

### Product Leadership

**What they cared about**: Revenue growth, partner acquisition velocity, ecosystem competitiveness, the north-star conversion rate metric.

**Their concern with this project**: "This is infrastructure work. It doesn't ship features. How does it connect to our revenue targets?"

**How I managed them**:
- Framed the DX overhaul as a revenue accelerator: "Every month we cut from onboarding time is a month earlier that a new OBT starts sending booking traffic through our platform. That traffic converts to bookings. Bookings convert to revenue."
- Connected the 35% user adoption increase (from market research across DACH and Europe) to the improved integration experience: new partners in previously underserved markets could onboard faster, which expanded our content distribution.
- The 80% latency reduction from SOAP-to-REST was positioned as a conversion metric improvement: faster API responses mean faster search results in OBTs, which means travelers are more likely to book through our content before abandoning to a competitor.
- Showed the support cost reduction: hours freed from answering recurring partner questions were hours the team could spend on new partnerships and product improvements.

**What they needed from me**: A connection between DX investment and revenue metrics, proof that onboarding was actually getting faster, and confidence that the migration wouldn't break existing integrations.

**Alignment mechanism**: Quarterly updates with onboarding timeline improvements, latency reduction metrics, support ticket trends, and new partner pipeline velocity.

---

## How Stakeholder Dynamics Shifted Over the Project Lifecycle

| Phase | Who Had the Loudest Voice | My Focus |
|-------|--------------------------|----------|
| **Documentation overhaul** | Engineering team (support burden) + OBT partners (recurring questions) | Collecting 5 years of tribal knowledge, categorizing by frequency, publishing in partner-accessible format |
| **Certification program** | OBT partners (self-service demand) + account managers (onboarding timeline questions) | Designing test scenarios, building self-service environment, positioning certification as service not gatekeeping |
| **SOAP-to-REST migration** | Vendor partners (content latency) + product leadership (performance metrics) | Partner-by-partner migration coordination, parallel support planning, SOAP sunset policy |
| **Ongoing operations** | Customers (indirectly via account managers) | Configuration issues, content quality, new market support |

---

## Key Takeaway

The defining insight on this project was that developer experience is product management for a different user. The "users" of this DX overhaul were partner engineering teams at 100+ other companies. They didn't file feature requests. They filed support tickets. They didn't churn visibly. They just took 6 months to integrate instead of 6 weeks, and during that time, their travelers booked hotels through someone else.

Treating support tickets as the backlog, treating onboarding time as the north-star metric, and treating partner engineering teams as users (not vendors, not customers, but users of our API product) was the framing shift that made the prioritization clear. Documentation before migration. Certification before features. Self-service before handholding.

---

*All company names, client names, and partner names have been anonymized. Stakeholder dynamics and management approaches are accurate as experienced.*
