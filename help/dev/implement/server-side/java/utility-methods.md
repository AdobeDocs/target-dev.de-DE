---
title: Verwenden von Dienstprogrammmethoden in der  [!DNL Adobe Target] -Java-SDK
description: Erfahren Sie, wie Sie Hilfsmethoden verwenden, die über Controller hinweg wiederverwendet werden können und in eine separate Dienstprogrammklasse verschoben werden können.
feature: APIs/SDKs
exl-id: 19418126-c4d8-4e6b-bb84-036b7fe0e6ec
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '47'
ht-degree: 2%

---

# Dienstprogrammmethoden (Java)

Diese Hilfsmethoden sind über Controller hinweg wiederverwendbar und können in eine separate Dienstprogrammklasse verschoben werden.

## Methoden

```javascript {line-numbers="true"}
public class TargetRequestUtils {

    public static Context getContext(HttpServletRequest request) {
        Context context = new Context()
                .channel(ChannelType.WEB)
                .timeOffsetInMinutes(330.0)
                .address(getAddress(request));
        return context;
    }

    public static Address getAddress(HttpServletRequest request) {
        Address address = new Address()
                .referringUrl(request.getHeader("referer"))
                .url(request.getRequestURL().toString());
        return address;
    }

    public static List<TargetCookie> getTargetCookies(Cookie[] cookies) {
        if (cookies == null) {
            return Collections.emptyList();
        }
        return Arrays.stream(cookies)
                .filter(Objects::nonNull)
                .filter(cookie -> CookieUtils.getTargetCookieNames().contains(cookie.getName()))
                .map(cookie -> new TargetCookie(cookie.getName(), cookie.getValue(), cookie.getMaxAge()))
                .collect(Collectors.toList());
    }

    public static HttpServletResponse setCookies(List<TargetCookie> targetCookies,
                                                  HttpServletResponse response) {
        targetCookies
                .stream()
                .map(targetCookie -> new Cookie(targetCookie.getName(), targetCookie.getValue()))
                .forEach(cookie -> {
                    cookie.setPath("/");
                    response.addCookie(cookie);
                });
        return response;
    }

    public static List<MboxRequest> getMboxRequests(String... name) {
        List<MboxRequest> mboxRequests = new ArrayList<>();
        for (int i = 0; i < name.length; i++) {
            mboxRequests.add(new MboxRequest().name(name[i]).index(i));
        }
        return mboxRequests;
    }

    public static PrefetchRequest getPrefetchRequest() {
        PrefetchRequest prefetchRequest = new PrefetchRequest();
        ViewRequest viewRequest = new ViewRequest();
        prefetchRequest.setViews(Arrays.asList(viewRequest));
        return prefetchRequest;
    }
}
```
