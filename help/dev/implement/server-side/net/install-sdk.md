---
title: .NET SDK installieren
description: Erfahren Sie, wie Sie die [!DNL Adobe Target] .NET SDK.
feature: APIs/SDKs
exl-id: 3cc84775-4692-4d14-9e82-db2873140835
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '60'
ht-degree: 0%

---

# .NET SDK installieren

Das .NET SDK wird von [NuGet](https://www.nuget.org/packages/Adobe.Target.Client). Fügen Sie ihn zunächst als Abhängigkeit hinzu, indem Sie über `Package Manage` oder `.NET CLI`:

## Package Manager

>[!BEGINTABS]

>[!TAB Package Manager]

```csharp {line-numbers="true"}
Install-Package Adobe.Target.Client
```

>[!TAB .NET CLI]

```csharp {line-numbers="true"}
dotnet add package Adobe.Target.Client
```

>[!ENDTABS]

Den Open-Source-Code finden Sie unter [https://github.com/adobe/target-dotnet-sdk](https://github.com/adobe/target-dotnet-sdk).
