# file.delete - Manus API

**URL:** https://open.manus.ai/docs/v2/file.delete

---

Deletes a file. Files are automatically deleted 48 hours after upload, so manual deletion is only needed for early cleanup.

POST /v2/file.delete

Questions or issues? Contact us at api-support@manus.ai.

#### Authorizations

x-manus-api-key

string

header

required

#### Body

application/json

file_id

string

required

The unique identifier of the file to delete.

#### Response

200

application/json

File deleted successfully.

ok

boolean

Whether the request was successful.

Example:

`true`

request_id

string

Unique identifier for this API request.

#### Code Example

##### cURL

```bash
curl --request POST \
  --url https://api.manus.ai/v2/file.delete \
  --header 'Content-Type: application/json' \
  --header 'x-manus-api-key: <api-key>' \
  --data '
{
  "file_id": "<string>"
}
'
```

##### 200 Response Example

```json
{
  "ok": true,
  "request_id": "<string>"
}
```