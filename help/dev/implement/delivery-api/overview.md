---
title: Übersicht über die Adobe Target-Bereitstellungs-API
description: Übersicht über die Adobe Target-Bereitstellungs-API
keywords: Bereitstellungs-API
exl-id: e760bddc-b1ae-4b7b-bff2-aba81c6b6d34
feature: APIs/SDKs
source-git-commit: ccc27e66207e58dcd33865e5d28a51644e8e1931
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# Übersicht über die Bereitstellungs-API

Die [!DNL Adobe Target Delivery API] basiert auf REST. In dieser Dokumentation werden die Ressourcen beschrieben, aus denen die [!DNL Adobe Target] [!DNL Delivery API] besteht. HTTP-Methoden werden verwendet, um Vorgänge für diese Ressourcen auszuführen.

Mit [!UICONTROL Adobe Target's Delivery API] können Sie:

* Bereitstellen von Erlebnissen im Web, einschließlich SPAs und mobilen Kanälen sowie Nicht-Browser-basierten IoT-Geräten wie einem verbundenen TV, Kiosk oder digitalen Bildschirmen im Geschäft.
* Bereitstellen von Erlebnissen von jeder Server-seitigen Plattform oder Anwendung, die HTTP/s-Aufrufe ausführen kann.
* Bereitstellen konsistenter und personalisierter Erlebnisse für Benutzer, unabhängig davon, über welchen Kanal oder welche Geräte der Benutzer mit Ihrem Unternehmen interagiert hat.
* Speichern Sie Erlebnisse für einen Benutzer innerhalb einer Sitzung auf Ihrem Server zwischen, damit mehrere API-Aufrufe vermieden werden können und so eine bessere Leistung erzielt wird.
* Nahtlose Integration mit [!DNL Adobe Experience Cloud] Produkten wie [!DNL Adobe Analytics], [!DNL Adobe Audience Manager] und dem [!DNL Experience Cloud ID Service] von der Serverseite aus.

>[!IMPORTANT]
>
>Seien Sie vorsichtig, wenn Sie Ihre [!DNL Recommendations]-[!UICONTROL Catalog] über die [!DNL Delivery API] aktualisieren. Der [!DNL Delivery API] ist öffentlich. Vermeiden Sie es daher, ihn zum Ausfüllen anklickbarer Elemente in Ihrem Recommendations-Katalog zu verwenden. Dies kann zu ungültigen Inhalten führen und Ihren Katalog belasten.
>
>Best Practices:
>
>Verwenden Sie die [!DNL Delivery API] nur zum Aktualisieren von Katalogattributen, die:
>* sich häufig ändern (z. B. Preis, Lagerbestand).
>* Verwenden Sie ein vordefiniertes Format, das auf Ihrer Website einfach validiert werden kann.
>* Verwenden Sie sie nicht zum Hinzufügen oder Ändern anklickbarer Elemente oder anderer nicht verifizierter Inhalte.
>
>Bei Bedarf können Sie den Kunden-Support anfordern, um Katalogaktualisierungen über die Bereitstellungs-API zu deaktivieren.

Weitere Informationen finden Sie in der [[!UICONTROL Adobe Target Delivery API]](https://developer.adobe.com/target/implement/delivery-api/){target=_blank}.

>[!NOTE]
>
>Sie können weiterhin auf die [alte /v1/mbox- und /v2/batchmbox-API-Dokumentation](https://developers.adobetarget.com/api/legacy-api/index.html) zugreifen. Funktionen werden jedoch in der Bereitstellungs-API entwickelt (wie hier dokumentiert) und nicht in die Legacy-APIs rückportiert.
