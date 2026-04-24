# project.create

Creates a new project. Projects let you group related tasks and apply shared instructions. Pass the returned ID as `project_id` in [task.create](https://open.manus.ai/docs/v2/task.create) to create tasks within this project.

**Use in tasks:** Pass the returned project ID as `project_id` in [task.create](https://open.manus.ai/docs/v2/task.create) to create tasks within this project.

**Instructions:** The project’s `instruction` will be automatically applied to all tasks in the project.

#### Authorizations

| Name | Type | In | Required |
|---|---|---|---|
| `x-manus-api-key` | `string` | `header` | `required` |

#### Body

`application/json`

| Name | Type | Description | Required |
|---|---|---|---|
| `name` | `string` | Display name for the project. | `required` |
| `instruction` | `string` | Default instruction that will be automatically prepended to all tasks created within this project. Use this to enforce consistent behavior across related tasks (e.g., "Always respond in formal English" or "Focus on financial analysis"). | |

#### Response

`200`

`application/json`

Project created successfully.

| Name | Type | Description |
|---|---|---|
| `ok` | `boolean` | Whether the request was successful. |
| `request_id` | `string` | Unique identifier for this API request. |
| `project` | `object` | The created project object. |

**`project` attributes:**

| Name | Type | Description |
|---|---|---|
| `project.id` | `string` | Unique identifier for the project. |
| `project.name` | `string` | Display name of the project. |
| `project.created_at` | `integer<int64>` | Unix timestamp (seconds) when the project was created. |
| `project.instruction` | `string` | Default instruction applied to all tasks in this project. |

#### Code Examples

**cURL**

```bash
curl --request POST \
  --url https://api.manus.ai/v2/project.create \
  --header 'Content-Type: application/json' \
  --header 'x-manus-api-key: <api-key>' \
  --data '
{
  "name": "<string>",
  "instruction": "<string>"
}
'
```

**200 Response Example**

```json
{
  "ok": true,
  "request_id": "<string>",
  "project": {
    "id": "<string>",
    "name": "<string>",
    "created_at": 123,
    "instruction": "<string>"
  }
}
```