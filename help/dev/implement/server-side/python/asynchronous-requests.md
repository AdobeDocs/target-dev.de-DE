---
title: Verwenden asynchroner Anfragen in der Python [!DNL Adobe Target] SDK
description: Erfahren Sie [!DNL Target]  wie Python SDK asynchrone Anforderungen unterstützt, wodurch die effektive Zielzeit auf null reduziert werden kann.
feature: APIs/SDKs
exl-id: 44ab74e5-3c1a-49cf-9fff-fe523b0c2592
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 4%

---

# Asynchrone Anfragen (Python)

## Beschreibung

Ein Vorteil der Server-seitigen Integration besteht darin, dass die auf der Server-Seite verfügbaren enormen Bandbreite- und Rechenressourcen durch die Verwendung von Parallelität genutzt werden können. [!DNL Target] Python SDK unterstützt asynchrone Anfragen, die die effektive Zielzeit auf null reduzieren können.

## Unterstützte Methoden

### Python

```python {line-numbers="true"}
get_offers(options)
send_notifications(options)
get_attributes(mbox_names, options)
```

## Beispiel

Eine Beispielanwendung, die das asynchrone/erwartete Verhalten des `asyncio`-Moduls in Python 3.9+ verwendet, könnte wie folgt aussehen:

### Python

```python {line-numbers="true"}
async def execute_mboxes(self, mboxes):
    context = Context(channel=ChannelType.WEB)
    execute = ExecuteRequest(mboxes=mboxes)
    delivery_request = DeliveryRequest(context=context, execute=execute)

    get_offers_options = {
      "request": delivery_request
    }
    return await asyncio.to_thread(target_client.get_offers, get_offers_options)

async def get_target_delivery_response(mboxes):
    target_delivery_response = await execute_mboxes(mboxes)
    response = Response(target_delivery_response.get("response").to_str(), status=200, mimetype='application/json')
    return response

mboxes = [MboxRequest(name="a1-serverside-ab", index=1)]
return asyncio.run(get_target_delivery_response(mboxes)
```

In diesem Beispiel wird davon ausgegangen, dass Sie Python 3.9+ verwenden. Wenn Sie eine ältere Python-Version verwenden, können Sie weiterhin asynchrone Anfragen senden, indem Sie `options.callback` an `get_offers` übergeben. In der Beispiel-Flask-App finden Sie weitere Informationen zur asynchronen Ausführung mithilfe von Callbacks oder async/await ([) &#x200B;](https://github.com/adobe/target-python-sdk/blob/main/samples/app.py).
