# usage.list - Manus API

Lists the current user’s credit change history at session granularity, sorted by change time (newest first).

#### Authorizations

| Parameter | Type | Location | Required |
|---|---|---|---|
| `x-manus-api-key` | string | header | required |

#### Query Parameters

| Parameter | Type | Description |
|---|---|---|
| `limit` | integer | Number of records to return per page. Default: 20, Max: 100. |
| `cursor` | string | Pagination cursor from the previous response's `next_cursor` field. Omit for the first page. |

#### Response

**200 OK**

`application/json`

Usage records retrieved successfully.

| Field | Type | Description |
|---|---|---|
| `ok` | boolean | Whether the request was successful. Example: `true` |
| `request_id` | string | Unique identifier for this API request. |
| `data` | object[] | Array of credit consumption records, one per task. |
| `data.task_id` | string | The task (session) ID this change is associated with. |
| `data.title` | string | The task title. Returns "Deleted conversation" if the session has been deleted. |
| `data.credits` | integer | Credit change amount. Negative values represent consumption; positive values represent refunds or subscription/admin grants. |
| `data.created_at` | integer | Time of the most recent change as a Unix timestamp in seconds. |
| `data.type` | enum<string> | Change type: `cost` — credit consumption (task usage or admin deduction), `refund` — credit returned after consumption (e.g., task failure rollback), `grant` — credits gained (subscription grant, upgrade bonus, recurring issuance, credit pack purchase, admin compensation). Available options: `cost`, `refund`, `grant` |
| `data.collaborate_infos` | object[] | Per-collaborator credit breakdown for team tasks. Empty for personal tasks. |
| `data.collaborate_infos.user_id` | string | Collaborator's user ID. |
| `data.collaborate_infos.user_name` | string | Collaborator's display name. |
| `data.collaborate_infos.credits` | integer | Credits attributed to this collaborator for the task. |
| `has_more` | boolean | Whether there are more records beyond this page. If true, use `next_cursor` to fetch the next page. |
| `next_cursor` | string | Cursor to pass as the cursor parameter for the next page. Only present when `has_more` is true. |

#### Code Examples

**cURL**

```bash
curl --request GET \
  --url https://api.manus.ai/v2/usage.list \
  --header 'x-manus-api-key: <api-key>'
```

**200 Response Example**

```json
{
  "ok": true,
  "request_id": "<string>",
  "data": [
    {
      "task_id": "<string>",
      "title": "<string>",
      "credits": 123,
      "created_at": 123,
      "type": "cost",
      "collaborate_infos": [
        {
          "user_id": "<string>",
          "user_name": "<string>",
          "credits": 123
        }
      ]
    }
  ],
  "has_more": true,
  "next_cursor": "<string>"
}
```