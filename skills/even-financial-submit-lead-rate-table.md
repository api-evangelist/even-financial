---
name: Submit a lead and get a rate table
description: Submit a consumer lead (user info + product search criteria) to Engine by MoneyLion and retrieve a rate table of personalized financial product offers.
api: openapi/even-financial-openapi-original.json
operations: [submitLead, getRateTableForSpecifiedLead, getRateTable, getLead, updateLead]
---

# Submit a lead and get a rate table

Engine by MoneyLion (formerly Even Financial) matches a consumer to financial products.
You submit a **lead** (a user plus product search criteria) and receive a **rate table**
(a list of offers).

## Auth
All requests use `Authorization: Bearer {token}`. Use a **publishable** token for lead submission;
a **confidential** token is required for sensitive lead/analytics reads. See
`authentication/even-financial-authentication.yml`.

## Steps
1. **Submit the lead** — `POST /leads/rateTables` (`submitLead`) with the applicant profile and the
   product search criteria. The response returns the created lead and its rate table of offers.
   - Alternatively, if you already created a lead, call `POST /leads/{leadUuid}/rateTables`
     (`getRateTableForSpecifiedLead`) to submit it and get its rate table.
2. **Re-fetch the rate table** — `GET /originator/rateTables/{uuid}` (`getRateTable`) using the
   rate table UUID from step 1.
3. **Read the lead** — `GET /leads/{uuid}` (`getLead`) to retrieve the stored lead (confidential token).
4. **Amend if needed** — `PATCH /leads/{uuid}` (`updateLead`) to correct or enrich lead attributes.

## Rules
- Errors come back as a JSON array of `ApiError` objects (`attribute`, `type`, `details`) — not
  RFC 9457. Handle `400` (invalid request), `409` (duplicate lead), and `422` (unprocessable).
  See `errors/even-financial-problem-types.yml`.
- Follow the provider's disclosure and consent requirements when displaying offers
  (Developer Center → Compliance Guidelines).
- No idempotency key is supported; a resubmitted identical lead may return `409 Duplicate lead`.
