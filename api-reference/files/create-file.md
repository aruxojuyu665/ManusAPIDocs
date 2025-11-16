# Create File

> Creates a file record and returns a presigned URL for uploading the file content to S3.

## OpenAPI

````yaml POST /v1/files
paths:
  path: /v1/files
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
              filename:
                allOf:
                  - type: string
                    description: Name of the file to upload
            required: true
            requiredProperties:
              - filename
        examples:
          example:
            value:
              filename: <string>
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
                    description: Initial status is "pending"
              upload_url:
                allOf:
                  - type: string
                    description: >-
                      Presigned S3 URL for uploading the file content (PUT
                      request)
              upload_expires_at:
                allOf:
                  - type: string
                    format: date-time
                    description: ISO 8601 timestamp when the upload URL expires
              created_at:
                allOf:
                  - type: string
                    format: date-time
                    description: ISO 8601 timestamp when the file record was created
            refIdentifier: '#/components/schemas/FileCreate'
        examples:
          example:
            value:
              id: <string>
              object: <string>
              filename: <string>
              status: <string>
              upload_url: <string>
              upload_expires_at: '2023-11-07T05:31:56Z'
              created_at: '2023-11-07T05:31:56Z'
        description: File record created successfully.
  deprecated: false
  type: path
components:
  schemas: {}

````