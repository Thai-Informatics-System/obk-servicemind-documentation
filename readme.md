
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

## Available WebSocket Events

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
        "route": "client/init-chat-with-concierge",
        "body": {
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

Step 2: Continue with Old Chat Session

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
           "messageContent": "whatever messages needs to be sent"
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
            "metadata": null
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

### 6. Delete Sent Message

- **Description**: This API allows the user to delete a previously sent message within a chat session. The deletion is based on the `chatSessionId` and the message ID.

#### Request Payload:

```json
{
    "action": "api",
    "data": {
        "route": "client/delete-message",
        "body": {
            "chatSessionId": "318c7696-e88b-4cd3-86da-06a4abb50e99"
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

### 7. End Chat Session

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


