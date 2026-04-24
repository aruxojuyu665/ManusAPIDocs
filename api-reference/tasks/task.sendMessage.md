# task.sendMessage - Manus API

Sends a follow-up message to a task for multi-turn conversation. Use this after task.create to continue talking, or to reply when waiting_for_event_type is messageAskUser. For other waiting types, use task.confirmAction instead.

POST /v2/task.sendMessage

Questions or issues? Contact us at api-support@manus.ai.

**Shortcut:** Use `agent-default-main_task` as `task_id` to send messages to the IM agent directly.
**Attach files:** Upload via [file.upload]() and pass the `file_id` in the message content, or use `file_url` / `file_data` directly.
**Connectors:** Pass connector IDs in `message.connectors`. Get IDs from [connector.list]() or the [Connectors]() guide. If omitted and `project_id` is set, the project’s default connectors will be used.
**Enable skills:** Pass skill IDs from [skill.list]() in `message.enable_skills` to control which skills are available for the agent. If omitted, the user’s default enabled skills are loaded automatically.
**Force skills:** Pass skill IDs in `message.force_skills` to ensure the agent invokes them. Forced skills are automatically available even if not listed in enable_skills.
**Waiting events:** Use this endpoint to reply when the agent asks a question (messageAskUser). For other waiting types like `gmailSendAction` or `deployAction`, use [task.confirmAction]() instead.

#### Authorizations

x-manus-api-key

string

header

required

#### Body

application/json

task_id

string

required

The unique identifier of the task to send the message to. Supports the shortcut agent-default-main_task for the IM agent's main task.

message

object

required

The follow-up message. Supports the same content formats as task.create (plain text or multi-part with files).

Hide child attributes

message.content

(Text · object | File · object | Voice · object)[]

string

(Text · object | File · object | Voice · object)[]

required

String (plain text) or array of ContentPart objects.

*   Text
    
*   File
    
*   Voice
    

Hide child attributes

message.content.type

enum<string>

required

Must be "text".

Available options: text 

message.content.text

string

required

The text content of the message.

message.connectors

string[]

List of connector IDs to enable for this task. Resolution order when omitted: 1) if the task belongs to a project, the project’s default connectors are used; 2) otherwise, the user’s default enabled connectors are used. Use connector.list to get the connectors installed in your account.

message.enable_skills

string[]

Skill IDs to enable for this task. If empty or omitted, loads the skills the user has enabled in their account settings. Use skill.list to retrieve available skill IDs.

message.force_skills

string[]

Skill IDs the agent must invoke during this task. Forced skills are automatically available even if not listed in enable_skills.

#### Response

200

application/json

Message sent successfully. The task will resume processing.

ok

boolean

Whether the request was successful.

Example:

`true`

request_id

string

Unique identifier for this API request.

task_id

string

The ID of the task the message was sent to.