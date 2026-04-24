# file.detail - Manus API

**URL:** https://open.manus.ai/docs/v2/file.detail

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
POST
file.upload
GET
file.detail
POST
file.delete
Webhooks
Usage
Connectors
Browser
Website
v2
Files
file.detail
Copy page

Retrieves a file’s details including upload status, size, and expiration time. Check that status is uploaded before using the file in task.create. Files expire 48 hours after upload.

GET
/
v2
/
file.detail
Try it
Questions or issues? Contact us at api-support@manus.ai.
Authorizations
​
x-manus-api-key
stringheaderrequired
Query Parameters
​
file_id
stringrequired

The unique identifier of the file to retrieve.

Response
200
application/json

File retrieved successfully.

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
file
object

The file object with full details.

Hide child attributes

​
file.id
string

Unique identifier for the file.

​
file.filename
string

Name of the file.

​
file.status
enum<string>

File status. "pending" — waiting for upload. "uploaded" — ready to use. "deleted" — file has been deleted. "error" — upload failed.

Available options: pending, uploaded, deleted, error 
​
file.created_at
integer<int64>

Unix timestamp (seconds) when the file record was created.

​
file.bytes
integer<int64> | null

File size in bytes. Only available after upload is complete.

​
file.content_type
string

MIME type of the file (e.g., "application/pdf", "text/csv").

​
file.expires_at
integer<int64>

Unix timestamp (seconds) when the file will be automatically deleted (48 hours after upload).

​
file.error_message
string | null

Error description if the file status is "error".