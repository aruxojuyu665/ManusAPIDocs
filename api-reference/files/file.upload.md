# file.upload - Manus API

**URL:** https://open.manus.ai/docs/v2/file.upload

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
file.upload
Copy page

Creates a file record and returns a presigned upload URL. Upload the file content to the returned upload_url via PUT before it expires. Then use the file.id as file_id in task.create or task.sendMessage message content.

POST
/
v2
/
file.upload
Try it
Questions or issues? Contact us at api-support@manus.ai.
Upload: Send file content to the returned upload_url via PUT request.
Use in tasks: Pass the file.id as file_id in task.create or task.sendMessage message content.
Expiration: The upload_url expires in 3 minutes. Files are automatically deleted 48 hours after upload.
Authorizations
​
x-manus-api-key
stringheaderrequired
Body
application/json
​
filename
stringrequired

Name of the file to upload, including extension (e.g., "report.pdf", "data.csv"). The extension helps determine the file type.

Response
200
application/json

File record created successfully.

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

The created file record. Status will be pending until the upload completes.

Hide child attributes

​
file.id
string

Unique identifier for the file. Use this as file_id when attaching to tasks.

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
upload_url
string

Presigned S3 URL for uploading the file content. Send a PUT request with the file bytes as the body. Expires in 3 minutes.

​
upload_expires_at
integer<int64>

Unix timestamp (seconds) when the upload_url expires. Complete the upload before this time.