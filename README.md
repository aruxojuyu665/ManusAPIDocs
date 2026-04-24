# Manus API Documentation

Welcome to the **Manus API Documentation** repository. This is a complete Markdown copy of the official Manus API v2 documentation, organized for easy navigation and reference.

## 📚 Table of Contents

- [Getting Started](#getting-started)
- [API Reference](#api-reference)
  - [Tasks API](#tasks-api)
  - [Projects API](#projects-api)
  - [Skills API](#skills-api)
  - [Agents API](#agents-api)
  - [Files API](#files-api)
  - [Webhooks API](#webhooks-api)
  - [Usage API](#usage-api)
  - [Connectors API](#connectors-api)
  - [Browser API](#browser-api)
  - [Website API](#website-api)
- [Webhooks Guide](#webhooks-guide)
- [Connectors](#connectors)
- [Integrations](#integrations)
- [Data Integrations](#data-integrations)
- [Repository Structure](#repository-structure)

---

## 🚀 Getting Started

Learn the basics of the Manus API and make your first API call.

- **[Overview](getting-started/overview.md)** - Introduction to Manus API v2 and its capabilities
- **[Authentication](getting-started/authentication.md)** - Create and use API keys
- **[Task Lifecycle](getting-started/task-lifecycle.md)** - Poll task status, handle confirmations, and process results
- **[Agents](getting-started/agents.md)** - Interact with agents and their tasks via the API
- **[Website](getting-started/website.md)** - Manage websites built by Manus agents
- **[Rate Limits](getting-started/rate-limits.md)** - Per-user request limits for v2 endpoints

---

## 📖 API Reference

Complete API endpoint specifications for all Manus API v2 resources.

### Tasks API
Manage AI tasks with the Manus API.
- [Create Task](api-reference/tasks/task.create.md) (`POST /v2/task.create`)
- [Get Task Detail](api-reference/tasks/task.detail.md) (`GET /v2/task.detail`)
- [List Tasks](api-reference/tasks/task.list.md) (`GET /v2/task.list`)
- [Update Task](api-reference/tasks/task.update.md) (`POST /v2/task.update`)
- [Stop Task](api-reference/tasks/task.stop.md) (`POST /v2/task.stop`)
- [Delete Task](api-reference/tasks/task.delete.md) (`POST /v2/task.delete`)
- [Send Message](api-reference/tasks/task.sendMessage.md) (`POST /v2/task.sendMessage`)
- [List Messages](api-reference/tasks/task.listMessages.md) (`GET /v2/task.listMessages`)
- [Confirm Action](api-reference/tasks/task.confirmAction.md) (`POST /v2/task.confirmAction`)

### Projects API
- [Create Project](api-reference/projects/project.create.md) (`POST /v2/project.create`)
- [List Projects](api-reference/projects/project.list.md) (`GET /v2/project.list`)

### Skills API
- [List Skills](api-reference/skills/skill.list.md) (`GET /v2/skill.list`)

### Agents API
- [List Agents](api-reference/agents/agent.list.md) (`GET /v2/agent.list`)
- [Get Agent Detail](api-reference/agents/agent.detail.md) (`GET /v2/agent.detail`)
- [Update Agent](api-reference/agents/agent.update.md) (`POST /v2/agent.update`)

### Files API
- [Upload File](api-reference/files/file.upload.md) (`POST /v2/file.upload`)
- [Get File Detail](api-reference/files/file.detail.md) (`GET /v2/file.detail`)
- [Delete File](api-reference/files/file.delete.md) (`POST /v2/file.delete`)

### Webhooks API
- [Create Webhook](api-reference/webhooks/webhook.create.md) (`POST /v2/webhook.create`)
- [List Webhooks](api-reference/webhooks/webhook.list.md) (`GET /v2/webhook.list`)
- [Delete Webhook](api-reference/webhooks/webhook.delete.md) (`POST /v2/webhook.delete`)
- [Get Public Key](api-reference/webhooks/webhook.publicKey.md) (`GET /v2/webhook.publicKey`)

### Usage API
- [List Usage](api-reference/usage/usage.list.md) (`GET /v2/usage.list`)
- [Team Statistic](api-reference/usage/usage.teamStatistic.md) (`GET /v2/usage.teamStatistic`)
- [Team Log](api-reference/usage/usage.teamLog.md) (`GET /v2/usage.teamLog`)

### Connectors API
- [List Connectors](api-reference/connectors/connector.list.md) (`GET /v2/connector.list`)

### Browser API
- [List Online Browsers](api-reference/browser/browser.onlineList.md) (`GET /v2/browser.onlineList`)

### Website API
- [Website Status](api-reference/website/website.status.md) (`GET /v2/website.status`)
- [List Checkpoints](api-reference/website/website.listCheckpoints.md) (`GET /v2/website.listCheckpoints`)
- [Publish Website](api-reference/website/website.publish.md) (`POST /v2/website.publish`)

---

## 🔔 Webhooks Guide

Set up real-time notifications for task lifecycle events.

- **[Overview](webhooks/overview.md)** - Real-time notifications for task lifecycle events
- **[Security](webhooks/security.md)** - Verify webhook signatures to ensure requests are from Manus

---

## 🔌 Connectors

Connect Manus with external services to enhance your workflows.

- **[Overview](connectors/overview.md)** - Connect external apps to Manus and use them in API tasks

---

## 🔗 Integrations

Integrate Manus into your favorite platforms.

- **[Overview](integrations/overview.md)** - Use Manus from your favorite apps
- **[Slack](integrations/slack.md)** - Start sessions directly from Slack channels or DM the Manus bot

---

## 📊 Data Integrations

Access built-in third-party data directly in Manus.

- **[Overview](data-integrations/overview.md)** - Access built-in third-party data directly in Manus
- **[Similarweb](data-integrations/similarweb.md)** - Access website traffic and digital market intelligence data

---

## 📂 Repository Structure

For a detailed view of the repository structure, see [STRUCTURE.md](STRUCTURE.md).

---

## 📌 Additional Resources

- **Official Documentation**: [https://open.manus.ai/docs/v2/](https://open.manus.ai/docs/v2/)
- **Manus Website**: [https://manus.im/](https://manus.im/)
- **API Base URL**: `https://api.manus.ai`

---

## 📝 License

This repository contains documentation sourced from the official Manus API documentation. All rights belong to Manus.

---

## 🤝 Contributing

This is a mirror repository for reference purposes. For updates or corrections, please refer to the official Manus API documentation.

---

**Last Updated**: April 24, 2026
