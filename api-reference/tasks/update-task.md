# Update Task

> Updates a task's metadata.

## OpenAPI

````yaml PUT /v1/tasks/{task_id}
paths:
  path: /v1/tasks/{task_id}
  method: put
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
        task_id:
          schema:
            - type: string
              required: true
              description: The ID of the task to update
      query: {}
      header: {}
      cookie: {}
    body:
      application/json:
        schemaArray:
          - type: object
            properties:
              title:
                allOf:
                  - type: string
                    description: New title for the task
              enableShared:
                allOf:
                  - type: boolean
                    description: Whether to enable public sharing
              enableVisibleInTaskList:
                allOf:
                  - type: boolean
                    description: Whether the task should be visible in the task list
            required: true
            additionalProperties: false
        examples:
          example:
            value:
              title: <string>
              enableShared: true
              enableVisibleInTaskList: true
  response:
    '200':
      application/json:
        schemaArray:
          - type: object
            properties:
              task_id:
                allOf:
                  - type: string
              task_title:
                allOf:
                  - type: string
              task_url:
                allOf:
                  - type: string
              share_url:
                allOf:
                  - type: string
                    description: Public share URL if sharing is enabled
        examples:
          example:
            value:
              task_id: <string>
              task_title: <string>
              task_url: <string>
              share_url: <string>
        description: Task updated successfully.
  deprecated: false
  type: path
components:
  schemas: {}

````