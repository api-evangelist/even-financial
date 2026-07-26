---
name: Preview product offers
description: Fetch preview offers for loans, credit cards, and savings from Engine by MoneyLion without submitting a full lead.
api: openapi/even-financial-openapi-original.json
operations: [getPreviewLoanOffers, getPreviewCreditCardOffers, getPreviewSavingsOffers, getFeaturedFinancialInstitutions]
---

# Preview product offers

Use the Offer Preview endpoints to show indicative offers before a consumer completes a full lead.

## Auth
`Authorization: Bearer {token}` (publishable token is sufficient for previews).

## Steps
1. **Loan previews** — `GET /offerPreview/loanOffers` (`getPreviewLoanOffers`).
2. **Credit card previews** — `GET /offerPreview/creditCardOffers` (`getPreviewCreditCardOffers`).
3. **Savings previews** — `GET /offerPreview/savingsOffers` (`getPreviewSavingsOffers`).
4. **Featured institutions** — `GET /uiUtil/featuredFinancialInstitutions`
   (`getFeaturedFinancialInstitutions`) to surface featured providers in the UI.

## Rules
- Preview offers are indicative, not personalized underwriting decisions — submit a lead
  (`submitLead`) to get a binding rate table.
- Honor offer display and disclosure rules from the Developer Center compliance guidelines.
