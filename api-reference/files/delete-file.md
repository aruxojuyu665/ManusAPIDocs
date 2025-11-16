# Delete File

> Deletes a file by ID. This removes both the file record and the file from S3 storage.

## OpenAPI

````yaml DELETE /v1/files/{file_id}
paths:
  path: /v1/files/{file_id}
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
        file_id:
          schema:
            - type: string
              required: true
              description: The ID of the file to delete
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
                    description: The ID of the deleted file
              object:
                allOf:
                  - type: string
                    description: Always "file.deleted"
              deleted:
                allOf:
                  - type: boolean
                    description: Always true if successful
        examples:
          example:
            value:
              id: <string>
              object: <string>
              deleted: true
        description: File deleted successfully.
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