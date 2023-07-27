---
title: Überlegungen zur Adobe Target-Bereitstellungs-API und bekannte Einschränkungen
description: Welche Überlegungen und bekannten Einschränkungen sollte ich bei der Verwendung von [!UICONTROL Adobe Target-Bereitstellungs-API]?
keywords: Versandschnittstelle
exl-id: 49fe13b0-efcb-4b1c-a4cb-03b64fbd9214
feature: APIs/SDKs
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 7%

---

# Überlegungen und bekannte Einschränkungen

* Es gibt keine Authentifizierung für [!DNL Target] Bereitstellungs-APIs.
* Diese API verarbeitet keine Cookies oder Weiterleitungsaufrufe.
* Unterstützung für [!UICONTROL Automated Personalization] AP und [!UICONTROL Recommendations] Aktivitäten: Diese API verfügt über zwei Modi zum Abrufen von Inhalten: den Ausführungsmodus und den Vorabruf. Der Vorabruf-Modus kann nur für [!UICONTROL AB-Test] und [!UICONTROL Erlebnis-Targeting] (XT). Verwenden Sie den Vorabruf-Modus nicht für [!UICONTROL Automated Personalization] AP, [!UICONTROL Automatische Zuordnung], [!UICONTROL Automatisches Targeting]oder [!UICONTROL Recommendations] Aktivitätstypen.
* Sowohl HTTP/1.1- als auch HTTP/2-Header-Namen unterscheiden nicht zwischen Groß- und Kleinschreibung. HTTP/2 erzwingt jedoch Kleinbuchstaben-Header-Namen. Weitere Informationen finden Sie unter [Dokumentation zum Hypertext Transfer Protocol Version 2 (HTTP/2)](https://www.rfc-editor.org/rfc/rfc7540#section-8.1.2){target=_blank}.

  Wenn Sie einen Endpunkt verwenden, der Besucher durch unsere neue Lastenausgleichsinfrastruktur führt, werden deren Verbindungen automatisch auf HTTP/2 aktualisiert. Bei diesem Aktualisierungsprozess werden Anforderungsheader in Kleinbuchstaben umgewandelt, sodass sie nicht als falsch formatiert betrachtet werden.

  Dieses Problem kann für Kunden möglicherweise ein Problem darstellen, wenn ihre Bibliotheken so eingerichtet sind, dass sie nach Anforderungs-/Antwortheadern suchen, die zwischen Groß- und Kleinschreibung unterscheiden (nicht zwischen Kleinschreibung).
