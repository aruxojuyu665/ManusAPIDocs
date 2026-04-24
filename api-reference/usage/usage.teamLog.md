# usage.teamLog - Manus API

**URL:** https://open.manus.ai/docs/v2/usage.teamLog

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
GET
usage.list
GET
usage.teamStatistic
GET
usage.teamLog
Connectors
Browser
Website
v2
Usage
usage.teamLog
Copy page

Lists team members’ task counts and total credit consumption over the requested range — one row per user.

GET
/
v2
/
usage.teamLog
Try it
Questions or issues? Contact us at api-support@manus.ai.
Team only: This endpoint is only available to team users. Individual users will receive a permission_denied error.
Visibility: Owner / Super Admin / Admin sees every team member’s row. Member sees only their own row.
Data freshness: Enterprise teams have T+1 latency — today’s data becomes visible the next day because it is sourced from an offline sync table. Non-Enterprise teams aggregate in real time.
Authorizations
​
x-manus-api-key
stringheaderrequired
Query Parameters
​
limit
integer

Number of records to return per page. Default: 20, Max: 100.

​
cursor
string

Pagination cursor from the previous response's next_cursor field. Omit for the first page.

​
start_date
integer

Filter start time as a Unix timestamp in seconds.

​
end_date
integer

Filter end time as a Unix timestamp in seconds.

​
sort_by
enum<string>

Field to sort by. Default: task_count.

Available options: task_count, credits 
​
is_asc
boolean

Sort in ascending order. Default: false (descending).

Response
200
application/json

Team usage log retrieved successfully.

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
data
object[]

Array of per-user daily consumption records.

Hide child attributes

​
data.user_id
string

Team member's user ID.

​
data.user_name
string

Team member's display name.

​
data.email
string

Team member's email address.

​
data.task_count
integer

Number of tasks the member created within the requested range.

​
data.credits
integer

Total credits consumed by this user within the requested range.

​
has_more
boolean

Whether there are more records beyond this page. If true, use next_cursor to fetch the next page.

​
next_cursor
string

Cursor to pass as the cursor parameter for the next page. Only present when has_more is true.