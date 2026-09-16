## Admin-Azure-T181-P079
## Problem Statement 

# Project: Azure Lighthouse Delegated Administration Design Study Course Code: 24CC3046 · Project Number: P079 Team: T181 (4 students)

# Background

Managed service providers (MSPs) and IT departments overseeing multiple Azure AD tenants face a structural challenge: Azure's native tools are built around single-tenant administration. To manage a customer's resources today without Azure Lighthouse, an MSP has only two poor options — create guest (B2B) accounts in every customer tenant, or ask customers to share credentials. Both approaches carry real risk:

Guest accounts multiply attack surface across every customer tenant, are easy to forget to revoke, and give the MSP no unified view of what access it actually holds.
Credential sharing breaks least-privilege entirely and eliminates any meaningful audit trail of who did what.

Azure Lighthouse solves this by letting a provider tenant project delegated, role-scoped access into customer tenants — without guest accounts or shared secrets. But delegation introduces its own failure modes, which are exactly what this design study asks Team T181 to confront.

# Bottlenecks
Cross-tenant permission scoping mistakes are high impact. Because a single misconfigured registrationAssignment can grant a provider-side security group Owner or Contributor rights across an entire customer subscription instead of a single resource group, a scoping error doesn't just affect one tenant's blast radius — it can expose customer data or resources the MSP was never meant to touch. There is no "undo" once a bad delegation has been exercised.
Auditing across tenants is fragmented. Azure Activity Logs, sign-in logs, and policy compliance data are generated and stored per-tenant by default. Without deliberate design, an MSP managing ten customer tenants ends up with ten disconnected logging silos, making it difficult to answer basic security questions like "which provider engineer touched which customer resource, and when?"

# The Design Problem

How do you architect an Azure Lighthouse delegation model that gives a service provider exactly the access it needs to operate customer environments efficiently — no more, no less — while still producing a single, coherent audit trail across every delegated tenant?

Teams are expected to propose a concrete delegation and role-mapping scheme, and a monitoring architecture, that directly resolves both bottlenecks above rather than just acknowledging them.
