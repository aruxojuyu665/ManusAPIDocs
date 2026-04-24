# browser.onlineList - Manus API

**URL:** https://open.manus.ai/docs/v2/browser.onlineList

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
Usage
Connectors
Browser
GET
browser.onlineList
Website
v2
Browser
browser.onlineList
Copy page

Lists the user’s online browser clients. Use the returned client_id with task.confirmAction when the agent triggers a needConnectMyBrowser waiting event. See the Task Lifecycle guide.

GET
/
v2
/
browser.onlineList
Try it
Questions or issues? Contact us at api-support@manus.ai.
Use in tasks: When the agent triggers a needConnectMyBrowser waiting event, pass the returned client_id via task.confirmAction to select a browser.
Guide: See the Task Lifecycle for the full browser integration flow.
Authorizations
​
x-manus-api-key
stringheaderrequired
Response
200
application/json

Online browser clients retrieved successfully.

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
data
object[]

Array of online browser client objects.

Hide child attributes

​
data.client_id
string

Unique identifier for the browser client.

​
data.client_name
string

Display name of the browser client.

​
data.ua
string

User-Agent string of the browser.