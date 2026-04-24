# website.status - Manus API

**URL:** https://open.manus.ai/docs/v2/website.status

---

Skip to main content
Manus API home page
Search...
Ctrl K
Getting Started
Introduction
Authentication
Task Lifecycle
Connectors
Webhooks Guide
Agents
Integrations
Data Integrations
Website
Rate Limits
API Reference
Tasks
Projects
Skills
Agents
Files
Webhooks
Usage
Connectors
Browser
Website
GET
website.status
GET
website.listCheckpoints
POST
website.publish
POST
website.update
v2
Website
website.status
Copy page

Retrieves a website’s publish status, live URL, and visibility. Use website.listCheckpoints to browse version history, or website.publish to deploy changes. See the Website guide.

GET
/
v2
/
website.status
Try it
Questions or issues? Contact us at api-support@manus.ai.
Poll after publish: Call this after website.publish until publish_status settles to published or failed.
Live version: Match the response’s version_id against entries from website.listCheckpoints to see which checkpoint is serving traffic. See the Website guide.
Authorizations
​
x-manus-api-key
stringheaderrequired
Query Parameters
​
task_id
string

Session UID. Mutually exclusive with website_id — exactly one must be provided. The session must contain exactly one website.

​
website_id
string

Unique website ID. Mutually exclusive with task_id — exactly one must be provided. Obtain from the response of website.status or website.publish.

Response
200
application/json

Web status retrieved successfully.

​
ok
boolean

Whether the request was successful.

Example:

true

​
request_id
string

Unique identifier for this API request.

​
website_id
string

Unique website ID.

​
publish_status
enum<string>

unpublished — never published or has been taken down; call website.publish to bring it online. publishing — deployment in progress; poll again. published — live and site_urls is reachable. failed — last deployment failed.

Available options: unpublished, publishing, published, failed 
​
site_urls
string[]

Public URLs where the live site can be reached, ordered from default to most specific: the space URL (https://{space_id}.manus.space, always present when published), an optional sub-domain URL (https://{sub_domain}.manus.space), and any active custom domains bound by the owner. All entries include the https:// scheme. Returned as an empty array unless publish_status is published.

​
version_id
string

Optional. Checkpoint version_id currently deployed. Present only when the site has been published.

​
status_updated_at
integer<int64>

Optional. Last time the publish status changed (Unix seconds). Present only when the site has been published.

​
visibility
enum<string>

Who can access the published site. public — anyone. team — current team members only (team accounts). private — owner and invited collaborators only.

Available options: public, team, private