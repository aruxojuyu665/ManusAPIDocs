# agent.list - Manus API



**Talk to an agent:** Use [task.sendMessage]() with the agent’s `task_id` to send messages to an agent’s main task. See the [Agents]() guide.

#### Authorizations

x-manus-api-key

string

header

required

#### Response

200

application/json

Agents retrieved successfully.

ok

boolean

Whether the request was successful.

Example:

`true`

request\_id

string

Unique identifier for this API request.

data

object\[\]

Array of agent objects.

Hide child attributes

data.id

string

Unique identifier for the agent. Use this as `agent_id` in [task.list]() (with `scope=agent_subtask`) to view this agent\'s subtasks.

data.task\_id

string

The task ID associated with this agent\'s creation or configuration. Use [task.detail]() to view the associated task.

data.nickname

string

Display name of the agent. Can be updated via [agent.update]().

data.about

string

Description or bio of the agent explaining its purpose and specialization. Can be updated via [agent.update]().