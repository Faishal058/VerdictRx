# VerdictRx

### AI-Powered Pharmaceutical Cold-Chain Excursion Intelligence & Quality Decision Support System

> **From Temperature Alerts to Evidence-Backed QA Decisions.**

VerdictRx is an AI-assisted investigation and workflow automation system
designed to help pharmaceutical Quality Assurance (QA) teams handle
temperature excursions across cold-chain shipments.

Instead of stopping at temperature alerts, VerdictRx turns an excursion
into a structured, evidence-backed case: it resolves shipment and
product context, retrieves applicable evidence, performs deterministic
thermal assessment, identifies uncertainty and evidence gaps, initiates
a quarantine workflow, prepares a QA-ready evidence pack, and records
the final human disposition in an auditable workflow.

------------------------------------------------------------------------

## The Problem

A temperature alert is only the beginning of a pharmaceutical cold-chain
investigation.

When an excursion occurs, QA teams may need to determine whether
affected stock should be:

-   Quarantined
-   Investigated further
-   Cleared for use

The required evidence can be distributed across:

-   Temperature logs
-   Shipment records
-   Manufacturer stability references
-   WMS / inventory information
-   Historical cases

Manual investigation and coordination can delay quality decisions while
products remain quarantined.

### The gap

Traditional monitoring systems can detect breaches, display graphs, and
send alerts. Detection does not complete the investigation.

**VerdictRx focuses on investigation-to-QA workflow automation rather
than another temperature dashboard.**

------------------------------------------------------------------------

## What VerdictRx Does

``` text
Temperature Event
       ↓
Context Resolution
       ↓
Thermal Assessment
       ↓
AI Investigation
       ↓
Quarantine & Notifications
       ↓
Human QA Review
       ↓
Auditable Closure
```

### 1. Context Resolution

Determines the relevant shipment, product, batch, and historical
context.

### 2. Deterministic Thermal Assessment

Calculates exposure using defined product and manufacturer context.

The deterministic engine supports:

-   Product-specific exposure calculations
-   Manufacturer excursion allowances
-   Cumulative exposure versus stability budget
-   Uncertainty bounds
-   MKT only when applicability is validated

Thermal calculations are separated from the AI reasoning layer.

### 3. AI Investigation

The AI layer helps:

-   Retrieve approved contextual information
-   Assemble evidence
-   Synthesize the investigation narrative
-   Identify missing evidence
-   Prepare a recommendation

The LLM does **not** define or override stability thresholds.

### 4. Quarantine & Notifications

The workflow can initiate the demonstrated quarantine process and notify
relevant stakeholders.

For the prototype, the WMS integration is mocked.

### 5. Human QA Review

An authorized QA reviewer remains responsible for the final disposition:

-   Approve
-   Reject
-   Request additional evidence

Every final decision is intended to be recorded in the audit trail.

> **VerdictRx prepares the verdict; authorized QA delivers it.**

------------------------------------------------------------------------

## Core Innovation

VerdictRx combines three capabilities into one closed-loop system.

### 01 --- Deterministic Thermal Adjudication

-   Product-specific exposure calculations
-   Manufacturer allowances applied first
-   MKT only through an applicability gate
-   Uncertainty bounds on results

### 02 --- Explainable AI Investigation

-   Context retrieval across five sources
-   Evidence synthesis and narrative generation
-   Missing-evidence escalation
-   Retrieval over approved documents
-   LLM does not set stability thresholds

### 03 --- Closed-Loop QA Automation

-   Quarantine execution and verification
-   Stakeholder notifications and SLA timers
-   Human disposition capture
-   Immutable / hash-chained audit trail

> **Deterministic science decides the numbers. AI does the investigation
> homework. Authorized QA makes the final call.**

------------------------------------------------------------------------

## AI Agents

VerdictRx uses four AI agents:

  -----------------------------------------------------------------------
  Agent                               Responsibility
  ----------------------------------- -----------------------------------
  **Triage Agent**                    AI-driven triage and severity
                                      processing

  **Context Agent**                   Shipment, product, batch and
                                      historical context gathering

  **Investigation Agent**             Evidence assembly and investigation
                                      tasks

  **CAPA/Learning Agent**             Corrective / preventive follow-up
                                      actions and learning patterns
  -----------------------------------------------------------------------

The AI layer is constrained by deterministic rules and the evidence
available to the system.

------------------------------------------------------------------------

## System Architecture

``` text
                    ┌─────────────────────┐
                    │   React QA Dashboard│
                    └──────────┬──────────┘
                               │ REST API
                               ▼
                    ┌─────────────────────┐
                    │    n8n Orchestrator │
                    │ Event-driven Core   │
                    └──────────┬──────────┘
                               │
              ┌────────────────┼─────────────────┐
              │                │                 │
              ▼                ▼                 ▼
       Triage Agent      Context Agent    Investigation Agent
              │                │                 │
              └────────────────┼─────────────────┘
                               │
                         CAPA/Learning
                             Agent
                               │
              ┌────────────────┴────────────────┐
              │                                 │
              ▼                                 ▼
     Deterministic Thermal                Workflow Actions
          Engine                       Hold / Notify / Audit
              │                                 │
              └────────────────┬────────────────┘
                               ▼
                         PostgreSQL
```

### Prototype integrations

-   **Simulated IoT telemetry** --- scripted spike, drift, freeze and
    logger-gap scenarios
-   **Mocked WMS** --- accepts and verifies quarantine holds

These are demonstration integrations, not claims of production
deployment.

------------------------------------------------------------------------

## n8n Workflow

n8n is the central event-driven workflow engine for the PS22
implementation.

The demonstrated workflow includes:

1.  Webhook trigger
2.  Data validation
3.  Severity assignment
4.  Data enrichment
5.  Exposure calculation
6.  Evidence assembly
7.  Stock quarantine
8.  Notifications and SLA handling
9.  QA approval / rejection
10. Tamper-evident audit closure
11. CAPA / learning follow-up

### Exception handling

``` text
Missing stability data
        → Data escalation

Logger gaps
        → Data-quality flag

Ambiguous identity
        → Human confirmation

Hold failure
        → QA escalation
```

------------------------------------------------------------------------

## Scientific Trust & Safety Guardrails

### Deterministic Engine

-   Thermal calculations
-   Versioned rules
-   Exposure and uncertainty calculations
-   Manufacturer allowance application

### AI Agents

-   Context understanding
-   Evidence retrieval
-   Evidence synthesis
-   Drafting and routing recommendations

### Authorized QA

-   Final disposition
-   Approval / rejection / evidence request
-   Signed decision

### Non-negotiable guardrails

-   Manufacturer excursion allowances are primary
-   Biologics default to manufacturer-data-only handling
-   Uncertainty bounds remain visible
-   Insufficient evidence escalates rather than being guessed
-   The AI layer does not invent or override stability thresholds
-   No autonomous product release

------------------------------------------------------------------------

## Tech Stack

  Layer                          Technology
  ------------------------------ -----------------------------------------
  Frontend                       React
  Backend                        Python + FastAPI
  Database                       PostgreSQL
  Workflow orchestration         n8n
  AI layer                       LLM API / open-source LLM
  Thermal engine                 Python deterministic calculation module
  Demo telemetry                 Simulated IoT telemetry
  WMS                            Mocked WMS
  Development / infrastructure   Docker Compose, Git

------------------------------------------------------------------------

## Prototype Scenarios

The prototype is designed around controlled demonstration scenarios,
including:

-   Temperature spike
-   Gradual temperature drift
-   Freeze event
-   Logger data gap
-   Re-entry of a subsequent excursion with cumulative state

The prototype uses simulated telemetry and demonstration profiles rather
than claiming production pharmaceutical telemetry or proprietary
stability datasets.

------------------------------------------------------------------------

## Product Prototype

The QA interface is designed to surface:

-   Excursion case queue
-   Temperature timeline
-   Exposure assessment
-   Cumulative exposure
-   MKT where applicable
-   Uncertainty
-   Evidence completeness
-   Quarantine status
-   QA disposition controls
-   Sealed audit-trail status

> **Illustrative prototype with simulated telemetry and demonstration
> values.**

------------------------------------------------------------------------

## PS22 Alignment

VerdictRx is designed around the PS22 requirement to go beyond simple
task automation.

  -----------------------------------------------------------------------
  PS22 Challenge                      VerdictRx Response
  ----------------------------------- -----------------------------------
  Repetitive human effort             Automated investigation and
                                      evidence assembly

  Fragmented information              Five sources resolved into one
                                      contextual case dossier

  Frequent decisions                  Deterministic assessment + AI
                                      reasoning, with QA decision
                                      authority

  n8n                                 Central event-driven orchestration

  Beyond simple automation            Multi-step reasoning, exception
                                      routing, stateful replanning and
                                      closed-loop execution
  -----------------------------------------------------------------------

The system demonstrates AI + workflow automation coordinating a real
operational process rather than simply generating text or sending an
alert.

------------------------------------------------------------------------

## Feasibility

The prototype is intentionally designed to be buildable without
proprietary pharmaceutical datasets.

-   React + Python / FastAPI + PostgreSQL + n8n
-   Deterministic Python thermal engine
-   Versioned demonstration profiles
-   Simulated telemetry
-   Mocked WMS
-   Approved-document retrieval
-   Human-in-the-loop QA decision

------------------------------------------------------------------------

## Impact Hypothesis

The project aims to validate whether automated investigation and
orchestration can lead to:

-   Less manual coordination
-   Faster evidence assembly
-   More traceable QA decisions
-   Better visibility into evidence gaps
-   More consistent handling of excursion cases

These are **impact hypotheses to validate**, not claimed production
results.

------------------------------------------------------------------------

## Demo Status

**Current scope: prototype / hackathon demonstration**

The system uses:

-   Simulated telemetry
-   Demonstration profiles
-   Mocked WMS integration
-   Controlled scenarios

It should not be interpreted as a production pharmaceutical quality
system or as an autonomous medicine-release system.

------------------------------------------------------------------------

## Suggested Repository Structure

``` text
VerdictRx/
├── frontend/
├── backend/
├── agents/
├── thermal-engine/
├── workflows/
├── data/
├── docs/
├── docker-compose.yml
└── README.md
```

> The exact repository structure should match the implementation as the
> project is built.

------------------------------------------------------------------------

## Key Differentiator

Most temperature monitoring workflows answer:

> **"Did the temperature breach occur?"**

VerdictRx addresses the next operational question:

> **"What evidence do we have, what does the exposure calculation show,
> what is still uncertain, what actions should be executed, and what
> does the authorized QA reviewer need to decide?"**

That is the core of the **investigation-to-QA automation** approach.

------------------------------------------------------------------------

## Disclaimer

VerdictRx is a hackathon prototype / demonstration system. It uses
simulated telemetry, demonstration values and mocked integrations. It is
not a validated pharmaceutical quality-management system and must not be
used to make real-world product-release decisions without appropriate
validation, approved procedures, qualified personnel and applicable
regulatory controls.

------------------------------------------------------------------------

# VerdictRx

**From Temperature Alerts to Evidence-Backed QA Decisions.**
