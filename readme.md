
# WebSocket API Documentation

This document provides details on how to use the WebSocket API, including how to establish a connection, available events, and the flow for interacting with the API.

## WebSocket API Base URL

- **WebSocket API URL/ SocketOrigin**: 
  `wss://vqywy57hqe.execute-api.ap-southeast-1.amazonaws.com/uat`

---

## Prerequisites

Before connecting to the WebSocket API, ensure you have the following:

1. **Access Token**: A valid `accessToken` is required for authentication. You can retrieve this token from your authentication service.
2. **Device ID**: A unique identifier for the device or client connecting to the WebSocket API.

---

## How to Connect to the WebSocket API

To connect to the WebSocket API, the following URL needs to be called:

`{{socketOrigin}}?Auth={{accessToken}}&deviceId=123-postman-321`

### Parameters:

- `Auth`: The `accessToken` that authorizes the connection.
- `deviceId`: A unique identifier for the device making the connection (e.g., "123-postman-321").

### Example

Here’s an example connection URL:

wss://vqywy57hqe.execute-api.ap-southeast-1.amazonaws.com/uat?Auth=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...&deviceId=123-postman-321

To establish a connection, use a WebSocket client (e.g., Postman, a browser, or a Node.js client).

### Connection Steps:

1. **Establish the WebSocket Connection**:
   - The first step is to establish a WebSocket connection using the URL provided above. 
   - Replace `{{accessToken}}` with your actual access token and `{{deviceId}}` with your device identifier.
   
2. **Receive Connection Acknowledgment**:
   - Upon successful connection, you should receive an acknowledgment message from the server confirming that the connection is active.

---

## Available WebSocket Events to Call 

### 1. Init Chat With Concierge

- **Description**: Initializes a chat session with a concierge. This API creates a new chat session and returns details such as the `chatSessionId`, connection details, and tenant profile information.

#### Request Payload:

```json
{
    "action": "api",
    "data": {
        "route": "client/init-chat-with-concierge",
        "body": {
            "newSession": true
        }
    }
}
```

#### Response:

```json
{
    "channel": "client/init-chat-with-concierge",
    "status": 200,
    "body": {
        "chatSessionId": "4482e256-da14-47cc-b119-9575bbb3b6d3",
        "chatSession": {
            "id": "100",
            "orgId": "367",
            "chatSessionId": "4482e256-da14-47cc-b119-9575bbb3b6d3",
            "chatInitiatedByEntityType": "TENANT",
            "chatInitiatedByEntityId": "34",
            "lastPingedByChatInitiator": "1727939180543",
            "chatJoinedByEntityType": null,
            "chatJoinedByEntityId": null,
            "lastPingedByChatJoiner": null,
            "isSessionClosed": false
        },
        "connection": {
            "id": "2260",
            "connectionId": "fD9QxcHGSQ0CF1w=",
            "entityType": "TENANT",
            "entityId": "34",
            "deviceId": "123-postman-321",
            "expiredAt": "1727942779137",
            "createdAt": "1727938788101",
            "updatedAt": "1727939179137",
            "orgId": "367"
        },
        "tenant": {
            "id": "34",
            "email": "deepak@tis.co.th",
            "countryId": "99",
            "code": "+66",
            "phoneNumber": "09928640281",
            "residentProfile": {
                "firstName": "Deepak",
                "lastName": "Pandey",
                "gender": "M",
                "idcard": "UP-324234",
                "passport": "ZXT230540-2",
                "note": null,
                "cardNumber": "3248722389237",
                "isActive": true,
                "emails": [
                    {
                        "email": "deepakpandeygonda@gmail.com",
                        "isActive": true
                    },
                    {
                        "email": "deepakpandey.tis@gmail.com",
                        "isActive": true
                    }
                ],
                "phones": [
                    {
                        "countryCode": "+91",
                        "phoneNumber": "7007353725",
                        "isActive": true
                    }
                ]
            },
            "propertyOwnerProfile": {
                "firstName": "Deepak",
                "lastName": "Pandey",
                "isActive": true
            },
            "properties": [
                {
                    "propertyUnitId": "5",
                    "unitNumber": "3/0008",
                    "houseNumber": "3/0008",
                    "thirdPartyIntegration": {
                        "homeId": "66bdc54b12dcd64e310d93bd"
                    },
                    "floors": [
                        {
                            "floorZoneCode": "FL3",
                            "floorId": 7,
                            "floorDescription": "Third Floor"
                        }
                    ],
                    "buildingPhaseCode": "OB1",
                    "buildingId": "1",
                    "buildingPhaseName": "OB1",
                    "projectCode": "C3A",
                    "projectId": "3",
                    "projectsName": "ONE89 wireless",
                    "projectsNameThai": "วันเอทตี้ไนน์ ไวร์เลส",
                    "hideLogoFromFrontEnd": false,
                    "companyName": "One Bangkok",
                    "isPropertyOwner": true,
                    "isPropertyResident": false,
                    "isDefaultPropertyUnit": false,
                    "backgroundUrl": "https://obk-servicemind-uat-resources.s3.ap-southeast-1.amazonaws.com/project_background/e7f2d79f-0991-46bf-a7dd-ed3ef9ed7977.png",
                    "iconUrl": "https://obk-servicemind-uat-resources.s3.ap-southeast-1.amazonaws.com/project_logo/17292844-6144-4307-8912-c1c66dd641f5.png"
                }
            ]
        }
    }
}
```


---

### 2. Continue Previous Chat Session

#### Step 1: Check if Chat Session is Not Closed (Get Chat Session)

Request Payload:
```json
{
    "action": "api",
    "data": {
        "route": "client/get-chat-session",
        "body": {
            "chatSessionId": "4482e256-da14-47cc-b119-9575bbb3b6d3"
        }
    }
}
```

Response:
```json
{
    "channel": "client/get-chat-session",
    "status": 200,
    "body": {
        "chatSessionId": "4482e256-da14-47cc-b119-9575bbb3b6d3",
        "chatSession": {
            "id": "100",
            "orgId": "367",
            "chatSessionId": "4482e256-da14-47cc-b119-9575bbb3b6d3",
            "chatInitiatedByEntityType": "TENANT",
            "chatInitiatedByEntityId": "34",
            "lastPingedByChatInitiator": "1727940143164",
            "chatJoinedByEntityType": null,
            "chatJoinedByEntityId": null,
            "lastPingedByChatJoiner": null,
            "isSessionClosed": false
        },
        "connection": {
            "id": "2262",
            "connectionId": "fD_nMeRhyQ0CEqg=",
            "entityType": "TENANT",
            "entityId": "34",
            "deviceId": "123-postman-321",
            "expiredAt": "1727943741791",
            "createdAt": "1727940141791",
            "updatedAt": "1727940141791",
            "orgId": "367"
        },
        "tenant": {
            "id": "34",
            "email": "deepak@tis.co.th",
            "countryId": "99",
            "code": "+66",
            "phoneNumber": "09928640281"
        }
    }
}
```

####  Step 2: If Session not closed, Continue with Old Chat Session

Request Payload:
```json
{
    "action": "api",
    "data": {
        "route": "client/init-chat-with-concierge",
        "body": {
            "newSession": false,
            "chatSessionId": "4482e256-da14-47cc-b119-9575bbb3b6d3"
        }
    }
}
```

Response:
```json
{
    "channel": "client/init-chat-with-concierge",
    "status": 200,
    "body": {
        "chatSessionId": "4482e256-da14-47cc-b119-9575bbb3b6d3",
        "chatSession": {
            "id": "100",
            "orgId": "367",
            "chatSessionId": "4482e256-da14-47cc-b119-9575bbb3b6d3",
            "chatInitiatedByEntityType": "TENANT",
            "chatInitiatedByEntityId": "34",
            "lastPingedByChatInitiator": "1727940144304",
            "chatJoinedByEntityType": "BACKEND_USER",
            "chatJoinedByEntityId": "32314",
            "lastPingedByChatJoiner": "1727940474801",
            "isSessionClosed": false
        },
        "connection": {
            "id": "2262",
            "connectionId": "fEBAifRtyQ0CEMg=",
            "entityType": "TENANT",
            "entityId": "34",
            "deviceId": "123-postman-321",
            "expiredAt": "1727944313567",
            "createdAt": "1727940141791",
            "updatedAt": "1727940713567",
            "orgId": "367"
        },
        "tenant": {
            "id": "34",
            "email": "deepak@tis.co.th",
            "countryId": "99",
            "code": "+66",
            "phoneNumber": "09928640281"
        }
    }
}
```

---

### 3. Get All Chat Messages (Tenant and Concierge)

- **Description**: Retrieves all chat messages between the tenant and the concierge for a specific chat session. The messages are returned in a paginated format based on the `page` and `limit` parameters.

#### Request Payload:

```json
{
    "action": "api",
    "data": {
        "route": "client/get-chat-messages?page=1&limit=50",
        "body": {
            "chatSessionId": "4482e256-da14-47cc-b119-9575bbb3b6d3"
        }
    }
}
```

Response:
```json
{
    "channel": "client/get-chat-messages?page=1&limit=20",
    "status": 200,
    "body": {
        "messages": [
            {
                "id": "1",
                "orgId": "367",
                "chatSessionId": "2d58d310-4614-4a0d-b84e-fc0a371ce647",
                "senderEntityType": "BACKEND_USER",
                "senderEntityId": "32314",
                "messageContent": "hello",
                "sentAt": "1727359984643",
                "status": 3,
                "seenAt": null,
                "deliveredAt": "1727359984643",
                "contentType": "TEXT",
                "metadata": null
            },
            {
                "id": "2",
                "orgId": "367",
                "chatSessionId": "2d58d310-4614-4a0d-b84e-fc0a371ce647",
                "senderEntityType": "TENANT",
                "senderEntityId": "34",
                "messageContent": "hi there",
                "sentAt": "1727359993636",
                "status": 3,
                "seenAt": null,
                "deliveredAt": "1727359993636",
                "contentType": "TEXT",
                "metadata": null
            }
        ],
        "paginate": {
            "per_page": 20,
            "offset": 0,
            "page": 1
        }
    }
}
```


---

### 4. Ping Chat Session

- **Description**: This API is used to keep the chat session active. If the user is actively using the chat page, the frontend app should call this API every 30 seconds to ensure the chat session stays alive.

#### Request Payload:

```json
{
    "action": "api",
    "data": {
        "route": "client/ping-on-chat-session",
        "body": {
            "chatSessionId": "4482e256-da14-47cc-b119-9575bbb3b6d3"
        }
    }
}
```

Response:
```json
{
    "channel": "client/ping-on-chat-session",
    "status": 200,
    "body": {
        "chatSessionId": "4482e256-da14-47cc-b119-9575bbb3b6d3",
        "chatSession": {
            "id": "100",
            "orgId": "367",
            "chatSessionId": "4482e256-da14-47cc-b119-9575bbb3b6d3",
            "chatInitiatedByEntityType": "TENANT",
            "chatInitiatedByEntityId": "34",
            "lastPingedByChatInitiator": "1727941854419",
            "chatJoinedByEntityType": "BACKEND_USER",
            "chatJoinedByEntityId": "32314",
            "lastPingedByChatJoiner": "1727940474801",
            "isSessionClosed": false
        },
        "connection": {
            "id": "2269",
            "connectionId": "fEDwdfYYSQ0AbsQ=",
            "entityType": "TENANT",
            "entityId": "34",
            "deviceId": "123-postman-321",
            "expiredAt": "1727945439544",
            "createdAt": "1727941839544",
            "updatedAt": "1727941839544",
            "orgId": "367"
        },
        "tenant": {
            "id": "34",
            "email": "deepak@tis.co.th",
            "countryId": "99",
            "code": "+66",
            "phoneNumber": "09928640281"
        }
    }
}
```

---

### 5. Send Message

- **Description**: This API allows the user to send a message in an active chat session. The message can be of various content types, such as `TEXT`, `FILE`, or `IMAGE`.

#### Request Payload:

```json
{
    "action": "api",
    "data": {
        "route": "client/send-message",
        "body": {
           "chatSessionId": "4482e256-da14-47cc-b119-9575bbb3b6d3",
           "contentType": "TEXT",      // Can be TEXT, FILE, or IMAGE
           "messageContent": "whatever messages needs to be sent",
           "metdata": {
              "any_non_mandatory_key": "any_value"
            }
        }
    }
}
```

Response:
```json
{
    "channel": "client/send-message",
    "status": 200,
    "body": {
        "chatSessionId": "4482e256-da14-47cc-b119-9575bbb3b6d3",
        "chatMessage": {
            "id": "133",
            "orgId": "367",
            "chatSessionId": "4482e256-da14-47cc-b119-9575bbb3b6d3",
            "senderEntityType": "TENANT",
            "senderEntityId": "34",
            "messageContent": "whatever messages needs to be sent",
            "sentAt": "1727942303646",
            "status": 3,
            "seenAt": null,
            "deliveredAt": "1727942303646",
            "contentType": "TEXT",
            "metdata": {
              "any_non_mandatory_key": "any_value"
            }
        }
    }
}
```

### 5b. Send Message with Image/File Payload


- **Description**: This API generates a pre-signed URL for uploading chat images to the server. The response provides the URL to upload the image and the public URL to access the image once it has been uploaded.

#### Request

- **URL**: `{{serverUrl}}/file-new/get-upload-url`
- **Method**: `POST`
- **Content-Type**: `application/json`

#### Request Payload:

```json
{
    "filename": "512x512.png",
    "mimeType": "image/png",
    "type": "chat-images"
}
```

#### Response:

```json
{
    "data": {
        "uploadUrlData": {
            "uploadURL": "https://obk-servicemind-uat-resources.s3.ap-southeast-1.amazonaws.com/chat-images/d9bcf98b-063f-4286-ae70-8862dc7ebc1d.png?Content-Type=image%2Fpng&...",
            "fileName": "512x512.png",
            "uploadPath": "/chat-images/d9bcf98b-063f-4286-ae70-8862dc7ebc1d.png",
            "resourceUrl": "https://obk-servicemind-uat-resources.s3.ap-southeast-1.amazonaws.com/chat-images/d9bcf98b-063f-4286-ae70-8862dc7ebc1d.png"
        }
    },
    "message": "Upload Url generated successfully!"
}
```

- **Response Fields**:
  - `uploadURL`: The pre-signed URL to upload the image to the server.
  - `fileName`: The name of the file to be uploaded.
  - `uploadPath`: The path where the file will be stored on the server.
  - `resourceUrl`: The public URL to access the image once uploaded.

#### Next Step:

- **Upload the Image**: 
  After receiving the `uploadURL` from the above response, a `PUT` request should be made to upload the image to this URL. If the upload is successful, you will receive a status code `200`.

- **Call Send Message API**: 
  We can call send message API, with `contentType`: `FILE` or `IMAGE` .  And in `messageContent` we can pass `resourceUrl`

---

### 6. UnSent Message

- **Description**: This API allows the user to unsent a previously sent message within a chat session. The deletion is based on the `chatSessionId` and the message ID.

#### Request Payload:

```json
{
    "action": "api",
    "data": {
        "route": "client/delete-message",
        "body": {
            "chatSessionId": "4482e256-da14-47cc-b119-9575bbb3b6d3",
            "messageId": 133
        }
    }
}
```

Response:
```json
{
    "channel": "client/delete-message",
    "status": 200,
    "body": {
        "messageId": 133
    }
}
```

---

### 7. Mark Message As seen

- **Description**: This API allows the tenant to mark any message as seen which has been sent by 'BACKEND_USER'.  Once the message is visible in viewport, app should call this api with latest `chatSessionId` and `messageId`

#### Request Payload:

```json
{
    "action": "api",
    "data": {
        "route": "client/update-message-seen-at",
        "body": {
            "messageId": 133,
            "chatSessionId": "4482e256-da14-47cc-b119-9575bbb3b6d3"
        }
    }
}
```

Response:
```json
{
    "channel": "client/update-message-seen-at",
    "status": 200,
    "body": {
        "chatSessionId": "35b4f23f-1cf7-4a8a-809f-7e20e8404ba8",
        "chatMessage": {
            "id": "268",
            "orgId": "367",
            "chatSessionId": "35b4f23f-1cf7-4a8a-809f-7e20e8404ba8",
            "senderEntityType": "BACKEND_USER",
            "senderEntityId": "32314",
            "messageContent": "zXzX",
            "sentAt": "1728290170951",
            "status": 4,
            "seenAt": "1728290232663",
            "deliveredAt": "1728290170951",
            "contentType": "TEXT",
            "metadata": null
        }
    }
}
```

---

### 8. Get Unread Message Count

- **Description**: This API get the total unread messages count for chat for tenant who has connected to the socket.

#### Request Payload:

```json
{
    "action": "api",
    "data": {
        "route": "client/get-unread-msg-count",
        "body": {
        }
    }
}
```

Response:
```json
{
    "channel": "client/get-unread-msg-count",
    "status": 200,
    "body": {
        "unreadMsgCount": "0"
    }
}
```

---

### 9. End Chat Session

- **Description**: This API is used to end an active chat session between the tenant and the concierge. Once the session is closed, it cannot be reopened, and a new session must be started for further communication.

#### Request Payload:

```json
{
    "action": "api",
    "data": {
        "route": "client/end-chat-with-concierge",
        "body": {
            "chatSessionId": "4482e256-da14-47cc-b119-9575bbb3b6d3"
        }
    }
}
```

Response:
```json
{
    "channel": "client/end-chat-with-concierge",
    "status": 200,
    "body": {
        "chatSessionId": "4482e256-da14-47cc-b119-9575bbb3b6d3",
        "chatSession": {
            "id": "100",
            "orgId": "367",
            "chatSessionId": "4482e256-da14-47cc-b119-9575bbb3b6d3",
            "chatInitiatedByEntityType": "TENANT",
            "chatInitiatedByEntityId": "34",
            "lastPingedByChatInitiator": "1727942303646",
            "chatJoinedByEntityType": "BACKEND_USER",
            "chatJoinedByEntityId": "32314",
            "lastPingedByChatJoiner": "1727940474801",
            "isSessionClosed": true
        }
    }
}
```

---

## Available WebSocket Events for Subscription 

After establishing a connection with the socket, the following events can be listened to for receiving updates on chat sessions and messages.

### Event: `chat-session-update-${chatSessionId}`

Triggered when there is an update in a chat session. The payload provides data about the chat session state and participant details.

#### Payload Structure
```typescript
payload.chatSession : ChatSessionDataType

interface ChatSessionDataType {
    id: number,
    chatInitiatedByEntityId: number,
    chatInitiatedByEntityType: 'TENANT' | 'BACKEND_USER',
    chatJoinedByEntityId: number,
    chatJoinedByEntityType: 'TENANT' | 'BACKEND_USER',
    chatSessionId: string,
    isSessionClosed: boolean,
    lastPingedByChatInitiator: number,
    lastPingedByChatJoiner: number,
    orgId: number
}
```

| Field                   | Type                        | Description                                              |
|-------------------------|-----------------------------|----------------------------------------------------------|
| `id`                    | `number`                    | Unique identifier for the chat session.                  |
| `chatInitiatedByEntityId` | `number`                | ID of the entity that initiated the chat.                |
| `chatInitiatedByEntityType` | `'TENANT' \| 'BACKEND_USER'` | Type of entity that initiated the chat. |
| `chatJoinedByEntityId`     | `number`                | ID of the entity that joined the chat.                   |
| `chatJoinedByEntityType`   | `'TENANT' \| 'BACKEND_USER'` | Type of entity that joined the chat. |
| `chatSessionId`         | `string`                    | Unique identifier for the chat session.                  |
| `isSessionClosed`       | `boolean`                   | Status indicating if the session is closed.              |
| `lastPingedByChatInitiator` | `number`              | Last ping timestamp by the chat initiator.               |
| `lastPingedByChatJoiner`    | `number`              | Last ping timestamp by the chat joiner.                  |
| `orgId`                 | `number`                    | Organization ID associated with the chat session.        |

### Event: `chat-message-delete`

Triggered when a chat message is unsent. 

#### Payload Structure
```typescript
payload?.messageId : number
```

| Field         | Type    | Description                    |
|---------------|---------|--------------------------------|
| `messageId`   | `number`| Identifier for the deleted message.|

### Event: `chat-message-${chatSessionId}`

Triggered when a new message is sent within a chat session.

#### Payload Structure
```typescript
payload.chatMessage : ChatMessageDataType

interface ChatMessageDataType {
    id: number,
    type: 1 | 2 | 3,
    chatSessionId: string,
    contentType: string,
    deliveredAt: number,
    messageContent: string,
    metadata: any,
    orgId: number,
    seenAt: number | null,
    senderEntityId: number,
    senderEntityType: 'BACKEND_USER' | 'TENANT',
    sentAt: number,
    status: number,
}
```

| Field                | Type                            | Description                                      |
|----------------------|---------------------------------|--------------------------------------------------|
| `id`                 | `number`                        | Unique identifier for the message.               |
| `type`               | `1 \| 2 \| 3`                   | Type of the message.                             |
| `chatSessionId`      | `string`                        | Chat session ID to which the message belongs.    |
| `contentType`        | `string`                        | Content type (e.g., `TEXT`, `FILE`, `IMAGE`).    |
| `deliveredAt`        | `number`                        | Timestamp when the message was delivered.        |
| `messageContent`     | `string`                        | Content of the message.                          |
| `metadata`           | `any`                           | Additional metadata associated with the message. |
| `orgId`              | `number`                        | Organization ID related to the message.          |
| `seenAt`             | `number \| null`                | Timestamp when the message was seen (or `null`). |
| `senderEntityId`     | `number`                        | ID of the sender entity.                         |
| `senderEntityType`   | `'BACKEND_USER' \| 'TENANT'`    | Type of the sender entity.                       |
| `sentAt`             | `number`                        | Timestamp when the message was sent.             |
| `status`             | `number`                        | Status of the message.                           |

## Usage

To use this socket, connect to the appropriate socket server and add listeners for the events listed above. Make sure to use `chatSessionId` as part of the event name for `chat-session-update` and `chat-message` events to listen to specific sessions.

---

