# Get Tasks

> Retrieves a list of tasks with optional filtering and pagination.

## OpenAPI

````yaml GET /v1/tasks
paths:
  path: /v1/tasks
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
      query:
        after:
          schema:
            - type: string
              description: >-
                Cursor for pagination. ID of the last task from the previous
                page.
        limit:
          schema:
            - type: integer
              description: 'Maximum number of tasks to return. Default: 100, Range: 1-1000.'
        order:
          schema:
            - type: string
              description: 'Sort direction: "asc" or "desc". Default: "desc".'
        orderBy:
          schema:
            - type: string
              description: 'Sort field: "created_at" or "updated_at". Default: "created_at".'
        query:
          schema:
            - type: string
              description: Search term to filter by title and body content.
        status:
          schema:
            - type: array
              items:
                allOf:
                  - type: string
              description: >-
                Filter by task status: "pending", "running", "completed",
                "failed".
        createdAfter:
          schema:
            - type: integer
              description: Filter tasks created after this Unix timestamp (seconds).
        createdBefore:
          schema:
            - type: integer
              description: Filter tasks created before this Unix timestamp (seconds).
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
                      $ref: '#/components/schemas/Task'
              first_id:
                allOf:
                  - type: string
                    description: ID of the first task in the list
              last_id:
                allOf:
                  - type: string
                    description: >-
                      ID of the last task in the list (use as 'after' for next
                      page)
              has_more:
                allOf:
                  - type: boolean
                    description: Whether there are more tasks available
        examples:
          example:
            value:
              object: <string>
              data:
                - id: <string>
                  object: <string>
                  created_at: 123
                  updated_at: 123
                  status: pending
                  error: <string>
                  incomplete_details: <string>
                  instructions: <string>
                  max_output_tokens: 123
                  model: <string>
                  metadata: {}
                  output:
                    - id: <string>
                      status: <string>
                      role: user
                      type: <string>
                      content:
                        - type: output_text
                          text: <string>
                          fileUrl: <string>
                          fileName: <string>
                          mimeType: <string>
                  locale: <string>
                  credit_usage: 123
              first_id: <string>
              last_id: <string>
              has_more: true
        description: Tasks retrieved successfully.
  deprecated: false
  type: path
components:
  schemas:
    Task:
      type: object
      properties:
        id:
          type: string
          description: Unique identifier for the task
        object:
          type: string
          description: Always "task"
        created_at:
          type: integer
          format: int64
          description: Unix timestamp (seconds) when the task was created
        updated_at:
          type: integer
          format: int64
          description: Unix timestamp (seconds) when the task was last updated
        status:
          type: string
          enum:
            - pending
            - running
            - completed
            - failed
          description: Current status of the task
        error:
          type: string
          description: Error message if the task failed (optional)
        incomplete_details:
          type: string
          description: Details about why the task is incomplete (optional)
        instructions:
          type: string
          description: The original prompt/instructions for the task (optional)
        max_output_tokens:
          type: integer
          format: int32
          description: Maximum output tokens limit (optional)
        model:
          type: string
          description: Model used for the task
        metadata:
          type: object
          additionalProperties:
            type: string
          description: Custom metadata key-value pairs
        output:
          type: array
          items:
            $ref: '#/components/schemas/TaskMessage'
          description: Array of task messages (conversation history)
        locale:
          type: string
          description: User's preferred locale (optional)
        credit_usage:
          type: integer
          format: int32
          description: Credits consumed by this task (optional)
    TaskMessage:
      type: object
      properties:
        id:
          type: string
          description: Unique identifier for the message
        status:
          type: string
          description: Status of the message
        role:
          type: string
          enum:
            - user
            - assistant
          description: Role of the message sender - "assistant" or "user"
        type:
          type: string
          description: Type here is "message"
        content:
          type: array
          items:
            $ref: '#/components/schemas/MessageContent'
          description: Array of message content items (text or files)
    MessageContent:
      type: object
      properties:
        type:
          type: string
          enum:
            - output_text
            - output_file
          description: Content type - "output_text" or "output_file"
        text:
          type: string
          description: Text content (for output_text type)
        fileUrl:
          type: string
          description: File URL (for output_file type)
        fileName:
          type: string
          description: File name (for output_file type)
        mimeType:
          type: string
          description: MIME type of the file (for output_file type)

````