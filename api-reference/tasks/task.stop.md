# task.stop - Manus API

**URL:** https://open.manus.ai/docs/v2/task.stop

---

Skip to main content
Manus API home page
Search...
⌘K
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
POST
task.create
GET
task.detail
GET
task.list
POST
task.update
POST
task.stop
POST
task.delete
POST
task.sendMessage
GET
task.listMessages
POST
task.confirmAction
Projects
Skills
Agents
Files
Webhooks
Usage
Connectors
Browser
Website
v2
Tasks
task.stop
Copy page

Stops a running task. The task status will change to stopped. A stopped task can still be resumed with task.sendMessage.

POST
/
v2
/
task.stop
Try it
Questions or issues? Contact us at api-support@manus.ai.
Resumable: A stopped task can still be resumed by sending a new message via task.sendMessage.
Authorizations
​
x-manus-api-key
stringheaderrequired
Body
application/json
​
task_id
stringrequired

The unique identifier of the running task to stop. Supports the shortcut agent-default-main_task for the IM agent's main task.

Response
200
application/json

Task stopped successfully.

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