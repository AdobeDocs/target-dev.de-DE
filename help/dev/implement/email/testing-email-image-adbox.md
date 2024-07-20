---
keywords: E-Mail, AdBox, E-Mail-Bild-AdBox
description: Erfahren Sie, wie Sie mit [!DNL Adobe Target] Bilder dynamisch in E-Mails testen und diese Bilder gegebenenfalls im Handumdrehen ändern können, wenn jemand die E-Mail öffnet.
title: Wie teste ich eine E-Mail-Bild-AdBox?
feature: Implement Email
exl-id: 4512741a-567f-41bb-9721-3e1c4f5302e1
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 79%

---

# Testen einer E-Mail-Bild-AdBox

Testen Sie dynamisch Bilder in E-Mails und ändern Sie diese Bilder gegebenenfalls im Handumdrehen, wenn jemand die E-Mail öffnet.

Weiterleitungen in E-Mails können genutzt werden, um Klicks nachzuverfolgen und dynamisch zu steuern, auf welche Landingpages Personen geleitet werden.

Zum Testen von E-Mail-Bildern werden modifizierte Versionen von AdBoxes verwendet. Da E-Mail-Clients keine Cookies zulassen, muss für jede E-Mail eine eindeutige Kennung erzeugt werden. Diese Nummer wird an die AdBox-URL und sämtliche in der E-Mail verwendeten Weiterleitungen angehängt, um Klicks aus der E-Mail zurückzuverfolgen.

>[!NOTE]
>
>Obwohl [!DNL Target] die Bildoptimierung technisch zum Zeitpunkt der Öffnung bereitstellen kann, verarbeitet jeder E-Mail-Client die Zwischenspeicherung unterschiedlich, sodass der Erfolg variiert. Unabhängig von dem verwenden E-Mail-Anbieter bestimmt der vom Endbenutzer zum Öffnen der E-Mail verwendete Client (Gmail-App, Outlook, Hotmail usw.), ob das Bild tatsächlich beim Öffnen abgerufen wird. Gmail speichert beispielsweise fast alles zwischen, sodass es davon abhängt, wann Gmail ein Bild abruft und speichert, welches Bild Benutzern angezeigt wird.

**Beispielcode für eine Bild-AdBox in einer E-Mail:**

```
<img src="https://{clientcode}.tt.omtrdc.net/m2/​{clientcode}/ubox/​image?
mbox={email_header}&
mboxDefault=​{http%3A%2F%2Fwww.domain.com%2Fheader.jpg}&
mboxXDomain=disabled&
mboxSession={123456}&
mboxPC={123456}" border=:"0"/>
```

Hierbei sind die unten stehenden Werte spezifisch für Sie:

| Wert | Beschreibung |
|--- |--- |
| clientcode | Clientcode Ihres Unternehmens. In at.js ist dies als `clientCode='yourclientcode'` gelistet. Er besteht ausschließlich aus Kleinbuchstaben ohne Sonderzeichen. |
| image | Der Angebotstyp. Er ist immer „image“ für Grafikanzeigen und „page“ für Weiterleitungen. |
| email_header | Der Name der AdBox. |
| `mboxDefault=http%3A%2F%2Fwww.domain.com%2Fheader.jpg` | Erforderlich. Ersetzen Sie die URL durch den entsprechenden Standardinhalt für Ihre AdBox. Hierbei muss es sich um einen URL-codierten, absoluten Verweis handeln. |
| `mboxXDomain=disabled` | Weist [!DNL Target] an, kein Cookie zu setzen. |
| `mboxSession=123456` und `mboxPC=123456` | Zwei Werte, die für [!DNL Target] erforderlich sind, um dieses Benutzerprofil mit dem vorhandenen Profil für Ihre Site zusammenzuführen. 123456 ist die eindeutige Kennung, die für die E-Mail erzeugt wird. Fügen sie diesen Wert dynamisch in jede AdBox- und Weiterleitungs-URL ein. Diese Nummer muss für jede gesendete E-Mail eindeutig sein. Wird eine wöchentliche E-Mail an 1.000 Personen gesendet, müssen also 1.000 eindeutige Kennungen erzeugt werden.<br />Die eindeutige E-Mail-Kennung muss mboxSession und mboxPC in jeder AdBox- und Weiterleitungs-URL zugewiesen werden. Zeitstempel-NNNNN ist das empfohlene Format für diese Kennzeichnung, wobei NNNNN eine zufällige fünfstellige Zahl ist. Jedes alphanumerische Format ist zulässig. Einige Services für Massen-E-Mails sowie jede Programmiersprache sind zur Erzeugung dieser eindeutigen Kennung in der Lage. |
