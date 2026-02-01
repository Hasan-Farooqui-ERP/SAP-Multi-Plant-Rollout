# Multi-Site ERP Rollout: Plant 22 & Plant 56

## Testing Version Control & Rollover Logic
To maintain data integrity across Plant 22 and Plant 56, I designed a tiered naming convention for all SIT/UAT documentation to ensure 100% traceability.

### The Naming Format
` <Functional Area>-<Plant ID>-<Version>-<Test Sequence> `

### Scalability & Rollover Logic
* **Automated Trigger:** Implemented a rollover trigger at sequence **99**.
* **Versioning Shift:** When a test sequence reached `<xx-xx-xx-99>`, the versioning tier was automatically incremented to `<xx-xx-xx+1-xx-01>`.
* **Example:** A sequence at `AA-22-01-99` would roll over to `AA-22-02-01`.

### Business Impact
This framework allowed for infinite scalability during long-term Greenfield testing phases. It effectively prevented data collisions and overlap between legacy tests and refined test cases, ensuring a "clean" audit trail for final sign-off.
