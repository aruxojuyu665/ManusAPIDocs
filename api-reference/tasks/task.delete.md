# task.delete - Manus API

Deletes a task permanently. If the task is still running, use task.stop first. Agent-related tasks (e.g. agent main tasks and subtasks) cannot be deleted.

Questions or issues? Contact us at api-support@manus.ai.

## Authorizations

| Parameter | Type   | Location | Required |
| :-------- | :----- | :------- | :------- |
| x-manus-api-key | string | header   | required |

## Body

`application/json`

| Parameter | Type   | Required | Description                                                |
| :-------- | :----- | :------- | :--------------------------------------------------------- |
| task_id   | string | required | The unique identifier of the task to delete. Agent-related tasks cannot be deleted. |

## Response

`200 application/json`

Task deleted successfully.

| Field      | Type    | Description                       |
| :--------- | :------ | :-------------------------------- |
| ok         | boolean | Whether the request was successful. |
| request_id | string  | Unique identifier for this API request. |
| id         | string  | The ID of the deleted task.       |
| deleted    | boolean | Always true when the deletion was successful. |

Example:

```json
{
  "ok": true,
  "request_id": "<string>",
  "id": "<string>",
  "deleted": true
}
```

## Code Example

### cURL

```bash
curl --request POST \
  --url https://api.manus.ai/v2/task.delete \
  --header 'Content-Type: application/json' \
  --header 'x-manus-api-key: <api-key>' \
  --data '
{
  "task_id": "<string>"
}
'
```