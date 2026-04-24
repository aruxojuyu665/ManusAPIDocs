# task.listMessages - Manus API

**URL:** https://open.manus.ai/docs/v2/task.listMessages

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
task.listMessages
Copy page

Lists event messages for a task with cursor-based pagination. Use this to poll for progress after task.create or task.sendMessage. See the Task Lifecycle guide for how to handle each status.

GET
/
v2
/
task.listMessages
Try it
Questions or issues? Contact us at api-support@manus.ai.
Shortcut: Use agent-default-main_task as task_id to read the IM agent’s conversation history.
Status handling: Check status_update events — running → keep polling, stopped → read results, waiting → respond with task.sendMessage or task.confirmAction, error → read error details.
See the Task Lifecycle guide for the complete flow.
Authorizations
​
x-manus-api-key
stringheaderrequired
Query Parameters
​
task_id
stringrequired

The unique identifier of the task to list messages for. Supports the shortcut agent-default-main_task for the IM agent's main task.

​
limit
integer

Number of messages to return per page. Default: 50, Range: 1-200.

​
cursor
string

Pagination cursor from the previous response's next_cursor field. Omit for the first page.

​
order
enum<string>

Sort direction by timestamp. "desc" (default) returns newest first, "asc" returns oldest first (chronological order).

Available options: asc, desc 
​
verbose
boolean

When true, includes detailed events: tool_used (tools the agent invoked), plan_update (full plan snapshots), new_plan_step (individual step additions), and explanation (agent reasoning). Default: false — only returns user_message, assistant_message, error_message, status_update, and user_stop.

​
slides_format
enum<string>

Format for slides attachments in the response. "html" (default) returns raw HTML slides. "pptx" auto-converts HTML slides to PowerPoint format.

Available options: html, pptx 
Response
200
application/json

Messages retrieved successfully.

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
task_id
string

The task ID these messages belong to.

​
messages
object[]

Array of task event objects representing the conversation and agent activity.

Hide child attributes

​
messages.id
string

Unique identifier for this event.

​
messages.type
enum<string>

Event type. Determines which payload field is present. tool_used, plan_update, new_plan_step, and explanation are only included when verbose=true.

Available options: user_message, assistant_message, error_message, status_update, tool_used, plan_update, new_plan_step, explanation, user_stop 
​
messages.timestamp
integer<int64>

Unix timestamp (seconds) when this event occurred.

​
messages.user_message
object

Present when type="user_message". Contains a message sent by the user.

Hide child attributes

​
messages.user_message.content
string

The text content of the user's message.

​
messages.user_message.message_type
enum<string>

How the message was sent. "text" for typed input, "voice" for voice input.

Available options: text, voice 
​
messages.user_message.attachments
object[]

Files or images the user attached to their message.

Hide child attributes

​
messages.user_message.attachments.type
enum<string>

Type of attachment. "image" for images, "file" for documents, "voice" for audio recordings, "slides" for presentation slides.

Available options: image, file, voice, slides 
​
messages.user_message.attachments.filename
string

Display name of the attachment file.

​
messages.user_message.attachments.url
string

URL to download the attachment content.

​
messages.user_message.attachments.content_type
string

MIME type of the attachment (e.g., "application/pdf", "image/png").

​
messages.assistant_message
object

Present when type="assistant_message". Contains a response from the agent.

Hide child attributes

​
messages.assistant_message.content
string

The text content of the agent's response.

​
messages.assistant_message.attachments
object[]

Files, images, or slides the agent generated as output.

Hide child attributes

​
messages.assistant_message.attachments.type
enum<string>

Type of attachment. "image" for images, "file" for documents, "voice" for audio recordings, "slides" for presentation slides.

Available options: image, file, voice, slides 
​
messages.assistant_message.attachments.filename
string

Display name of the attachment file.

​
messages.assistant_message.attachments.url
string

URL to download the attachment content.

​
messages.assistant_message.attachments.content_type
string

MIME type of the attachment (e.g., "application/pdf", "image/png").

​
messages.error_message
object

Present when type="error_message". Indicates the task encountered an error.

Hide child attributes

​
messages.error_message.error_type
string

Category of the error.

​
messages.error_message.content
string

Human-readable error description.

​
messages.status_update
object

Present when type="status_update". Indicates a change in the agent's processing state.

Hide child attributes

​
messages.status_update.agent_status
enum<string>

The agent's current state. "waiting" means the agent needs user confirmation — check status_detail for the event to confirm.

Available options: running, stopped, waiting, error 
​
messages.status_update.status_detail
object

Additional details when agent_status is "waiting". Contains the event ID needed for task.confirmAction.

Hide child attributes

​
messages.status_update.status_detail.waiting_for_event_id
string

The event ID to pass as event_id when calling task.confirmAction.

​
messages.status_update.status_detail.waiting_for_event_type
string

Type of action awaiting confirmation (e.g., "email_send", "calendar_create").

​
messages.status_update.status_detail.waiting_description
string

Human-readable description of what the agent is waiting for.

​
messages.status_update.status_detail.confirm_input_schema
object

JSON Schema defining the expected input format for the confirmation, if additional input is needed.

​
messages.status_update.brief
string

Short summary of the current agent activity.

​
messages.status_update.description
string

Detailed description of what the agent is doing.

​
messages.tool_used
object

Present when type="tool_used" (verbose=true only). Records a tool invocation by the agent.

Hide child attributes

​
messages.tool_used.tool
string

Name of the tool that was used (e.g., "browser", "code_executor").

​
messages.tool_used.action_id
string

Unique identifier for this tool action.

​
messages.tool_used.status
enum<string>

Result of the tool invocation.

Available options: success, error, rollback 
​
messages.tool_used.brief
string

Short summary of the tool action.

​
messages.tool_used.description
string

Detailed description of what the tool did.

​
messages.tool_used.message
object

Structured details of the tool invocation.

Hide child attributes

​
messages.tool_used.message.action
string

The specific action performed by the tool.

​
messages.tool_used.message.param
string

Parameters passed to the tool action.

​
messages.plan_update
object

Present when type="plan_update" (verbose=true only). A full snapshot of the agent's current execution plan.

Hide child attributes

​
messages.plan_update.steps
object[]

All steps in the current plan with their statuses.

Hide child attributes

​
messages.plan_update.steps.status
enum<string>

Current status of this plan step.

Available options: todo, doing, done, failed 
​
messages.plan_update.steps.title
string

Description of this plan step.

​
messages.plan_update.steps.started_at
integer<int64> | null

Unix timestamp when this step started. Null if not yet started.

​
messages.plan_update.steps.end_at
integer<int64> | null

Unix timestamp when this step finished. Null if not yet completed.

​
messages.new_plan_step
object

Present when type="new_plan_step" (verbose=true only). A new step was added to the plan.

Hide child attributes

​
messages.new_plan_step.step_id
string

Unique identifier for the new plan step.

​
messages.new_plan_step.title
string

Description of the new plan step.

​
messages.explanation
object

Present when type="explanation" (verbose=true only). The agent's internal reasoning or thought process.

Hide child attributes

​
messages.explanation.content
string

The agent's explanation of its reasoning or approach.

​
has_more
boolean

Whether there are more messages beyond this page.

​
next_cursor
string

Cursor for fetching the next page. Only present when has_more is true.