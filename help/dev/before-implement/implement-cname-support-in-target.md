---
keywords: Client Care;CNAME;Zertifikatprogramm;kanonischer Name;Cookies;Zertifikat;AMC;Adobe Managed Certificate;DigiCert;Domain Control Validation;DCV
description: Arbeiten Sie  [!DNL Adobe]  der Kundenunterstützung zusammen, um die CNAME-Unterstützung (Canonical Name [!DNL Adobe Target]  zu implementieren und Probleme mit der Anzeigenblockierung zu beheben.
title: Wie verwende ich CNAME in Target?
feature: Privacy & Security
role: Developer
exl-id: bf533771-6d46-48ba-964c-3ad9ce9f7352
TQID: https://experienceleague.adobe.com/gTS60hypD2WGc2fJh-sUkq2-pkzt2KnM4CzSQ050L40
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: d095671a-1355-40aa-8b5f-06c33c68080bid: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 1313
ht-degree: 1%

---

# CNAME und [!DNL Target]

Anweisungen für die Arbeit mit [!DNL Adobe] Client Care zur Implementierung der CNAME-Unterstützung (Canonical Name) in [!DNL Adobe Target]. Verwenden Sie CNAME, um Probleme mit Anzeigen oder Sperren von ITP-bezogenen (Intelligent Tracking Prevention) Cookie-Richtlinien zu behandeln. Mit CNAME wird eine Domain aufgerufen, die dem Kunden gehört, und keine Domain, die [!DNL Adobe] gehört.

## CNAME-Unterstützung in [!DNL Target] anfordern

1. Bestimmen Sie die Liste der Hostnamen, die Sie für Ihr SSL-Zertifikat benötigen (siehe FAQ unten).
1. [Füllen Sie dieses Formular aus](/help/dev/implement/assets/FPC_Request_Form.xlsx) und fügen Sie es ein, wenn Sie [ein Ticket für die  [!DNL Adobe] -Kundenunterstützung öffnen, um CNAME-Unterstützung anzufordern](https://experienceleague.adobe.com/en/docs/target/using/cmp-resources-and-contact-information#reference_ACA3391A00EF467B87930A450050077C):

   * [!DNL Adobe Target] Clientcode:
   * Hostnamen für SSL-Zertifikate (Beispiel: `target.example.com target.example.org`):
   * SSL-Zertifikatkäufer ([!DNL Adobe] wird dringend empfohlen, siehe FAQ): Adobe/Kunde
   * Wenn der Kunde das Zertifikat, auch bekannt als „Bring Your Own Certificate“ (BYOC), kauft, füllen Sie diese zusätzlichen Details aus:

      * Zertifikatorganisation (Beispiel: Firma Inc):
      * Organisationseinheit des Zertifikats (optional, Beispiel: Marketing):
      * Zertifikatland (Beispiel: USA):
      * Zertifikatstaat/-region (Beispiel: Kalifornien):
      * Zertifikatstadt (Beispiel: San Jose):

1. Für jede Hostnamenanforderung erstellt Adobe die Implementierung und kehrt mit einem CNAME-Datensatznamen zurück, den Sie erstellen können. Dieser enthält eine zufällige Zeichenfolge mit dem Suffix `tt.omtrdc.net`

   Wenn Sie beispielsweise eine Anfrage für `target.example.com` gestellt haben, senden wir Ihnen einen CNAME in Form von `abcdefgh.tt.omtrdc.net` zurück. Ihr DNS-CNAME-Eintrag sollte in etwa wie folgt aussehen:

   ```
   target.example.com.  IN  CNAME  abcdefgh.tt.omtrdc.net.
   ```

   >[!IMPORTANT]
   >
   >Die Zertifizierungsstelle von [!DNL Adobe], DigiCert, kann erst dann ein Zertifikat ausstellen, wenn dieser Schritt abgeschlossen ist. Daher können [!DNL Adobe] Ihre Anfrage nach einer CNAME-Implementierung erst erfüllen, wenn dieser Schritt abgeschlossen ist.

1. Wenn [!DNL Adobe] das Zertifikat kauft, kauft [!DNL Adobe] mit DigiCert Ihr Zertifikat und stellt es auf [!DNL Adobe] Produktions-Servern bereit.

   Wenn der Kunde das Zertifikat (BYOC) erwirbt, sendet Ihnen [!DNL Adobe] Kundenunterstützung die Certificate Signing Request (CSR). Verwenden Sie die CSR beim Kauf des Zertifikats über Ihre Zertifizierungsstelle Ihrer Wahl. Senden Sie nach Ausstellung des Zertifikats eine Kopie des Zertifikats und aller Zwischenzertifikate zur Bereitstellung an [!DNL Adobe] Kundenunterstützung.

   [!DNL Adobe] Kundenunterstützung benachrichtigt Sie, wenn Ihre Implementierung bereit ist.

1. Aktualisieren Sie den `serverDomain` ([documentation](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md#serverDomain)) auf den neuen CNAME-Hostnamen und legen Sie `overrideMboxEdgeServer` in Ihrer at.js-Konfiguration auf `false` ([documentation](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md#overridemboxedgeserver)) fest.

## Häufig gestellte Fragen

Mit den folgenden Informationen werden häufig gestellte Fragen zur Anfrage und Implementierung von CNAME-Unterstützung in [!DNL Target] beantwortet:

### Kann ich mein eigenes Zertifikat (bringen Sie Ihr eigenes Zertifikat oder BYOC)?

Sie können Ihr eigenes Zertifikat bereitstellen. [!DNL Adobe] raten jedoch dringend davon ab. Die Verwaltung des Lebenszyklus des SSL-Zertifikats ist sowohl für [!DNL Adobe] als auch für Sie einfacher, wenn [!DNL Adobe] das Zertifikat kauft und kontrolliert. Die Lebensdauer von SSL-Zertifikaten wird nur kürzer (siehe nächster Abschnitt zur Zertifikatlebensdauer). Daher muss sich [!DNL Adobe] Kundenunterstützung jedes Mal an Sie wenden, um rechtzeitig ein neues Zertifikat zu erhalten. Dies wird zu einer Herausforderung, wenn die Gültigkeitsdauer des Zertifikats auf nur 47 Tage verkürzt wird. Ihre [!DNL Target]-Implementierung ist gefährdet, wenn das Zertifikat abläuft, da Browser Verbindungen verweigern.

>[!IMPORTANT]
>
>Wenn Sie eine CNAME-Implementierung mit [!DNL Target] bring-your-own-certificate anfordern, sind Sie dafür verantwortlich, [!DNL Adobe] Client Care jedes Mal, wenn sie abläuft, erneuerte Zertifikate bereitzustellen. Wenn Ihr CNAME-Zertifikat abläuft, bevor [!DNL Adobe] ein erneuertes Zertifikat bereitstellen können, führt dies für Ihre spezifische [!DNL Target] zu einem Ausfall.

### Wie lange läuft mein neues SSL-Zertifikat ab?

Die Lebensdauer aller Zertifikate wird im Rahmen einer größeren Initiative der Zertifizierungsstellen reduziert. Für DigiCert, den Zertifikatanbieter von [!DNL Adobe], gilt der folgende Zeitplan:

Bis zum 15. März 2026 beträgt die maximale Lebensdauer für ein TLS-Zertifikat 398 Tage.
Ab dem 15. März 2026 beträgt die maximale Lebensdauer für ein TLS-Zertifikat 200 Tage.
Ab dem 15. März 2027 beträgt die maximale Lebensdauer für ein TLS-Zertifikat 100 Tage.
Ab dem 15. März 2029 beträgt die maximale Lebensdauer für ein TLS-Zertifikat 47 Tage.
Weitere Informationen finden Sie im [DigiCert-Artikel zum Reduzieren der Zertifikatlebensdauer](https://www.digicert.com/blog/tls-certificate-lifetimes-will-officially-reduce-to-47-days)

### Welche Hostnamen sollte ich auswählen? Wie viele Hostnamen pro Domain sollte ich auswählen?

[!DNL Target] CNAME-Implementierungen erfordern nur einen Hostnamen pro Domain im SSL-Zertifikat und im DNS des Kunden. [!DNL Adobe] empfiehlt einen Hostnamen pro Domain. Einige Kunden benötigen für ihre eigenen Zwecke mehr Hostnamen pro Domain (z. B. zum Testen in der Staging-Umgebung), was unterstützt wird.

Die meisten Kunden wählen einen Hostnamen wie `target.example.com`. [!DNL Adobe] empfiehlt, diese Vorgehensweise zu befolgen, aber letztendlich haben Sie die Wahl. Fordern Sie keinen Hostnamen eines vorhandenen DNS-Eintrags an. Dies führt zu einem Konflikt und verzögert die Lösung Ihrer [!DNL Target] CNAME-Anfrage.

### Ich habe bereits eine CNAME-Implementierung für [!DNL Adobe Analytics]. Kann ich dasselbe Zertifikat oder denselben Hostnamen verwenden?

Nein, [!DNL Target] erfordert einen separaten Hostnamen und ein separates Zertifikat.

### Hat ITP 2.x Auswirkungen auf meine aktuelle Implementierung von [!DNL Target]?

Apple Intelligent Tracking Prevention (ITP) Version 2.3 hat die CNAME-Funktion zur Begrenzung von Cloaking (Maskierung) eingeführt, die in der Lage ist, [!DNL Adobe Target] CNAME-Implementierungen zu erkennen und den Cookie-Ablauf auf sieben Tage zu reduzieren. Derzeit gibt es in [!DNL Target] keine Problemumgehung für die CNAME Cloaking Mitigation von ITP. Weitere Informationen zu ITP finden Sie unter [Apple Intelligent Tracking Prevention (ITP) 2.x](/help/dev/before-implement/privacy/apple-itp-2x.md).

### Mit welcher Art von Service-Unterbrechungen kann ich rechnen, wenn meine CNAME-Implementierung bereitgestellt wird?

Bei der Bereitstellung des Zertifikats kommt es zu keiner Service-Unterbrechung (einschließlich Zertifikatsverlängerungen).

Nachdem Sie jedoch den Hostnamen in Ihrem [!DNL Target]-Implementierungs-Code (`serverDomain` in at.js) in den neuen CNAME-Hostnamen (`target.example.com`) geändert haben, behandeln Webbrowser wiederkehrende Besucher als neue Besucher. Die Profildaten der wiederkehrenden Besucher gehen verloren, da unter dem alten Hostnamen (`clientcode.tt.omtrdc.net`) nicht auf das vorherige Cookie zugegriffen werden kann. Auf das vorherige Cookie kann aufgrund von Browser-Sicherheitsmodellen nicht zugegriffen werden. Diese Unterbrechung tritt nur beim erstmaligen Umschalten auf den neuen CNAME auf. Zertifikatsverlängerungen haben nicht dieselbe Wirkung, da sich der Hostname nicht ändert.

### Welcher Schlüsseltyp und welcher Zertifikatsignaturalgorithmus wird für meine CNAME-Implementierung verwendet?

Alle Zertifikate sind RSA SHA-256 und die Schlüssel sind standardmäßig RSA 2048-Bit. Schlüsselgrößen über 2048-Bit sollten explizit von der Kundenunterstützung angefordert werden.

### Wie kann ich überprüfen, ob meine CNAME-Implementierung für Traffic bereit ist?

Verwenden Sie die folgenden Befehle (im macOS- oder Linux-Befehlszeilen-Terminal mit bash und curl >=7.49):

1. Kopieren Sie diese Bash-Funktion und fügen Sie sie in Ihr Terminal ein, oder fügen Sie sie in Ihre Bash-Startskriptdatei ein (normalerweise `~/.bash_profile` oder `~/.bashrc`), damit die Funktion in allen Terminalsitzungen verfügbar ist:

```
function adobeTargetCnameValidation {
  local hostname="$1"
  
  if [ -z "$hostname" ]; then
    echo "ERROR: no hostname specified"
    return 1
  fi
  
  local service="Adobe Target CNAME implementation"
  local edges="41 42 44 45 46 47 48"
  local edgeDomain="tt.omtrdc.net"
  local edgeFormat="mboxedge%d%s.$edgeDomain"
  local poolDomain="pool.data.adobedc.net"
  local shards=5
  local shardsFoundCount=0
  local shardsFound=""
  local shardsFoundOutput=""
  local curlRegex="subject:.*CN=|expire date:|issuer:"
  local curlValidation="SSL certificate verify ok"
  local curlResponseValidation='"OK"'
  local curlEndpoint="/uptime?mboxClient=uptime3"
  local url="https://$hostname$curlEndpoint"
  local sslShopperUrl="https://www.sslshopper.com/ssl-checker.html#hostname=$hostname"
  local success="✅"
  local failure="🚫"
  local info="🔎"
  local rule="="
  local horizontalRule="$(seq ${COLUMNS:-30} | xargs printf "$rule%.0s")"
  local miniRule="$(seq 5 | xargs printf "$rule%.0s")"
  local curlVersion="$(curl --version | head -1 | cut -d' ' -f2)"
  local curlVersionRequired=7.49
  local edgeCount="$(wc -w <<< "$edges" | tr -d ' ')"
  local cnameExists=""
  local endToEndTestSucceeded=""
  
  for region in IRL1 IND1 SIN OR SYD VA TYO; do
    local currShard="${region}-${poolDomain}"
    local curlResult="$(curl -vsm20 --connect-to "$hostname:443:$currShard:443" "$url" 2>&1)"
    
    if grep -q "$curlValidation" <<< "$curlResult"; then
      shardsFound+=" $currShard"
      
      if grep -q "$curlResponseValidation" <<< "$curlResult"; then
        shardsFoundCount=$((shardsFoundCount+1))
        shardsFoundOutput+="\n\n$miniRule $success $hostname [edge shard: $currShard] $miniRule\n"
      else
        shardsFoundOutput+="\n\n$miniRule $failure $hostname [edge shard: $currShard] $miniRule\n"
      fi
      
      shardsFoundOutput+="$(grep -E "$curlRegex" <<< "$curlResult" | sort)"
      
      if ! grep -q "$curlResponseValidation" <<< "$curlResult"; then
        shardsFoundOutput+="\nERROR: unexpected HTTP response from this shard using $url"
      fi
    fi
  done
  
  echo
  echo "$horizontalRule"
  echo
  echo "$service validation for hostname $hostname:"
  
  local dnsOutput="$(dig -t CNAME +short "$hostname" 2>&1)"
  if grep -qFi ".$edgeDomain" <<< "$dnsOutput"; then
    echo "$success $hostname passes DNS CNAME validation"
    cnameExists=true
  else
    echo -n "$failure $hostname FAILED DNS CNAME validation -- "
    if [ -n "$dnsOutput" ]; then
      echo -e "$dnsOutput is not in the subdomain $edgeDomain"
    else
      echo "required DNS CNAME record pointing to <target-client-code>.$edgeDomain not found"
    fi
  fi
  
  for region in IRL1 IND1 SIN OR SYD VA TYO; do
    local curlResult="$(curl -vsm20 --connect-to "$hostname:443:${region}-pool.data.adobedc.net:443" "https://$hostname$curlEndpoint" 2>&1)"
    
    if grep -q "$curlValidation" <<< "$curlResult"; then
      if grep -q "$curlResponseValidation" <<< "$curlResult"; then
        echo -en "$success $hostname passes TLS and HTTP response validation for region $region"
        if [ -n "$cnameExists" ]; then
          echo
        else
          echo " -- the DNS CNAME is not pointing to the correct subdomain for ${service}s with Adobe-managed certificates" \
            "(bring-your-own-certificate implementations don't have this requirement), but this test passes as configured"
        fi
        endToEndTestSucceeded=true
      else
        echo -n "$failure $hostname FAILED HTTP response validation for region $region --" \
          "unexpected response from $url -- "
        if [ -n "$cnameExists" ]; then
          echo "DNS is NOT pointing to the correct shard, notify Adobe Client Care"
        else
          echo "the required DNS CNAME record is missing, see above"
        fi
      fi
    else
      echo -n "$failure $hostname FAILED TLS validation for region $region -- "
      if [ -n "$cnameExists" ]; then
        echo "DNS is likely NOT pointing to the correct shard or there's a validation issue with the certificate or" \
          "protocols, see curl output below and optionally SSL Shopper ($sslShopperUrl):"
        echo ""
        echo "$horizontalRule"
        echo "$curlResult" | sed 's/^/    /g'
        echo "$horizontalRule"
        echo ""
      else
        echo "the required DNS CNAME record is missing, see above"
      fi
    fi
  done
  
  if [ "$shardsFoundCount" -ge "$edgeCount" ]; then
    echo -n "$success $hostname passes shard validation for the following $shardsFoundCount edge shards:"
    echo -e "$shardsFoundOutput"
    echo
    
    if [ -n "$cnameExists" ] && [ -n "$endToEndTestSucceeded" ]; then
      echo "$horizontalRule"
      echo ""
      echo "  For additional TLS/SSL validation, see SSL Shopper:"
      echo ""
      echo "    $info  $sslShopperUrl"
      echo ""
      echo "  To check DNS propagation around the world, see whatsmydns.net:"
      echo ""
      echo "    $info  DNS A records:     https://whatsmydns.net/#A/$hostname"
      echo "    $info  DNS CNAME record:  https://whatsmydns.net/#CNAME/$hostname"
    fi
  else
    echo -n "$failure $hostname FAILED shard validation -- shards found: $shardsFoundCount," \
      "expected: $edgeCount"
    echo ""
  fi
  
  echo
  echo "$horizontalRule"
  echo
}  
```

1. Fügen Sie diesen Befehl ein (und ersetzen Sie `target.example.com` durch Ihren Hostnamen):

   ```
   adobeTargetCnameValidation target.example.com
   ```

   Wenn die Implementierung fertig ist, sehen Sie eine Ausgabe wie unten. Wichtig ist, dass alle Validierungsstatuszeilen `✅` statt `🚫` anzeigen. Jede [!DNL Target]-Edge-CNAME-Shard sollte `CN=target.example.com` anzeigen, die dem primären Hostnamen im angeforderten Zertifikat entspricht (zusätzliche SAN-Hostnamen im Zertifikat werden in dieser Ausgabe nicht gedruckt).

```
$ adobeTargetCnameValidation target.example.com

==========================================================

Adobe Target CNAME implementation validation for hostname target.example.com:
✅ target.example.com passes DNS CNAME validation
✅ target.example.com passes TLS and HTTP response validation for region IRL1
✅ target.example.com passes TLS and HTTP response validation for region IND1
✅ target.example.com passes TLS and HTTP response validation for region SIN
✅ target.example.com passes TLS and HTTP response validation for region OR
✅ target.example.com passes TLS and HTTP response validation for region SYD
✅ target.example.com passes TLS and HTTP response validation for region VA
✅ target.example.com passes TLS and HTTP response validation for region TYO
✅ target.example.com passes shard validation for the following 7 edge shards:

===== ✅ target.example.com [edge shard: IRL1-pool.data.adobedc.net] =====
*  expire date: Feb 20 23:59:59 2026 GMT
*  issuer: C=US; O=DigiCert Inc; CN=DigiCert Global G2 TLS RSA SHA256 2020 CA1
*  subject: C=US; ST=California; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com

===== ✅ target.example.com [edge shard: IND1-pool.data.adobedc.net] =====
*  expire date: Feb 20 23:59:59 2026 GMT
*  issuer: C=US; O=DigiCert Inc; CN=DigiCert Global G2 TLS RSA SHA256 2020 CA1
*  subject: C=US; ST=California; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com

===== ✅ target.example.com [edge shard: SIN-pool.data.adobedc.net] =====
*  expire date: Feb 20 23:59:59 2026 GMT
*  issuer: C=US; O=DigiCert Inc; CN=DigiCert Global G2 TLS RSA SHA256 2020 CA1
*  subject: C=US; ST=California; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com

===== ✅ target.example.com [edge shard: OR-pool.data.adobedc.net] =====
*  expire date: Feb 20 23:59:59 2026 GMT
*  issuer: C=US; O=DigiCert Inc; CN=DigiCert Global G2 TLS RSA SHA256 2020 CA1
*  subject: C=US; ST=California; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com

===== ✅ target.example.com [edge shard: SYD-pool.data.adobedc.net] =====
*  expire date: Feb 20 23:59:59 2026 GMT
*  issuer: C=US; O=DigiCert Inc; CN=DigiCert Global G2 TLS RSA SHA256 2020 CA1
*  subject: C=US; ST=California; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com

===== ✅ target.example.com [edge shard: VA-pool.data.adobedc.net] =====
*  expire date: Feb 20 23:59:59 2026 GMT
*  issuer: C=US; O=DigiCert Inc; CN=DigiCert Global G2 TLS RSA SHA256 2020 CA1
*  subject: C=US; ST=California; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com

===== ✅ target.example.com [edge shard: TYO-pool.data.adobedc.net] =====
*  expire date: Feb 20 23:59:59 2026 GMT
*  issuer: C=US; O=DigiCert Inc; CN=DigiCert Global G2 TLS RSA SHA256 2020 CA1
*  subject: C=US; ST=California; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com

==========================================================  

For additional TLS/SSL validation, see SSL Shopper:

    🔎  https://www.sslshopper.com/ssl-checker.html#hostname=target.example.com  

To check DNS propagation around the world, see whatsmydns.net:

    🔎  DNS A records:     https://whatsmydns.net/#A/target.example.com
    🔎  DNS CNAME record:  https://whatsmydns.net/#CNAME/target.example.com 
```

>[!NOTE]
>
>Wenn dieser Validierungsbefehl bei der DNS-Validierung fehlschlägt, Sie jedoch bereits die erforderlichen DNS-Änderungen vorgenommen haben, müssen Sie möglicherweise warten, bis Ihre DNS-Aktualisierungen vollständig weitergegeben werden. DNS-Einträge sind mit einer [TTL (Time-to-Live) verknüpft](https://en.wikipedia.org/wiki/Time_to_live#DNS_records) die die Gültigkeitsdauer des Cache für DNS-Antworten dieser Einträge bestimmt. Daher müssen Sie möglicherweise mindestens so lange warten, wie Ihre TTLs. Sie können den `dig target.example.com`-Befehl oder [die G Suite Toolbox](https://toolbox.googleapps.com/apps/dig/#CNAME) verwenden, um Ihre spezifischen TTLs zu suchen. Informationen zur Überprüfung der DNS-Verbreitung auf der ganzen Welt finden Sie unter [whatsmydns.net](https://whatsmydns.net/#CNAME).

### Wie verwende ich einen Ausschluss-Link mit CNAME?

Wenn Sie CNAME verwenden, sollte der Ausschluss-Link beispielsweise den Parameter „client=`clientcode`&quot; enthalten:
`https://my.cname.domain/optout?client=clientcode`.

Ersetzen Sie `clientcode` durch Ihren Client-Code und fügen Sie dann den Text oder das Bild hinzu, das mit der [Opt-out-URL) verknüpft ](/help/dev/before-implement/privacy/privacy.md) soll.

## Bekannte Einschränkungen

* Der QA-Modus bleibt bei CNAME- und at.js-Versionen 1.x nicht hängen, da er auf einem Drittanbieter-Cookie basiert. Um dieses Problem zu umgehen, fügen Sie die Vorschauparameter zu jeder URL hinzu, zu der Sie navigieren. Der QA-Modus bleibt bestehen, wenn Sie CNAME und at.js 2.x verwenden.
* Bei Verwendung von CNAME ist es wahrscheinlicher, dass die Größe der Cookie-Kopfzeile für [!DNL Target] Aufrufe zunimmt. [!DNL Adobe] empfiehlt, die Cookie-Größe unter 8 KB zu halten.
