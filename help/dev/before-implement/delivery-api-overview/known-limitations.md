---
title: Überlegungen zur Adobe Target-Bereitstellungs-API und bekannte Einschränkungen
description: Welche Überlegungen und bekannten Einschränkungen sollte ich bei der Verwendung der [!UICONTROL Adobe Target Delivery API] beachten?
keywords: Bereitstellungs-API
exl-id: 49fe13b0-efcb-4b1c-a4cb-03b64fbd9214
feature: APIs/SDKs
source-git-commit: 413b16ed0b098de6914558fa29b9ca59aaba958e
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 3%

---

# Überlegungen und bekannte Einschränkungen

Die folgenden Informationen enthalten Überlegungen und bekannte Einschränkungen zur Verwendung der [!DNL Adobe Target]-[!DNL Delivery API].

* Es gibt keine Authentifizierung für [!DNL Target] Bereitstellungs-APIs.
* Diese API verarbeitet keine Cookies oder Weiterleitungsaufrufe.
* Bei HTTP/1.1- und HTTP/2-Header-Namen wird nicht zwischen Groß- und Kleinschreibung unterschieden. HTTP/2 erzwingt jedoch Header-Namen in Kleinbuchstaben. Weitere Informationen finden Sie in der Dokumentation [Hypertext Transfer Protocol Version 2 (HTTP/2)](https://www.rfc-editor.org/rfc/rfc7540#section-8.1.2){target=_blank}.

  Wenn Sie einen Endpunkt verwenden, der Besucher durch unsere neue Load-Balancer-Infrastruktur leitet, werden ihre Verbindungen automatisch auf HTTP/2 aktualisiert. Bei diesem Upgrade-Prozess werden Anfrage-Header in Header in Kleinbuchstaben umgewandelt, damit sie nicht als fehlerhaft betrachtet werden.

  Dieses Problem kann möglicherweise ein Problem für Kunden sein, wenn ihre Bibliotheken so eingerichtet sind, dass sie nach Anfrage-/Antwort-Headern suchen, bei denen zwischen Groß- und Kleinschreibung unterschieden wird (insbesondere nicht nach Headern mit Kleinschreibung).

* Seien Sie vorsichtig, wenn Sie Ihre [!DNL Recommendations]-[!UICONTROL Catalog] über die [!DNL Delivery API] aktualisieren. Der [!DNL Delivery API] ist öffentlich. Vermeiden Sie es daher, ihn zum Ausfüllen anklickbarer Elemente in Ihrem Recommendations-Katalog zu verwenden. Dies kann zu ungültigen Inhalten führen und Ihren Katalog belasten.

  **Best Practices**:

  Verwenden Sie die [!DNL Delivery API] nur zum Aktualisieren von Katalogattributen, die:
   * sich häufig ändern (z. B. Preis, Lagerbestand).
   * Verwenden Sie ein vordefiniertes Format, das auf Ihrer Website einfach validiert werden kann.
   * Verwenden Sie sie nicht zum Hinzufügen oder Ändern anklickbarer Elemente oder anderer nicht verifizierter Inhalte.
   * Bei Bedarf können Sie den Kunden-Support anfordern, um Katalogaktualisierungen über die Bereitstellungs-API zu deaktivieren.

  Weitere Informationen finden Sie in der [[!UICONTROL Adobe Target Delivery API]](https://developer.adobe.com/target/implement/delivery-api/){target=_blank}.
