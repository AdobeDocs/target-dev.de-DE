---
title: Adobe Target-API zur Aktualisierung von einzelnen Profilen
description: Erfahren Sie, wie Sie  [!DNL Adobe Target] [!UICONTROL Single Profile Update API] verwenden, um die Profildaten eines einzelnen Besuchers an zu senden [!DNL Target].
feature: APIs/SDKs
contributors: https://github.com/icaraps
exl-id: 4e022db3-215f-461b-9222-38ce2f2dbc28
source-git-commit: e2462d12cf58ab5a588c13a96df5e6abafb9d675
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 3%

---

# [!DNL Adobe Target Single Profile Update API]

Mit dem [!DNL Adobe Target] [!UICONTROL Single Profile Update API] können Sie eine Profilaktualisierung für einen einzelnen Benutzer senden. Der [!UICONTROL Single Profile Update API] ist fast identisch mit dem [!UICONTROL Bulk Profile Update API], aber es wird jeweils ein Besucherprofil aktualisiert, und zwar inline mit dem API-Aufruf anstelle mit einer .cvs-Datei.

Die [!UICONTROL Single Profile Update API] und werden im Allgemeinen verwendet, wenn eine Aktualisierung in Bezug auf eine Transaktion erfolgen muss, die in einem Kanal stattfindet, der [!DNL Target] nicht implementiert wurde. Sie möchten beispielsweise das Profil eines einzelnen Besuchers aktualisieren, der eine Offline-Aktion ausführt. Aktionen können das Erreichen eines Callcenters, ein Kredit wird finanziert, eine Kundenkarte im Geschäft verwenden, auf einen Kiosk zugreifen und so weiter.

Zu den Vorteilen des [!UICONTROL Single Profile Update API] gehören:

* Keine Begrenzung der Anzahl der Profilattribute.
* Profilattribute, die über die Site gesendet werden, können über die API aktualisiert werden und umgekehrt.

## Einschränkungen 

* Die [!UICONTROL Single Profile Update API] ist auf die Durchführung von 1 Million Aktualisierungen in einem rollierenden Zeitraum von 24 Stunden beschränkt.
* Aktualisierungen werden im Allgemeinen in weniger als einer Stunde durchgeführt, es kann jedoch bis zu 24 Stunden dauern, bis sie widergespiegelt werden.

  Wenn Sie mehr Aktualisierungen senden müssen oder Aktualisierungen in kürzeren Zeitrahmen verarbeitet werden müssen, sollten Sie Transaktionsprofilaktualisierungen über Client-seitige Aktualisierungen (bevorzugt) oder über die [!DNL Adobe Target] Server-seitige [Bereitstellungs-API) &#x200B;](/help/dev/implement/delivery-api/overview.md).

* Die [!UICONTROL Single Profile Update API] ist eine Server-zu-Server-API und nicht für die Verwendung auf einer Web-Seite konzipiert. Um ein Besucherprofil auf Ihrer Web-Seite zu aktualisieren, können Sie die Funktion [trackEvent()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md) oder die [Bereitstellungs-API](/help/dev/implement/delivery-api/overview.md) verwenden.

## Format

Geben Sie die Profilparameter im `profile.paramName=value` Format an.

Um das Profil für eine `pcId` zu aktualisieren, verwenden Sie:

``` ```
https://&lt;your-client-code>.tt.omtrdc.net/m2/client/profile/update?mboxPC=1368007744041-575948.01_00&profile.attr=0&profile.attr2=1...
``` ```

Um das Profil für eine `mbox3rdPartyId` zu aktualisieren, verwenden Sie:

``` ```
shell http://&lt;your-client-code>.tt.omtrdc.net/m2/client/profile/update?mbox3rdPartyId=123456&profile.attr=0&profile.attr2=1...
``` ```

Die [!UICONTROL Single Profile Update API] ist nur für Aktualisierungen vorgesehen. Wenn nichts gefunden wird, wird kein Profil erstellt.

## Hinweise

* Parameter und Werte müssen mit UTF-8 URL-codiert sein.
* Parameterformat ist `profile.paramName`.
* Es müssen nicht alle Parameterwerte für alle pcIds und mbox3rdPartyIds vorhanden sein.
* Bei Parametern und Werten wird zwischen Groß- und Kleinschreibung unterschieden.
* Sowohl GET als auch POST werden unterstützt.
* Die aktuellen Größenbeschränkungen für Limit sind 8 KB für GET und 60 KB für POST.

## Antwort

Eine Beispielantwort für die oben genannten Anfragen sieht wie folgt aus:

`trueRequest successfully submitted`

Diese Antwort zeigt an, dass die Antwort übermittelt wurde und in Kürze verarbeitet wird.
