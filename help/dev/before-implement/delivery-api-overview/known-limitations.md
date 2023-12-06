---
title: Überlegungen zur Adobe Target-Bereitstellungs-API und bekannte Einschränkungen
description: Welche Überlegungen und bekannten Einschränkungen sollte ich bei der Verwendung von [!UICONTROL Adobe Target-Bereitstellungs-API]?
keywords: Versandschnittstelle
exl-id: 49fe13b0-efcb-4b1c-a4cb-03b64fbd9214
feature: APIs/SDKs
source-git-commit: 49acf92bbe06dbcee36fef2b7394acd7ce37baad
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 6%

---

# Überlegungen und bekannte Einschränkungen

* Es gibt keine Authentifizierung für [!DNL Target] Bereitstellungs-APIs.
* Diese API verarbeitet keine Cookies oder Weiterleitungsaufrufe.
* Sowohl HTTP/1.1- als auch HTTP/2-Header-Namen unterscheiden nicht zwischen Groß- und Kleinschreibung. HTTP/2 erzwingt jedoch Kleinbuchstaben-Header-Namen. Weitere Informationen finden Sie unter [Dokumentation zum Hypertext Transfer Protocol Version 2 (HTTP/2)](https://www.rfc-editor.org/rfc/rfc7540#section-8.1.2){target=_blank}.

  Wenn Sie einen Endpunkt verwenden, der Besucher durch unsere neue Lastenausgleichsinfrastruktur führt, werden deren Verbindungen automatisch auf HTTP/2 aktualisiert. Bei diesem Aktualisierungsprozess werden Anforderungsheader in Kleinbuchstaben umgewandelt, sodass sie nicht als falsch formatiert betrachtet werden.

  Dieses Problem kann für Kunden möglicherweise ein Problem darstellen, wenn ihre Bibliotheken so eingerichtet sind, dass sie nach Anforderungs-/Antwortheadern suchen, die zwischen Groß- und Kleinschreibung unterscheiden (nicht zwischen Kleinschreibung).
