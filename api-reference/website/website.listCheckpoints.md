Lists all checkpoints of a website, newest first. Match published_version_id against data[].version_id to identify the live checkpoint, or call website.publish to deploy the latest. See the Website guide.

GET
/
v2
/
website.listCheckpoints
Try it
Questions or issues? Contact us at api-support@manus.ai.

**Live version:** Match published_version_id against data[].version_id to find which row is currently deployed. Use website.publish to deploy the latest, or website.status to check deployment progress.
**Checkpoint status ≠ publish state:** The per-checkpoint status only reflects whether the snapshot was generated successfully — for deployment state, see website.status. See the Website guide.

#### Authorizations

x-manus-api-key

string

header

required

#### Query Parameters

task_id

string

Session UID. Mutually exclusive with `website_id` — exactly one must be provided. The session must contain exactly one website.

website_id

string

Unique website ID. Mutually exclusive with `task_id` — exactly one must be provided. Obtain from the response of `website.status` or `website.publish`.

#### Response

200

application/json

Checkpoints retrieved successfully.

ok

boolean

Whether the request was successful.

Example:

`true`

request_id

string

Unique identifier for this API request.

website_id

string

Unique website ID.

data

object[]

Checkpoints in reverse chronological order (newest first). Empty array if the site has no checkpoints yet.

Hide child attributes

data.version_id

string

Unique checkpoint version ID (the underlying git commit hash).

data.message

string

Checkpoint description — the commit message written when the checkpoint was saved.

data.status

enum<string>

Whether the checkpoint itself was generated successfully. This is independent of publish state — use published_version_id from website.listCheckpoints to identify the version currently live.

Available options: pending, success, failed, unspecified 

data.created_at

integer<int64>

Checkpoint creation time (Unix seconds).

published_version_id

string

Optional. version_id of the checkpoint currently published. Present only when the site has been published. Match against data[].version_id to find the live checkpoint.