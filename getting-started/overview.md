# Introduction

> **You are viewing API v2** — the latest version of the Manus API. API v1 has been deprecated and will be removed in the future.

## Manus API

The Manus API allows you to programmatically create and manage AI agent tasks. Build automations, orchestrate multi-step workflows, and integrate Manus into your applications through a simple REST API.

Before making API calls, you'll need to create an API key. Head over to [Authentication](authentication.md) to get started.

## What You Can Do

| Feature | Description |
|---|---|
| **Tasks** | Create tasks, send follow-up messages, and retrieve results — full multi-turn conversation support |
| **Projects** | Organize tasks with shared instructions that apply automatically |
| **Files** | Upload files as task attachments — PDFs, images, CSVs, and more |
| **Webhooks** | Get real-time notifications when tasks complete or need input |
| **Skills** | Extend agent capabilities with built-in and custom skills |
| **Agents** | Manage and configure your custom agents |

## Base URL

All API requests are made to:

```
https://api.manus.ai
```

## Response Format

All responses use a consistent wrapper:

**Success:**
```json
{
  "ok": true,
  "request_id": "req_abc123",
  ...
}
```

**Error:**
```json
{
  "ok": false,
  "request_id": "req_abc123",
  "error": {
    "code": "invalid_argument",
    "message": "task_id is required"
  }
}
```

## Error Codes

| Error Code | Description |
|---|---|
| `invalid_argument` | Missing or invalid request parameters |
| `not_found` | The requested resource does not exist |
| `permission_denied` | API key lacks permission for this action |
| `rate_limited` | Too many requests — see [Rate Limits](rate-limits.md) for per-endpoint limits and backoff guidance |
