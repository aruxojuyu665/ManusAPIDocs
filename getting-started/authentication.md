# Authentication

## Create an API Key

**Step 1 — Open API settings.** Go to [Manus API Integration settings](https://manus.im/app/settings/api) in the Manus webapp.

**Step 2 — Generate a key.** Click **Create API Key** and give it a descriptive name (e.g. `"production"`, `"dev-testing"`). Each account can have up to **50 API keys**.

**Step 3 — Copy and store securely.** Copy the key immediately — it will only be shown once. Store it in a secure location such as an environment variable or secrets manager.

> **Security Warning:** Keep your API keys secure and never share them publicly. Each key provides full access to your Manus account. If a key is compromised, revoke it immediately from the settings page.

> **Note:** Rate limits apply per user (shared across all of your API keys). See [Rate Limits](rate-limits.md) for the per-endpoint numbers.

## Use the API Key

Include the key in the `x-manus-api-key` header with every request:

**cURL:**
```bash
curl -X POST https://api.manus.ai/v2/task.create \
  -H "Content-Type: application/json" \
  -H "x-manus-api-key: $MANUS_API_KEY" \
  -d '{
    "message": {
      "content": "hello"
    }
  }'
```

**Python:**
```python
import requests

headers = {
    "x-manus-api-key": "YOUR_API_KEY",
    "Content-Type": "application/json"
}

response = requests.post(
    "https://api.manus.ai/v2/task.create",
    headers=headers,
    json={"message": {"content": "hello"}}
)
```

**TypeScript:**
```typescript
const response = await fetch("https://api.manus.ai/v2/task.create", {
  method: "POST",
  headers: {
    "x-manus-api-key": process.env.MANUS_API_KEY!,
    "Content-Type": "application/json",
  },
  body: JSON.stringify({ message: { content: "hello" } }),
});
```

## Authentication Errors

If the key is missing or invalid, the API returns:

```json
{
  "ok": false,
  "request_id": "req_abc123",
  "error": {
    "code": "permission_denied",
    "message": "Invalid or missing API key"
  }
}
```
