---
title: "Delete smsAuthenticationMethodConfiguration"
description: "Delete a smsAuthenticationMethodConfiguration object."
author: "mmcla"
localization_priority: Normal
ms.prod: "microsoft-identity-platform"
doc_type: apiPageType
---

# Delete smsAuthenticationMethodConfiguration
Namespace: microsoft.graph

[!INCLUDE [beta-disclaimer](../../includes/beta-disclaimer.md)]

Remove changes made to the [Text Message authentication method policy](../resources/smsauthenticationmethodconfiguration.md) by reverting the policy to its default configuration.

## Permissions
One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Permissions](/graph/permissions-reference).

|Permission type|Permissions (from least to most privileged)|
|:---|:---|
|Delegated (work or school account)|Policy.ReadWrite.AuthenticationMethod|
|Delegated (personal Microsoft account)|Not supported.|
|Application|Policy.ReadWrite.AuthenticationMethod|

For delegated scenarios, the administrator needs the Global admin role. For more information, see [role](/azure/active-directory/users-groups-roles/directory-assign-admin-roles#available-roles).

## HTTP request

<!-- {
  "blockType": "ignored"
}
-->
``` http
DELETE /policies/authenticationMethodsPolicy/authenticationMethodConfigurations/sms
```

## Request headers
|Name|Description|
|:---|:---|
|Authorization|Bearer {token}. Required.|

## Request body
Do not supply a request body for this method.

## Response

If successful, this method returns a `204 No Content` response code.

## Examples

### Request
<!-- {
  "blockType": "request",
  "name": "delete_smsauthenticationmethodconfiguration"
}
-->
``` http
DELETE https://graph.microsoft.com/beta/policies/authenticationMethodsPolicy/authenticationMethodConfigurations/sms
```


### Response
**Note:** The response object shown here might be shortened for readability.
<!-- {
  "blockType": "response",
  "truncated": true
}
-->
``` http
HTTP/1.1 204 No Content
```

