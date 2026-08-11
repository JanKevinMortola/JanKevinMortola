# Make & Zapier Integration Patterns

**Concept / reusable integration notes by Jan Kevin Mortola**

Make and Zapier are strongest when used deliberately for the workflows they fit best, rather than forcing every integration into one platform.

## Zapier patterns

Use Zapier when the workflow is relatively linear, speed of implementation matters, and the required SaaS apps have reliable native actions.

Good fits:
- form → CRM
- CRM → email / Slack notification
- calendar event → task creation
- lead source → GHL / HubSpot update
- lightweight approvals and reminders

Controls I still add:
- deduplication key
- required-field filters
- paths for alternate outcomes
- failure notifications
- clear ownership of retry/manual recovery

## Make patterns

Use Make when visual branching, iterators, aggregators, data shaping, and multi-step SaaS scenarios matter.

Good fits:
- multi-source lead normalization
- array/item processing
- order or booking enrichment
- document-generation sequences
- CRM + Sheets + email + storage workflows
- scenarios requiring visible branches and transformations

Controls I design for:
- partial-bundle failures
- pagination
- rate limits
- empty/missing fields
- duplicate bundles
- scenario re-runs
- downstream failures after earlier writes

## When I move to n8n

I prefer n8n when the workflow needs deeper API work, custom JavaScript/logic, AI orchestration, self-hosting, reusable sub-workflows, complex reconciliation, or tighter control over error paths.

## Cross-platform architecture

`SaaS Trigger → Zapier/Make → Normalized Payload → n8n/API Layer → CRM/Operations System → Verification → Exception Queue`

The platforms can coexist. A business may use Zapier for simple department-owned automations, Make for visual operations scenarios, and n8n as the technical orchestration layer for APIs and AI.

## Migration checklist

When replacing or consolidating an existing automation:
1. inventory triggers and downstream side effects
2. identify hidden dependencies and manual workarounds
3. preserve stable IDs and mappings
4. rebuild validation and exception paths
5. test duplicates and replays
6. shadow-run when possible
7. switch production traffic
8. monitor discrepancies before retiring the old workflow

[Back to Automation Labs](README.md) · [CRM & Automation Portfolio](https://jankevinmortola.github.io/Portfolio/crm-automation-consultant.html)
