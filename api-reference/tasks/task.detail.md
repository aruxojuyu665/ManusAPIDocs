# task.detail - Manus API

Retrieves a task’s status and metadata. Use [task.listMessages]() for the full event history, or [task.sendMessage]() to continue the conversation.

GET /v2/task.detail

Questions or issues? Contact us at [api-support@manus.ai]().

**Status only:** This endpoint returns status and metadata. Use [task.listMessages]() for the full conversation history and agent outputs.

**Shortcut:** Use `agent-default-main_task` as `task_id` to check the IM agent’s main task.

#### Authorizations

- **x-manus-api-key** (string, header, required)

#### Query Parameters

- **task_id** (string, required)
  The unique identifier of the task to retrieve. Supports the shortcut `agent-default-main_task` for the IM agent's main task.

#### Response

**200 application/json**
Task retrieved successfully.

- **ok** (boolean)
  Whether the request was successful.
  Example: `true`

- **request_id** (string)
  Unique identifier for this API request.

- **task** (object)
  The task object with current status and metadata.
  - **task.id** (string)
    Unique identifier for the task.
  - **task.status** (enum<string>)
    Current task status. "running" — agent is actively working. "stopped" — task has finished or been stopped. "waiting" — agent is paused and waiting for user input or confirmation. "error" — task encountered an unrecoverable error.
    Available options: `running`, `stopped`, `waiting`, `error`
  - **task.created_at** (integer<int64>)
    Unix timestamp (seconds) when the task was created.
  - **task.updated_at** (integer<int64>)
    Unix timestamp (seconds) when the task was last updated.
  - **task.task_type** (enum<string>)
    Type of the task. "standard" — a regular standalone task. "project" — a task within a project. "agent_subtask" — a subtask created by an agent. Use [task.list]() with `scope` to filter by task type.
    Available options: `standard`, `project`, `agent_subtask`
  - **task.share_visibility** (enum<string>)
    Who can view the task. "private" — only the task creator. "team" — all team members. "public" — anyone with the share link.
    Available options: `private`, `team`, `public`
  - **task.title** (string)
    Title of the task.
  - **task.credit_usage** (integer<int32>)
    Total credits consumed by the task. Only present when the task has consumed credits.
  - **task.task_url** (string)
    URL to view the task in the Manus webapp (e.g., [https://manus.im/app/{task_id}]()).
  - **task.created_by_api_key** (object)
    The API key that created this task. Present when the task was created via the API; null or absent when created through the UI or other means. The name reflects the API key's current name, not a snapshot from creation time.
    - **task.created_by_api_key.id** (string)
      The API key ID.
    - **task.created_by_api_key.name** (string)
      The current display name of the API key.

#### Code Examples

**cURL**
```bash
curl --request GET \
  --url 'https://api.manus.ai/v2/task.detail?task_id=<string>' \
  --header 'x-manus-api-key: <api-key>'
```

**Response 200**
```json
{
  "ok": true,
  "request_id": "<string>",
  "task": {
    "id": "<string>",
    "status": "running",
    "created_at": 123,
    "updated_at": 123,
    "task_type": "standard",
    "share_visibility": "private",
    "title": "<string>",
    "credit_usage": 123,
    "task_url": "<string>",
    "created_by_api_key": {
      "id": "<string>",
      "name": "<string>"
    }
  }
}
```