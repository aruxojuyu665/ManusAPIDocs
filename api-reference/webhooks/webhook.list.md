# webhook.list - Manus API

Lists all webhooks in your account. Use the returned IDs with webhook.delete to remove a webhook.

Questions or issues? Contact us at api-support@manus.ai.

## Authorizations

| Name            | Type   | In     | Required |
| :-------------- | :----- | :----- | :------- |
| x-manus-api-key | string | header | true     |

## Response

### Status Code: 200

**Description:** Webhooks retrieved successfully.

| Field         | Type          | Description                                                               |
| :------------ | :------------ | :------------------------------------------------------------------------ |
| ok            | boolean       | Whether the request was successful. Example: `true`                       |
| request_id    | string        | Unique identifier for this API request.                                   |
| data          | object[]      | Array of webhook objects.                                                 |
| data.id       | string        | Unique identifier for the webhook.                                        |
| data.url      | string        | The endpoint URL receiving webhook POST notifications.                    |
| data.status   | enum<string>  | Webhook status. "active" — receiving notifications. "inactive" — paused. Available options: `active`, `inactive` |
| data.created_at | integer<int64> | Unix timestamp (seconds) when the webhook was created.                    |

## Code Examples

### cURL

```bash
curl --request GET \
  --url https://api.manus.ai/v2/webhook.list \
  --header 'x-manus-api-key: <api-key>'
```

### 200 Response Example

```json
{
  "ok": true,
  "request_id": "<string>",
  "data": [
    {
      "id": "<string>",
      "url": "<string>",
      "status": "active",
      "created_at": 123
    }
  ]
}
```

Powered by This documentation is built and hosted on Mintlify, a developer documentation platform