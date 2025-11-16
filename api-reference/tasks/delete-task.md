# Delete Task

> Deletes a task by ID.

## OpenAPI

````yaml DELETE /v1/tasks/{task_id}
paths:
  path: /v1/tasks/{task_id}
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
        task_id:
          schema:
            - type: string
              required: true
              description: The ID of the task to delete
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
                    description: The ID of the deleted task
              object:
                allOf:
                  - type: string
                    description: Always "task.deleted"
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
        description: Task deleted successfully.
  deprecated: false
  type: path
components:
  schemas: {}

````