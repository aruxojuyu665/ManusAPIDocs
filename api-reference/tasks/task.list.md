# task.list - Manus API

**URL:** https://open.manus.ai/docs/v2/task.list

---

Skip to main content
Manus API home page
Search...
⌘K
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
POST
task.create
GET
task.detail
GET
task.list
POST
task.update
POST
task.stop
POST
task.delete
POST
task.sendMessage
GET
task.listMessages
POST
task.confirmAction
Projects
Skills
Agents
Files
Webhooks
Usage
Connectors
Browser
Website
v2
Tasks
task.list
Copy page

Lists tasks with optional filtering and cursor-based pagination. Use scope to filter by task type, e.g. agent_subtask with agent_id for agent subtasks. See task.detail for full details on a specific task.

GET
/
v2
/
task.list
Try it
Questions or issues? Contact us at api-support@manus.ai.
Scope: Filter by task type — standard for regular tasks, project with project_id for project tasks, agent_subtask with agent_id for agent subtasks.
Shortcut: Use agent-default as agent_id for the IM agent. See the Agents guide.
Authorizations
​
x-manus-api-key
stringheaderrequired
Query Parameters
​
limit
integer

Number of tasks to return per page. Default: 20, Max: 100.

​
cursor
string

Pagination cursor from the previous response's next_cursor field. Omit for the first page.

​
order
enum<string>

Sort direction by creation time. "desc" (default) returns newest first, "asc" returns oldest first.

Available options: asc, desc 
​
scope
enum<string>

Filter by task type. "all" (default) returns all tasks. "standard" returns regular tasks. "project" returns tasks within a project (requires project_id). "agent_subtask" returns subtasks created by an agent (requires agent_id).

Available options: all, agent_subtask, project, standard 
​
agent_id
string

Filter tasks by agent. Required when scope="agent_subtask". Supports the shortcut agent-default for the IM agent. Use agent.list to get available agent IDs.

​
project_id
string

Filter tasks by project. Required when scope="project". Use project.list to get available project IDs.

Response
200
application/json

Tasks retrieved successfully.

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

Array of task objects matching the filter criteria.

Hide child attributes

​
data.id
string

Unique identifier for the task.

​
data.status
enum<string>

Current task status. "running" — agent is actively working. "stopped" — task has finished or been stopped. "waiting" — agent is paused and waiting for user input or confirmation. "error" — task encountered an unrecoverable error.

Available options: running, stopped, waiting, error 
​
data.created_at
integer<int64>

Unix timestamp (seconds) when the task was created.

​
data.updated_at
integer<int64>

Unix timestamp (seconds) when the task was last updated.

​
data.task_type
enum<string>

Type of the task. "standard" — a regular standalone task. "project" — a task within a project. "agent_subtask" — a subtask created by an agent. Use task.list with scope to filter by task type.

Available options: standard, project, agent_subtask 
​
data.share_visibility
enum<string>

Who can view the task. "private" — only the task creator. "team" — all team members. "public" — anyone with the share link.

Available options: private, team, public 
​
data.title
string

Title of the task.

​
data.credit_usage
integer<int32>

Total credits consumed by the task. Only present when the task has consumed credits.

​
data.task_url
string

URL to view the task in the Manus webapp (e.g., https://manus.im/app/{task_id}).

​
data.created_by_api_key
object

The API key that created this task. Present when the task was created via the API; null or absent when created through the UI or other means. The name reflects the API key's current name, not a snapshot from creation time.

Hide child attributes

​
data.created_by_api_key.id
string

The API key ID.

​
data.created_by_api_key.name
string

The current display name of the API key.

​
has_more
boolean

Whether there are more tasks beyond this page. If true, use next_cursor to fetch the next page.

​
next_cursor
string

Cursor to pass as the cursor parameter for the next page. Only present when has_more is true.