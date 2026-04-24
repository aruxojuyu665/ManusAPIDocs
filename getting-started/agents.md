# Agents

Agents are custom AI entities in Manus with their own identity (nickname and description) that can be customized for specific use cases. Each agent has a **main task** that serves as its persistent conversation thread. You can manage agents and interact with their tasks through the API.

Every account comes with a default **IM (Instant Messaging) agent** for general-purpose conversations. You can access it directly using shortcuts without looking up its UUID.

## Quick Start: Talk to an Agent

Use the shortcut `agent-default-main_task` as `task_id` to directly interact with the IM agent's main task — no need to look up UUIDs first:

**cURL:**
```bash
# Send a message to the IM agent
curl -X POST https://api.manus.ai/v2/task.sendMessage \
  -H "Content-Type: application/json" \
  -H "x-manus-api-key: $MANUS_API_KEY" \
  -d '{
    "task_id": "agent-default-main_task",
    "message": { "content": "Summarize today'\''s tech news" }
  }'
```

Then poll for the agent's response:

```bash
curl 'https://api.manus.ai/v2/task.listMessages?task_id=agent-default-main_task&order=desc&limit=5' \
  -H 'x-manus-api-key: $MANUS_API_KEY'
```

**Python:**
```python
import requests

headers = {
    "x-manus-api-key": "YOUR_API_KEY",
    "Content-Type": "application/json"
}

# Send a message to the IM agent
response = requests.post(
    "https://api.manus.ai/v2/task.sendMessage",
    headers=headers,
    json={
        "task_id": "agent-default-main_task",
        "message": {"content": "Summarize today's tech news"}
    }
)
```

## Shortcuts

The following shortcuts are available so you don't need to look up UUIDs first:

| Shortcut | Description |
|---|---|
| `agent-default` | The default IM agent |
| `agent-default-main_task` | The main task of the default IM agent |

## Managing Agents

Use the `agent.*` endpoints to list, view, and update your agents:

| Endpoint | Description |
|---|---|
| [`agent.list`](../api-reference/agents/agent.list.md) | List all agents in your account |
| [`agent.detail`](../api-reference/agents/agent.detail.md) | Get details of a specific agent |
| [`agent.update`](../api-reference/agents/agent.update.md) | Update agent nickname or description |

## Agent Subtasks

Agents can create subtasks during execution. To view an agent's subtasks, use `task.list` with `scope=agent_subtask`:

```bash
curl 'https://api.manus.ai/v2/task.list?scope=agent_subtask&agent_id=agent-default' \
  -H 'x-manus-api-key: $MANUS_API_KEY'
```

Subtasks have `task_type: "agent_subtask"` in the response and can be interacted with like any other task — `task.sendMessage`, `task.listMessages`, `task.stop`, etc.
