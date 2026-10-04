# Changelog

All notable methodological changes to the **Threat Scenario-Based Detection Use Case Framework** are documented here.

## Draft v0.2 — 2026-09-30

### Added

- Formal definition of **Detection Capability (CD)**.
- Formal definition of **Detection Unit (UD)**.
- Five baseline threat-scenario phases:
  - Reconnaissance
  - Initial Access
  - Execution / Action
  - Persistence / Lateral Movement
  - Exfiltration / Impact
- End-to-end methodological flow from risk and threat context through detection, coverage, response, and improvement.
- Explicit relationship between UD and telemetry.
- UD automation eligibility model.
- Progressive automation levels from observation to controlled containment.
- Early automation focus for Reconnaissance and Initial Access.
- Automation Coverage as an additional measurement dimension.
- English overview for broader technical accessibility.

### Changed

- Replaced the detection use case as the only design unit with the CD/UD hierarchy.
- Extended the framework from detection coverage into detection-and-response engineering.
- Updated the main README and introductory chapter to reflect v0.2.

## Draft v0.1 — 2026-08-17

### Added

- Initial framework concept.
- Threat scenario as the primary design and evaluation unit.
- Initial relationship between Threat Intelligence, Threat Modeling, detection opportunities, telemetry, detection use cases, coverage, and improvement.
- Initial gap categories:
  - Detection Gap
  - Telemetry Gap
  - Visibility Gap
  - Control / Architecture Gap
