# webhook.create - Manus API

**URL:** https://open.manus.ai/docs/v2/webhook.create

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
webhook.create
Copy page

Creates a webhook for receiving task event notifications. Use webhook.publicKey to get the key for verifying signatures. See the Webhooks guide for event types.

POST
/
v2
/
webhook.create
Try it
Questions or issues? Contact us at api-support@manus.ai.
Verify signatures: Use webhook.publicKey to get the public key for validating incoming requests.
Guides: See Webhooks for event types and Webhook Security for verification examples.
Authorizations
​
x-manus-api-key
stringheaderrequired
Body
application/json
​
url
stringrequired

The HTTPS endpoint URL that will receive POST webhook notifications. Must be publicly accessible and return a 2xx status code.

Response
200
application/json

Webhook created successfully.

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

​
webhook
object

The created webhook object.

Hide child attributes

​
webhook.id
string

Unique identifier for the webhook.

​
webhook.url
string

The endpoint URL receiving webhook POST notifications.

​
webhook.status
enum<string>

Webhook status. "active" — receiving notifications. "inactive" — paused.

Available options: active, inactive 
​
webhook.created_at
integer<int64>

Unix timestamp (seconds) when the webhook was created.