# connector.list



**Use in tasks:** Pass connector IDs in the `connectors` array of [task.create]() or [task.sendMessage]().**Setup:** See the [Connectors]() guide for authorization and configuration.

#### Authorizations

x-manus-api-key

string

header

required

#### Response

200

application/json

Connectors retrieved successfully.

ok

boolean

Whether the request was successful.

Example:

`true`

request\_id

string

Unique identifier for this API request.

data

object\[\]

Array of connectors installed in the user\'s account.

Hide child attributes

data.id

string

Unique identifier for the connector. Use this as the connector ID when creating tasks.

data.name

string

Display name of the connector.

data.type

enum<string>

Connector type. "builtin" — built-in connector provided by Manus. "byok" — bring-your-own-key connector. "mcp" — MCP (Model Context Protocol) connector.

Available options:

`builtin`,

`byok`,

`mcp`

data.description

string

Human-readable description of the connector\'s functionality.

data.category

string

Category grouping for the connector (e.g., "productivity", "communication").