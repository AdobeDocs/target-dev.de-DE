---
title: Client-Hinweise zur Adobe Target-Bereitstellungs-API
description: Wie verwende ich Client Hints in der  [!DNL Adobe Target] -Bereitstellungs-API?
exl-id: 317b9d7d-5b98-464e-9113-08b899ee1455
feature: APIs/SDKs
TQID: https://experienceleague.adobe.com/ijbOsWitZdNHpjNduh8xtPyEYdw2tsWz2rB6jZ5JbQA
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: e0eb8757-182f-49f3-94a4-1587d16f5094id: ff2b9b37-92e0-45fc-b853-379d44c08c89
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 278
ht-degree: 0%

---

# Client Hints und die [!UICONTROL Adobe Target Delivery API]

Client Hints müssen bei der Angebotsanfrage an [!DNL Adobe Target] gesendet werden.

Im Allgemeinen wird empfohlen, alle verfügbaren Client Hints an [!DNL Target] zu senden. Weitere Informationen finden Sie [User-agent und Client Hints](/help/dev/implement/client-side/atjs/user-agent-and-client-hints.md) im Abschnitt [Client-seitige Implementierung](../../implement/client-side/overview.md).

## Bereitstellungs-API - Direktaufrufe

### Vom Browser

In diesem Fall sendet der Browser Client Hints mit niedriger Entropie automatisch über Anfrage-Header an [!DNL Target]. Es gibt jedoch einige Einschränkungen auf Browser-Ebene bei dieser Implementierung. Erstens - es werden keine Client Hints-Header vom Browser gesendet, es sei denn, die Anfrage erfolgt über HTTPS. Zweitens - Client-Hinweise werden bei der ersten Anforderung nicht an [!DNL Target] auf der Seite gesendet. Client Hints-Header werden nur bei der zweiten Anfrage und danach bei allen Anfragen gesendet. Dies bedeutet, dass die Zielgruppensegmentierung und Personalisierung vom [!DNL Target] beim ersten Seitenbesuch nicht durchgeführt werden kann. Um diese beiden Einschränkungen zu umgehen, empfehlen wir dringend, die User Agent Client Hints-API im Browser zu verwenden, um die Client Hints direkt zu erfassen und über die Anfrage-Payload zu senden.

### Von einem Server

In diesem Fall müssen die Client Hints manuell vom Browser an [!DNL Target] auf der Bereitstellungs-API-Anfrage weitergeleitet werden.

```
curl -X POST 'http://mboxedge28.tt.omtrdc.net/rest/v1/delivery?client=myClientCode&sessionId=abcdefghijkl00014' -d '{
  "context": {
    "userAgent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Safari/537.36",
    "clientHints": {
      "Sec-CH-UA-Model": "iPhone",
      "Sec-CH-UA-Mobile": true,
      "Sec-CH-UA-Platform": "iOS",
      "Sec-CH-UA": "[ { \"brand\": \"Chromium\", \"version\": \"91\" }, { \"brand\": \" Not;A Brand\", \"version\": \"99\" } ]",
      "Sec-CH-UA-Full-Version-List": "[ { \"brand\": \"Chromium\", \"version\": \"91.1.1.1\" }, { \"brand\": \" Not;A Brand\", \"version\": \"99.1.1.1\" } ]",
      "Sec-CH-UA-Platform-Version": "10.0.0",
      "Sec-CH-UA-Arch": "x86",
      "Sec-CH-UA-Bitness": "64"
    }
  },
  "execute": {
    "mboxes": [{
      "name": "home",
      "index": 1
    }]
  }
}'
```

## Formatierung

Die Client Hints-Header Sec-CH-UA und Sec-CH-UA-Full-Version-List haben ein anderes Format als die Ergebnisse aus der Browser-API für Client Hints (navigator.userAgentData.brands/navigator.userAgentData.getHighEntropyValues). Beide Formate werden von der Bereitstellungs-API akzeptiert. Die Bereitstellungs-API normalisiert die Werte in das in den Anfragekopfzeilen verwendete Format. Dies ist wichtig, wenn Sie in Profilskripten auf Client-Hinweise zugreifen.
