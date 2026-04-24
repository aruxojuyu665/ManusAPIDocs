# agent.detail - Manus API

Retrieves an agent’s details including its nickname, description, and associated task. Use agent.update to modify, or task.list with scope=agent_subtask to view this agent’s subtasks.

GET /v2/agent.detail

Questions or issues? Contact us at api-support@manus.ai.

**Talk to this agent:** Use task.sendMessage with the agent’s `task_id` to send messages to its main task.

**View subtasks:** Use task.list with scope=agent_subtask and this agent’s ID to list all subtasks.

#### Authorizations

x-manus-api-key

string

header

required

#### Query Parameters

agent_id

string

required

The unique identifier of the agent to retrieve.

#### Response

200

application/json

Agent retrieved successfully.

ok

boolean

Whether the request was successful.

Example:

`true`

request_id

string

Unique identifier for this API request.

agent

object

The agent object with full details.

Hide child attributes

agent.id

string

Unique identifier for the agent. Use this as agent_id in task.list (with scope=agent_subtask) to view this agent's subtasks.

agent.task_id

string

The task ID associated with this agent's creation or configuration. Use task.detail to view the associated task.

agent.nickname

string

Display name of the agent. Can be updated via agent.update.

agent.about

string

Description or bio of the agent explaining its purpose and specialization. Can be updated via agent.update.