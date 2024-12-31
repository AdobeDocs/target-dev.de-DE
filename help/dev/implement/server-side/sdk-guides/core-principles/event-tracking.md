---
title: Ereignis-Tracking
description: Verwenden Sie  [!DNL Adobe Target] Ereignisverfolgungsfunktionen von , um Metriken effektiv zu messen, die für Ihr Unternehmen und Ihre Anwendungsfälle am wichtigsten sind.
exl-id: a47fa692-c633-4c53-82da-878b1e451a3f
feature: Implement Server-side
source-git-commit: 09a50aa67ccd5c687244a85caad24df56c0d78f5
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 2%

---

# Ereignis-Tracking

Nutzen Sie die Ereignisverfolgungsfunktionen von [!DNL Adobe Target], um effektiv Metriken zu messen, die für Ihr Unternehmen und Ihre Anwendungsfälle am wichtigsten sind. Das Nachverfolgen von Ereignissen ist der Schlüssel zur Messung des Erfolgs Ihrer Experimentier- oder Personalisierungsaktivitäten, da sie Ihnen mitteilen, welche Variante oder welches Erlebnis gewinnt oder verliert. Wenn Sie dies verstehen, können Sie besser verstehen, wie Ihre Benutzerinnen und Benutzer mit Ihrem Produkt interagieren oder sich in einer sich ständig verändernden Landschaft entwickeln.

Um Ereignisse über die SDKs von [!DNL Adobe Target] zu verfolgen, führen Sie diesen zweistufigen Prozess aus:

1. Installieren Sie SDK und stellen Sie Code bereit, der Ereignisse an [!DNL Adobe Target] sendet.

1. Erstellen und aktivieren Sie eine [!DNL Adobe Target] Aktivität mit einer Zielmetrik in der -Benutzeroberfläche.

   ![ALT-Bild](./assets/report-settings.png)

## Zielmetriken und Ereignisse

In der folgenden Tabelle wird die Kombination von Zielen und Ereignissen definiert, die Sie mit einer [!DNL Target] Aktivität mithilfe der Reporting-Funktionen von [!DNL Target] definieren und messen können:

| Primäres Ziel | Ereignis- |
| --- | --- |
| Konversion | hat eine Seite angezeigt, eine Mbox angezeigt und auf mbox geklickt |
| Umsatz | hat eine Mbox angezeigt und auf mbox geklickt |
| Interaktion | Seitenansichten, Kundenbewertung und Besuchszeit pro Site |

## Auslösen von Impressions

Target-SDKs rufen die zugrunde liegende [Bereitstellungs-API](/help/dev/implement/delivery-api/overview.md) auf. Wenn sich ein Ausführungsobjekt mit erforderlichen Parametern in der Anfrage selbst befindet, wird die Impression automatisch für qualifizierte Aktivitäten inkrementiert. SDK-Methoden, die eine Impression automatisch inkrementieren:

* getOffers()
* getAttributes()

>[!NOTE]
>
>Wenn ein Prefetch-Objekt innerhalb der Anfrage übergeben wird, wird die Impression für die Aktivitäten mit Mboxes innerhalb des Prefetch-Objekts nicht automatisch inkrementiert.

Die `sendNotifications`-Methode kann verwendet werden, um Ereignisse manuell an [!DNL Adobe Target] zu senden und eine Impression an den Trigger zu senden.

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
TargetClient.sendNotifications(options: Object): Promise
```

>[!TAB Java]

```java {line-numbers="true"}
ResponseStatus TargetClient.sendNotifications(TargetDeliveryRequest request)
```

>[!ENDTABS]

## Beispielcode 

Die folgenden Code-Beispiele funktionieren für alle Zielmetriktypen, unabhängig davon, ob es sich um Konversion, Umsatz oder Interaktion handelt.

### hat eine Seite oder Mbox angezeigt

Dieses Beispiel ruft zuerst ein Ziel-Mbox-Angebot mithilfe von `getOffers` ab. Anschließend wird eine Anfrage mit einer Benachrichtigung erstellt, die auf diesem Mbox-Angebot basiert.

Die Benachrichtigungs-`type` ist auf `display` festgelegt.

Um anzugeben, dass eine Seite angezeigt wurde, müssen Sie das Adressobjekt in der Benachrichtigungs-Payload angeben. Stellen Sie sicher, dass Sie die URL entsprechend einstellen.

Bei Mboxes müssen Sie die Eigenschaft „mbox“ für das Benachrichtigungsobjekt festlegen und ein Array von Token basierend auf dem Optionenarray im `targetResult` bereitstellen.

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");
const { v4: uuidv4 } = require("uuid");

const client = TargetClient.create({
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg",
  events: { clientReady: onTargetReady },
});

async function onTargetReady() {
  const targetResult = await client.getOffers({
    request: {
      targetRequest,
      prefetch: {
        mboxes: [
          {
            name: "homepage",
            index: 1
          }
        ]
      },
      sessionId: uuidv4()
    }
  });

  const { mboxes = [] } = targetResult.response.prefetch;

  const request = {
    context: { channel: "web" },
    notifications: mboxes.map(mbox => {
      const { options = [] } = mbox;

      return {
        id: targetResult.response.id,
        impressionId: uuidv4(),
        address: {
          url: "http://www.target-demo-site.com"
        },
        timestamp: new Date().getTime(),
        type: "display",
        mbox: {
          name: mbox.name
        },
        tokens: options.map(option => option.eventToken)
      };
    })
  };
  // send the notification event
  await client.sendNotifications({ request });
}
```

>[!TAB Java]

```java {line-numbers="true"}
ClientConfig clientConfig = ClientConfig.builder()
                .client("acmeclient")
                .organizationId("1234567890@AdobeOrg")
                .build();

TargetClient targetClient = TargetClient.create(clientConfig);

Context context = new Context()
        .channel(ChannelType.WEB)
        .address(new Address().url("http://www.target-demo-site.com"));

TargetDeliveryResponse targetResult = targetJavaClient.getOffers(TargetDeliveryRequest.builder()
        .context(context
        )
        .prefetch(new PrefetchRequest()
                .mboxes(new ArrayList() {{
                    add(new MboxRequest().name("homepage").index(1));
                }})
        )
        .build());

List<Notification> notifications = new ArrayList<>();
List<PrefetchMboxResponse> mboxes = targetResult.getResponse().getPrefetch().getMboxes();

for (PrefetchMboxResponse mbox : mboxes) {
    List<Option> options = mbox.getOptions();

    notifications.add((Notification) new Notification()
            .id(targetResult.getResponse().getRequestId())
            .impressionId(UUID.randomUUID().toString())
            .timestamp(System.currentTimeMillis())
            .type(MetricType.DISPLAY)
            .mbox(new NotificationMbox().name(mbox.getName()))
            .tokens(options.stream().map(Option::getEventToken).collect(Collectors.toList()))
            .address(new Address().url("http://www.target-demo-site.com"))
    );
}

TargetDeliveryRequest notificationRequest = TargetDeliveryRequest.builder()
        .context(context)
        .notifications(notifications).build();

targetJavaClient.sendNotifications(notificationRequest);
```

>[!ENDTABS]

### Auf eine Mbox geklickt

Dieses Beispiel ruft zuerst ein Ziel-Mbox-Angebot mithilfe von `getOffers` ab. Anschließend wird eine Anfrage mit einer Benachrichtigung erstellt, die auf diesem Mbox-Angebot basiert.

Die Benachrichtigungs-`type` ist auf `click` festgelegt.

Sie müssen die `mbox`-Eigenschaft für das Benachrichtigungsobjekt festlegen und ein Array von Token bereitstellen, das auf dem Metrik-Array im `targetResult` basiert.

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");
const { v4: uuidv4 } = require("uuid");

const client = TargetClient.create({
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg",
  events: { clientReady: onTargetReady },
});

async function onTargetReady() {
  const targetResult = await client.getOffers({
    request: {
      targetRequest,
      prefetch: {
        mboxes: [
          {
            name: "homepage",
            index: 1
          }
        ]
      },
      sessionId: uuidv4()
    }
  });

  const { mboxes = [] } = targetResult.response.prefetch;

  const request = {
    context: { channel: "web" },
    notifications: mboxes.map(mbox => {
      const { options = [], metrics = [] } = mbox;

      return {
        id: targetResult.response.id,
        impressionId: uuidv4(),
        address: {
          url: "http://www.target-demo-site.com"
        },
        timestamp: new Date().getTime(),
        type: "click",
        mbox: {
          name: mbox.name
        },
        tokens: metrics
                  .filter(metric => metric.type === "click")
                  .map(metric => metric.eventToken)
      };
    })
  };
  // send the notification event
  await client.sendNotifications({ request });
}
```

>[!TAB Java]

```java {line-numbers="true"}
ClientConfig clientConfig = ClientConfig.builder()
                .client("acmeclient")
                .organizationId("1234567890@AdobeOrg")
                .build();

TargetClient targetClient = TargetClient.create(clientConfig);

Context context = new Context()
        .channel(ChannelType.WEB)
        .address(new Address().url("http://www.target-demo-site.com"));

TargetDeliveryResponse targetResult = targetJavaClient.getOffers(TargetDeliveryRequest.builder()
        .context(context
        )
        .prefetch(new PrefetchRequest()
                .mboxes(new ArrayList() {{
                    add(new MboxRequest().name("homepage").index(1));
                }})
        )
        .build());

List<Notification> notifications = new ArrayList<>();
List<PrefetchMboxResponse> mboxes = targetResult.getResponse().getPrefetch().getMboxes();

for (PrefetchMboxResponse mbox : mboxes) {
    List<Metric> metrics = mbox.getMetrics();

    notifications.add((Notification) new Notification()
            .id(targetResult.getResponse().getRequestId())
            .impressionId(UUID.randomUUID().toString())
            .timestamp(System.currentTimeMillis())
            .type(MetricType.CLICK)
            .mbox(new NotificationMbox().name(mbox.getName()))
            .tokens(metrics.stream()
                    .filter(metric -> MetricType.CLICK.equals(metric.getType()))
                    .map(Metric::getEventToken)
                    .collect(Collectors.toList()))
            .address(new Address().url("http://www.target-demo-site.com"))
    );
}

TargetDeliveryRequest notificationRequest = TargetDeliveryRequest.builder()
        .context(context)
        .notifications(notifications).build();

targetJavaClient.sendNotifications(notificationRequest);
```

>[!ENDTABS]

### Ansicht angezeigt

Dieses Beispiel ruft zunächst Zielansichten mithilfe von `getOffers` ab. Anschließend wird eine Anfrage mit einer auf diesen Ansichten basierenden Benachrichtigung erstellt.

Die Benachrichtigungs-`type` ist auf `display` festgelegt.

Für Ansichten müssen Sie die `view`-Eigenschaft für das Benachrichtigungsobjekt festlegen und ein Array von Token bereitstellen, das auf dem Optionenarray im targetResult basiert.

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");
const { v4: uuidv4 } = require("uuid");

const client = TargetClient.create({
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg",
  events: { clientReady: onTargetReady },
});

async function onTargetReady() {
  const targetResult = await client.getOffers({
    request: {
      targetRequest,
      prefetch: {
        views: [{}]
      },
      sessionId: uuidv4()
    }
  });

  const { views = [] } = targetResult.response.prefetch;

  const request = {
    context: { channel: "web" },
    notifications: views.map(view => {
      const { options = [], metrics = [] } = view;

      return {
        id: targetResult.response.id,
        impressionId: uuidv4(),
        address: {
          url: "http://www.target-demo-site.com"
        },
        timestamp: new Date().getTime(),
        type: "display",
        view: {
          name: view.name
        },
        tokens: options.map(option => option.eventToken)
      };
    })
  };
  // send the notification event
  await client.sendNotifications({ request });
}
```

>[!TAB Java]

```java {line-numbers="true"}
ClientConfig clientConfig = ClientConfig.builder()
                .client("acmeclient")
                .organizationId("1234567890@AdobeOrg")
                .build();

TargetClient targetClient = TargetClient.create(clientConfig);

Context context = new Context()
        .channel(ChannelType.WEB)
        .address(new Address().url("http://www.target-demo-site.com"));

TargetDeliveryResponse targetResult = targetJavaClient.getOffers(TargetDeliveryRequest.builder()
        .context(context)
        .prefetch(new PrefetchRequest()
                .views(new ArrayList() {{
                    add(new ViewRequest());
                }})
        )
        .build());

List<Notification> notifications = new ArrayList<>();
List<View> views = targetResult.getResponse().getPrefetch().getViews();

for (View view : views) {
    List<Option> options = view.getOptions();
    List<Metric> metrics = view.getMetrics();

    notifications.add((Notification) new Notification()
            .id(targetResult.getResponse().getRequestId())
            .impressionId(UUID.randomUUID().toString())
            .timestamp(System.currentTimeMillis())
            .type(MetricType.DISPLAY)
            .view(new NotificationView().name(view.getName()))
            .tokens(options.stream().map(Option::getEventToken).collect(Collectors.toList()))
            .address(new Address().url("http://www.target-demo-site.com"))
    );
}

TargetDeliveryRequest notificationRequest = TargetDeliveryRequest.builder()
        .context(context)
        .notifications(notifications).build();

targetJavaClient.sendNotifications(notificationRequest);
```

>[!ENDTABS]

### Auf Ansicht geklickt

Dieses Beispiel ruft zunächst Zielansichten mithilfe von `getOffers` ab. Anschließend wird eine Anfrage mit Benachrichtigungen basierend auf diesen Ansichten erstellt.

Die Benachrichtigungs-`type` ist auf `click` festgelegt.

Sie müssen die `view`-Eigenschaft für das Benachrichtigungsobjekt festlegen und ein Array von Token bereitstellen, das auf dem Metrik-Array im targetResult basiert.

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");
const { v4: uuidv4 } = require("uuid");

const client = TargetClient.create({
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg",
  events: { clientReady: onTargetReady },
});

async function onTargetReady() {
  const targetResult = await client.getOffers({
    request: {
      targetRequest,
      prefetch: {
        views: [{}]
      },
      sessionId: uuidv4()
    }
  });

  const { views = [] } = targetResult.response.prefetch;

  const request = {
    context: { channel: "web" },
    notifications: views.map(view => {
      const { options = [], metrics = [] } = view;

      return {
        id: targetResult.response.id,
        impressionId: uuidv4(),
        address: {
          url: "http://www.target-demo-site.com"
        },
        timestamp: new Date().getTime(),
        type: "click",
        view: {
          name: view.name
        },
        tokens: metrics
                  .filter(metric => metric.type === "click")
                  .map(metric => metric.eventToken)
      };
    })
  };
  // send the notification event
  await client.sendNotifications({ request });
}
```

>[!TAB Java]

```java {line-numbers="true"}
ClientConfig clientConfig = ClientConfig.builder()
                .client("acmeclient")
                .organizationId("1234567890@AdobeOrg")
                .build();

TargetClient targetClient = TargetClient.create(clientConfig);

Context context = new Context()
        .channel(ChannelType.WEB)
        .address(new Address().url("http://www.target-demo-site.com"));

TargetDeliveryResponse targetResult = targetJavaClient.getOffers(TargetDeliveryRequest.builder()
        .context(context)
        .prefetch(new PrefetchRequest()
                .views(new ArrayList() {{
                    add(new ViewRequest());
                }})
        )
        .build());

List<Notification> notifications = new ArrayList<>();
List<View> views = targetResult.getResponse().getPrefetch().getViews();

for (View view : views) {
    List<Option> options = view.getOptions();
    List<Metric> metrics = view.getMetrics();

    notifications.add((Notification) new Notification()
            .id(targetResult.getResponse().getRequestId())
            .impressionId(UUID.randomUUID().toString())
            .timestamp(System.currentTimeMillis())
            .type(MetricType.CLICK)
            .view(new NotificationView().name(view.getName()))
            .tokens(metrics.stream()
                    .filter(metric -> MetricType.CLICK.equals(metric.getType()))
                    .map(Metric::getEventToken)
                    .collect(Collectors.toList()))
            .address(new Address().url("http://www.target-demo-site.com"))
    );
}

TargetDeliveryRequest notificationRequest = TargetDeliveryRequest.builder()
        .context(context)
        .notifications(notifications).build();

targetJavaClient.sendNotifications(notificationRequest);
```

>[!ENDTABS]
