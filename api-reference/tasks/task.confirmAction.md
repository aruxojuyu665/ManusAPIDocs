# task.confirmAction - Manus API

Confirms a pending action to resume the task. Use when `task.listMessages` shows `agent_status: "waiting"`. For `messageAskUser` events, use `task.sendMessage` instead. See the [Task Lifecycle](https://open.manus.ai/docs/v2/task.confirmAction) guide for input formats.

POST /v2/task.confirmAction

Questions or issues? Contact us at [api-support@manus.ai](mailto:api-support@manus.ai).

**Input format:** Depends on `waiting_for_event_type` from the `status_update` event. Check the `confirm_input_schema` field in the event for the expected JSON Schema. See the [Task Lifecycle](https://open.manus.ai/docs/v2/task.confirmAction) guide for all event types and examples.

**messageAskUser:** Use `task.sendMessage` instead — do not use this endpoint for agent questions.

## Authorizations

| Name            | Type   | In     | Required |
| :-------------- | :----- | :----- | :------- |
| `x-manus-api-key` | string | header | required |

## Body

`application/json`

| Name      | Type   | Required | Description                                                                                                                                                                    |
| :-------- | :----- | :------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `task_id`   | string | required | The unique identifier of the task with a pending action. Supports the shortcut `agent-default-main_task` for the IM agent's main task.                                         |
| `event_id`  | string | required | The `waiting_for_event_id` value from the `status_update` event that triggered the confirmation request. This identifies which specific action to confirm. |
| `input`     | object | optional | Optional input data for the pending action. The expected schema is defined by the `confirm_input_schema` field in the `status_update` event. For simple confirmations, this can be omitted. |

## Response

### 200 OK

`application/json`

Action confirmed successfully. The task will resume processing.

| Name         | Type    | Description                                   |
| :----------- | :------ | :-------------------------------------------- |
| `ok`           | boolean | Whether the request was successful.           |
| `request_id`   | string  | Unique identifier for this API request.       |
| `task_id`      | string  | The ID of the task that was confirmed.        |
| `confirmed`    | boolean | Always true when the confirmation was accepted. |

**Example:**

```json
{
  "ok": true,
  "request_id": "<string>",
  "task_id": "<string>",
  "confirmed": true
}
```

## Code Example

### cURL

```bash
curl --request POST \
  --url https://api.manus.ai/v2/task.confirmAction \
  --header 'Content-Type: application/json' \
  --header 'x-manus-api-key: <api-key>' \
  --data '
{
  "task_id": "<string>",
  "event_id": "<string>",
  "input": {}
}
'
```