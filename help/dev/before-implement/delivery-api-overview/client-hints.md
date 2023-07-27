---
title: Client-Hinweise zur Adobe Target-Bereitstellungs-API
description: Wie verwende ich Client-Hinweise im [!DNL Adobe Target] Bereitstellungs-API?
exl-id: 317b9d7d-5b98-464e-9113-08b899ee1455
feature: APIs/SDKs
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%

---

# Client-Hinweise und die [!UICONTROL Adobe Target-Bereitstellungs-API]

Client-Hinweise müssen an [!DNL Adobe Target] auf der Angebotsanforderung.

Im Allgemeinen wird empfohlen, alle verfügbaren Client-Hinweise an zu senden. [!DNL Target]. Weitere Informationen finden Sie unter [Benutzeragent und Client-Hinweise](/help/dev/implement/client-side/atjs/user-agent-and-client-hints.md) im [Clientseitige Implementierung](../../implement/client-side/overview.md) Abschnitt.

## Direkte Aufrufe der Bereitstellungs-API

### Über den Browser

In diesem Fall sendet der Browser Client-Hinweise mit geringer Entropie an [!DNL Target] automatisch über Anfragekopfzeilen. Bei dieser Implementierung gibt es jedoch einige Einschränkungen auf Browserebene. Zuerst werden vom Browser keine Client Hints-Header gesendet, es sei denn, die Anfrage wird über HTTPS gesendet. Zweitens: Client-Hinweise werden bei der ersten Anfrage an nicht gesendet [!DNL Target] auf der Seite. Client Hints-Header werden nur bei der zweiten Anforderung und anschließend bei allen Anfragen gesendet. Das bedeutet, dass die Zielgruppensegmentierung und Personalisierung nicht durch [!DNL Target] beim ersten Seitenbesuch. Um diese beiden Einschränkungen zu umgehen, empfehlen wir dringend, die User Agent Client Hints-API im Browser zu verwenden, um die Client-Hinweise direkt zu erfassen und in der Anfrage-Payload zu senden.

### Von einem Server

In diesem Fall müssen die Client-Hinweise manuell vom Browser an weitergeleitet werden [!DNL Target] auf der Anfrage der Bereitstellungs-API.

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

Die Header &quot;Client Hints&quot;Sec-CH-UA und Sec-CH-UA-Full-Version-List haben ein anderes Format als die Ergebnisse der Browser-API &quot;Client Hints&quot;(navigator.userAgentData.brands/navigator.userAgentData.getHighEntropyValues). Beide Formate werden von der Bereitstellungs-API akzeptiert. Die Bereitstellungs-API normalisiert die Werte in dem Format, das in den Anforderungsheadern verwendet wird. Beachten Sie dies beim Zugriff auf Client-Hints in Profilskripten.
