---
title: Konfigurieren der Authentifizierung für [!DNL Adobe Target] APIs
description: Wie generiere ich Authentifizierungstoken, die für eine erfolgreiche Interaktion mit [!DNL Adobe Target] APIs?
feature: APIs/SDKs, Administration & Configuration
exl-id: fc67363c-6527-40aa-aff1-350b5af884ab
source-git-commit: 2fba03b3882fd23a16342eaab9406ae4491c9044
workflow-type: tm+mt
source-wordcount: '1942'
ht-degree: 2%

---

# Authentifizierung für [!DNL Adobe Target] APIs

Die [!DNL Adobe Target] Admin-APIs, einschließlich [!DNL Recommendations Admin] APIs werden durch Authentifizierung gesichert, um sicherzustellen, dass nur autorisierte Benutzer sie für den Zugriff verwenden [!DNL Adobe Target]. Verwenden Sie die [Adobe Developer-Konsole](https://developer.adobe.com/console/home) um diese Authentifizierung für alle [!DNL Adobe Experience Cloud solutions], einschließlich [!DNL Adobe Target].

>[!IMPORTANT]
>
>Die in diesem Artikel beschriebenen Anmeldedaten für Dienstkonten (JWT) werden nicht mehr zugunsten der neuen OAuth Server-zu-Server-Anmeldedaten unterstützt.
>
>Die Anmeldedaten für das Dienstkonto (JWT) funktionieren bis zum 1. Januar 2025 weiterhin. Sie müssen Ihre Anwendung oder Integration migrieren, um die neue OAuth-Server-zu-Server-Berechtigung vor dem 1. Januar 2025 zu verwenden.
>
>Weitere Informationen und schrittweise Anweisungen zum Migrieren Ihrer Integration finden Sie unter [Migration von JWT-Anmeldedaten (Service Account) zu OAuth-Server-zu-Server-Anmeldedaten](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/){target=_blank} im *Entwicklerkonsole* Dokumentation.
>
>Informationen zum Einrichten neuer OAuth-Anmeldeinformationen finden Sie unter [OAuth-Implementierung von Server-zu-Server-Anmeldedaten](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation/){target=_blank} im *Entwicklerkonsole* Dokumentation.

Im Folgenden finden Sie die ersten Schritte, die zum Generieren der Legacy-JWT-Authentifizierungstoken erforderlich sind, um erfolgreich mit [!DNL Adobe Target] APIs:

1. Erstellen Sie ein Projekt (zuvor als Integration bezeichnet) im [!DNL Adobe Developer Console].
1. Exportieren Sie Projektdetails in Postman.
1. Generieren Sie ein Bearer-Zugriffstoken.
1. Testen Sie das Trägerzugriffs-Token.

## Voraussetzungen

| Ressource | Details |
| --- | --- |
| Postman | Um diese Schritte erfolgreich abzuschließen, rufen Sie die [Postman-App](https://www.postman.com/downloads/) für Ihr Betriebssystem. Postman Basic ist mit der Kontoerstellung kostenlos. Für die Verwendung von [!DNL Adobe Target] -APIs im Allgemeinen vereinfacht Postman API-Workflows und [!DNL Adobe Target] bietet mehrere Postman-Sammlungen, die die Ausführung der APIs und deren Funktionsweise erleichtern. Der Rest dieses Handbuchs setzt Grundkenntnisse in Postman voraus. Weitere Informationen finden Sie im Abschnitt [Postman-Dokumentation](https://learning.getpostman.com/). |
| Verweise | Im Rest dieses Handbuchs wird davon ausgegangen, dass Sie mit den folgenden Ressourcen vertraut sind:<ul><li>[Adobe I/O Github](https://github.com/adobeio)</li><li>[Dokumentation zur Target-Admin- und Profil-API](../administer/admin-api/admin-api-overview-new.md)</li><li>[Dokumentation zur Recommendations API](https://developer.adobe.com/target/administer/recommendations-api/)</li></ul> |

## Erstellen eines Adobe I/O-Projekts

In diesem Abschnitt greifen Sie auf die [!DNL Adobe Developer Console] und ein Projekt für [!DNL Adobe Target]. Weitere Informationen finden Sie unter [Dokumentation zu Projekten](https://developer.adobe.com/developer-console/docs/guides/projects/).

&lt;!---(1. Generieren Sie Ihren privaten Schlüssel und Ihr öffentliches Zertifikat gemäß [Dokumentation zur Authentifizierung](https://developer.adobe.com/developer-console/docs/guides/authentication/). // [//]: # (wie beschrieben in **Schritt 1** von [Einrichten von Adobe IO: Authentifizierung - Schritt für Schritt](https://helpx.adobe.com/marketing-cloud-core/kb/adobe-io-authentication-step-by-step.html). Kehren Sie nach Abschluss von Schritt 1 zu diesem Handbuch zurück und fahren Sie mit Schritt 2 unten fort. // Das Ergebnis dieses Schritts sollte die Erstellung einer `private.key` und eine `certificate_pub.crt` -Datei. Kehren Sie nach der Erstellung dieser beiden Dateien zu diesem Handbuch zurück.)—>

1. Im [Adobe Admin Console](https://adminconsole.adobe.com/), stellen Sie sicher, dass [!DNL Adobe] Das Benutzerkonto wurde sowohl [Produktadministrator](https://helpx.adobe.com/enterprise/using/admin-roles.html) und [Entwickler](https://helpx.adobe.com/enterprise/using/manage-developers.html) Zugriff auf Ebene [!DNL Target].

1. Im [Adobe Developer-Konsole](https://developer.adobe.com/console/home), wählen Sie die [!UICONTROL Experience Cloud-Organisation] für die Sie diese Integration erstellen möchten. (Beachten Sie, dass Sie wahrscheinlich nur Zugriff auf eine [!UICONTROL Experience Cloud-Organisation].

   ![configure-io-target-createproject2.png](assets/configure-io-target-createproject2.png)

1. Klicks **[!UICONTROL Neues Projekt erstellen]**.

   ![configure-io-target-createproject3.png](assets/configure-io-target-createproject3.png)

1. Klicks **[!UICONTROL API hinzufügen]** , um Ihrem Projekt eine REST-API für den Zugriff auf hinzuzufügen [!DNL Adobe] Dienstleistungen und Produkte.

   ![API hinzufügen](assets/configure-io-target-createproject4.png)

1. Auswählen **[!DNL Adobe Target]** als [!DNL Adobe] Service, mit dem Sie integrieren möchten. Klicken Sie auf **[!UICONTROL Nächste]** -Schaltfläche angezeigt.

   ![configure-io-target-createproject5](assets/configure-io-target-createproject5.png)

1. Wählen Sie eine Option zum Verknüpfen öffentlicher und privater Schlüssel mit der Dienstkontointegration aus, für die Sie erstellen [!DNL Target]. Wählen Sie für dieses Beispiel **[!UICONTROL Option 1: Generieren eines Schlüsselpaars]** und klicken **[!UICONTROL Generieren von keypair]**.

   ![configure-io-target-createproject6](assets/configure-io-target-createproject6.png)

1. Notieren Sie sich, wie angegeben, die automatisch heruntergeladene Konfigurationsdatei (`config`), die Ihren privaten Schlüssel enthält. Klicken Sie auf **[!UICONTROL Weiter]**.

   ![configure-io-target-createproject7](assets/configure-io-target-createproject7.png)

1. Überprüfen Sie in Ihrem Dateisystem den Speicherort von `config`: die komprimierte Konfigurationsdatei, die im vorherigen Schritt erstellt wurde. Auch dies `config` enthält Ihren privaten Schlüssel, den Sie später benötigen werden. Der genaue Speicherort in Ihrem Dateisystem kann sich von dem hier gezeigten unterscheiden.

   ![configure-io-target-createproject8](assets/configure-io-target-createproject8.png)

1. Wählen Sie in der Adobe Developer Console die [Produktprofil(e)](https://helpx.adobe.com/de/enterprise/using/manage-products-and-profiles.html) entspricht den Eigenschaften, in denen Sie Adobe Recommendations verwenden. (Wenn Sie keine Eigenschaften verwenden, wählen Sie die Option Standardarbeitsbereich .) Klicks **[!UICONTROL Konfigurierte API speichern]**.

   ![configure-io-target-createproject9](assets/configure-io-target-createproject9.png)

1. Klicks **[!UICONTROL Integration erstellen]**. Sie sollten eine temporäre Meldung erhalten, die angibt, dass Ihre API erfolgreich konfiguriert wurde.
1. Benennen Sie Ihr Projekt als letzten Schritt in einen aussagekräftigeren Namen als den ursprünglichen. `Project 1`. Navigieren Sie dazu mithilfe des Navigationspfads wie angezeigt zum Projekt und klicken Sie auf **[!UICONTROL Projekt bearbeiten]** , um auf die **[!UICONTROL Projekt bearbeiten]** -Modal verwenden und das Projekt umbenennen.

   ![configure-io-target-createproject11](assets/configure-io-target-createproject11.png)

>[!NOTE]
>
>In diesem Beispiel nennen wir unser Projekt &quot;[!DNL Target] Integration.&quot; Wenn Sie davon ausgehen, Ihr Projekt für mehr als nur [!DNL Adobe Target], können Sie ihn entsprechend benennen. Sie können ihn beispielsweise &quot;Adobe-APIs&quot;oder &quot;Experience Cloud-APIs&quot;nennen, da er mit anderen Lösungen in der Adobe Experience Cloud verwendet werden kann.

## Exportieren von Projektdetails

Jetzt, da Sie über ein Adobe-Projekt verfügen, können Sie auf [!DNL Target]müssen Sie sicherstellen, dass Sie Details zu diesem Projekt zusammen mit Ihren Adobe-API-Anfragen senden. Diese Details sind erforderlich, um mit mehreren Adobe-APIs, darunter mehreren [!DNL Target] APIs. Die Integrationsdetails umfassen beispielsweise Autorisierungs- und Authentifizierungsinformationen, die für die [!DNL Target] Admin-APIs. Um die APIs mit Postman zu verwenden, müssen Sie daher diese Details in Postman übertragen.

Es gibt viele Möglichkeiten, die Details Ihres Projekts in Postman anzugeben. In diesem Abschnitt nutzen wir jedoch einige vordefinierte Funktionen und Sammlungen. Zunächst (in diesem Abschnitt) exportieren Sie die Details Ihrer Integration in eine Postman-Umgebung. Als Nächstes generieren Sie ein Bearer-Zugriffstoken, um Ihnen Zugriff auf die erforderlichen Adobe-Ressourcen zu gewähren.

>[!NOTE]
>
>Für Videoanleitungen für alle Experience Cloud-Lösungen, einschließlich [!DNL Target], siehe [Verwenden von Postman mit Experience Platform-APIs](https://experienceleague.adobe.com/docs/platform-learn/tutorials/platform-api-authentication.html). Die folgenden Abschnitte sind für die [!DNL Target] APIs: 1. Erstellen und exportieren Sie die Experience Platform-API in Postman 2. Generieren Sie ein Zugriffstoken mit Postman. Diese Schritte werden im Folgenden beschrieben.

1. Noch im [Adobe Developer-Konsole](https://developer.adobe.com/console/home), navigieren Sie zu , um die **[!UICONTROL Dienstkonto (JWT)]** Anmeldedaten. Verwenden Sie entweder die linke Navigation oder die **[!UICONTROL Anmeldeinformationen]** -Abschnitt angezeigt.

   ![JWT1](assets/configure-io-target-jwt1.png)

   In **[!UICONTROL Details zu Berechtigungen]**, beachten Sie, dass Sie Ihre **[!UICONTROL Öffentliche Schlüssel]**, **[!UICONTROL Client-ID]** und andere Informationen zu Ihrem Dienstkonto.

   ![JWT1a](assets/configure-io-target-jwt1a.png)

1. Klicken Sie auf , um zu Informationen zum **[!DNL Adobe Target]** API. Verwenden Sie entweder die linke Navigation oder die **Verbundene Produkte und Dienste** -Abschnitt angezeigt.

   ![JWT2](assets/configure-io-target-jwt2.png)

1. Klicks **[!UICONTROL Herunterladen für Postman]** > **[!UICONTROL Dienstkonto (JWT)]** , um eine JSON-Datei zu erstellen, die Ihre Authentifizierungsinformationen für eine Postman-Umgebung erfasst.

   ![JWT3](assets/configure-io-target-jwt3.png)

   Notieren Sie die JSON-Datei in Ihrem Dateisystem.

   ![JWT3a](assets/configure-io-target-jwt3a.png)

1. Klicken Sie in Postman auf das Zahnradsymbol, um Ihre Umgebungen zu verwalten, und klicken Sie dann auf **[!UICONTROL Import]** , um die JSON-Datei (Umgebung) zu importieren.

   ![JWT4](assets/configure-io-target-jwt4.png)

1. Wählen Sie Ihre Datei aus und klicken Sie auf **[!UICONTROL Öffnen]**.

   ![JWT5](assets/configure-io-target-jwt5.png)

1. In der Postman **Verwalten von Umgebungen** modal klicken Sie auf den Namen der neu importierten Umgebung, um sie zu überprüfen. (Ihr Umgebungsname kann sich von dem hier gezeigten unterscheiden. Bearbeiten Sie den Namen nach Bedarf. Es muss nicht unbedingt mit dem Namen der [!DNL Adobe] Projekt.)

   ![JWT6](assets/configure-io-target-jwt6.png)

1. Hinweis `CLIENT_SECRET` und `API_KEY` (zusammen mit anderen Variablen) deren Werte vorausgefüllt werden, die aus Ihrer Integration stammen, wie in der Adobe Developer-Konsole definiert. (Die Postman `CLIENT_SECRET` sollte mit der Variablen `CLIENT SECRET` Adobe-Anmeldedaten, wie in der Developer Console angezeigt, und `API_KEY` in Postman sollte ebenfalls `CLIENT ID` in der Entwicklerkonsole.) Beachten Sie hingegen `PRIVATE_KEY`, `JWT_TOKEN`, und `ACCESS_TOKEN` leer sind. Beginnen wir mit der Bereitstellung der `PRIVATE_KEY` -Wert.

   ![JWT7](assets/configure-io-target-jwt7.png)

1. Öffnen Sie in Ihrem Dateisystem Ihre `config` und öffnen Sie die `private` Schlüsseldatei.

   ![JWT8](assets/configure-io-target-jwt8.png)

1. Gesamten Inhalt der `private` Schlüsseldatei.

   ![JWT9](assets/configure-io-target-jwt9.png)

1. Fügen Sie in Postman Ihren privaten Schlüsselwert in die **[!UICONTROL ERSTER WERT]** und **[!UICONTROL AKTUELLER Wert]** -Felder.

   ![JWT10](assets/configure-io-target-jwt10.png)

1. Klicks **[!UICONTROL Aktualisieren]** und schließen Sie das Modal Umgebungen .

## Bearer-Zugriffstoken generieren

In diesem Abschnitt generieren Sie Ihr Bearer-Zugriffstoken, das zur Authentifizierung Ihrer Interaktion mit [!DNL Adobe Target] APIs. Um Ihr Bearer-Zugriffstoken zu generieren, müssen Sie Ihre Integrationsdetails (wie in den vorherigen Abschnitten beschrieben) an die [Adobe Identity Management Service (IMS)](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/AuthenticationOverview/AuthenticationGuide.md). Es gibt verschiedene Möglichkeiten, dies zu tun. In diesem Handbuch nutzen wir jedoch eine Postman-Sammlung mit einem vordefinierten IMS-Aufruf, der den Prozess direkt und einfach macht. Nachdem Sie die Sammlung importiert haben, können Sie sie bei Bedarf wiederverwenden, um neue Token zu generieren, nicht nur für [!DNL Adobe Target], aber auch andere Adobe-APIs.

1. Navigieren Sie zum [Beispielaufrufe für Adobe Identity Management Service-API](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims).

   ![token1](assets/configure-io-target-generatetoken1.png)

1. Klicken Sie auf **[!UICONTROL Postman-Sammlung zur Generierung von Adobe I/O-Zugriffstoken]**.

   ![token2](assets/configure-io-target-generatetoken2.png)

1. Rufen Sie die JSON-Rohdaten für diese Sammlung ab, indem Sie auf **[!UICONTROL Roh]**, kopieren Sie dann die resultierende JSON in die Zwischenablage. (Alternativ können Sie die JSON-Rohdatei als JSON-Datei speichern.)

   ![token3](assets/configure-io-target-generatetoken3.png)

1. Importieren Sie die Sammlung in Postman, indem Sie die JSON-Rohdaten aus der Zwischenablage einfügen und senden. (Alternativ können Sie die von Ihnen gespeicherte JSON-Datei hochladen.) Klicken Sie auf **[!UICONTROL Weiter]**.

   ![token4](assets/configure-io-target-generatetoken4.png)

1. Wählen Sie die **[!UICONTROL IMS: JWT-Generierung + Auth über Benutzer-Token]** Anforderung in der Postman-Sammlung &quot;Adobe I/O Access Token Generation&quot;, stellen Sie sicher, dass Ihre Umgebung ausgewählt ist, und klicken Sie auf **[!UICONTROL Senden]** , um das Token zu generieren.

   ![token5](assets/configure-io-target-generatetoken5.png)

   >[!NOTE]
   >
   >Dieses Bearer-Zugriffstoken ist 24 Stunden lang gültig. Senden Sie die Anfrage erneut, sobald Sie ein neues Token generieren müssen.

1. Öffnen Sie erneut das Modal Umgebungen verwalten und wählen Sie Ihre Umgebung aus.

   ![token6](assets/configure-io-target-jwt11.png)

1. Beachten Sie die `ACCESS_TOKEN` und `JWT_TOKEN` -Werte werden nun ausgefüllt.

   ![token7](assets/configure-io-target-generatetoken7.png)

Frage: Muss ich die Postman-Sammlung &quot;Adobe I/O Access Token Generation&quot;verwenden, um das JSON Web Token (JWT) und das Trägerzugriffstoken zu generieren?

Antwort: Nein. Die Postman-Sammlung zur Adobe I/O-Zugriffstoken-Generierung ist verfügbar, um das JWT- und Trägerzugriffstoken in Postman einfacher zu generieren. Alternativ können Sie Funktionen in der Adobe Developer-Konsole verwenden, um das Trägerzugriffstoken manuell zu generieren.

## Testen des Trägerzugriffs-Tokens

In dieser Übung verwenden Sie Ihr neues Bearer-Zugriffstoken, indem Sie eine API-Anfrage senden, die eine Liste der Aktivitäten von Ihrer [!DNL Target] -Konto. Eine erfolgreiche Antwort zeigt Ihre [!DNL Adobe] -Projekt und -Authentifizierung funktionieren erwartungsgemäß, um die API zu verwenden.

1. Importieren Sie [[!DNL Adobe Target] Postman-Sammlung für Admin-APIs](https://developers.adobetarget.com/api/#admin-postman-collection). Befolgen Sie alle Anweisungen, bis die Sammlung in Postman importiert wurde.

   ![testtoken1](assets/configure-io-target-testtoken0.png)

1. Erweitern Sie die Sammlung und beachten Sie die **[!UICONTROL Aktivitäten auflisten]** -Anfrage.

   ![testtoken1](assets/configure-io-target-testtoken1.png)

1. Beachten Sie, dass Variablen wie `{{access_token}}` zunächst ungelöst sind. Sie können dies auf verschiedene Weise beheben. Beispielsweise können Sie eine neue Kollektionsvariable mit dem Namen `{{access_token}}`- In diesem Handbuch ändern Sie stattdessen die API-Anfrage, um die zuvor verwendete Postman-Umgebung zu nutzen. Dadurch kann die Umgebung auch weiterhin als einheitliche, konsistente Konsolidierung aller Variablen dienen, die in allen Adobe-APIs verwendet werden.

   ![testtoken2](assets/configure-io-target-testtoken2.png)

1. Ersetzender Typ `{{access_token}}` mit `{{ACCESS_TOKEN}}`.

   ![testtoken3](assets/configure-io-target-testtoken3.png)

1. Ersetzender Typ `{{api_key}}` mit `{{API_KEY}}`.

   ![testtoken4](assets/configure-io-target-testtoken4.png)

1. Ersetzender Typ `{{tenant}}` mit `{{TENANT_ID}}`. Hinweis `{{TENANT_ID}}` noch nicht erkannt wurde.

   ![testtoken4](assets/configure-io-target-testtoken4a.png)

1. Öffnen Sie das Modal Umgebungen verwalten und wählen Sie Ihre Umgebung aus.

   ![JWT11](assets/configure-io-target-jwt11.png)

1. Typ zum Hinzufügen eines neuen `{{TENANT_ID}}` Umgebungsvariable. Kopieren Sie den Wert Ihrer Mandanten-ID und fügen Sie ihn in die **[!UICONTROL ERSTER WERT]** und **[!UICONTROL AKTUELLER Wert]** -Felder für Ihre neue `TENANT_ID` Umgebungsvariable.

   ![testtoken5](assets/configure-io-target-testtoken5.png)

   >[!NOTE]
   >
   >Die Mandantenkennung unterscheidet sich von Ihrer [!DNL Target] `clientcode`. Die Mandanten-ID ist in der URL vorhanden, wenn Sie sich bei [!DNL Target]. Um Ihre Mandantenkennung zu erhalten, melden Sie sich bei der Adobe Experience Cloud an, öffnen Sie [!DNL Target]und klicken Sie auf die Target -Karte. Verwenden Sie den Wert der Mandanten-ID, wie in der URL-Subdomäne angegeben. Wenn beispielsweise Ihre URL bei [!DNL Adobe Target] is `<https://mycompany.experiencecloud.adobe.com/...>` lautet dann Ihre Mandantenkennung &quot;mycompany&quot;.

1. Senden Sie Ihre Anfrage, nachdem Sie sichergestellt haben, dass Sie die richtige Umgebung ausgewählt haben. Sie sollten eine Antwort mit Ihrer Aktivitätenliste erhalten.

   ![testtoken6](assets/configure-io-target-testtoken6.png)

Nachdem Sie Ihre Adobe-Authentifizierung überprüft haben, können Sie damit interagieren [!DNL Adobe Target] APIs (sowie andere Adobe-APIs). Sie können beispielsweise [Verwenden von Recommendations-APIs](recs-api/overview.md) , um Empfehlungen zu erstellen oder zu verwalten, oder Sie können sie mit der [Target-Bereitstellungs-API](/help/dev/implement/delivery-api/overview.md).
