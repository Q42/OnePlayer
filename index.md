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

## Player JavaScript ready

After the OnePlayer in inserted into the DOM, it goes through an initialisation phase. Only after this phase the player is ready to be used by JavaScript.  
To use the player once it's ready, you can use a native EventListener.

```js
const onePlayer = document.querySelector('one-player');
onePlayer.addEventListener('onReady', start);
```

## The use of themes

There are two different ways to set themes on the player.

### 1. Add it to the content-slot

While embedding the player in the html, set the theme as an attribute

```html
<content-slot id="[slot-id]" theme="darkMode"></content-slot>
```

### With JavaScript

Select the OnePlayer element with javascript and set the theme.  
The player must be ready with the earlier mention initialisation phase.

```js
const onePlayer = document.querySelector('one-player');
onePlayer.addEventListener('onReady', start);

function start() {
  onePlayer.theme = 'darkMode';
}
```

## Subscribe on playerState events

```js
const onePlayer = document.querySelector('one-player');
onePlayer.addEventListener('onReady', subscribe);

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
