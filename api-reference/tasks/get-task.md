# Get Task

> Retrieves details of a specific task by ID.

## OpenAPI

````yaml GET /v1/tasks/{task_id}
paths:
  path: /v1/tasks/{task_id}
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
        task_id:
          schema:
            - type: string
              required: true
              description: The ID of the task to retrieve
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
                    description: Unique identifier for the task
              object:
                allOf:
                  - type: string
                    description: Always "task"
              created_at:
                allOf:
                  - type: integer
                    format: int64
                    description: Unix timestamp (seconds) when the task was created
              updated_at:
                allOf:
                  - type: integer
                    format: int64
                    description: Unix timestamp (seconds) when the task was last updated
              status:
                allOf:
                  - type: string
                    enum:
                      - pending
                      - running
                      - completed
                      - failed
                    description: Current status of the task
              error:
                allOf:
                  - type: string
                    description: Error message if the task failed (optional)
              incomplete_details:
                allOf:
                  - type: string
                    description: Details about why the task is incomplete (optional)
              instructions:
                allOf:
                  - type: string
                    description: The original prompt/instructions for the task (optional)
              max_output_tokens:
                allOf:
                  - type: integer
                    format: int32
                    description: Maximum output tokens limit (optional)
              model:
                allOf:
                  - type: string
                    description: Model used for the task
              metadata:
                allOf:
                  - type: object
                    additionalProperties:
                      type: string
                    description: Custom metadata key-value pairs
              output:
                allOf:
                  - type: array
                    items:
                      $ref: '#/components/schemas/TaskMessage'
                    description: Array of task messages (conversation history)
              locale:
                allOf:
                  - type: string
                    description: User's preferred locale (optional)
              credit_usage:
                allOf:
                  - type: integer
                    format: int32
                    description: Credits consumed by this task (optional)
            refIdentifier: '#/components/schemas/Task'
        examples:
          example:
            value:
              id: <string>
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
        description: Task retrieved successfully.
  deprecated: false
  type: path
components:
  schemas:
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