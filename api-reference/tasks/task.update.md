# task.update - Manus API



#### Authorizations

x-manus-api-key

string

header

required

#### Body

application/json

task\_id

string

required

The unique identifier of the task to update. Supports the shortcut `agent-default-main_task` for the IM agent\'s main task.

title

string

New title for the task. Replaces the auto-generated title.

share\_visibility

enum<string>

Controls who can view the task. "private" — only the task creator can view. "team" — all team members can view. "public" — anyone with the share\_url can view.

Available options:

`private`,

`team`,

`public`

enable\_visible\_in\_task\_list

boolean

When true, the task appears in the Manus webapp task list. When false, hides the task from the list (still accessible via direct URL).

#### Response

200

application/json

Task updated successfully.

ok

boolean

Whether the request was successful.

Example:

`true`

request\_id

string

Unique identifier for this API request.

task\_id

string

The ID of the updated task.

task\_title

string

The current title of the task.

task\_url

string

URL to view the task in the Manus webapp.

share\_url

string

Public share URL. Only present when share\_visibility is not "private".

share\_visibility

enum<string>

The actual visibility state of the task.

Available options:

`private`,

`team`,

`public`