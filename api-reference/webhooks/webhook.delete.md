# webhook.delete - Manus API

**URL:** https://open.manus.ai/docs/v2/webhook.delete

---

Skip to main content
Manus API home page
Search...
Ctrl K
Getting Started
Introduction
Authentication
Task Lifecycle
Connectors
Webhooks Guide
Agents
Integrations
Data Integrations
Website
Rate Limits
API Reference
Tasks
Projects
Skills
Agents
Files
Webhooks
POST
webhook.create
GET
webhook.list
POST
webhook.delete
GET
webhook.publicKey
Usage
Connectors
Browser
Website
v2
Webhooks
webhook.delete
Copy page

Deletes a webhook. The endpoint will stop receiving notifications immediately. Use webhook.list to find the webhook ID.

POST
/
v2
/
webhook.delete
Try it
Questions or issues? Contact us at api-support@manus.ai.
Authorizations
​
x-manus-api-key
stringheaderrequired
Body
application/json
​
webhook_id
stringrequired

The unique identifier of the webhook to delete.

Response
200
application/json

Webhook deleted successfully.

​
ok
boolean

Whether the request was successful.

Example:

true

​
request_id
string

Unique identifier for this API request.