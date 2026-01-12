# Create Project

> Creates a new project to organize tasks and apply consistent instructions.

## Endpoint

**POST** `/v1/projects`

**Base URL:** `https://api.manus.ai`

## Authentication

**Required Header:**
- `API_KEY` (string, required) - Your API authentication key

## Request Body

**Content-Type:** `application/json`

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `name` | string | Yes | The name of the project |
| `instruction` | string | No | Default instruction applied to all tasks in this project |

## Example Request

```bash
curl -X POST "https://api.manus.ai/v1/projects" \
  -H "Content-Type: application/json" \
  -H "API_KEY: your-api-key" \
  -d '{
    "name": "Research Project",
    "instruction": "You must start every response with a summary of key findings"
  }'
```

## Response

**Status Code:** 200 (Success)

**Content-Type:** `application/json`

### Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `id` | string | Unique identifier for the project |
| `name` | string | Name of the project |
| `instruction` | string | Default instruction applied to all tasks in this project |
| `created_at` | integer (int64) | Unix timestamp (seconds) when the project was created |

### Example Response

```json
{
  "id": "proj_abc123",
  "name": "Research Project",
  "instruction": "You must start every response with a summary of key findings",
  "created_at": 1699900000
}
```

## Using Projects with Tasks

Once created, assign tasks to a project by including `project_id` in task creation requests:

```bash
curl -X POST "https://api.manus.ai/v1/tasks" \
  -H "Content-Type: application/json" \
  -H "API_KEY: your-api-key" \
  -d '{
    "prompt": "Analyze this data",
    "agentProfile": "manus-1.6",
    "projectId": "proj_abc123"
  }'
```

The project's instruction automatically applies to all tasks created within that project.
