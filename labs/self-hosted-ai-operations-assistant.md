# Self-Hosted AI Operations Assistant

**Concept architecture by Jan Kevin Mortola**

A controlled internal assistant for searching business knowledge, summarizing operational context, and executing approved tool actions while keeping sensitive workflows inside infrastructure the business controls.

## Architecture

`User → Auth / Role → Query Router → Retrieval → Local LLM → Policy / Confidence Check → Answer or Tool Proposal → Human Approval → Tool Execution → Audit Log`

## Core components

### Local model layer

Ollama or LM Studio can expose a local OpenAI-compatible endpoint for models that fit the available hardware. The model should not be treated as the source of truth; it interprets retrieved information and proposes actions.

### Retrieval layer

Index approved SOPs, internal guides, operational records, and selected knowledge sources. Retrieval should return source references so the assistant can ground its answer.

### Permission-aware context

Before retrieval, map the requesting user to an allowed data scope. A general operations user should not automatically retrieve HR, finance, client-confidential, or credential information.

### Orchestration

n8n can handle:
- retrieval requests
- business-tool lookups
- prompt/context assembly
- confidence and policy gates
- human approval workflows
- ClickUp / CRM / Google Workspace actions
- logging and exception handling

### Tool use

The model should propose a structured action such as:

```json
{
  "action": "create_followup_task",
  "record_id": "example-123",
  "reason": "missing required document",
  "confidence": 0.91
}
```

Automation validates the action against an allowlist and required fields before execution.

## Human-in-the-loop rules

Require approval for actions involving:
- money or billing
- deletion
- sending external communications
- changing ownership or permissions
- high-impact CRM changes
- confidential records
- low-confidence or ambiguous matches

## Evaluation

Test the assistant against:
- unsupported questions
- conflicting documents
- stale information
- prompt injection inside retrieved content
- unauthorized data requests
- ambiguous entity names
- missing sources
- tool failures
- hallucinated IDs or actions

## Reliability goal

The assistant should be useful even when it refuses to automate. A safe escalation with the correct context is better than an incorrect autonomous action.

## Example stack

- Ollama / LM Studio
- local or private LLM
- n8n
- vector / retrieval store
- ClickUp / GHL / Google Workspace connectors
- approval channel
- audit log

[Back to Automation Labs](README.md) · [Agentic AI Portfolio](https://jankevinmortola.github.io/Portfolio/agentic-ai-automation.html)
