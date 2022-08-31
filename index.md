---
title: OnePlayer implementation with content-slots
---

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

The `<content-slot />` will load a OnePlayer, iFrame or Player collection.  
Once the te slot is done it will dispatch the `onReady` event.  
After the OnePlayer in inserted into the DOM, and is ready for use, it will also dispatch the `onReady` event.

```js
const contentSlot = document.querySelector('content-slot');
contentSlot.addEventListener('onReady', () => {
  const onePlayer = document.querySelector('one-player');
  onePlayer.addEventListener('onReady', () => {
    console.log('This is the first way');
  });
});
```

Although this is a clean way of waiting for all parts to be ready, it's also a little verbose.  
Therefore, the onePlayer also calls the `onePlayerReady` function once it's ready.  
You can already implement this function, wait for the player to be ready and go from there.

```js
function onePlayerReady(onePlayer) {
  // This onePlayer is the same as the reuslt of document.querySelector('one-player')
  console.log('This is the second way?!', onePlayer.state);
}
```

## Subscribe on playerState events

```js
function onePlayerReady() {
  subscribe();
}

function subscribe() {
  // The custom onePlayer way...
  onePlayer.events.on('onStateChange', (playerState) => {
    console.log('New Player state:', playerState);
  });

  // The native way...
  onePlayer.addEventListener('onStateChange', (evt) => {
    console.log('New Player state:', evt.detail);
  });
}
```

## Attributes of the OnePlayer

These are the supported attributes on the OnePlayer:

| Attribute | Type   | Optional | Default     | Change via API    |
| --------- | ------ | -------- | ----------- | ----------------- |
| theme     | string | true     | "lightMode" | Yes               |
| language  | string | true     | "nl"        | No \*<sup>1</sup> |

\*<sup>1</sup> = This will be implemented in the future

### 1. Add an attribute to the content-slot

While embedding the player in the html, set the attribute as an attribute

```html
<content-slot id="[slot-id]" theme="darkMode" language="en"></content-slot>
```

### With JavaScript

Select the OnePlayer element with JavaScript and set the attribute.

```js
function onePlayerReady() {
  onePlayer.theme = 'darkMode';
}
```

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
