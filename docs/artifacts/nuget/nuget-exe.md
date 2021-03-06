---
title: Use NuGet with Azure DevOps Services feeds
description: Authenticating to feeds with NuGet in Azure DevOps Services
ms.assetid: 10665DBC-846E-4192-8CAB-D5A4C6E40C65
ms.technology: devops-artifacts
ms.topic: conceptual
ms.date: 09/01/2017
monikerRange: '>= tfs-2018'
---

# Use NuGet with Azure DevOps Services feeds

**Azure DevOps Services**

> [!NOTE]
> This page covers interactive scenarios. In Azure Pipelines, use the NuGet step to [restore](/azure/devops/pipelines/packages/nuget-restore) and [publish](/azure/devops/pipelines/artifacts/nuget) packages. 

[!INCLUDE [nuget-recommended-version](../includes/nuget/nuget-recommended-version.md)]

## Add a feed to NuGet 4.8.2 or later
NuGet 4.8.2 and later supports the Azure Artifacts Credential Provider, which automatically acquires feed credentials when needed.

1. Navigate to your feed ([or create a feed if you haven't](../feeds/create-feed.md)). 

2. Select **Connect to feed**:

::: moniker range=">= azure-devops-2019"

   > [!div class="mx-imgBorder"] 
   >![Connect to feed button in the upper-right of the page](../media/connect-to-feed-azure-devops-newnav.png)
   > 

3. Select **NuGet.exe** under the **NuGet** header

4. Select **Get the tools** in the top right corner

5. Follow steps **1** and **2** to download the latest NuGet version and the credential provider.

6. Follow the instructions in the **Project setup**, **Restore packages**, and **Publish packages** sections to publish.

   > [!div class="mx-imgBorder"] 
   >![NuGet publish instructions in the Connect to feed](../media/nuget-azure-devops-newnav.png)
   > 

   > [!NOTE]
   > You can also paste the **Project setup** XML snippet in your default nuget.config file to use outside of a project.

::: moniker-end

::: moniker range="<= tfs-2018"

   ![Connect to feed button in the upper-right of the page](../media/connect-to-feed.png)

3. Follow steps 1, 2, and 3 to get the tools, add the feed to your local NuGet configuration, and push the package.

   ![NuGet publish instructions in the Connect to feed dialog](../media/nugeturl.png)

   ::: moniker-end

Then, run any [nuget command](/nuget/tools/nuget-exe-cli-reference).

## Add a feed to NuGet 2
NuGet 2 uses Personal Access Tokens to access feeds.

To use a 2.x client, first get the v3 feed URL: 

1. Navigate to your feed ([or create a feed if you haven't](../feeds/create-feed.md)). 

2. Select **Connect to feed**:

::: moniker range=">= azure-devops-2019"
   
   > [!div class="mx-imgBorder"] 
   >![Connect to feed button in the upper-right of the page](../media/connect-to-feed-azure-devops-newnav.png)
   > 

::: moniker-end

::: moniker range="<= tfs-2018"

   ![Connect to feed button in the upper-right of the page](../media/connect-to-feed.png)

   ::: moniker-end
   
3. Copy the NuGet package source URL:

::: moniker range=">= azure-devops-2019"

   > [!div class="mx-imgBorder"] 
   >![NuGet Package source URL in the Connect to feed dialog](../media/nuget-consume-url-azure-devops-newnav.png)
   > 

::: moniker-end

::: moniker range="<= tfs-2018"

   ![NuGet Package source URL in the Connect to feed dialog](../media/nuget-consume-url.png)

::: moniker-end

Then, at the end of the URL, replace `/v3/index.json` with `/v2`. 

[!INCLUDE [generate-pat](../includes/generate-pat.md)]

Run 

```no-highlight
nuget.exe sources add -name {your feed name} -source {your feed URL} -username {anything} -password {your PAT}
```

Then, run any [nuget command](/nuget/tools/nuget-exe-cli-reference).
