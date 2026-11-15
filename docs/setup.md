# Extended setup

## 1. Prepare n8n

Use an n8n release compatible with the exported node versions. The workflow JSON does not declare a minimum n8n version. Install the community package `@mohanvadivel/n8n-nodes-zoho-desk` if it is not already available. The workflow also uses n8n LangChain nodes.

## 2. Import the workflow

In n8n, use the workflow import control and select `workflow/zoho-ticket-triage.json`.

> Screenshot placeholder: workflow import screen.

## 3. Add credentials

Create a Zoho Desk OAuth2 credential and an OpenAI credential. Choose the correct Zoho data center during OAuth setup. See [credentials.md](credentials.md) for scope and organization ID notes.

> Screenshot placeholder: Zoho Desk OAuth2 credential configuration.

Select the Zoho credential on Zoho Desk Trigger, HTTP Request, HTTP Request1, HTTP Request2, and HTTP Request3. Select the OpenAI credential on OpenAI Chat Model and OpenAI Chat Model1.

> Screenshot placeholder: credential assignment on workflow nodes.

## 4. Set organization and region

Replace `YOUR_ORG_ID` in the `orgId` header in HTTP Request, HTTP Request1, HTTP Request2, and HTTP Request3. The sanitized release includes the header on each HTTP Request node.

Set the host in all four HTTP Request URL expressions to match the account region. The source host is `desk.zoho.com`. Confirm the correct API host for the organization's data center before running.

> Screenshot placeholder: HTTP Request headers and URL settings.

## 5. Configure AI nodes

Both model nodes use the model value `gpt-5-mini`. Assign/configure a valid OpenAI credential and confirm that model is available to your account. Connect OpenAI Chat Model to Sentiment Analysis and OpenAI Chat Model1 to Basic LLM Chain, as shown in the imported workflow.

> Screenshot placeholder: AI model credential and connection settings.

## 6. Test and activate

Create or select a non-production test ticket. Run a test and inspect the masked data before enabling the workflow. Confirm the resulting ticket tags, internal comment, and priority in Zoho Desk. The workflow's final HTTP Request3 call updates priority.

> Screenshot placeholder: successful execution and updated sample ticket.

Activate the workflow only after reviewing the effects and access granted to the credentials.
