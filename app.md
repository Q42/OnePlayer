---
title: OnePlayer implementation in app
---

[![Latest OnePlayer Version](https://img.shields.io/badge/OnePlayer-2.13.0-brightgreen)](https://oneplayer.42puzzles.com/)

## Embedding

```html
<iframe src="[src]" />
```

## OnePlayer parameters

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
<iframe src="[src]?theme=darkMode&language=en&userId=abc&isInWebView=true"></iframe>
```
