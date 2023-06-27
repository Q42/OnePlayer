---
title: OnePlayer implementation in app
---

[![Latest OnePlayer Version](https://img.shields.io/badge/OnePlayer-0.0.24-brightgreen)](https://oneplayer.42puzzles.com/)

## Embedding

```html
<iframe src="" />
```

## OnePlayer attributes

These are the supported attributes on the `<iframe/>`:

| Attribute   | Type   | Optional | Default     | Change via API |
| ----------- | ------ | -------- | ----------- | -------------- |
| id          | string | false    | -           | No             |
| theme       | string | true     | "lightMode" | setTheme       |
| language    | string | true     | "nl"        | setLanguage    |
| userId      | string | true     | undefined   | No             |
| isInWebView | bool   | true     | false       | setIsInWebView |

Set the attributes like this:

```html
<iframe src="[src]" theme="darkMode" language="en" userId="abc" isInWebView="true"></content-slot>
```