# webhook.publicKey - Manus API

**URL:** https://open.manus.ai/docs/v2/webhook.publicKey

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
webhook.publicKey
Copy page

Gets the public key for verifying webhook signatures. See the Webhook Security guide for verification examples.

GET
/
v2
/
webhook.publicKey
Try it
Questions or issues? Contact us at api-support@manus.ai.
Cache the public key on your server. It rarely changes, and fetching it on every webhook request adds unnecessary latency. See the Webhook Security guide for verification examples.
Authorizations
​
x-manus-api-key
stringheaderrequired
Response
200
application/json

Public key retrieved successfully.

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
public_key
string

PEM-encoded RSA public key for verifying webhook signatures.

​
algorithm
string

Signature algorithm. Always "RSA-SHA256".

Example:

"RSA-SHA256"