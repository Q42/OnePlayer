---
title: OnePlayer implementation in app
---

[![Latest OnePlayer Version](https://img.shields.io/badge/OnePlayer-2.13.0-brightgreen)](https://oneplayer.42puzzles.com/)

## Embedding

When embedding the puzzles in an iOS or Android WebView, you can point to an iFrame that we generate for your puzzles.
In web, you can also use this implementation but it's preferred to use the [custom element implementation](/).

The URL is in the format `https://cdn.42puzzles.com/iframe/[CUSTOMER_ID]/[EMBED_ID]-cdn-file.html`

```html
<iframe src="[URL]" />
```

## OnePlayer parameters

You can specify start parameters by putting them in the querystring of the iFrame URL.

These are the supported querystring parameters on the `<iframe/>`:

| Attribute   | Type   | Optional | Default     | Change via API |
| ----------- | ------ | -------- | ----------- | -------------- |
| src         | string | false    | -           | No             |
| theme       | string | true     | "lightMode" | setTheme       |
| language    | string | true     | "nl"        | setLanguage    |
| userId      | string | true     | undefined   | No             |
| isInWebView | bool   | true     | false       | setIsInWebView |

Set the parameters like this:

```html
<iframe src="[URL]?theme=darkMode&language=en&userId=abc&isInWebView=true"></iframe>
```

## iOS

The recommended method is embedding the URL within a `WKWebView`.

In the `WKWebViewConfiguration`, add yourself as a script message handler. We send all messages over the `allMessages` messagehandler.

```
webViewConfiguration.userContentController.add(self, name: "allMessages")
```

The script message handler that you registered will then be called like this:

```
func userContentController(_ userContentController: WKUserContentController, didReceive message: WKScriptMessage) {
    guard message.name == "allMessages" else { return }
    … decode the message.body and handle it …
}
```

## Android

TODO

## The WKScriptMessage.body

- name: PlayerExternalEvent;
- prevState?: PlayerState;
- nextState?: PlayerState;
- data?: any;

### PlayerExternalEvent

These are the event types the players emits:

- started
- completed
- closed
- aborted
- share
- visitUrl
- all

### PlayerState

- initializing
- ready
- playing
- finished
