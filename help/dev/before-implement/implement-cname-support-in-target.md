---
keywords: Client Care, CNAME, Zertifikatsprogramm, kanonischer Name, Cookies, Zertifikat, amc, adobe managed certificate, digicert, Domain Control Validation, dcv, Client Care2
description: Arbeiten mit [!UICONTROL Adobe Client Care] zur Implementierung der CNAME-Unterstützung (Canonical Name) in [!DNL Adobe Target] um Probleme mit der Anzeigenblockierung zu beheben.
title: Wie verwende ich CNAME in Target?
feature: Privacy & Security
exl-id: 5709df5b-6c21-4fea-b413-ca2e4912d6cb
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '1193'
ht-degree: 1%

---

# CNAME und Target

Anweisungen für die Arbeit mit [!DNL Adobe Client Care] zur Implementierung der CNAME-Unterstützung (Canonical Name) in [!DNL Adobe Target]. Verwenden Sie CNAME, um Probleme mit der Anzeigenblockierung oder ITP-bezogene Cookie-Richtlinien (Intelligent Tracking Prevention) zu verarbeiten. Mit CNAME werden Aufrufe an eine Domäne gesendet, die dem Kunden gehört, und nicht an eine Domäne, die der Adobe gehört.

## Unterstützung von CNAME anfordern in Target

1. Bestimmen Sie die Liste der Hostnamen, die Sie für Ihr SSL-Zertifikat benötigen (siehe FAQ unten).

1. Erstellen Sie für jeden Hostnamen einen CNAME-Eintrag in Ihrem DNS, der auf Ihren regulären Namen verweist. [!DNL Target] hostname `clientcode.tt.omtrdc.net`.

   Wenn Ihr Clientcode beispielsweise &quot;cnameccustomer&quot;lautet und Ihr Hostname vorgeschlagen wird, lautet `target.example.com`, sieht Ihr DNS-CNAME-Eintrag ähnlich aus:

   ```
   target.example.com.  IN  CNAME  cnamecustomer.tt.omtrdc.net.
   ```

   >[!WARNING]
   >
   >Die Zertifizierungsstelle der Adobe, DigiCert, kann erst nach Abschluss dieses Schritts ein Zertifikat ausstellen. Daher kann Adobe Ihre Anfrage nach einer CNAME-Implementierung erst nach Abschluss dieses Schritts erfüllen.

1. [Füllen Sie dieses Formular aus](assets/FPC_Request_Form.xlsx) und fügen Sie ihn bei [ein Adobe-Kundenunterstützungs-Ticket öffnen, in dem CNAME-Support angefordert wird](https://experienceleague.adobe.com/docs/target/using/cmp-resources-and-contact-information.html?#reference_ACA3391A00EF467B87930A450050077C):

   * [!DNL Adobe Target] client code:
   * SSL-Zertifikat-Hostnamen (Beispiel: `target.example.com target.example.org`):
   * SSL-Zertifikatkäufer (Adobe wird dringend empfohlen, siehe FAQ): Adobe/Kunde
   * Wenn der Kunde das Zertifikat kauft, auch bekannt als &quot;Bring Your Own Certificate&quot;(BYOC), füllen Sie diese zusätzlichen Details aus:
      * Zertifikatorganisation (Beispiel: Firma Beispiel Inc.):
      * Organisationseinheit des Zertifikats (optional, Beispiel: Marketing):
      * Zertifikatstaat (Beispiel: US):
      * Zertifikatstaat/-region (Beispiel: Kalifornien):
      * Zertifikatstadt (Beispiel: San Jose):

1. Wenn Adobe das Zertifikat kauft, kauft und stellt Adobe Ihr Zertifikat auf den Produktionsservern der Adobe bereit.

   Wenn der Kunde das Zertifikat (BYOC) kauft, sendet Ihnen der Adobe-Kundendienst die Certificate Signing Request (CSR). Verwenden Sie die CSR, wenn Sie das Zertifikat über Ihre Zertifizierungsstelle Ihrer Wahl erwerben. Nachdem das Zertifikat ausgestellt wurde, senden Sie eine Kopie des Zertifikats und etwaiger Zwischenzertifikate zur Bereitstellung an die Adobe Client Care.

   Adobe Der Kundendienst benachrichtigt Sie, wenn Ihre Implementierung fertig ist.

1. Aktualisieren Sie die `serverDomain` [Dokumentation](../implement/client-side/atjs/atjs-functions/targetglobalsettings.md#serverdomain) auf den neuen CNAME-Hostnamen und legen Sie `overrideMboxEdgeServer` nach `false` [Dokumentation](../implement/client-side/atjs/atjs-functions/targetglobalsettings.md#overridemboxedgeserver) in Ihrer at.js-Konfiguration.

## Häufig gestellte Fragen  

Die folgenden Informationen beantworten häufig gestellte Fragen zum Anfordern und Implementieren von CNAME-Unterstützung in Target:

### Kann ich ein eigenes Zertifikat bereitstellen (Eigenes Zertifikat mitbringen oder BYOC)?

Sie können Ihr eigenes Zertifikat bereitstellen. Diese Vorgehensweise wird von Adobe jedoch nicht empfohlen. Die Verwaltung des SSL-Zertifikatslebenszyklus ist sowohl für die Adobe als auch für Sie einfacher, wenn die Adobe das Zertifikat kauft und steuert. SSL-Zertifikate müssen jedes Jahr erneuert werden. Daher muss sich der Kundendienst von Adobe jedes Jahr an Sie wenden, um rechtzeitig ein neues Zertifikat zu erhalten. Einige Kunden können Schwierigkeiten haben, ein neues Zertifikat zeitnah zu erstellen. Ihre [!DNL Target] -Implementierung wird gefährdet, wenn das Zertifikat abläuft, da Browser Verbindungen ablehnen.

>[!WARNING]
>
>Wenn Sie eine [!DNL Target] die Implementierung des CNAME-Zertifikats für Ihr eigenes Zertifikat mitbringen, sind Sie dafür verantwortlich, der Adobe Client Care jedes Jahr neue Zertifikate zur Verfügung zu stellen. Wenn Sie zulassen, dass Ihr CNAME-Zertifikat abläuft, bevor Adobe ein neues Zertifikat bereitstellen kann, tritt für Ihre spezifischen [!DNL Target] Implementierung.

### Wie lange dauert es, bis mein neues SSL-Zertifikat abläuft?

Alle von der Adobe erworbenen Zertifikate sind ein Jahr gültig. Siehe [Artikel von DigiCert zu 1-Jahres-Zertifikaten](https://www.digicert.com/blog/position-on-1-year-certificates) für weitere Informationen.

### Welche Hostnamen sollte ich wählen? Wie viele Hostnamen pro Domäne sollte ich wählen?

Target-CNAME-Implementierungen erfordern nur einen Hostnamen pro Domäne auf dem SSL-Zertifikat und im DNS des Kunden. Adobe empfiehlt einen Hostnamen pro Domäne. Einige Kunden benötigen für ihre eigenen Zwecke (z. B. Tests im Staging) mehr Hostnamen pro Domäne, was unterstützt wird.

Die meisten Kunden wählen einen Hostnamen wie `target.example.com`. Adobe empfiehlt, dieser Praxis zu folgen, aber die Wahl liegt letztendlich bei Ihnen. Fordern Sie keinen Hostnamen eines vorhandenen DNS-Eintrags an. Dies führt zu einem Konflikt und verzögert die Behebung Ihrer [!DNL Target] CNAME-Anfrage.

### Ich habe bereits eine CNAME-Implementierung für Adobe Analytics. Kann ich dasselbe Zertifikat oder denselben Hostnamen verwenden?

Nein, [!DNL Target] erfordert einen separaten Hostnamen und ein separates Zertifikat.

### Ist meine aktuelle Implementierung von [!DNL Target] von ITP 2.x beeinflusst?

Apple Intelligent Tracking Prevention (ITP) Version 2.3 führte die CNAME Cloaking Mitigation-Funktion ein, die in der Lage ist, [!DNL Target] CNAME-Implementierungen und reduzieren die Gültigkeit des Cookies auf sieben Tage. Aktuell [!DNL Target] gibt keine Problemumgehung für die CNAME-Cloaking-Abmilderung von ITP. Weitere Informationen zu ITP finden Sie unter [Apple Intelligent Tracking Prevention (ITP) 2.x](../before-implement/privacy/apple-itp-2x.md).

### Welche Arten von Dienstunterbrechungen kann ich erwarten, wenn meine CNAME-Implementierung bereitgestellt wird?

Bei der Bereitstellung des Zertifikats gibt es keine Dienstunterbrechung (einschließlich Zertifikatsverlängerungen).

Nachdem Sie jedoch den Hostnamen in Ihrem [!DNL Target] Implementierungscode (`serverDomain` in at.js) auf den neuen CNAME-Hostnamen (`target.example.com`), behandeln Webbrowser wiederkehrende Besucher als neue Besucher. Die Profildaten der zurückgegebenen Besucher gehen verloren, da der Zugriff auf das vorherige Cookie unter dem alten Hostnamen (`clientcode.tt.omtrdc.net`). Der Zugriff auf das vorherige Cookie ist aufgrund von Browser-Sicherheitsmodellen nicht möglich. Diese Störung tritt nur beim ersten Cut-over auf den neuen CNAME auf. Zertifikatverlängerungen haben nicht die gleiche Wirkung, da sich der Hostname nicht ändert.

### Welcher Schlüsseltyp und welcher Zertifikatsignaturalgorithmus wird für meine CNAME-Implementierung verwendet?

Alle Zertifikate sind RSA SHA-256 und Schlüssel sind standardmäßig RSA 2048-Bit. Größen, die größer als 2048 Bit sind, werden derzeit nicht unterstützt.

### Wie kann ich überprüfen, ob meine CNAME-Implementierung für Traffic bereit ist?

Verwenden Sie den folgenden Befehlssatz (im Befehlszeilen-Terminal von macOS oder Linux mit bash und curl >=7.49):

1. Kopieren Sie diese Bash-Funktion und fügen Sie sie in Ihr Terminal ein oder fügen Sie die Funktion in Ihre Bash-Startskriptdatei ein (normalerweise `~/.bash_profile` oder `~/.bashrc`), damit die Funktion über alle Terminalsitzungen hinweg verfügbar ist:

   ```
   function adobeTargetCnameValidation {
     local hostname="$1"
     if [ -z "$hostname" ]; then
       echo "ERROR: no hostname specified"
       return 1
     fi
   
     local service="Adobe Target CNAME implementation"
     local edges="31 32 34 35 36 37 38"
     local edgeDomain="tt.omtrdc.net"
     local edgeFormat="mboxedge%d%s.$edgeDomain"
     local shardFormat="-alb%02d"
     local shards=5
     local shardsFoundCount=0
     local shardsFound
     local shardsFoundOutput
     local curlRegex="subject:.*CN=|expire date:|issuer:"
     local curlValidation="SSL certificate verify ok"
     local curlResponseValidation='"OK"'
     local curlEndpoint="/uptime?mboxClient=uptime3"
     local url="https://$hostname$curlEndpoint"
     local sslLabsUrl="https://ssllabs.com/ssltest/analyze.html?hideResults=on&latest&d=$hostname"
     local success="✅"
     local failure="🚫"
     local info="🔎"
     local rule="="
     local horizontalRule="$(seq ${COLUMNS:-30} | xargs printf "$rule%.0s")"
     local miniRule="$(seq 5 | xargs printf "$rule%.0s")"
     local curlVersion="$(curl --version | head -1 | cut -d' ' -f2 )"
     local curlVersionRequired=">=7.49"
     local edgeCount="$(wc -w <<< "$edges" | tr -d ' ')"
     local edge
     local shard
     local currEdgeShard
     local dnsOutput
     local cnameExists
     local endToEndTestSucceeded
     local curlResult
   
     for shard in $(seq $shards); do
       if [ "$shardsFoundCount" -eq 0 ]; then
         for edge in $edges; do
           if [ "$shard" -eq 1 ]; then
             currEdgeShard="$(printf "$edgeFormat" "$edge" "")"
           else
             currEdgeShard="$(
               printf "$edgeFormat" "$edge" "$(
                 printf -- "$shardFormat" "$shard"
               )"
             )"
           fi
           curlResult="$(curl -vsm20 --connect-to "$hostname:443:$currEdgeShard:443" "$url" 2>&1)"
           if grep -q "$curlValidation" <<< "$curlResult"; then
             shardsFound+=" $currEdgeShard"
             if grep -q "$curlResponseValidation" <<< "$curlResult"; then
               shardsFoundCount=$((shardsFoundCount+1))
               shardsFoundOutput+="\n\n$miniRule $success $hostname [edge shard: $currEdgeShard] $miniRule\n"
             else
               shardsFoundOutput+="\n\n$miniRule $failure $hostname [edge shard: $currEdgeShard] $miniRule\n"
             fi
             shardsFoundOutput+="$(grep -E "$curlRegex" <<< "$curlResult" | sort)"
             if ! grep -q "$curlResponseValidation" <<< "$curlResult"; then
               shardsFoundOutput+="\nERROR: unexpected HTTP response from this shard using $url"
             fi
           fi
         done
       fi
     done
   
     echo
     echo "$horizontalRule"
     echo
     echo "$service validation for hostname $hostname:"
     dnsOutput="$(dig -t CNAME +short "$hostname" 2>&1)"
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
   
     curlResult="$(curl -vsm20 "$url" 2>&1)"
     if grep -q "$curlValidation" <<< "$curlResult"; then
       if grep -q "$curlResponseValidation" <<< "$curlResult"; then
         echo -en "$success $hostname passes TLS and HTTP response validation"
         if [ -n "$cnameExists" ]; then
           echo
         else
           echo " -- the DNS CNAME is not pointing to the correct subdomain for ${service}s with Adobe-managed certificates" \
             "(bring-your-own-certificate implementations don't have this requirement), but this test passes as configured"
         fi
         endToEndTestSucceeded=true
       else
         echo -n "$failure $hostname FAILED HTTP response validation --" \
           "unexpected response from $url -- "
         if [ -n "$cnameExists" ]; then
           echo "DNS is NOT pointing to the correct shard, notify Adobe Client Care"
         else
           echo "the required DNS CNAME record is missing, see above"
         fi
       fi
     else
   
       echo -n "$failure $hostname FAILED TLS validation -- "
       if [ -n "$cnameExists" ]; then
         echo "DNS is likely NOT pointing to the correct shard or there's a validation issue with the certificate or" \
           "protocols, see curl output below and optionally SSL Labs ($sslLabsUrl):"
         echo ""
         echo "$horizontalRule"
         echo "$curlResult" | sed 's/^/    /g'
         echo "$horizontalRule"
         echo ""
       else
         echo "the required DNS CNAME record is missing, see above"
       fi
     fi
   
     if [ "$shardsFoundCount" -ge "$edgeCount" ]; then
       echo -n "$success $hostname passes shard validation for the following $shardsFoundCount edge shards:"
       echo -e "$shardsFoundOutput"
       echo
   
       if [ -n "$cnameExists" ] && [ -n "$endToEndTestSucceeded" ]; then
         echo "$horizontalRule"
         echo ""
         echo "  For additional TLS/SSL validation, including detailed browser/client support,"
         echo "  see SSL Labs (click the first IP address if prompted):"
         echo ""
         echo "    $info  $sslLabsUrl"
         echo ""
         echo "  To check DNS propagation around the world, see whatsmydns.net:"
         echo ""
         echo "    $info  DNS A records:     https://whatsmydns.net/#A/$hostname"
         echo "    $info  DNS CNAME record:  https://whatsmydns.net/#CNAME/$hostname"
       fi
     else
       echo -n "$failure $hostname FAILED shard validation -- shards found: $shardsFoundCount," \
         "expected: $edgeCount"
       if bc -l <<< "$(cut -d. -f1,2 <<< "$curlVersion") $curlVersionRequired" 2>/dev/null | grep -q 0; then
         echo -n " -- insufficient curl version installed: $curlVersion, but this script requires curl version" \
           "$curlVersionRequired because it uses the curl --connect-to flag to bypass DNS and directly test" \
           "each Adobe Target edge shards' SNI confirguation for $hostname"
       fi
       if [ -n "$shardsFoundOutput" ]; then
         echo -e ":\n$shardsFoundOutput"
       fi
       echo
     fi
     echo
     echo "$horizontalRule"
     echo
   }
   ```

1. Fügen Sie diesen Befehl ein (ersetzen `target.example.com` mit Ihrem Hostnamen):

   ```
   adobeTargetCnameValidation target.example.com
   ```

   Wenn die Implementierung bereit ist, sehen Sie die Ausgabe wie unten dargestellt. Wichtig ist, dass alle Validierungsstatuszeilen `✅` anstelle von `🚫`. Jeder CNAME-Shard der Target-Edge sollte `CN=target.example.com`, der mit dem primären Hostnamen im angeforderten Zertifikat übereinstimmt (zusätzliche SAN-Hostnamen auf dem Zertifikat werden in dieser Ausgabe nicht gedruckt).

   ```
   $ adobeTargetCnameValidation target.example.com
   
   ==========================================================
   
   Adobe Target CNAME implementation validation for hostname target.example.com:
   ✅ target.example.com passes DNS CNAME validation
   ✅ target.example.com passes TLS and HTTP response validation
   ✅ target.example.com passes shard validation for the following 7 edge shards:
   
   ===== ✅ target.example.com [edge shard: mboxedge31-alb02.tt.omtrdc.net] =====
   *  expire date: Jul 22 23:59:59 2022 GMT
   *  issuer: C=US; O=DigiCert Inc; CN=DigiCert TLS RSA SHA256 2020 CA1
   *  subject: C=US; ST=California; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com
   
   ===== ✅ target.example.com [edge shard: mboxedge32-alb02.tt.omtrdc.net] =====
   *  expire date: Jul 22 23:59:59 2022 GMT
   *  issuer: C=US; O=DigiCert Inc; CN=DigiCert TLS RSA SHA256 2020 CA1
   *  subject: C=US; ST=California; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com
   
   ===== ✅ target.example.com [edge shard: mboxedge34-alb02.tt.omtrdc.net] =====
   *  expire date: Jul 22 23:59:59 2022 GMT
   *  issuer: C=US; O=DigiCert Inc; CN=DigiCert TLS RSA SHA256 2020 CA1
   *  subject: C=US; ST=California; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com
   
   ===== ✅ target.example.com [edge shard: mboxedge35-alb02.tt.omtrdc.net] =====
   *  expire date: Jul 22 23:59:59 2022 GMT
   *  issuer: C=US; O=DigiCert Inc; CN=DigiCert TLS RSA SHA256 2020 CA1
   *  subject: C=US; ST=California; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com
   
   ===== ✅ target.example.com [edge shard: mboxedge36-alb02.tt.omtrdc.net] =====
   *  expire date: Jul 22 23:59:59 2022 GMT
   *  issuer: C=US; O=DigiCert Inc; CN=DigiCert TLS RSA SHA256 2020 CA1
   *  subject: C=US; ST=California; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com
   
   ===== ✅ target.example.com [edge shard: mboxedge37-alb02.tt.omtrdc.net] =====
   *  expire date: Jul 22 23:59:59 2022 GMT
   *  issuer: C=US; O=DigiCert Inc; CN=DigiCert TLS RSA SHA256 2020 CA1
   *  subject: C=US; ST=California; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com
   
   ===== ✅ target.example.com [edge shard: mboxedge38-alb02.tt.omtrdc.net] =====
   *  expire date: Jul 22 23:59:59 2022 GMT
   *  issuer: C=US; O=DigiCert Inc; CN=DigiCert TLS RSA SHA256 2020 CA1
   *  subject: C=US; ST=California; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com
   
   ==========================================================
   
     For additional TLS/SSL validation, including detailed browser/client support,
     see SSL Labs (click the first IP address if prompted):
   
       🔎  https://ssllabs.com/ssltest/analyze.html?hideResults=on&latest&d=target.example.com
   
     To check DNS propagation around the world, see whatsmydns.net:
   
       🔎  DNS A records:     https://whatsmydns.net/#A/target.example.com
       🔎  DNS CNAME record:  https://whatsmydns.net/#CNAME/target.example.com
   
   ==========================================================
   ```

>[!NOTE]
>
>Wenn dieser Überprüfungsbefehl bei der DNS-Validierung fehlschlägt, Sie jedoch bereits die erforderlichen DNS-Änderungen vorgenommen haben, müssen Sie möglicherweise warten, bis Ihre DNS-Updates vollständig propagiert werden. DNS-Einträge sind mit [TTL (Time-to-Live)](https://en.wikipedia.org/wiki/Time_to_live#DNS_records) die die Cache-Ablaufzeit für DNS-Antworten dieser Datensätze vorgibt. Daher müssen Sie möglicherweise mindestens so lange warten, wie Ihre TTLs sind. Sie können die `dig target.example.com` Befehl oder [G Suite Toolbox](https://toolbox.googleapps.com/apps/dig/#CNAME) , um Ihre spezifischen TTLs nachzuschlagen. Informationen zur weltweiten DNS-Verbreitung finden Sie unter [whatsmydns.net](https://whatsmydns.net/#CNAME).

### Wie verwende ich einen Ausschluss-Link mit CNAME?

Wenn Sie CNAME verwenden, sollte der Ausschluss-Link den Wert &quot;client=&quot;enthalten.`clientcode` -Parameter, beispielsweise:
`https://my.cname.domain/optout?client=clientcode`.

Ersetzen `clientcode` mit Ihrem Clientcode verwenden, fügen Sie dann den Text oder das Bild hinzu, der/das mit der [Ausschluss-URL](privacy/privacy.md).

## Bekannte Einschränkungen

* Der QA-Modus ist nicht fixierbar, wenn Sie CNAME und at.js 1.x verwenden, da er auf einem Drittanbieter-Cookie basiert. Um dieses Problem zu umgehen, fügen Sie jeder URL, zu der Sie navigieren, die Vorschauparameter hinzu. Der QS-Modus hängt bei CNAME und at.js 2.x an.
* Bei Verwendung von CNAME wird es wahrscheinlicher, dass die Größe des Cookie-Headers für [!DNL Target] -Aufrufe zunehmen. Adobe empfiehlt, die Cookie-Größe unter 8 KB zu halten.
