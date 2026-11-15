# Credentials and Zoho Desk organization ID

## Zoho Desk OAuth2

The workflow uses one Zoho Desk OAuth2 credential on the Zoho Desk Trigger and four HTTP Request nodes. Those HTTP calls read a ticket's latest thread and write tags, an internal comment, and priority. Each HTTP Request node includes an `orgId` header placeholder in this sanitized release.

Zoho Desk documents `Desk.tickets.READ` for read access and `Desk.tickets.UPDATE` for updates to tickets and related data. These are the ticket API scopes indicated by the endpoints used here. The trigger also subscribes to `Ticket_Add`; its exact event/subscription scopes depend on the installed `@mohanvadivel/n8n-nodes-zoho-desk` implementation. The JSON does not encode that scope requirement. Check the node's documentation and OAuth consent errors; do not assume the ticket scopes alone cover event subscription management. Request the narrowest scopes that let the trigger and these API calls work.

Zoho data centers use region-specific OAuth and API hosts. Select the data center that matches the Desk account and use its corresponding API domain in all HTTP Request URLs.

## Find the organization ID

Use the organization ID for the same Zoho Desk account authenticated by the OAuth credential. The workflow sends it in an `orgId` HTTP header on all four HTTP Request nodes. Replace each `YOUR_ORG_ID` placeholder with the account's organization ID.

> Screenshot placeholder: Zoho Desk organization details showing the organization ID.

If the interface location differs, consult the current Zoho Desk account/organization details. Keep the organization ID private to your deployment and verify it matches the OAuth account.

## OpenAI

Create an OpenAI credential in n8n and assign it to both OpenAI Chat Model and OpenAI Chat Model1. The source workflow's credential entries are placeholders and do not contain an API key. The selected model value is `gpt-5-mini`.
