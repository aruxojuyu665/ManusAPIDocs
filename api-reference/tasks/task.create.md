# task.create

Creates a new task. The task runs asynchronously. Poll for progress with `task.listMessages`, send follow-ups with `task.sendMessage`. See the [Task Lifecycle guide](../../getting-started/task-lifecycle.md) for the complete flow.

**Endpoint:** `POST /v2/task.create`

> **Talk to an agent:** To send a message to an existing agent instead of creating a new task, use `task.sendMessage` with `agent-default-main_task` as `task_id`. See the [Agents guide](../../getting-started/agents.md).
>
> **Attach files:** Upload via `file.upload` and pass the `file_id` in the message content, or use `file_url` / `file_data` directly.
>
> **Connectors:** Pass connector IDs in `message.connectors`. Get IDs from `connector.list` or the [Connectors guide](../../connectors/overview.md). If omitted and `project_id` is set, the project's default connectors will be used.
>
> **Enable skills:** Pass skill IDs from `skill.list` in `message.enable_skills` to control which skills are available for the agent. If omitted, the user's default enabled skills are loaded automatically.
>
> **Force skills:** Pass skill IDs in `message.force_skills` to ensure the agent invokes them. Forced skills are automatically available even if not listed in `enable_skills`.

## Authorization

| Header | Type | Required | Description |
|---|---|---|---|
| `x-manus-api-key` | string | Yes | Your Manus API key |

## Request Body

**Content-Type:** `application/json`

### `message` (object, required)

The message to start the task with. Contains the prompt text, optional file attachments, and connector/skill configuration.

| Field | Type | Required | Description |
|---|---|---|---|
| `message.content` | string or array | Yes | String (plain text) or array of ContentPart objects |
| `message.connectors` | string[] | No | List of connector IDs to enable for this task |
| `message.enable_skills` | string[] | No | Skill IDs to enable for this task |
| `message.force_skills` | string[] | No | Skill IDs the agent must invoke during this task |

**ContentPart types:**

*Text:*
| Field | Type | Required | Description |
|---|---|---|---|
| `type` | enum | Yes | Must be `"text"` |
| `text` | string | Yes | The text content of the message |

*File:*
| Field | Type | Required | Description |
|---|---|---|---|
| `type` | enum | Yes | Must be `"file"` |
| `file_id` | string | No | ID from `file.upload` |
| `file_url` | string | No | Publicly accessible URL |
| `file_data` | string | No | Base64-encoded file content |

*Voice:*
| Field | Type | Required | Description |
|---|---|---|---|
| `type` | enum | Yes | Must be `"voice"` |
| `file_id` | string | No | ID from `file.upload` |
| `file_url` | string | No | Publicly accessible URL |

### Top-level Parameters

| Parameter | Type | Default | Description |
|---|---|---|---|
| `project_id` | string | — | Project ID to associate this task with. The project's instruction will be automatically applied. |
| `locale` | string | account setting | Locale for the task output language (e.g., `"en"`, `"zh-CN"`, `"ja"`). |
| `interactive_mode` | boolean | `false` | When enabled, the agent may pause and ask follow-up questions if the input is insufficient. |
| `hide_in_task_list` | boolean | `false` | When `true`, the task will not appear in the Manus webapp task list. Useful for automated/background tasks. |
| `share_visibility` | enum | `"private"` | Controls who can view the task: `"private"`, `"team"`, or `"public"`. |
| `agent_profile` | enum | `"manus-1.6"` | Agent profile: `"manus-1.6"` (standard), `"manus-1.6-lite"` (faster), `"manus-1.6-max"` (maximum capability). |
| `title` | string | auto-generated | Custom title for the task. |

## Response

**HTTP 200** — Task created successfully.

| Field | Type | Description |
|---|---|---|
| `ok` | boolean | Whether the request was successful. Example: `true` |
| `request_id` | string | Unique identifier for this API request, useful for debugging. |
| `task_id` | string | Unique identifier for the created task. |
| `task_title` | string | Title for the task (custom or auto-generated). |
| `task_url` | string | URL to view the task in the Manus webapp (e.g., `https://manus.im/app/{task_id}`). |
| `share_url` | string | Publicly accessible URL for sharing. Only present when `share_visibility` is not `"private"`. |
| `share_visibility` | enum | The actual visibility state: `"private"`, `"team"`, or `"public"`. |

## Example

```bash
curl -X POST https://api.manus.ai/v2/task.create \
  -H "Content-Type: application/json" \
  -H "x-manus-api-key: $MANUS_API_KEY" \
  -d '{
    "message": {
      "content": "Research the top 5 AI companies and write a brief report"
    },
    "agent_profile": "manus-1.6",
    "share_visibility": "private"
  }'
```

**Response:**
```json
{
  "ok": true,
  "request_id": "req_abc123",
  "task_id": "task_xyz789",
  "task_title": "Research the top 5 AI companies",
  "task_url": "https://manus.im/app/task_xyz789",
  "share_visibility": "private"
}
```
