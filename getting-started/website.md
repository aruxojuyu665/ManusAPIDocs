# Website

Manus agents can build web apps. When an agent builds a site inside a task, it produces a **website** with its own version history and a hosted URL once published. The `website.*` endpoints manage those websites:

- [`website.status`](../api-reference/website/website.status.md) — inspect publish state, live URL, visibility
- [`website.listCheckpoints`](../api-reference/website/website.listCheckpoints.md) — browse version history
- [`website.publish`](../api-reference/website/website.publish.md) — deploy the latest checkpoint
- `website.update` — change metadata (title, visibility) without redeploying

> To have an agent **build** a website, create a task with `task.create`. Once the session has a website attached, the endpoints on this page take over.

## Quickstart: Publish a Site

After the agent has built something (the task's session now has a website), deploy it with one call and poll for the live URL:

```bash
# 1. Deploy the latest checkpoint — defaults to public
curl -X POST 'https://api.manus.ai/v2/website.publish' \
  -H 'x-manus-api-key: YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"task_id": "session-xxx"}'
# → { "ok": true, "website_id": "site-abc", "version_id": "v003" }

# 2. Poll status until published / failed
while true; do
  RESP=$(curl -sS "https://api.manus.ai/v2/website.status?website_id=site-abc" \
    -H 'x-manus-api-key: YOUR_API_KEY')
  STATUS=$(echo "$RESP" | jq -r .publish_status)
  echo "status: $STATUS"
  [[ "$STATUS" == "published" || "$STATUS" == "failed" ]] && break
  sleep 2
done

# 3. Read the primary site URL and open it
echo "$RESP" | jq -r '.site_urls[0]'
```

> **Note:** Deployment is asynchronous — `website.publish` returns immediately while the deploy runs in the background.

## Other Common Flows

**Ship an updated build.** After the agent makes more changes (new checkpoints), call `website.publish` again — it always deploys the **latest** checkpoint. There is no way to pin an older checkpoint via this API.

**Browse version history:**
```bash
curl 'https://api.manus.ai/v2/website.listCheckpoints?task_id=session-xxx' \
  -H 'x-manus-api-key: YOUR_API_KEY'
```

Match each `data[].version_id` against `published_version_id` in the same response to find which checkpoint is currently live.

**Change metadata without redeploying:**
```bash
curl -X POST 'https://api.manus.ai/v2/website.update' \
  -H 'x-manus-api-key: YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"website_id": "site-abc", "title": "My landing page", "visibility": "team"}'
```

Pass any combination of `title` and `visibility` — omitted fields are left unchanged. This does **not** trigger a new deployment, only a metadata update and a CDN refresh; it works even before the site has ever been published.

**Take a site offline.** There is no public unpublish endpoint at this time. If you need to take a site down, contact [api-support@manus.ai](mailto:api-support@manus.ai).

## Reference

### Anatomy of a Website

A website in Manus consists of:

- A **website ID** (`website_id`) — unique identifier for the website
- A **version history** — list of checkpoints (snapshots) created during agent builds
- A **publish state** — whether the site is currently deployed and accessible
- **Site URLs** — the hosted URLs where the site can be accessed

### Locating a Website

All four endpoints accept either `task_id` or `website_id` — exactly one must be provided. Passing both or neither returns `400 invalid_argument`. A session is expected to contain exactly one website; if more exist, the first is used.

### Site URLs

When a site is published, `website.status` returns `site_urls` — an array of every hostname the site can be reached on, ordered from default to most specific:

| Priority | URL Type | Format |
|---|---|---|
| 1 | Space URL | `https://{space_id}.manus.space` — Always present for a published site |
| 2 | Sub-domain URL | `https://{sub_domain}.manus.space` — Only when the owner has configured a sub-domain |
| 3 | Custom domains | `https://{custom_domain}` — For each active custom domain bound by the owner |

For a simple "open the site" flow, `site_urls[0]` is enough — it's always the space URL. The array is empty whenever `publish_status` is not `published`.

### Publish States

| State | Description |
|---|---|
| `unpublished` | Site has never been deployed |
| `publishing` | Deployment is in progress |
| `published` | Site is live and accessible |
| `failed` | Deployment failed |

### Checkpoint Status vs. Publish State

A checkpoint's own `status` (`pending` / `success` / `failed` / `unspecified`) only says whether the snapshot was generated successfully — a `success` checkpoint is **not** automatically live. To find the live version, compare `website.status.version_id` (or `website.listCheckpoints.published_version_id`) against `data[].version_id`.

### Visibility

| Value | Description |
|---|---|
| `owner` | Only the owner can view the site |
| `team` | All team members can view the site |
| `public` | Anyone with the URL can view the site |

Sites may additionally cap the maximum visibility they accept — for example, a team-only site cannot be set to `public`. Requests that exceed the allowed visibility return `403 permission_denied`.

### `website.publish` vs. `website.update`

| Operation | `website.publish` | `website.update` |
|---|---|---|
| Triggers deployment | Yes | No |
| Updates metadata | No | Yes |
| Works before first publish | No | Yes |
| Async operation | Yes | No |
