---
keywords: TLS, TLS 1.0, Transport Layer Security, Verschlüsselung, TLS 1.1, TLS 1.2
description: Erfahren Sie [!DNL Target]  wie das TLS-Protokoll (Transport Layer Security) verwendet, um die höchsten Sicherheitsstandards zu wahren und die Sicherheit Ihrer Kundendaten zu fördern.
title: Wie  [!DNL Target]  TLS Sicherheit?
feature: Privacy & Security
exl-id: f5ea2272-27ab-49c9-b096-b15dd277d4e5
TQID: https://experienceleague.adobe.com/2Ka08Kp8jLd6u7-gtwbfU1rq7SGDxE-dwBTHWz1mS3E
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: adee20bd-51f4-461d-b9db-d215f8756eeb
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2:
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 1231
ht-degree: 43%

---

# Änderungen der TLS-Verschlüsselung (Transport Layer Security)

Informationen über Änderungen bei der Verwendung von TLS (Transport Layer Security) durch [!DNL Adobe] und [!DNL Adobe Target], um die höchsten Sicherheitsstandards aufrechtzuerhalten und die Sicherheit von Kundendaten zu fördern.

Transport Layer Security (TLS) ist das am weitesten verbreitete Sicherheitsprotokoll, das aktuell in Webbrowsern und anderen Anwendungen Verwendung findet, bei denen über ein Netzwerk übertragene Daten geschützt werden müssen. Um die Sicherheitsstandards von Adobe einzuhalten, muss die Unterstützung für ältere Protokolle beendet und durch TLS 1.2 als obligatorisches Sicherheitsprotokoll ersetzt werden, damit die Daten durch die neueste und sicherste Version des Protokolls geschützt sind.

>[!WARNING]
>
>Seit dem 1. März 2020 unterstützt [!DNL Target] keine TLS 1.1-Verschlüsselung mehr für Visual Experience Composer (VEC), Enhanced Experience Composer (EEC), Aktivitätsbereitstellung, APIs usw. Bitte aktualisieren Sie auf TLS 1.2, um Probleme zu vermeiden.

Wir gehen davon aus, dass dies keine wesentlichen Auswirkungen auf Kundendaten oder die Berichterstattung haben wird.

## Visual Experience Composer (VEC) mit aktiviertem Enhanced Experience Composer (EEC)

TLS 1.2 ist seit dem 1. März 2020 der Standard und TLS 1.1 wird nicht mehr unterstützt.

Adobe transferiert Kunden schrittweise zu TLS 1.2. Für diejenigen Domains, deren Domains bereits mit 1.2 kompatibel sind, verschieben wir sie auf TLS 1.2, ohne dass Änderungen von Ihnen erforderlich sind. Die meisten Kunden-Domains unterstützen TLS 1.2 bereits. Wenn Ihre Domain TLS 1.2 jedoch nicht unterstützt, behalten wir diese Domains wie heute (bis März 2020) auf TLS 1.1 bei.

In dieser Übergangsphase sollten keine Probleme auftreten. Wenn der VEC das Laden einer zuvor funktionierenden Site beendet hat, [Öffnen Sie ein Ticket für die Kundenunterstützung](https://experienceleague.adobe.com/docs/target/using/cmp-resources-and-contact-information.html?#reference_ACA3391A00EF467B87930A450050077C) und geben Sie diese Migration als mögliche Ursache an.

Wenn Sie jedoch zu den Kundinnen und Kunden gehören, die TSL 1.1 ohne Unterstützung für TLS 1.2 verwenden, sollten Sie die Umstellung Ihrer Domains/Infrastruktur auf TLS 1.2 planen. Wir werden das Protokoll TLS 1.1 bis zum 1. März 2020 weiterhin unterstützen. Ab dem 1. März 2020 unterstützt [!DNL Target] das TLS 1.1-Protokoll nicht mehr, das für den VEC über die Enhanced Experience Composer-Funktion verwendet werden soll.

Auch wenn allen Kunden der Umstieg auf TLS 1.2 empfohlen wird – falls Sie als neuer Kunde TLS 1.2 *NICHT* unterstützen, teilen Sie dem Kundendienst mit, dass Sie TLS 1.1 für Enhanced Experience Composer verwenden müssen. Planen Sie jedoch den Übergang zu TLS 1.2 ein, da TLS 1.0 nur noch bis zum Montag, 1. März 2020 unterstützt wird.

## Aktivitätsversand

Ab dem 1. März 2020 unterstützen [!DNL Target]-Server TLS 1.1 nicht mehr. Mit dieser Änderung akzeptieren [!DNL Target]-Server keine Anfragen mehr von Besuchern mit älteren Geräten oder Webbrowsern, die TLS 1.2 (oder höher) nicht unterstützen. Daher erhalten ältere Geräte und Browser, die nur TLS 1.1 unterstützen (oder standardmäßig TLS 1.1 unterstützen), keine Aktivitätsinhalte von Adobe Target. Standardinhalte der Site werden gerendert.

Zu den betroffenen älteren Geräten und Browsern gehören:

* Google Chrome (Chrome for Android), Version 29 und früher
* Opera Browser (Opera Mobile) Versionen 12.17 und früher
* Mozilla Firefox (Firefox für Mobile) Versionen 26 und früher
* Android 4.3 und frühere Versionen
* Internet Explorer 8 bis 10 unter Windows 7 und frühere Versionen
* Internet Explorer 10 unter Windows Phone 8.0
* Safari 6.0.4/OS X 10.8.4 und frühere Versionen

Berücksichtigen Sie Folgendes bei der Planung für diese Änderung (beachten Sie, dass der Termin am Montag, 1. März 2020 für alle Punkte gilt):

* Sie müssen sicherstellen, dass Ihre Standardsite vorbereitet ist und auf kompatiblen Geräten und Browsern genutzt werden kann.
* Beachten Sie, dass die Anzahl der Besucher in Ihren [!DNL Target] möglicherweise einen unbedeutenden Rückgang der Besucherzahl verzeichnen kann.
* Möglicherweise müssen Sie Zielgruppen ändern, die speziell für ältere Geräte oder Browser erstellt wurden, die TLS 1.2 nicht unterstützen. Der Versand an diese Geräte und Browser funktioniert nicht mehr.

Weitere Informationen zu unterstützten Browsern und ihren Versionen finden Sie unter [Unterstützte Browser](supported-browsers.md).

## [!DNL Adobe Target]-APIs

Ab dem 1. März 2020 unterstützen [!DNL Target] APIs keine TLS 1.1-Verschlüsselung mehr. Kunden, die auf die API zugreifen, sollten sicherstellen, dass sie nicht von den Auswirkungen betroffen sind.

* API-Clients, die Java 7 mit Standardeinstellungen verwenden, müssen geändert werden, um TLS 1.2 zu unterstützen. Weitere Informationen finden Sie unter &quot;[Ändern der standardmäßigen TLS-Protokollversion für Client-Endpunkte: TLS 1.0 in TLS 1.2](https://www.java.com/en/configure_crypto.html)&quot; auf der Java-Website.
* API-Clients, die Java 8 verwenden, sollten nicht beeinträchtigt werden, da die Standardeinstellung TLS 1.2 ist.
* Bei API-Clients, die andere Frameworks verwenden, müssen Sie die Details zur Unterstützung von TLS 1.2 beim jeweiligen Anbieter erfragen.

## Zugriff auf Experience Cloud Solutions-Benutzeroberflächen

Da die Benutzeroberfläche von [!DNL Target] Standard/Premium bereits einen [modernen Webbrowser](supported-browsers.md) erfordert, gehen wir von Problemen nicht aus. Wenn Sie keine Verbindung zu Target herstellen können, sollten Sie Ihren Browser auf die neueste Version aktualisieren.

## Überprüfen, welche TLS-Version Ihr Browser verwendet

So überprüfen Sie die TLS-Version auf Ihrer Website mit Google Chrome:

1. Öffnen Sie die betroffene Website in Chrome.
1. Klicken Sie im Chrome-Menü (mit den drei senkrechten Auslassungspunkten) auf Weitere Tools > Entwickler-Tools .

   ![Chrome Developer Tools](assets/chrome-developer-tools.png)

1. Öffnen Sie die Registerkarte Sicherheit und überprüfen Sie dann die TLS-Versionsinformationen unter Verbindung:

   ![TLS-Versionsdetails](assets/chrome-tls-version.png)

>[!NOTE]
>
>Diese Anleitungen sind zum Zeitpunkt der Veröffentlichung aktuell und können sich ändern. Eine schnelle Internet-Suche sollte helfen, falls sich diese Anweisungen ändern. Andere Browser weisen ähnliche Schritte auf.

## Erwartetes Verhalten bei Browsern, die TLS-Versionen unter 1.2 unterstützen

In diesem Abschnitt wird beschrieben, was bei Browsern zu erwarten ist, die TLS-Versionen unter 1.2 nur bei Verwendung einer at.js-Implementierung unterstützen. Zu Vergleichszwecken wird in diesem Abschnitt auch beschrieben, was bei Browsern zu erwarten ist, die TLS 1.2 unterstützen.

### Zentrale Endpunkte

| [!DNL Target] JavaScript-Implementierung | Details |
|--- |--- |
| at.js | Bei aktiviertem TLS 1.0 oder TLS 1.1:<ul><li>Mit Browser-Entwicklungstools wird auf der Registerkarte „Netzwerk“ die Meldung „200 OK“ angezeigt. Das bedeutet, dass die Anfrage erfolgreich war.</li><li>Benutzer sehen die Meldung „Keine sichere Verbindung zu dieser Seite möglich“. In der Nachricht wird erläutert, dass dies möglicherweise daran liegt, dass die Site veraltete oder unsichere TLS-Sicherheitseinstellungen verwendet.</li><li>Es wird kein Konsolenfehler angezeigt.</li></ul>Bei aktiviertem TLS 1.2:<ul><li>Die „at.js“-Datei wird heruntergeladen.</li></ul> |

### Edge-Endpunkte

| [!DNL Target] JavaScript-Implementierung | Details |
|--- |--- |
| Adobe Experience Platform Web SDK | Bei aktiviertem TLS 1.0 oder TLS 1.1:<ul><li>Mit Browser-Entwicklungstools wird auf der Registerkarte „Netzwerk“ die Meldung „200 OK“ angezeigt. Das bedeutet, dass die Anfrage erfolgreich war.</li><li>Benutzer sehen die Meldung „Keine sichere Verbindung zu dieser Seite möglich“. In der Nachricht wird erläutert, dass dies möglicherweise daran liegt, dass die Site veraltete oder unsichere TLS-Sicherheitseinstellungen verwendet.</li><li>Es wird kein Konsolenfehler angezeigt.</li><li>Der Standardinhalt wird bereitgestellt.</li></ul>Bei aktiviertem TLS 1.2:<ul><li>Der Angebotsinhalt wird bereitgestellt.</li></ul> |
| at.js | Bei aktiviertem TLS 1.0 oder TLS 1.1:<ul><li>Mit Browser-Entwicklungstools wird auf der Registerkarte „Netzwerk“ die Meldung „200 OK“ angezeigt. Das bedeutet, dass die Anfrage erfolgreich war.</li><li>Benutzer sehen die Meldung „Keine sichere Verbindung zu dieser Seite möglich“. In der Nachricht wird erläutert, dass dies möglicherweise daran liegt, dass die Site veraltete oder unsichere TLS-Sicherheitseinstellungen verwendet.</li><li>Es wird kein Konsolenfehler angezeigt.</li><li>Der Standardinhalt wird bereitgestellt.</li></ul>Bei aktiviertem TLS 1.2:<ul><li>Der Angebotsinhalt wird bereitgestellt.</li></ul> |

### Aktivität, die auf die Zielgruppe der Browser-Version ausgerichtet ist (Internet Explorer, Versionen 6, 7 oder 8)

Zielgruppen funktionieren nicht mehr.

| [!DNL Target] JavaScript-Implementierung | Details |
|--- |--- |
| Adobe Experience Platform Web SDK | Die Platform SDK wird in Internet Explorer-Versionen vor Version 10 nicht unterstützt. |
| at.js | „at.js“ wird erst ab Internet Explorer 10 unterstützt. |
