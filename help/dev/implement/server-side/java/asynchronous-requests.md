---
title: Verwenden asynchroner Anforderungen in der [!DNL Adobe Target] Java-SDK
description: Erfahren Sie, wie [!DNL Target] Java SDK asynchrone Anfragen unterstützt, die die effektive Zielzeit auf null reduzieren können.
feature: APIs/SDKs
exl-id: e11f8d16-76f6-4d39-822a-34a1cf7f623f
TQID: 'https://experienceleague.adobe.com/Y9oTl8aU4-4HpMajdmy5KfvAwEFOpV0y9vUg7BdBRk8'
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
    internal-label: Target
feature_v2:
  - id: a19e8738-9679-599a-b83b-5f2f15f8e4d6
    internal-label: APIs/SDKs
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 5d119ccf18b09b3ba864a69642458597f65c754f
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 3%
---
# Asynchrone Anforderungen (Java)

## Beschreibung

Ein Vorteil der Server-seitigen Integration besteht darin, dass die auf der Server-Seite verfügbaren enormen Bandbreite- und Rechenressourcen durch die Verwendung von Parallelität genutzt werden können. [!DNL Target] Java SDK unterstützt asynchrone Anfragen, die die effektive Zielzeit auf null reduzieren können.

## Unterstützte Methoden

### Methoden

```javascript {line-numbers="true"}
CompletableFuture<TargetDeliveryResponse> getOffersAsync(TargetDeliveryRequest request);
CompletableFuture<ResponseStatus> sendNotificationsAsync(TargetDeliveryRequest request);
CompletableFuture<Attributes> getAttributesAsync(TargetDeliveryRequest targetRequest, String ...mboxes);
```

## Beispiel

Ein Beispiel für `Spring` Anwendungs-Controller könnte wie folgt aussehen:

### Stichprobenkontroller

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

In diesem Beispiel wird davon ausgegangen[ dass Sie SDK als ](initialize-sdk.md)-Bean initialisiert haben und [Dienstprogrammmethoden](utility-methods.md) verfügbar sind.

Die [!DNL Target]-Anfrage wird vor dem `simulateIO` ausgelöst und zum Zeitpunkt ihrer Ausführung sollte auch das Zielergebnis bereit sein. Selbst wenn dies nicht der Fall ist, werden Sie in den meisten Fällen erhebliche Einsparungen erzielen.
