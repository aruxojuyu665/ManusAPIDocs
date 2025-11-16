# Manus API Documentation - Repository Structure

This repository contains a complete copy of the official Manus API documentation in Markdown format.

## Directory Structure

```
ManusAPIDocs/
├── README.md                          # Main navigation and overview
├── STRUCTURE.md                       # This file - repository structure description
├── getting-started/                   # Getting started guides
│   ├── overview.md                    # API overview and introduction
│   └── quickstart.md                  # Quick start guide
├── webhooks/                          # Webhooks documentation
│   ├── overview.md                    # Webhooks introduction
│   └── security.md                    # Webhook security and signature verification
├── api-reference/                     # API endpoints reference
│   ├── tasks/                         # Task management endpoints
│   │   ├── create-task.md             # POST /v1/tasks
│   │   ├── get-tasks.md               # GET /v1/tasks
│   │   ├── get-task.md                # GET /v1/tasks/{task_id}
│   │   ├── update-task.md             # PUT /v1/tasks/{task_id}
│   │   └── delete-task.md             # DELETE /v1/tasks/{task_id}
│   ├── files/                         # File management endpoints
│   │   ├── create-file.md             # POST /v1/files
│   │   ├── list-files.md              # GET /v1/files
│   │   ├── get-file.md                # GET /v1/files/{file_id}
│   │   └── delete-file.md             # DELETE /v1/files/{file_id}
│   └── webhooks/                      # Webhook management endpoints
│       ├── create-webhook.md          # POST /v1/webhooks
│       └── delete-webhook.md          # DELETE /v1/webhooks/{webhook_id}
├── sdk/                               # SDK documentation
│   └── openai-compatibility.md        # OpenAI SDK compatibility guide
├── connectors/                        # Connectors documentation
│   ├── overview.md                    # Connectors overview
│   ├── gmail.md                       # Gmail connector
│   ├── notion.md                      # Notion connector
│   └── google-calendar.md             # Google Calendar connector
└── integrations/                      # Integrations documentation
    ├── overview.md                    # Integrations overview
    └── slack.md                       # Slack integration
```

## Documentation Categories

### Getting Started
Introduction and quick start guides for new users.

### Webhooks
Real-time notifications for task lifecycle events, including security best practices.

### API Reference
Complete API endpoint specifications organized by resource type:
- **Tasks**: Create, retrieve, update, and delete AI tasks
- **Files**: Manage file uploads and downloads
- **Webhooks**: Register and manage webhook endpoints

### SDK
Integration guides for using Manus API with popular SDKs.

### Connectors
Documentation for connecting Manus with external services like Gmail, Notion, and Google Calendar.

### Integrations
Guides for integrating Manus into platforms like Slack.

## Source

All documentation is sourced from the official Manus API documentation at https://open.manus.ai/docs/

Last updated: November 16, 2025
