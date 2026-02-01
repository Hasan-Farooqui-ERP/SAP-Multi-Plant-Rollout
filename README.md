# Multi-Site ERP Rollout: Plant 22 & Plant 56

## Technical Case Study: Organizational & Asset Governance
**The Challenge:** The project involved two standalone plants separated by 200km in a mountainous region. The extreme terrain and unpredictable weather conditions presented significant risks to physical infrastructure (towers and cabling) and made manual site inspections difficult. Legacy data systems lacked the granularity to isolate specific "points of failure" in these high-stakes environments.

**The Solution:** I architected a 7-tier naming logic: `<Country>-<Area>-<Plant ID>-<Site ID>-<Asset Group>-<Version>-<Sequence>`.

**Future-Proofing (SCADA):** Drawing on lessons learned from SCADA infrastructure projects, this logic was specifically designed to bridge the gap between back-office ERP data and future real-time monitoring. By providing granular asset-level identifiers, the system is prepared to handle the eventual integration of complex linear assets, allowing for a transition from reactive to predictive maintenance.

## Testing Version Control & Rollover Logic
To maintain data integrity across Plant 22 and Plant 56, I designed a tiered naming convention for all SIT/UAT documentation to ensure 100% traceability.

### The Naming Format
`<Country>-<Area>-<Plant ID>-<Site ID>-<Asset Group>-<Version>-<Sequence>`

Example for your portfolio: IE-AA-P56-S01-A01-01-86

IE-AA: Ireland - Functional Area

P56-S01: Plant 56 - Site 01 (One of the 200km+ locations)

A01-01-86: Asset Group - Version - Test Sequence

### Scalability & Rollover Logic
* **Automated Trigger:** Implemented a rollover trigger at sequence **99**.
* **Versioning Shift:** When a test sequence reached `<xx-xx-xx-99>`, the versioning tier was automatically incremented to `<xx-xx-xx+1-xx-01>`.
* **Example:** A sequence at `AA-22-01-99` would roll over to `AA-22-02-01`.

### Business Impact
   Business Impact: The "Digital Eyes" Framework
   
This architecture was designed to provide "Digital Eyes" in a mountainous region where extreme weather and terrain make physical asset inspection a high-risk, high-cost operation.

Precision in Harsh Terrain: By utilizing a 7-tier logic, the ERP can pinpoint failure locations across 200km of remote infrastructure, allowing for informed deployment of maintenance crews only when and where necessary.

Infinite Scalability: The framework prevented data collisions between legacy systems and new Greenfield data, ensuring a clean audit trail for final sign-off.

Predictive Readiness: The transition from reactive to predictive maintenance is now possible; the system can ingest real-time data to identify specific asset degradation before a physical failure occurs in the field.
This framework allowed for infinite scalability during long-term Greenfield testing phases. It effectively prevented data collisions and overlap between legacy tests and refined test cases, ensuring a "clean" audit trail for final sign-off.

```mermaid

graph TD
    Start([New Test Case Created]) --> Format[Format: Country-Area-Plant-Site-Asset-Ver-Seq]
    Format --> Check{Sequence > 99?}
    
    Check -- No --> Increment[Increment Sequence +1]
    Check -- Yes --> Rollover[Reset Sequence to 01]
    
    Rollover --> UpdateVersion[Increment Version +1]
    
    Increment --> Final[ID: IE-AA-P56-S01-A01-01-86]
    UpdateVersion --> Final
    
    Final --> Impact[Outcome: Digital Eyes Traceability]
    
    style Final fill:#28a745,stroke:#fff,color:#fff
    style Rollover fill:#f39c12,stroke:#fff,color:#fff
    style Impact fill:#007bff,stroke:#fff,color:#fff```

 
