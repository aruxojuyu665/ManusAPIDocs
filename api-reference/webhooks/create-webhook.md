# Create Webhook

> Creates a new webhook.

## OpenAPI

````yaml POST /v1/webhooks
paths:
  path: /v1/webhooks
  method: post
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
      path: {}
      query: {}
      header: {}
      cookie: {}
    body:
      application/json:
        schemaArray:
          - type: object
            properties:
              webhook:
                allOf:
                  - type: object
                    properties:
                      url:
                        type: string
                    required:
                      - url
            required: true
            requiredProperties:
              - webhook
        examples:
          example:
            value:
              webhook:
                url: <string>
  response:
    '200':
      application/json:
        schemaArray:
          - type: object
            properties:
              webhook_id:
                allOf:
                  - type: string
        examples:
          example:
            value:
              webhook_id: <string>
        description: Webhook created successfully.
  deprecated: false
  type: path
components:
  schemas: {}

````