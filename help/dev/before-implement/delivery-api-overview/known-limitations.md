---
title: Überlegungen zur Adobe Target-Bereitstellungs-API und bekannte Einschränkungen
description: Welche Überlegungen und bekannten Einschränkungen sollte ich bei der Verwendung der [!UICONTROL Adobe Target Delivery API] beachten?
keywords: Bereitstellungs-API
exl-id: 49fe13b0-efcb-4b1c-a4cb-03b64fbd9214
feature: APIs/SDKs
source-git-commit: 49acf92bbe06dbcee36fef2b7394acd7ce37baad
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 6%

---

# Überlegungen und bekannte Einschränkungen

* Es gibt keine Authentifizierung für [!DNL Target] Bereitstellungs-APIs.
* Diese API verarbeitet keine Cookies oder Weiterleitungsaufrufe.
* Bei HTTP/1.1- und HTTP/2-Header-Namen wird nicht zwischen Groß- und Kleinschreibung unterschieden. HTTP/2 erzwingt jedoch Header-Namen in Kleinbuchstaben. Weitere Informationen finden Sie in der Dokumentation [Hypertext Transfer Protocol Version 2 (HTTP/2)](https://www.rfc-editor.org/rfc/rfc7540#section-8.1.2){target=_blank}.

  Wenn Sie einen Endpunkt verwenden, der Besucher durch unsere neue Load-Balancer-Infrastruktur leitet, werden ihre Verbindungen automatisch auf HTTP/2 aktualisiert. Bei diesem Upgrade-Prozess werden Anfrage-Header in Header in Kleinbuchstaben umgewandelt, damit sie nicht als fehlerhaft betrachtet werden.

  Dieses Problem kann möglicherweise ein Problem für Kunden sein, wenn ihre Bibliotheken so eingerichtet sind, dass sie nach Anfrage-/Antwort-Headern suchen, bei denen zwischen Groß- und Kleinschreibung unterschieden wird (insbesondere nicht nach Headern mit Kleinschreibung).
