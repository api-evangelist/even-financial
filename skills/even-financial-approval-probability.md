---
name: Get a loan approval probability report
description: Request and retrieve a loan approval probability report from Engine by MoneyLion to gauge a consumer's likelihood of approval before submitting a lead.
api: openapi/even-financial-openapi-original.json
operations: [createLoansApprovalProbabilityReport, getLoansApprovalProbabilityReport]
---

# Get a loan approval probability report

Estimate how likely a consumer is to be approved across loan partners.

## Auth
`Authorization: Bearer {token}` — a confidential token is required.

## Steps
1. **Create the report** — `POST /approvalProbability/loanReports`
   (`createLoansApprovalProbabilityReport`) with the applicant profile. The response returns the
   report UUID.
2. **Retrieve the report** — `GET /approvalProbability/loanReports/{uuid}`
   (`getLoansApprovalProbabilityReport`) to read the computed approval probabilities.

## Rules
- Errors are a JSON array of `ApiError` objects; handle `400`, `401`, `404`, `422`.
- Use the probabilities to prioritize which offers to surface — they are not a guarantee of approval.
