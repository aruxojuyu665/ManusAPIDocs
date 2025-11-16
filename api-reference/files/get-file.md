# Get File

> Retrieves details of a specific file by ID.

## OpenAPI

````yaml GET /v1/files/{file_id}
paths:
  path: /v1/files/{file_id}
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
      path:
        file_id:
          schema:
            - type: string
              required: true
              description: The ID of the file to retrieve
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
              id:
                allOf:
                  - type: string
                    description: Unique identifier for the file
              object:
                allOf:
                  - type: string
                    description: Always "file"
              filename:
                allOf:
                  - type: string
                    description: Name of the file
              status:
                allOf:
                  - type: string
                    enum:
                      - pending
                      - uploaded
                      - deleted
                    description: Current status of the file
              created_at:
                allOf:
                  - type: string
                    format: date-time
                    description: ISO 8601 timestamp when the file was created
            refIdentifier: '#/components/schemas/File'
        examples:
          example:
            value:
              id: <string>
              object: <string>
              filename: <string>
              status: pending
              created_at: '2023-11-07T05:31:56Z'
        description: File retrieved successfully.
    '404':
      application/json:
        schemaArray:
          - type: object
            properties:
              code:
                allOf:
                  - type: integer
                    example: 5
              message:
                allOf:
                  - type: string
                    example: file not found or has been deleted
              details:
                allOf:
                  - type: array
                    items: {}
                    example: []
        examples:
          example:
            value:
              code: 5
              message: file not found or has been deleted
              details: []
        description: File not found or has been deleted.
  deprecated: false
  type: path
components:
  schemas: {}

````