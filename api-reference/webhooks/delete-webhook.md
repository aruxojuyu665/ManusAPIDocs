# Delete Webhook

> Deletes a webhook.

## OpenAPI

````yaml DELETE /v1/webhooks/{webhook_id}
paths:
  path: /v1/webhooks/{webhook_id}
  method: delete
  servers:
    - url: https://api.manus.ai
  request:
    security:
      - title: bearerAuth
        parameters:
          query: {}
          header:
            API_KEY:
              type: apiKey
          cookie: {}
    parameters:
      path:
        webhook_id:
          schema:
            - type: string
              required: true
      query: {}
      header: {}
      cookie: {}
    body: {}
  response:
    '204':
      _mintlify/placeholder:
        schemaArray:
          - type: any
            description: Webhook deleted successfully.
        examples: {}
        description: Webhook deleted successfully.
  deprecated: false
  type: path
components:
  schemas: {}

````