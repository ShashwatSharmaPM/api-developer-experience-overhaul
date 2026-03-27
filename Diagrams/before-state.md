# Before state: legacy APIs, slow onboarding, tribal knowledge

> 100+ OBT integrations, 20+ vendor integrations, SOAP still in production, onboarding taking 2-6 months, and 5 years of support questions living in people's heads.

```mermaid
graph TD
    VENDOR[Vendors<br/>hotels, chains, GDS] -->|Content in| HRS[HRS Content layer]
    HRS -->LEGACY[Mix of SOAP and REST<br/>endpoints in production]
    LEGACY --> |Content out| OBT[OBTs<br/>online booking tools]
    OBT --> TRAV[Travelers book hotels]


    classDef hrs fill:#c68a2e,color:#fff,stroke:#a06e1e
    classDef ext fill:#4a8bc2,color:#fff,stroke:#3670a0
    classDef legacy fill:#d94f4f,color:#fff,stroke:#b33a3a
    classDef trav fill:#777,color:#fff,stroke:#555

    class HRS hrs
    class VENDOR,OBT ext
    class LEGACY legacy
    class TRAV trav
```

### The onboarding bottleneck

```mermaid
graph TD
    NEW[New OBT partner wants<br/>to integrate] --> READ[Reads API documentation]
    READ --> GAPS[Docs cover happy path only<br/>edge cases undocumented]
    GAPS --> ASK[Partner asks questions<br/>via support tickets]
    ASK --> WAIT[Engineering team answers<br/>from tribal knowledge]
    WAIT --> MORE[More questions arise<br/>during implementation]
    MORE --> ASK

    ASK --> TIMELINE[2-6 months to go live]

    classDef start fill:#4a8bc2,color:#fff,stroke:#3670a0
    classDef problem fill:#e8a0a0,color:#2a0a0a,stroke:#c27070
    classDef loop fill:#d94f4f,color:#fff,stroke:#b33a3a
    classDef result fill:#c68a2e,color:#fff,stroke:#a06e1e

    class NEW start
    class READ,GAPS problem
    class ASK,WAIT,MORE loop
    class TIMELINE result
```

### SOAP vs. REST: the technical debt

```mermaid
graph TD
    SOAP[Legacy SOAP endpoints] --> SLOW[Higher latency]
    SOAP --> HARD[Harder to debug]
    SOAP --> NOVERSION[No clean versioning]
    SOAP --> DEVPAIN[New developers struggle<br/>with SOAP tooling]

    REST[Modern REST endpoints] --> FAST[Lower latency]
    REST --> EASY[Standard tooling]
    REST --> VERSION[Proper versioning]

    SOAP --- MIXED[Both running in production<br/>partners on different protocols]
    REST --- MIXED

    classDef soap fill:#d94f4f,color:#fff,stroke:#b33a3a
    classDef rest fill:#2d9d78,color:#fff,stroke:#1d7a5c
    classDef problem fill:#e8a0a0,color:#2a0a0a,stroke:#c27070
    classDef good fill:#a3dcc8,color:#0a2a1e,stroke:#5dbfa0
    classDef mixed fill:#c68a2e,color:#fff,stroke:#a06e1e

    class SOAP soap
    class REST rest
    class SLOW,HARD,NOVERSION,DEVPAIN problem
    class FAST,EASY,VERSION good
    class MIXED mixed
```


## Pain points summary

| Problem | Impact |
|---------|--------|
| **SOAP endpoints still in production** | Higher latency, harder debugging, no clean versioning. New developers avoid SOAP tooling. |
| **Onboarding takes 2-6 months** | Extensive back-and-forth on edge cases, workflow variations, and configuration behavior. Every integration repeats the same questions. |
| **Documentation covers only happy path** | 5 years of recurring support questions live in senior engineers' heads, not in docs. Partners can't self-serve. |
| **No formal certification process** | "It works on our end" debates. No standardized pass/fail criteria. Going live is subjective. |
| **Configuration hierarchy undocumented** | Partners don't understand how global, entity, sub-entity, and role-level rules interact to filter API responses. Causes integration bugs. |
| **Vendor onboarding even slower** | Content sanitization adds significant time on top of workflow integration. Checking if content comes in cleanly is a manual, lengthy process. |
| **Engineering time consumed by support** | Every hour answering partner questions is an hour not spent on new partnerships or product improvements. |
