# List Files

> Retrieves a list of the 10 most recently uploaded files.

## OpenAPI

````yaml GET /v1/files
paths:
  path: /v1/files
  method: get
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
    body: {}
  response:
    '200':
      application/json:
        schemaArray:
          - type: object
            properties:
              object:
                allOf:
                  - type: string
                    description: Always "list"
              data:
                allOf:
                  - type: array
                    items:
                      $ref: '#/components/schemas/File'
                    description: Array of file objects (max 10)
        examples:
          example:
            value:
              object: <string>
              data:
                - id: <string>
                  object: <string>
                  filename: <string>
                  status: pending
                  created_at: '2023-11-07T05:31:56Z'
        description: Files retrieved successfully.
  deprecated: false
  type: path
components:
  schemas:
    File:
      type: object
      properties:
        id:
          type: string
          description: Unique identifier for the file
        object:
          type: string
          description: Always "file"
        filename:
          type: string
          description: Name of the file
        status:
          type: string
          enum:
            - pending
            - uploaded
            - deleted
          description: Current status of the file
        created_at:
          type: string
          format: date-time
          description: ISO 8601 timestamp when the file was created

````