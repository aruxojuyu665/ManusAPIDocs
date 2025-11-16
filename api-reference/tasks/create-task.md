# Create Task

> Creates a new task.

## OpenAPI

````yaml POST /v1/tasks
paths:
  path: /v1/tasks
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
              prompt:
                allOf:
                  - type: string
                    title: prompt
                    description: The task prompt or instruction for the Manus agent.
                    example: Write a function to calculate fibonacci numbers
              attachments:
                allOf:
                  - type: array
                    items:
                      oneOf:
                        - type: object
                          title: File ID Attachment
                          properties:
                            filename:
                              type: string
                              description: Name of the file attachment
                            file_id:
                              type: string
                              description: >-
                                ID of a previously uploaded file (via POST
                                /v1/files)
                          required:
                            - filename
                            - file_id
                        - type: object
                          title: URL Attachment
                          properties:
                            filename:
                              type: string
                              description: Name of the file attachment
                            url:
                              type: string
                              description: Publicly accessible URL to a file or image
                            mimeType:
                              type: string
                              description: MIME type of the file (optional)
                          required:
                            - filename
                            - url
                        - type: object
                          title: Base64 Data Attachment
                          properties:
                            filename:
                              type: string
                              description: Name of the file attachment
                            fileData:
                              type: string
                              description: >-
                                Base64 encoded file/image data in format:
                                'data:<mime_type>;base64,<encoded_content>'
                          required:
                            - filename
                            - fileData
                    title: attachments
                    description: >-
                      Array of file/image attachments. No distinction between
                      files and images - both are treated the same way.
              taskMode:
                allOf:
                  - type: string
                    enum:
                      - chat
                      - adaptive
                      - agent
                    title: task_mode
                    description: chat, adaptive or agent
              connectors:
                allOf:
                  - type: array
                    items:
                      type: string
                    title: connectors
                    description: >-
                      List of connector IDs to enable for this task. Only
                      connectors already configured in the user's account can be
                      used.
              hideInTaskList:
                allOf:
                  - type: boolean
                    title: hide_in_task_list
                    description: >-
                      Whether to hide this task from the Manus webapp task list.
                      The task will still be accessible via the provided link.
              createShareableLink:
                allOf:
                  - type: boolean
                    title: create_shareable_link
                    description: >-
                      Whether to make the chat publicly accessible to others on
                      the Manus website.
              taskId:
                allOf:
                  - type: string
                    title: task_id
                    description: For continuing existing tasks (multi-turn)
              agentProfile:
                allOf:
                  - type: string
                    enum:
                      - manus-1.5
                      - manus-1.5-lite
                      - speed
                      - quality
                    title: agent_profile
                    description: >-
                      manus-1.5, manus-1.5-lite, speed (deprecated, use
                      manus-1.5-lite), or quality (deprecated, use manus-1.5)
                    default: manus-1.5
              locale:
                allOf:
                  - type: string
                    title: locale
                    description: >-
                      Your default locale that you've set on Manus (e.g.,
                      "en-US", "zh-CN")
            required: true
            requiredProperties:
              - prompt
              - agentProfile
            additionalProperties: false
            example:
              prompt: Write a function to calculate fibonacci numbers
              agentProfile: manus-1.5
        examples:
          example:
            value:
              prompt: Write a function to calculate fibonacci numbers
              agentProfile: manus-1.5
  response:
    '200':
      application/json:
        schemaArray:
          - type: object
            properties:
              task_id:
                allOf:
                  - type: string
                    title: task_id
              task_title:
                allOf:
                  - type: string
                    title: task_title
              task_url:
                allOf:
                  - type: string
                    title: task_url
              share_url:
                allOf:
                  - type: string
                    title: share_url
                    description: >-
                      Optional publicly accessible link to the chat. Only
                      present if create_shareable_link was set to true.
            additionalProperties: false
        examples:
          example:
            value:
              task_id: <string>
              task_title: <string>
              task_url: <string>
              share_url: <string>
        description: Task created successfully.
  deprecated: false
  type: path
components:
  schemas: {}

````