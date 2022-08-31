---
title: Implementeren van de OnePlayer met content-slots
---

## Embedding

Om de player in een website te embedden, zet je het volgende script-element in de head van de html:

```html
<script
  type="module"
  src="https://cdn.42puzzles.com/slot/v1/slot.js"
  crossorigin
  async
  defer
></script>
```

En vervolgens het `<content-slot>` custom element ergens in het body-element:

```html
<content-slot id="[slot-id]"></content-slot>
```

## Player ready voor JavaScript

Bij het inladen van de player doet deze een aantal initialisaties. Pas na initialisatie fase kan de player worden aangesproken door JavaScript.  
Om de player te gebruiken zodra deze klaar is, gebruik je een native EventListener.

```js
const onePlayer = document.querySelector('one-player');
onePlayer.addEventListener('onReady', start);
```

## Gebruik van thema's

Er zijn verschillende manieren om het thema op een player te zetten.

### Toevoegen aan het content slot.

Tijdens het embedden zet je het thema in de html

```html
<content-slot id="[slot-id]" theme="darkMode"></content-slot>
```

### Met JavaScript

Selecteer het onePlayer element met javascript en zet de naam van het thema.  
Hiervoor met de player wel klaar zijn met initialisatie fase.

```js
const onePlayer = document.querySelector('one-player');
onePlayer.addEventListener('onReady', start);

function start() {
  onePlayer.theme = 'darkMode';
}
```

## Subscribe op playerState events

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

Zorg er voor dat de parent van het content-slot een hoogte en breedte heeft, voor optimale werking.

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
