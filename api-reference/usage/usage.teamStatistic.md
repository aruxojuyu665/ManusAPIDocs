# usage.teamStatistic



**Team only:** This endpoint is only available to team users. Individual users will receive a `permission_denied` error.

**Visibility:** Owner / Super Admin / Admin sees the entire team’s daily consumption totals. Member sees only their own daily consumption.

#### Authorizations

x-manus-api-key

string

header

required

#### Query Parameters

start\_date

integer

Filter start time as a Unix timestamp in seconds.

end\_date

integer

Filter end time as a Unix timestamp in seconds.

#### Response

200

application/json

Daily usage statistics retrieved successfully.

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

Array of daily statistics sorted by date in ascending order.

Hide child attributes

data.date

integer

Date as a Unix timestamp in seconds, representing 00:00:00 of that day.

data.credits

integer

Total credits consumed on this day.