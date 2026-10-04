# Threat Scenario-Based Detection Use Case Framework — English Overview

> **Draft v0.2**

## Overview

The **Threat Scenario-Based Detection Use Case Framework** is a vendor-neutral, threat-informed Detection Engineering methodology designed to transform relevant **threat scenarios** into measurable and improvable detection and response capabilities.

Instead of starting from isolated SIEM rules, alerts, signatures, or available log sources, the framework starts with a different question:

> **Which threat scenario must the organization be able to detect, how can it evolve, what adversary behaviors can be observed, and what detection and response capabilities are required across its progression?**

The framework connects:

**Risk / Security Objective**  
→ **Threat Intelligence / Context**  
→ **Threat Scenario**  
→ **Threat Modeling**  
→ **Attack Phases**  
→ **Adversary Behaviors**  
→ **Detection Capabilities (CD)**  
→ **Detection Units (UD)**  
→ **Data Sources / Telemetry**  
→ **Detection Logic**  
→ **MITRE ATT&CK Mapping**  
→ **Coverage & Gaps**  
→ **Response / Automation**  
→ **Validation & Continuous Improvement**

## Detection Capability (CD)

A **Detection Capability (CD)** represents a methodological detection requirement: what behavior, condition, or manifestation of a threat scenario the organization needs to be able to detect.

A Detection Capability is intentionally independent from a specific SIEM query, vendor product, or detection language.

## Detection Unit (UD)

A **Detection Unit (UD)** is a concrete, implementable, testable, and measurable detection logic that materializes part of a Detection Capability.

A Detection Unit should define, at minimum:

- related threat scenario;
- attack phase;
- parent Detection Capability;
- observable behavior;
- required data sources and telemetry;
- detection conditions and time window;
- exclusions;
- expected evidence;
- MITRE ATT&CK mapping where applicable;
- confidence and criticality;
- response action;
- automation eligibility;
- reversibility and escalation conditions.

## Attack phases

The v0.2 baseline uses five phases:

1. **Reconnaissance**
2. **Initial Access**
3. **Execution / Action**
4. **Persistence / Lateral Movement**
5. **Exfiltration / Impact**

These phases provide a common structure for modeling progression and measuring detection coverage. They are not intended to imply that every attack follows a strictly linear sequence.

## Coverage model

The framework aims to measure more than the number of implemented detection rules.

Coverage should be evaluated across:

- threat scenario;
- attack phase;
- adversary behavior;
- Detection Capability;
- Detection Unit;
- telemetry availability;
- validation status;
- response and automation readiness.

## Gap model

The framework distinguishes four major gap types:

- **Detection Gap:** sufficient telemetry exists, but an adequate Detection Unit is missing.
- **Telemetry Gap:** no available source provides the required evidence.
- **Visibility Gap:** the source exists, but the required data is not enabled, collected, normalized, or accessible.
- **Control / Architecture Gap:** architecture or controls limit the ability to observe, detect, or respond.

## Early response automation

A core objective of v0.2 is to connect Detection Units to controlled response automation, particularly in the earliest phases of an attack.

Examples include:

- automatic enrichment;
- reputation and geolocation checks;
- risk scoring;
- watchlist updates;
- rate limiting;
- temporary IP blocking;
- session termination;
- token revocation;
- temporary account containment;
- endpoint isolation where appropriate.

Automation is not treated as a binary decision. The framework uses progressive levels ranging from observation and enrichment to reversible containment and, under strict governance, higher-impact response.

## Related fields

This project intersects with:

- Threat Modeling
- Threat-Informed Defense
- Detection Engineering
- Security Operations / SOC
- SIEM
- SOAR
- MITRE ATT&CK
- Detection Coverage
- Telemetry Engineering
- Detection Automation
- Incident Response
- Detection Use Case Management

## Project status

The project is currently under active development as **Draft v0.2**. The next major milestone is to publish a complete end-to-end reference threat scenario showing the relationship between attack phases, Detection Capabilities, Detection Units, telemetry, MITRE ATT&CK mapping, coverage, gaps, and response automation.
