---
title: Verwendung asynchroner Anforderungen im Java-SDK [!DNL Adobe Target] Java
description: Erfahren Sie, wie das Java-SDK [!DNL Target] asynchrone Anforderungen unterstützt, wodurch die effektive Zielzeit auf null reduziert werden kann.
feature: APIs/SDKs
exl-id: e11f8d16-76f6-4d39-822a-34a1cf7f623f
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 3%

---

# Asynchrone Anforderungen (Java)

## Beschreibung

Ein Vorteil der serverseitigen Integration besteht darin, dass Sie die enorme Bandbreite und die Computerressourcen, die auf Server-Seite verfügbar sind, mit Parallelismus nutzen können. [!DNL Target] Java SDK unterstützt asynchrone Anfragen, wodurch die effektive Zielzeit auf null reduziert werden kann.

## Unterstützte Methoden

### Methoden

```javascript {line-numbers="true"}
CompletableFuture<TargetDeliveryResponse> getOffersAsync(TargetDeliveryRequest request);
CompletableFuture<ResponseStatus> sendNotificationsAsync(TargetDeliveryRequest request);
CompletableFuture<Attributes> getAttributesAsync(TargetDeliveryRequest targetRequest, String ...mboxes);
```

## Beispiel

Ein Beispiel für einen `Spring`-Anwendungscontroller könnte wie folgt aussehen:

### Beispiel-Controller

```javascript {line-numbers="true"}
@RestController
public class TargetRestController {

    @Autowired
    private TargetClient targetJavaClient;

    @GetMapping("/mboxTargetOnlyAsync")
        public TargetDeliveryResponse mboxTargetOnlyAsync(
                @RequestParam(name = "mbox", defaultValue = "server-side-mbox") String mbox,
                HttpServletRequest request, HttpServletResponse response) {
            ExecuteRequest executeRequest = new ExecuteRequest()
                    .mboxes(getMboxRequests(mbox));

            TargetDeliveryRequest targetDeliveryRequest = TargetDeliveryRequest.builder()
                    .context(getContext(request))
                    .execute(executeRequest)
                    .cookies(getTargetCookies(request.getCookies()))
                    .build();
            CompletableFuture<TargetDeliveryResponse> targetResponseAsync =
                    targetJavaClient.getOffersAsync(targetDeliveryRequest);
            targetResponseAsync.thenAccept(tr -> setCookies(tr.getCookies(), response));
            simulateIO();
            TargetDeliveryResponse targetResponse = targetResponseAsync.join();
            return targetResponse;
        }

    /**
     * Function for simulating network calls like other microservices and database calls
     */
    private void simulateIO() {
        try {
            Thread.sleep(200L);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }

}
```

In diesem Beispiel wird davon ausgegangen, dass Sie [das SDK](initialize-sdk.md) als Frühjahrsbean initialisiert haben und über [Dienstprogrammmethoden](utility-methods.md) verfügen.

Die [!DNL Target] -Anfrage wird vor `simulateIO` ausgelöst und bis zum Zeitpunkt der Ausführung sollte das Zielergebnis ebenfalls bereit sein. Auch wenn dies nicht der Fall ist, werden Sie in den meisten Fällen erhebliche Einsparungen erzielen.
