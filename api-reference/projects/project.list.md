# project.list - Manus API

Lists all projects. Use the returned IDs as project_id in task.create or task.list.

GET /v2/project.list

Questions or issues? Contact us at api-support@manus.ai.

#### Authorizations

x-manus-api-key

string

header

required

#### Response

200

application/json

Projects retrieved successfully.

ok

boolean

Whether the request was successful.

Example:

`true`

request_id

string

Unique identifier for this API request.

data

object[]

Array of project objects.

Hide child attributes

data.id

string

Unique identifier for the project.

data.name

string

Display name of the project.

data.created_at

integer<int64>

Unix timestamp (seconds) when the project was created.

data.instruction

string

Default instruction applied to all tasks in this project.

#### Code Examples

cURL

```bash
curl --request GET \
  --url https://api.manus.ai/v2/project.list \
  --header 'x-manus-api-key: <api-key>'
```

200 Response Example:

```json
{
  "ok": true,
  "request_id": "<string>",
  "data": [
    {
      "id": "<string>",
      "name": "<string>",
      "created_at": 123,
      "instruction": "<string>"
    }
  ]
}
```