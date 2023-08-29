---
keywords: Datenschutz, IP-Adresse, GeoSegmentation, Opt-out, Opt-out, Opt-out, Datenschutz, Datenschutz, Regierungsbestimmungen, Vorschriften, DSGVO, ccpa, Datenschutz, personenbezogene Daten, personenbezogene Daten
description: Erfahren Sie mehr [!DNL Adobe Target] erfüllt die geltenden Datenschutzgesetze, einschließlich der Erfassung und Verarbeitung von IP-Adressen, PII und Opt-out-Anweisungen.
title: Wie behandelt Target Datenschutzprobleme, einschließlich PII?
feature: Privacy & Security
exl-id: 4330e034-2483-4a25-9c87-48dbef6fc9de
source-git-commit: d9ac5bab3a09cf49b2178a62c06eebe733b9048d
workflow-type: tm+mt
source-wordcount: '865'
ht-degree: 39%

---

# Datenschutz

[!DNL Adobe Target] verfügt über Prozesse und Einstellungen, die es Ihnen ermöglicht, [!DNL Target] gemäß den geltenden Datenschutzgesetzen zu verwenden.

## Erfassung von IP-Adressen und persönlich identifizierbaren Informationen (PII)

Die IP-Adresse eines Besuchers Ihrer Website wird an das Adobe-Datenverarbeitungscenter übergeben. Abhängig von der Netzwerkkonfiguration des Besuchers stellt die IP-Adresse nicht unbedingt die IP-Adresse des Computers des Besuchers dar. Bei der IP-Adresse kann es sich z. B. um die externe IP-Adresse einer Network Address Translation-(NAT-)Firewall, eines HTTP-Proxys oder eines Internet-Gateways handeln.

>[!IMPORTANT]
>
>[!DNL Target] speichert keine IP-Adressen des Benutzers oder personenbezogene Daten (PII). IP-Adressen werden nur von [!DNL Target] während der Sitzung (im Speicher, nie beibehalten).

## Ersetzen des letzten Oktetts von IP-Adressen

Adobe hat eine &quot;eingebaute Privatsphäre&quot;-Einstellung entwickelt, die Benutzer zum Adobe aktivieren können. [!DNL Target]. Wenn diese Option aktiviert ist, Adobe [!DNL Target] verschleiert sofort das letzte Oktett (den letzten Teil) der IP-Adresse zum Zeitpunkt der Erfassung der IP-Adresse. Diese Anonymisierung wird vor jeder weiteren Verarbeitung der IP-Adresse durchgeführt, auch vor einer optionalen Geo-Suche der IP-Adresse.

Wenn diese Funktion aktiviert ist, wird die IP-Adresse so stark anonymisiert, dass sie nicht mehr als persönliche Information identifiziert werden kann. Daher [!DNL Target] kann in Ländern, die die Erfassung personenbezogener Daten nicht zulassen, unter Einhaltung der Datenschutzgesetze verwendet werden. Das Ermitteln von Information auf Stadtebene wird durch die Verschleierung der IP-Adresse wahrscheinlich merklich beeinträchtigt. Das Ermitteln von Informationen auf Regions- und Landesebene dürfte nur leicht beeinträchtigt sein.

Die folgenden Einstellungen sind im [!DNL Target] Benutzeroberfläche durch Navigieren zu **[!UICONTROL Administration]** > **[!UICONTROL Implementierung]**:

* [!UICONTROL Verschleierung des letzten Oktetts]: [!DNL Target] blendet das letzte Oktett der IP-Adresse aus.
* [!UICONTROL Gesamte IP-Verschleierung]: [!DNL Target] blendet die gesamte IP-Adresse aus.
* [!UICONTROL Keines]: [!DNL Target] verdeckt keinen Teil der IP-Adresse.

  ![obfuscate-ip-options](assets/obfuscate-ip.png)

[!DNL Target] empfängt die vollständige IP-Adresse und verschleiert sie (wenn auf Letztes Oktett oder Ganze IP gesetzt) wie angegeben. [!DNL Target] speichert dann die verschleierte IP-Adresse nur während der aktuellen Sitzung im Speicher.

### IP-Verschleierung auf Datenasterebene bei Verwendung der [!DNL Adobe Experience Platform Web SDK]

Bei Verwendung von [!DNL Platform Web SDK] (Version 23.4 oder höher) hat die Einstellung der IP-Verschleierung auf Datasterebene Vorrang vor allen IP-Verschleierungsoptionen, die in [!DNL Target]. Wenn beispielsweise die IP-Verschleierungsoption auf Datenasterebene auf [!UICONTROL Voll] und [!DNL Target] Die IP-Verschleierungsoption ist auf [!UICONTROL Verschleierung des letzten Oktetts], [!DNL Target] eine vollständig verschleierte IP-Adresse erhält. Da IP-Verschleierung in [!DNL Target] vor der Geolocation-Suche eintritt, hat die Einstellung für die IP-Verschleierung auf Datenasterebene keine Auswirkungen.

Nachdem die IP-Verschleierung auf Datenasterebene festgelegt wurde und Ihre Daten über das Edge-Netzwerk verarbeitet werden, werden Anfragen an [!DNL Target] und [!DNL Adobe Audience Manager] (AAM) enthalten nur die verschleierte IP-Adresse und jede Logik, die auf der Client-IP basiert, wird von der Option IP-Verschleierung auf Datenasterebene beeinflusst. Alle in festgelegten IP-Verschleierungen [!DNL Target] oder AAM auf die bereits verschleierte IP angewendet wird.

Weitere Informationen finden Sie unter [!UICONTROL IP-Verschleierung] in [Konfigurieren eines Datenspeichers](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html){target=_blank} im *[!DNL Adobe Experience Platfrom]Datastreams-Handbuch*.

## GeoSegmentation

Wenn Sie die Ersetzung des letzten 8-Bit-Zeichens der IP-Adresse aktivieren, können die verbleibenden Werte der IP-Adresse mithilfe von Berichten unter [!DNL Target]. Wenn das letzte Oktett der IP-Adresse nicht verschleiert wurde, kann die vollständige IP-Adresse unter [!DNL Target]. Sie können die GeoSegmentation-Funktion verwenden, um den Besucherstandort nach geografischer Region abzugrenzen. GeoSegmentation-Daten sind nur auf Ebene der Stadt oder der Postleitzahl granular und nicht auf individueller Ebene.

Wenn IP-Adressen vollständig verschleiert werden, stehen GeoSegmentation und Geo-Targeting nicht zur Verfügung.

## Ausschluss-Link

Sie können einen Ausschluss-Link zu Ihren Sites hinzufügen, um Besuchern zu ermöglichen, die Zählung über und Inhaltsbereitstellung auszuschließen.

1. Fügen Sie den folgenden Link zu Ihrer Site hinzu:

   `<a href="https://clientcode.tt.omtrdc.net/optout"> Your Opt Out Language Here</a>`

1. (Bedingt) Wenn Sie CNAME verwenden, sollte der Link die Zeichenfolge &quot;client=&quot;enthalten.`clientcode` -Parameter, beispielsweise:
   `https://my.cname.domain/optout?client=clientcode`.

1. Ersetzen Sie `clientcode` durch Ihren Client-Code, und fügen Sie den Text oder das Bild hinzu, das mit der Ausschluss-URL verknüpft werden soll.

Ein Besucher, der auf diesen Link klickt, wird während der Browser-Sitzung nicht in Mbox-Anforderungen einbezogen, bis er den Cookie löscht oder nach Ablauf von zwei Jahren (je nachdem, was zuerst eintritt). Dies funktioniert durch Einsetzen eines Cookies namens `disableClient` in der Domain `clientcode.tt.omtrdc.net` für den Besucher.

Auch wenn Sie eine Erstanbieter-Cookie-Implementierung verwenden, erfolgt der Ausschluss über ein Drittanbieter-Cookie. Wenn der Client nur ein Erstanbieter-Cookie verwendet, [!DNL Target] prüft, ob ein Opt-out-Cookie gesetzt ist.

## Datenschutz und Datenschutzvorschriften

Siehe [Vorschriften zum Datenschutz](/help/dev/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.md) Informationen über die Datenschutz-Grundverordnung (DSGVO) der Europäischen Union, den California Consumer Privacy Act (CCPA) und andere internationale Datenschutzanforderungen sowie darüber, wie sich diese Vorschriften auf Ihre Organisation auswirken und [!DNL Target].

## Erfassung von Funktionsnutzungsdaten

Zu internen Adobe-Zwecken werden individuelle Nutzungsdaten erfasst, um festzustellen, ob [!DNL Target] Funktionen funktionieren wie gewünscht oder um Funktionen zu identifizieren, die nicht ausreichend genutzt werden. Es werden verschiedene Latenzwerte erfasst, um Leistungsproblemen vorzubeugen. Personenbezogene Daten werden nicht erfasst.

Sie können die Erfassung der Nutzungsdaten in unseren SDKs deaktivieren, indem Sie `telemetryEnabled` in den Client-Initialisierungsoptionen auf „false“ setzen. Weitere Informationen finden Sie unter [telemetryEnabled in targetGlobalSettings](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md#telemetryenabled).
