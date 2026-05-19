---
title: Überlegungen zur Adobe Target-Bereitstellungs-API und bekannte Einschränkungen
description: Welche Überlegungen und bekannten Einschränkungen sollte ich bei der Verwendung der [!UICONTROL Adobe Target Delivery API] beachten?
keywords: Bereitstellungs-API
exl-id: 49fe13b0-efcb-4b1c-a4cb-03b64fbd9214
feature: APIs/SDKs
TQID: https://experienceleague.adobe.com/LCgGZONQpYfw6JxNCNc2Iu13Mft8Zfx-3Uxvm2EeUVk
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 154
ht-degree: 7%

---

# Überlegungen und bekannte Einschränkungen

Die folgenden Informationen enthalten Überlegungen und bekannte Einschränkungen zur Verwendung der [!DNL Adobe Target]-[!DNL Delivery API].

* Es gibt keine Authentifizierung für [!DNL Target] Bereitstellungs-APIs.
* Diese API verarbeitet keine Cookies oder Weiterleitungsaufrufe.
* Bei HTTP/1.1- und HTTP/2-Header-Namen wird nicht zwischen Groß- und Kleinschreibung unterschieden. HTTP/2 erzwingt jedoch Header-Namen in Kleinbuchstaben. Weitere Informationen finden Sie in der Dokumentation [Hypertext Transfer Protocol Version 2 (HTTP/2)](https://www.rfc-editor.org/rfc/rfc7540#section-8.1.2){target=_blank}.

  Wenn Sie einen Endpunkt verwenden, der Besucher durch unsere neue Load-Balancer-Infrastruktur leitet, werden ihre Verbindungen automatisch auf HTTP/2 aktualisiert. Bei diesem Upgrade-Prozess werden Anfrage-Header in Header in Kleinbuchstaben umgewandelt, damit sie nicht als fehlerhaft betrachtet werden.

  Dieses Problem kann möglicherweise ein Problem für Kunden sein, wenn ihre Bibliotheken so eingerichtet sind, dass sie nach Anfrage-/Antwort-Headern suchen, bei denen zwischen Groß- und Kleinschreibung unterschieden wird (insbesondere nicht nach Headern mit Kleinschreibung).
