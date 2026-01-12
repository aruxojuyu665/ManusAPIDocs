# List Projects

> Retrieves a list of all projects associated with your account.

## Endpoint

**GET** `/v1/projects`

**Base URL:** `https://api.manus.ai`

## Authentication

**Required Header:**
- `API_KEY` (string, required) - Your API authentication key

## Query Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `limit` | integer (int32) | Maximum number of projects to return. Default: 100, Range: 1-1000 |

## Example Request

```bash
curl -X GET "https://api.manus.ai/v1/projects?limit=100" \
  -H "API_KEY: your-api-key"
```

## Response

**Status Code:** 200 (Success)

**Content-Type:** `application/json`

### Response Format

```json
{
  "data": [
    {
      "id": "<string>",
      "name": "<string>",
      "instruction": "<string>",
      "created_at": 123
    }
  ]
}
```

### Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `data` | object[] | Array of project objects |
| `data[].id` | string | Unique identifier for the project |
| `data[].name` | string | Name of the project |
| `data[].instruction` | string | Default instruction applied to all tasks in this project |
| `data[].created_at` | integer (int64) | Unix timestamp (seconds) when the project was created |

### Example Response

```json
{
  "data": [
    {
      "id": "proj_abc123",
      "name": "My Research Project",
      "instruction": "You must always cite your sources",
      "created_at": 1699900000
    },
    {
      "id": "proj_def456",
      "name": "Customer Support",
      "instruction": "Be friendly and helpful",
      "created_at": 1699800000
    }
  ]
}
```
