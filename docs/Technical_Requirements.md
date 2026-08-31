# Support Copilot — Technical Requirements

Phase 1 Pilot · Contact Centre Transformation

| Document version | 1.4 |
|---|---|
| Status | Draft for review |
| Last updated | 2026-08-07 |
| Author | R. Okonkwo (Business Analyst) |
| Reviewers | A. Lindqvist (Eng Lead), M. Duarte (Product) |
| Distribution | Programme team, Steering |

# 1. Purpose

This document specifies the functional and non-functional requirements for Phase 1 of Support Copilot, a generative-AI assistant that drafts suggested replies for human contact centre agents. It is the reference specification for the pilot only. It does not describe the general-availability product.

# 2. Scope

In scope for Phase 1:

- Suggested-reply drafting surfaced inside the existing agent console.

- Retrieval grounded in the published help-centre article corpus.

- Redaction of personal data from all transcript material prior to external processing.

- Language coverage: English, German and French.

- Pilot cohort of six agents drawn from the EMEA Tier-1 queue.

Out of scope for Phase 1:

- Any customer-facing reply that has not been reviewed by a human agent.

- Voice and telephony channels.

- Autonomous ticket resolution, routing or closure.

- Model fine-tuning. Phase 1 is prompt engineering plus retrieval only.

# 3. Functional requirements

| Ref | Requirement | Priority |
|---|---|---|
| FR-01 | The system shall generate a draft reply for an open ticket on agent request. | Must |
| FR-02 | Every draft shall cite the help-centre article identifiers used to produce it. | Must |
| FR-03 | The agent shall be able to accept, edit or discard a draft. | Must |
| FR-04 | The system shall record the agent's disposition of each draft. | Must |
| FR-05 | The system shall capture an optional free-text reason on discard. | Should |
| FR-06 | Personal data shall be redacted from transcripts before external processing. | Must |
| FR-07 | The system shall exclude superseded and archived articles from retrieval. | Must |
| FR-08 | The system shall record the prompt version used for each response. | Must |
| FR-09 | The system shall log token consumption and cost per request. | Must |
| FR-10 | The system shall fall back to blank compose if the model is unavailable. | Must |
| FR-11 | The system shall support draft regeneration with an agent-supplied hint. | Could |
| FR-12 | The system shall expose an administrative kill switch disabling all drafting. | Must |

# 4. Non-functional requirements

- NFR-01 — Draft returned within 3 seconds at p95.

- NFR-02 — Retrieval query latency within 400ms at p95.

- NFR-03 — Service availability 99.5% during EMEA business hours.

- NFR-04 — Index rebuild completes within 2 hours.

- NFR-05 — A model provider outage must never prevent an agent replying manually.

- NFR-06 — All inference for EU customer data must occur within the EU region.

# 5. Data and privacy

Transcript data is customer personal data. It may not be transmitted to any third-party model provider until redaction has been applied and a Data Protection Impact Assessment has been approved by the Data Protection Officer. Redaction must execute within our own infrastructure. Original and redacted pairs are retained for 90 days for audit and are then purged.

Redaction is required to reach at least 99% recall against a hand-labelled sample. Over-redaction is preferred to under-redaction.

# 6. Milestones

| Requirements baselined | 2026-08-14 |
|---|---|
| Architecture agreed | 2026-08-21 |
| DPIA approved | 2026-09-18 |
| Feature complete | 2026-10-16 |
| Evaluation baseline established | 2026-10-23 |
| Pilot start | 2026-11-01 |
| Pilot review | 2026-12-05 |

Note: the pilot start date above is taken from the programme plan issued on 2026-08-05. It has not been reconciled against the commercial readiness date discussed in discovery.

# 7. Assumptions and open items

- Model provider has not been selected. Requirements are written to be provider-neutral.

- Help-centre corpus is assumed to be current. See architecture notes for a challenge to this assumption.

- Agent console vendor is assumed to permit an embedded panel of the required width. Unconfirmed.

- Pilot cohort size of six is assumed sufficient to detect a 20% handling-time change. Not power-tested.

- Budget envelope is assumed to cover inference at pilot volumes. See cost model.
