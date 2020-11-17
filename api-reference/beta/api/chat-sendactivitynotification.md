---
title: "chat: sendActivityNotification"
description: Send an activity feed notification in scope of a chat
author: RamjotSingh
localization_priority: Normal
ms.prod: microsoft-teams
doc_type: apiPageType
---

# chat: sendActivityNotification
Namespace: microsoft.graph

Sends an activity feed notification in scope of a chat. For more details about sending notifications and the requirements for the same, refer to the documentation
[sending Teams activity notifications](/graph/teams-send-activityfeednotifications).

## Permissions
One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Permissions](/graph/permissions-reference).

|Permission type|Permissions (from most to least privileged)|
|:---|:---|
|Delegated (work or school account)|TeamsActivity.Send|
|Delegated (personal Microsoft account)|Not Supported.|
|Application|TeamsActivity.Send|

## HTTP request

<!-- {
  "blockType": "ignored"
}
-->
``` http
POST /chats/{chatId}/sendActivityNotification
```

## Request headers
|Name|Description|
|:---|:---|
|Authorization|Bearer {token}. Required.|
|Content-Type|application/json. Required.|

## Request body
In the request body, supply JSON representation of the parameters.

The following table shows the parameters that can be used with this action.

|Parameter|Type|Description|
|:---|:---|:---|
|topic|[teamworkActivityTopic](../resources/teamworkactivitytopic.md)|Topic of the notification. Specifies the resource being talked about.|
|activityType|String|Activity type. This must be declared in the [Teams app manifest](/microsoftteams/platform/overview).|
|chainId|Int64|Optional. Used to override a previous notification. Use the same `chainId` in subsequent requests to override the previous notification.|
|previewText|[itemBody](../resources/itembody.md)|Preview text for the notification. Microsoft Teams will only show first 150 characters.|
|templateParameters|[keyValuePair](../resources/keyvaluepair.md) collection|Values for template variables defined in the activity feed entry corresponding to `activityType` in [Teams app manifest](/microsoftteams/platform/overview).|
|recipient|[teamworkNotificationRecipient](../resources/teamworknotificationrecipient.md)|Recipient of the notification. Only AzureAD users are supported. See also [aadUserNotificationRecipient](aadusernotificationrecipient.md). |

Following resources are supported when setting `source` of `topic` to entity url

- [Chat](../resources/chat.md)
- [Chat message](../resources/chatmessage.md)

> **Note:** The entity url must be same or under the chat in the url. Additionally, the [teams app](/microsoftteams/platform/overview) must be installed in the chat.

## Response

If successful, this action returns a `204 No Content` response code.

## Examples

### Example 1 : Notify a user about a task created in a chat

This example shows how you can send an activity feed notification for a new task created in a chat. For more details about sending notifications and the requirements for the same, refer to the documentation
[sending Teams activity notifications](/graph/teams-send-activityfeednotifications).

#### Request
<!-- {
  "blockType": "request",
  "name": "chat_sendactivitynotification"
}
-->
``` http
POST https://graph.microsoft.com/beta/chats/{chatId}/sendActivityNotification

Content-Type: application/json

{
    "topic": {
        "source": "entityUrl",
        "value": "https://graph.microsoft.com/beta/chats/{chatId}"
    },
    "activityType": "taskCreated",
    "previewText": {
        "content": "New Task Created"
    },
    "recipient": {
        "@odata.type": "microsoft.graph.aadUserNotificationRecipient",
        "userId": "569363e2-4e49-4661-87f2-16f245c5d66a"
    },
    "templateParameters": [
        {
            "name": "taskId",
            "value": "Task 12322"
        }
    ] 
}
```

#### Response
<!-- {
  "blockType": "response",
  "truncated": false
}
-->
``` http
HTTP/1.1 204 No Content
```

### Example 2 : Notify a user about a approval needed in a chat message

Similar to the example above, we are using `topic` as an `entityUrl`. However, in this case we are linking to a message in the chat. The message can contains a card with the approval button on it.

#### Request
<!-- {
  "blockType": "request",
  "name": "chat_sendactivitynotification"
}
-->
``` http
POST https://graph.microsoft.com/beta/chats/{chatId}/sendActivityNotification

Content-Type: application/json

{
    "topic": {
        "source": "entityUrl",
        "value": "https://graph.microsoft.com/beta/chats/{chatId}/messages/{messageId}"
    },
    "activityType": "approvalRequired",
    "previewText": {
        "content": "Deployment requires your approval"
    },
    "recipient": {
        "@odata.type": "Microsoft.Teams.GraphSvc.aadUserNotificationRecipient",
        "userId": "569363e2-4e49-4661-87f2-16f245c5d66a"
    },
    "templateParameters": [
        {
            "name": "approvalTaskId",
            "value": "2020AAGGTAPP"
        }
    ]
}
```

#### Response
<!-- {
  "blockType": "response",
  "truncated": false
}
-->
``` http
HTTP/1.1 204 No Content
```

### Example 3 : Notify a user about an event in relation to a chat

As seen in examples above, you can link to different aspects of the chat. However if you want to link an aspect which is not part of the chat, or is not represented by Microsoft Graph. You can
set the source of the `topic` to `text` and pass in a custom value for it. `webUrl` is required when using `topic` source as `text`.

#### Request
<!-- {
  "blockType": "request",
  "name": "chat_sendactivitynotification"
}
-->
``` http
POST https://graph.microsoft.com/beta/chats/{chatId}/sendActivityNotification

Content-Type: application/json

{
    "topic": {
        "source": "text",
        "value": "Deployment Approvals Channel",
        "webUrl": "https://teams.microsoft.com/l/message/19:448cfd2ac2a7490a9084a9ed14cttr78c@thread.skype/1605223780000?tenantId=c8b1bf45-3834-4ecf-971a-b4c755ee677d&groupId=d4c2a937-f097-435a-bc91-5c1683ca7245&parentMessageId=1605223771864&teamName=Approvals&channelName=Azure%20DevOps&createdTime=1605223780000"
    },
    "activityType": "deploymentApprovalRequired",
    "previewText": {
        "content": "New deployment requires your approval"
    },
    "recipient": {
        "@odata.type": "Microsoft.Teams.GraphSvc.aadUserNotificationRecipient",
        "userId": "569363e2-4e49-4661-87f2-16f245c5d66a"
    },
    "templateParameters": [
        {
            "name": "deploymentId",
            "value": "6788662"
        }
    ]
}
```

#### Response
<!-- {
  "blockType": "response",
  "truncated": false
}
-->
``` http
HTTP/1.1 204 No Content
```