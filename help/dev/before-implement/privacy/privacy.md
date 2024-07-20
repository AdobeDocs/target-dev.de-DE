---
keywords: Datenschutz, IP-Adresse, GeoSegmentation, Opt-out, Opt-out, Opt-out, Datenschutz, Datenschutz, Regierungsbestimmungen, Vorschriften, DSGVO, ccpa, Datenschutz, personenbezogene Daten, personenbezogene Daten
description: Erfahren Sie, wie [!DNL Adobe Target] die geltenden Datenschutzgesetze einhält, einschließlich der Erfassung und Verarbeitung von IP-Adressen, PII und Opt-out-Anweisungen.
title: Wie behandelt Target Datenschutzprobleme, einschließlich PII?
feature: Privacy & Security
exl-id: 4330e034-2483-4a25-9c87-48dbef6fc9de
source-git-commit: 88bde40aa6dfb96e1d53e4db6ba5547d38dbbb99
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 43%

---

# Datenschutz

[!DNL Adobe Target] verfügt über Prozesse und Einstellungen, die es Ihnen ermöglicht, [!DNL Target] gemäß den geltenden Datenschutzgesetzen zu verwenden.

## Erfassung von IP-Adressen und persönlich identifizierbaren Informationen (PII)

Die IP-Adresse eines Besuchers Ihrer Website wird an das Adobe-Datenverarbeitungscenter übergeben. Abhängig von der Netzwerkkonfiguration des Besuchers stellt die IP-Adresse nicht unbedingt die IP-Adresse des Computers des Besuchers dar. Bei der IP-Adresse kann es sich z. B. um die externe IP-Adresse einer Network Address Translation-(NAT-)Firewall, eines HTTP-Proxys oder eines Internet-Gateways handeln.

>[!IMPORTANT]
>
>[!DNL Target] speichert keine IP-Adressen des Benutzers oder personenbezogene Daten (PII). IP-Adressen werden nur von [!DNL Target] während der Sitzung verwendet (im Speicher, nie beibehalten).

## Ersetzen des letzten Oktetts von IP-Adressen

Adobe hat eine &quot;eingebaute Privatsphäre&quot;-Einstellung entwickelt, die Benutzer für Adobe [!DNL Target] aktivieren können. Wenn diese Option aktiviert ist, verschleiert Adobe [!DNL Target] sofort das letzte Oktett (den letzten Teil) der IP-Adresse zum Zeitpunkt der IP-Adresserfassung. Diese Anonymisierung wird vor jeder weiteren Verarbeitung der IP-Adresse durchgeführt, auch vor einer optionalen Geo-Suche der IP-Adresse.

Wenn diese Funktion aktiviert ist, wird die IP-Adresse so stark anonymisiert, dass sie nicht mehr als persönliche Information identifiziert werden kann. Daher kann [!DNL Target] unter Einhaltung der Datenschutzgesetze in Ländern verwendet werden, die die Erfassung personenbezogener Daten nicht zulassen. Das Ermitteln von Information auf Stadtebene wird durch die Verschleierung der IP-Adresse wahrscheinlich merklich beeinträchtigt. Das Ermitteln von Informationen auf Regions- und Landesebene dürfte nur leicht beeinträchtigt sein.

Die folgenden Einstellungen sind in der Benutzeroberfläche von [!DNL Target] verfügbar, indem Sie zu **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** navigieren:

* [!UICONTROL Last octet obfuscation]: [!DNL Target] blendet das letzte Oktett der IP-Adresse aus.
* [!UICONTROL Entire IP obfuscation]: [!DNL Target] blendet die gesamte IP-Adresse aus.
* [!UICONTROL None]: [!DNL Target] blendet keinen Teil der IP-Adresse aus.

  ![obfuscate-ip-options](assets/obfuscate-ip.png)

[!DNL Target] erhält die vollständige IP-Adresse und verschleiert sie (wenn auf Letztes Oktett oder Ganze IP gesetzt) wie angegeben. [!DNL Target] speichert dann die verschleierte IP-Adresse nur während der aktuellen Sitzung im Speicher.

### IP-Verschleierung auf Datenspeicherebene bei Verwendung von [!DNL Adobe Experience Platform Web SDK] {#aep}

Bei Verwendung von [!DNL Platform Web SDK] (Version 23.4 oder höher) hat die Einstellung für die IP-Verschleierung auf Datasterebene Vorrang vor allen in [!DNL Target] festgelegten IP-Verschleierungsoptionen. Wenn beispielsweise die Option für die IP-Verschleierung auf Datastream-Ebene auf [!UICONTROL Full] gesetzt ist und die Option für die IP-Verschleierung auf [!UICONTROL Last octet obfuscation] eingestellt ist, erhält [!DNL Target] eine vollständig verschleierte IP.[!DNL Target]

Weitere Informationen finden Sie unter [!UICONTROL IP Obfuscation] in [Konfigurieren eines Datastreams](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=de){target=_blank} im *[!DNL Adobe Experience Platfrom]Datastreams-Handbuch*.

## GeoSegmentation

Wenn Sie das Ersetzen des letzten 8-Bit-Zeichens der IP-Adresse aktivieren, können die verbleibenden Werte der IP-Adresse mithilfe von Berichten in [!DNL Target] analysiert werden. Wenn das letzte Oktett der IP-Adresse nicht verschleiert wurde, kann die vollständige IP-Adresse in [!DNL Target] analysiert werden. Sie können die GeoSegmentation-Funktion verwenden, um den Besucherstandort nach geografischer Region abzugrenzen. GeoSegmentation-Daten sind nur auf Ebene der Stadt oder der Postleitzahl granular und nicht auf individueller Ebene.

Wenn IP-Adressen vollständig verschleiert werden, stehen GeoSegmentation und Geo-Targeting nicht zur Verfügung.

## Ausschluss-Link

Sie können einen Ausschluss-Link zu Ihren Sites hinzufügen, um Besuchern zu ermöglichen, die Zählung über und Inhaltsbereitstellung auszuschließen.

1. Fügen Sie den folgenden Link zu Ihrer Site hinzu:

   `<a href="https://clientcode.tt.omtrdc.net/optout"> Your Opt Out Language Here</a>`

1. (Bedingt) Wenn Sie CNAME verwenden, sollte der Link den Parameter &quot;client=`clientcode` enthalten, z. B.:
   `https://my.cname.domain/optout?client=clientcode`.

1. Ersetzen Sie `clientcode` durch Ihren Client-Code, und fügen Sie den Text oder das Bild hinzu, das mit der Ausschluss-URL verknüpft werden soll.

Ein Besucher, der auf diesen Link klickt, wird während der Browser-Sitzung nicht in Mbox-Anforderungen einbezogen, bis er den Cookie löscht oder nach Ablauf von zwei Jahren (je nachdem, was zuerst eintritt). Dies funktioniert durch Einsetzen eines Cookies namens `disableClient` in der Domain `clientcode.tt.omtrdc.net` für den Besucher.

Auch wenn Sie eine Erstanbieter-Cookie-Implementierung verwenden, erfolgt der Ausschluss über ein Drittanbieter-Cookie. Wenn der Client nur ein Erstanbieter-Cookie verwendet, prüft [!DNL Target], ob ein Opt-out-Cookie gesetzt ist.

## Datenschutz und Datenschutzvorschriften

Unter [Datenschutz- und Datenschutzbestimmungen](/help/dev/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.md) finden Sie Informationen über die Datenschutz-Grundverordnung (DSGVO) der Europäischen Union, den California Consumer Privacy Act (CCPA) und andere internationale Datenschutzanforderungen sowie darüber, wie sich diese Vorschriften auf Ihre Organisation und [!DNL Target] auswirken.

## Erfassung von Funktionsnutzungsdaten

Zu internen Adobe Zwecken werden individuelle Nutzungsdaten für Funktionen erfasst, um festzustellen, ob die Funktionen von [!DNL Target] die gewünschte Leistung erbringen oder um Funktionen zu identifizieren, die nicht ausreichend genutzt werden. Es werden verschiedene Latenzwerte erfasst, um Leistungsproblemen vorzubeugen. Personenbezogene Daten werden nicht erfasst.

Sie können die Erfassung der Nutzungsdaten in unseren SDKs deaktivieren, indem Sie `telemetryEnabled` in den Client-Initialisierungsoptionen auf „false“ setzen. Weitere Informationen finden Sie unter [telemetryEnabled in targetGlobalSettings](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md#telemetryenabled).
