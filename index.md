---
title: OnePlayer implementation on web
---

[![Latest OnePlayer Version](https://img.shields.io/badge/OnePlayer-2.13.0-brightgreen)](https://oneplayer.42puzzles.com/)

## Embedding

To embed the OnePlayer in your website, start by adding the following script-element in the head of the html:

```html
<script
  type="module"
  src="https://cdn.42puzzles.com/slot/v1/slot.js"
  crossorigin
  async
  defer
></script>
```

Next, add the `<content-slot />` custom element somewhere in the body-element:

```html
<content-slot id="[slot-id]"></content-slot>
```

## ContentSlot and OnePlayer JavaScript ready

The `<content-slot />` will load an OnePlayer, iFrame or Player collection.  
Once the slot is done it will dispatch the `onReady` event.  
After the OnePlayer in inserted into the DOM, and is ready for use, it will also dispatch the `onReady` event.

```js
const contentSlot = document.querySelector('content-slot');
contentSlot.addEventListener('onReady', () => {
  const onePlayer = document.querySelector('one-player');
  onePlayer.addEventListener('onReady', () => {
    console.log('This is the first way!');
  });
});
```

Although this is a clean way of waiting for all parts to be ready, it's also a little verbose.  
Therefore, the onePlayer also calls the `onePlayerReady` function once it's ready.  
You can already implement this function, wait for the player to be ready and go from there.

```js
function onePlayerReady(onePlayer) {
  // This onePlayer is the same as the result of:
  // document.querySelector('one-player')
  console.log('This is the second way!');
}
```

## OnePlayer attributes

These are the supported attributes on the `<content-slot/>`:

| Attribute   | Type   | Optional | Default     | Change via API |
| ----------- | ------ | -------- | ----------- | -------------- |
| id          | string | false    | -           | No             |
| theme       | string | true     | "lightMode" | setTheme       |
| language    | string | true     | "nl"        | setLanguage    |
| userId      | string | true     | undefined   | No             |
| isInWebView | bool   | true     | false       | setIsInWebView |

While embedding the player in the html, set the attributes like this:

```html
<content-slot id="[id]" theme="darkMode" language="en" userId="abc" isInWebView="true"></content-slot>
```

## OnePlayer methods

### Start

Players can be configured to wait for the start method.  
This is how you start the player:

```js
function onePlayerReady(onePlayer) {
  onePlayer.start();
}
```

### Set theme & language

Use these methods to change the attributes set earlier

```js
function onePlayerReady(onePlayer) {
  onePlayer.setTheme('darkMode');
  onePlayer.setLanguage('nl');
}
```

## Subscribe to OnePlayer events

```js
function onePlayerReady(onePlayer) {
  // The custom onePlayer way...
  onePlayer.events.on('all', (eventObject) => {
    console.log('New event:', eventObject.name);
  });

  // The native way...
  onePlayer.addEventListener('all', (evt) => {
    console.log('New event:', evt.detail.name);
  });
}
```

### The eventObject

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

## Styling

Make sure the parent of the `<content-slot />` has a width and height for optimal performance.

```html
<style>
  .parent {
    /*or any other parent element*/
    margin: 0;
    padding: 0;
    height: 100vh;
    width: 100vw;
  }
</style>
```
