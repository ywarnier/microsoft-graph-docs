---
description: "Automatically generated file. DO NOT MODIFY"
---

```csharp

GraphServiceClient graphClient = new GraphServiceClient( authProvider );

var directoryRole = await graphClient.DirectoryRoles["roleTemplateId=4a5d8f65-41da-4de4-8968-e035b65339cf"]
	.Request()
	.GetAsync();

```