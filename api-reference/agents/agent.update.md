# agent.update - Manus API

Updates an agent’s nickname and description. Use agent.detail to view current values before updating.

## Authorizations

| Parameter | Type | Location | Required |
|---|---|---|---|
| `x-manus-api-key` | string | header | required |

## Body

`application/json`

| Parameter | Type | Description | Required |
|---|---|---|---|
| `agent_id` | string | The unique identifier of the agent to update. | required |
| `nickname` | string | New display name for the agent. | optional |
| `about` | string | New description or bio for the agent. | optional |

## Response

### 200 OK

`application/json`

Agent updated successfully.

| Field | Type | Description |
|---|---|---|
| `ok` | boolean | Whether the request was successful. Example: `true` |
| `request_id` | string | Unique identifier for this API request. |
| `agent` | object | The updated agent object. |
| `agent.id` | string | Unique identifier for the agent. Use this as `agent_id` in [task.list](https://open.manus.ai/docs/v2/task.list) (with `scope=agent_subtask`) to view this agent's subtasks. |
| `agent.task_id` | string | The task ID associated with this agent's creation or configuration. Use [task.detail](https://open.manus.ai/docs/v2/task.detail) to view the associated task. |
| `agent.nickname` | string | Display name of the agent. Can be updated via [agent.update](https://open.manus.ai/docs/v2/agent.update). |
| `agent.about` | string | Description or bio of the agent explaining its purpose and specialization. Can be updated via [agent.update](https://open.manus.ai/docs/v2/agent.update). |

## Code Examples

### cURL

```bash
curl --request POST \
  --url https://api.manus.ai/v2/agent.update \
  --header 'Content-Type: application/json' \
  --header 'x-manus-api-key: <api-key>' \
  --data '
{
  "agent_id": "<string>",
  "nickname": "<string>",
  "about": "<string>"
}
'
```

### 200 Response Example

```json
{
  "ok": true,
  "request_id": "<string>",
  "agent": {
    "id": "<string>",
    "task_id": "<string>",
    "nickname": "<string>",
    "about": "<string>"
  }
}
```