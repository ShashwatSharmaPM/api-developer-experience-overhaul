# After state: REST APIs, certification program, self-serve documentation

> 80% latency reduction. Onboarding cut from months to weeks. Documentation that pre-answers 5 years of support tickets. Certification as the standard for all new integrations.

```mermaid
graph TD
    VENDOR[Vendors<br/>hotels, chains, GDS] -->|Content in via REST| API[Unified REST API layer<br/>versioned, low latency]
    API -->|Content out via REST| OBT[OBTs<br/>100+ integrations]
    OBT --> TRAV[Travelers book hotels]

    API --- CERT[Certification program]
    API --- DOCS[Dual-layer documentation]
    API --- CONFIG[Configuration guide<br/>all 4 hierarchy levels]

    classDef api fill:#2d9d78,color:#fff,stroke:#1d7a5c
    classDef ext fill:#4a8bc2,color:#fff,stroke:#3670a0
    classDef support fill:#a3dcc8,color:#0a2a1e,stroke:#5dbfa0
    classDef trav fill:#777,color:#fff,stroke:#555

    class API api
    class VENDOR,OBT ext
    class CERT,DOCS,CONFIG support
    class TRAV trav
```

### New onboarding flow

```mermaid
graph TD
    NEW[New OBT partner<br/>wants to integrate] --> DOCS[Reads dual-layer documentation<br/>technical specs + functional context]
    DOCS --> SELF[Self-service testing environment<br/>runs certification scenarios]
    SELF --> PASS{Certification<br/>pass or fail?}

    PASS -->|Pass| LIVE[Go live<br/>weeks, not months]
    PASS -->|Fail| FIX[Specific failure reasons documented<br/>partner fixes and retests]
    FIX --> SELF

    classDef start fill:#4a8bc2,color:#fff,stroke:#3670a0
    classDef step fill:#a3dcc8,color:#0a2a1e,stroke:#5dbfa0
    classDef check fill:#c68a2e,color:#fff,stroke:#a06e1e
    classDef good fill:#2d9d78,color:#fff,stroke:#1d7a5c
    classDef fix fill:#e8a0a0,color:#2a0a0a,stroke:#c27070

    class NEW start
    class DOCS,SELF step
    class PASS check
    class LIVE good
    class FIX fix
```

### Documentation architecture

```mermaid
graph TD
    DOC[Dual-layer documentation] --> TECH[Technical layer<br/>endpoints, schemas, auth, versioning]
    DOC --> FUNC[Functional layer<br/>5 years of support questions answered]

    FUNC --> WF[Workflow variations<br/>by market and OBT type]
    FUNC --> EDGE[Edge case library<br/>with real examples]
    FUNC --> OTA[OTA standard mapping<br/>where we align and diverge]
    FUNC --> CONF[Configuration hierarchy guide<br/>global, entity, sub-entity, role]

    classDef doc fill:#2d9d78,color:#fff,stroke:#1d7a5c
    classDef tech fill:#4a8bc2,color:#fff,stroke:#3670a0
    classDef func fill:#c68a2e,color:#fff,stroke:#a06e1e
    classDef detail fill:#a3dcc8,color:#0a2a1e,stroke:#5dbfa0

    class DOC doc
    class TECH tech
    class FUNC func
    class WF,EDGE,OTA,CONF detail
```

## Before vs. after comparison

| Dimension | Before | After |
|-----------|--------|-------|
| **API protocol** | Mix of SOAP and REST in production | Unified REST. SOAP deprecated with parallel support during migration. |
| **Latency** | SOAP endpoints significantly slower | 80% reduction in API latency |
| **OBT onboarding time** | 2-6 months | 2-2.5 months (weeks for standard workflows) |
| **Documentation** | Technical specs only, happy path | Dual-layer: technical specs + functional documentation with 5 years of Q&A |
| **Edge cases** | Lived in engineers' heads | Documented edge case library with real examples |
| **Certification** | No formal process. Subjective "it works" sign-off. | Standardized certification with pass/fail criteria and self-service testing |
| **Configuration docs** | Poorly documented | Full hierarchy guide: global, entity, sub-entity, role-level rules |
| **OTA standard context** | Not documented | Explicit mapping showing alignment and divergences from OTA |
| **Support ticket volume** | High. Same questions repeated every integration. | Significantly reduced. Partners self-serve via documentation. |
| **User adoption** | Baseline | 35% increase across DACH and Europe |
| **Engineering time on support** | Major drain. Hours per week on recurring questions. | Freed up for new partnerships and product improvements. |

## Key architectural decisions

**Why dual-layer documentation, not just better API specs:**
API specs (endpoints, schemas, auth) are necessary but not sufficient. Partners needed functional context: why does a booking workflow in Germany differ from France? What happens when a vendor sends content our system doesn't recognize? How does the configuration hierarchy filter responses? These questions can't be answered by an OpenAPI spec. The functional layer addressed the questions that actually caused integration delays.

**Why a certification program, not just faster support:**
Faster support treats the symptom (partners waiting for answers). Certification treats the cause (ambiguity about what "working" means). By defining standardized test scenarios with binary pass/fail outcomes, we eliminated the subjective back-and-forth that dragged out every integration. Partners could self-test, fail fast, fix specific issues, and retest without waiting for our team.

**Why parallel SOAP/REST support during migration:**
Forcing partners to migrate on our timeline would have damaged relationships with our largest integrations. Some OBTs have annual release cycles. Some GDS systems move even slower. Parallel support was expensive (maintaining two protocol versions), but it was the only way to migrate without breaking trust. The cost was bounded (we knew when SOAP would sunset) and the payoff was permanent (80% latency reduction, cleaner versioning, easier maintenance).

**Why OTA standard mapping mattered:**
Most partners in the travel industry are familiar with OTA (Open Travel Alliance) standards. Our APIs mostly aligned with OTA but diverged in specific areas. Without documenting where we aligned and where we didn't, every partner had to discover the divergences through trial and error during integration. Explicitly calling out "we follow OTA for X, but we do Y differently because Z" saved weeks per integration.
