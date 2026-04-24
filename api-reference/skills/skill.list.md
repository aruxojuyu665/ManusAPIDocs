# skill.list - Manus API

Lists available skills. Includes project skills when project_id is provided. Use the returned IDs in `enable_skills` or `force_skills` of `task.create`.

Questions or issues? Contact us at api-support@manus.ai.

## Endpoint

`GET /v2/skill.list`

## Authorizations

| Parameter       | Type   | Location | Required |
|-----------------|--------|----------|----------|
| `x-manus-api-key` | string | header   | required |

## Query Parameters

| Parameter   | Type   | Description                                                                                             |
|-------------|--------|---------------------------------------------------------------------------------------------------------|
| `project_id` | string | When provided, includes project-specific skills in addition to the user's global skills. Use `project.list` to get available project IDs. |

## Response (200 OK)

`application/json`

Skills retrieved successfully.

| Field         | Type          | Description                                                                                                                               |
|---------------|---------------|-------------------------------------------------------------------------------------------------------------------------------------------|
| `ok`          | boolean       | Whether the request was successful. Example: `true`                                                                                       |
| `request_id`  | string        | Unique identifier for this API request.                                                                                                   |
| `data`        | object[]      | Array of skill objects. Use the `id` field when passing to `enable_skills` or `force_skills` in `task.create`.                            |
| `data.id`     | string        | Unique identifier for the skill. Use this in `enable_skills` or `force_skills` when creating tasks.                                       |
| `data.name`   | string        | Display name of the skill.                                                                                                                |
| `data.description` | string        | What the skill does and when it's useful.                                                                                                 |
| `data.owner_type` | enum<string>  | Who owns the skill. "personal" — user-created skill. "official" — built-in system skill. "team" — team-shared skill. "project" — project-specific skill. Available options: `personal`, `official`, `team`, `project` |
| `data.creator_info` | object        | Information about who created the skill.                                                                                                  |
| `data.creator_info.user_id` | string        | User ID of the skill creator.                                                                                                             |
| `data.creator_info.name` | string        | Display name of the skill creator.                                                                                                        |
| `data.created_at` | integer<int64> | Unix timestamp (seconds) when the skill was created.                                                                                      |
| `data.updated_at` | integer<int64> | Unix timestamp (seconds) when the skill was last updated.                                                                                 |

## Code Examples

### cURL

```bash
curl --request GET \
  --url https://api.manus.ai/v2/skill.list \
  --header 'x-manus-api-key: <api-key>'
```

### JSON Response (200 OK)

```json
{
  "ok": true,
  "request_id": "<string>",
  "data": [
    {
      "id": "<string>",
      "name": "<string>",
      "description": "<string>",
      "owner_type": "personal",
      "creator_info": {
        "user_id": "<string>",
        "name": "<string>"
      },
      "created_at": 123,
      "updated_at": 123
    }
  ]
}
```