# Manus API Documentation

Welcome to the **Manus API Documentation** repository. This is a complete Markdown copy of the official Manus API documentation, organized for easy navigation and reference.

## 📚 Table of Contents

- [Getting Started](#getting-started)
- [Webhooks](#webhooks)
- [API Reference](#api-reference)
  - [Tasks API](#tasks-api)
  - [Files API](#files-api)
  - [Webhooks API](#webhooks-api)
- [SDK](#sdk)
- [Connectors](#connectors)
- [Integrations](#integrations)
- [Repository Structure](#repository-structure)

---

## 🚀 Getting Started

Learn the basics of the Manus API and make your first API call.

- **[Overview](getting-started/overview.md)** - Introduction to Manus API and its capabilities
- **[Quickstart](getting-started/quickstart.md)** - Generate an API key and make your first call

---

## 🔔 Webhooks

Set up real-time notifications for task lifecycle events.

- **[Webhooks Overview](webhooks/overview.md)** - Real-time notifications for task lifecycle events
- **[Security](webhooks/security.md)** - Best practices for securing your webhook endpoints with RSA-SHA256 signatures

---

## 📖 API Reference

Complete API endpoint specifications for all Manus API resources.

### Tasks API

Manage AI tasks with the Manus API.

| Endpoint | Method | Description |
|----------|--------|-------------|
| [Create Task](api-reference/tasks/create-task.md) | `POST /v1/tasks` | Create a new AI task with custom parameters and attachments |
| [Get Tasks](api-reference/tasks/get-tasks.md) | `GET /v1/tasks` | Retrieve a list of tasks with filtering and pagination |
| [Get Task](api-reference/tasks/get-task.md) | `GET /v1/tasks/{task_id}` | Retrieve details of a specific task |
| [Update Task](api-reference/tasks/update-task.md) | `PUT /v1/tasks/{task_id}` | Update an existing task |
| [Delete Task](api-reference/tasks/delete-task.md) | `DELETE /v1/tasks/{task_id}` | Delete a specific task |

### Files API

Upload and manage files for use in tasks.

| Endpoint | Method | Description |
|----------|--------|-------------|
| [Create File](api-reference/files/create-file.md) | `POST /v1/files` | Upload a new file and get a presigned upload URL |
| [List Files](api-reference/files/list-files.md) | `GET /v1/files` | Retrieve a list of uploaded files |
| [Get File](api-reference/files/get-file.md) | `GET /v1/files/{file_id}` | Retrieve details of a specific file |
| [Delete File](api-reference/files/delete-file.md) | `DELETE /v1/files/{file_id}` | Delete a specific file |

### Webhooks API

Register and manage webhook endpoints for real-time notifications.

| Endpoint | Method | Description |
|----------|--------|-------------|
| [Create Webhook](api-reference/webhooks/create-webhook.md) | `POST /v1/webhooks` | Register a webhook to receive real-time notifications |
| [Delete Webhook](api-reference/webhooks/delete-webhook.md) | `DELETE /v1/webhooks/{webhook_id}` | Remove a previously registered webhook |

---

## 🛠 SDK

Integration guides for using Manus API with popular SDKs.

- **[OpenAI SDK Compatibility](sdk/openai-compatibility.md)** - Use the OpenAI Python SDK with Manus for complex reasoning tasks

---

## 🔌 Connectors

Connect Manus with external services to enhance your workflows.

- **[Connectors Overview](connectors/overview.md)** - Introduction to Manus connectors
- **[Gmail](connectors/gmail.md)** - Connect Manus with Gmail
- **[Notion](connectors/notion.md)** - Connect Manus with Notion
- **[Google Calendar](connectors/google-calendar.md)** - Connect Manus with Google Calendar

---

## 🔗 Integrations

Integrate Manus into your favorite platforms.

- **[Integrations Overview](integrations/overview.md)** - Introduction to Manus integrations
- **[Slack](integrations/slack.md)** - Integrate Manus with Slack

---

## 📂 Repository Structure

For a detailed view of the repository structure, see [STRUCTURE.md](STRUCTURE.md).

```
ManusAPIDocs/
├── getting-started/          # Getting started guides
├── webhooks/                 # Webhooks documentation
├── api-reference/            # API endpoints reference
│   ├── tasks/               # Task management endpoints
│   ├── files/               # File management endpoints
│   └── webhooks/            # Webhook management endpoints
├── sdk/                     # SDK documentation
├── connectors/              # Connectors documentation
└── integrations/            # Integrations documentation
```

---

## 📌 Additional Resources

- **Official Documentation**: [https://open.manus.ai/docs/](https://open.manus.ai/docs/)
- **Manus Website**: [https://manus.im/](https://manus.im/)
- **API Base URL**: `https://api.manus.ai`

---

## 📝 License

This repository contains documentation sourced from the official Manus API documentation. All rights belong to Manus.

---

## 🤝 Contributing

This is a mirror repository for reference purposes. For updates or corrections, please refer to the official Manus API documentation.

---

**Last Updated**: November 16, 2025
