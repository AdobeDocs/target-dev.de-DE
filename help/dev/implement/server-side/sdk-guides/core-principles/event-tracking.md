---
title: Ereignis-Tracking
description: Verwendung [!DNL Adobe Target]Die Ereignisverfolgungsfunktionen von , um Metriken effektiv zu messen, die für Ihr Unternehmen und Ihre Anwendungsfälle am wichtigsten sind.
exl-id: a47fa692-c633-4c53-82da-878b1e451a3f
feature: Implement Server-side
source-git-commit: 09a50aa67ccd5c687244a85caad24df56c0d78f5
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 3%

---

# Ereignis-Tracking

Verwendung [!DNL Adobe Target]Die Ereignisverfolgungsfunktionen von , um Metriken effektiv zu messen, die für Ihr Unternehmen und Ihre Anwendungsfälle am wichtigsten sind. Das Tracking von Ereignissen ist der Schlüssel zur Messung des Erfolgs Ihrer Experimentierungs- oder Personalisierungsaktivitäten, da sie Ihnen mitteilen, welche Variante oder welches Erlebnis gewinnt oder verliert. Dies hilft Ihnen zu verstehen, wie Ihre Benutzer mit Ihrem Produkt interagieren oder sich in einer sich ständig ändernden Landschaft entwickeln.

So verfolgen Sie Ereignisse bis [!DNL Adobe Target]-SDKs folgen Sie diesem zweistufigen Prozess:

1. Installieren Sie das SDK und stellen Sie den Code bereit, der Ereignisse an sendet. [!DNL Adobe Target].

1. Erstellen und Aktivieren einer [!DNL Adobe Target] -Aktivität mit einer Zielmetrik in der Benutzeroberfläche.

   ![ALT-Bild](./assets/report-settings.png)

## Zielmetriken und -ereignisse

Die folgende Tabelle definiert die Kombination aus Zielen und Ereignissen, die Sie definieren und mit einer [!DNL Target] Aktivität verwenden [!DNL Target]Reporting-Funktionen:

| Primäres Ziel | Ereignis- |
| --- | --- |
| Konversion | Eine Seite angezeigt, eine Mbox angezeigt und auf eine Mbox geklickt |
| Umsatz | mbox angezeigt und auf mbox geklickt |
| Interaktion | Seitenansichten, Kundenbewertung und Besuchszeit pro Site |

## Auslösen von Impressionen

Target SDKs rufen die zugrunde liegende [Bereitstellungs-API](/help/dev/implement/delivery-api/overview.md). Wenn sich ein execute -Objekt mit erforderlichen Parametern in der Anfrage selbst befindet, wird die Impression für qualifizierte Aktivitäten automatisch erhöht. SDK-Methoden, die eine Impression automatisch erhöhen, sind:

* getOffers()
* getAttributes()

>[!NOTE]
>
>Wenn ein Vorabruf-Objekt innerhalb der Anfrage übergeben wird, wird die Impression nicht automatisch für die Aktivitäten mit Mboxes innerhalb des Vorabruf-Objekts erhöht.

Die `sendNotifications` -Methode verwendet werden, um Ereignisse manuell an zu senden [!DNL Adobe Target] und Trigger eine Impression.

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
TargetClient.sendNotifications(options: Object): Promise
```

>[!TAB Java ]

```java {line-numbers="true"}
ResponseStatus TargetClient.sendNotifications(TargetDeliveryRequest request)
```

>[!ENDTABS]

## Beispielcode 

Die folgenden Codebeispiele funktionieren für alle Zielmetriktypen, unabhängig davon, ob es sich um Konversion, Umsatz oder Interaktion handelt.

### Anzeigen einer Seite oder Mbox

Dieses Beispiel ruft zunächst ein Target-Mbox-Angebot mit `getOffers`. Anschließend wird eine Anfrage mit einer Benachrichtigung erstellt, die auf diesem Mbox-Angebot basiert.

Benachrichtigung `type` -Eigenschaft auf `display`.

Um anzugeben, dass eine Seite angezeigt wurde, müssen Sie das Adressobjekt in der Benachrichtigungs-Payload angeben. Stellen Sie die URL entsprechend ein.

Bei Mboxes müssen Sie die mbox-Eigenschaft auf das Benachrichtigungsobjekt festlegen und basierend auf dem Optionsfeld im `targetResult`.

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

>[!TAB Java ]

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

### Auf eine mbox geklickt

Dieses Beispiel ruft zunächst ein Target-Mbox-Angebot mit `getOffers`. Anschließend wird eine Anfrage mit einer Benachrichtigung erstellt, die auf diesem Mbox-Angebot basiert.

Benachrichtigung `type` -Eigenschaft auf `click`.

Sie müssen die `mbox` -Eigenschaft auf dem Benachrichtigungsobjekt und stellen Sie basierend auf dem Metriken-Array im `targetResult`.

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

>[!TAB Java ]

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

### Anzeigen einer Ansicht

Dieses Beispiel ruft zunächst mithilfe von Zielansichten ab. `getOffers`. Anschließend wird basierend auf diesen Ansichten eine Anfrage mit einer Benachrichtigung erstellt.

Benachrichtigung `type` -Eigenschaft auf `display`.

Für Ansichten müssen Sie die `view` -Eigenschaft auf dem Benachrichtigungsobjekt und stellen Sie basierend auf dem Optionsfeld im targetResult-Objekt ein Array von Token bereit.

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

>[!TAB Java ]

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

### Klicken auf eine Ansicht

Dieses Beispiel ruft zunächst mithilfe von Zielansichten ab. `getOffers`. Anschließend wird eine Anfrage mit Benachrichtigungen basierend auf diesen Ansichten erstellt.

Benachrichtigung `type` -Eigenschaft auf `click`.

Sie müssen die `view` -Eigenschaft auf dem Benachrichtigungsobjekt und geben Sie ein Array von Token an, die auf dem Metriken-Array im targetResult basieren.

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

>[!TAB Java ]

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
