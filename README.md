# gleiten

super easy interactive html animations, based on vertical scroll, mouse position, etc.

## how to install

_coming soon_

## how to use

### standard way

```html
<p data-gleiten='{"0vh": {"rotate": "90deg", "opacity": 1},
                  "50vh": {"rotate": "0deg", "opacity": 0}}'>hellow</p>

<script>
window.addEventListener('load', function() {
  
  gleiten
    .animate()
    .on(gleiten.verticalScroll());
  
});
</script>
```

the `<p>` element will rotate 90 degrees and fades away as the page scrolls from `0vh` to `50vh`.

### bound to mouse motion

```html
<p id="main">hellow</p>

<script>
  window.addEventListener('load', function() {
    gleiten
      .animate(document.getElementById('main'), {
        '0vw': {translateX: '5vw', scale: 1.5},
        '50vw': { scale: 1 },
        '100vw': {translateX: '-5vw', scale: 1.5}
      })
      .on(gleiten.mouseMove.client.x);

    gleiten
      .animate(document.getElementById('main'), {
        '0vh': {translateY: '5vh', opacity: 0 },
        '50vh': { opacity: 1 },
        '100vh': {translateY: '-5vh', opacity: 0 }
      })
      .on(gleiten.mouseMove.client.y);
  });
</script>
```

the `<p#main>` element will move around, scale up and down and fade in and out as the mouse moves.

### multiple animations

```html
<p data-gleiten='{"0vh": {"scale": 1}, "50vh": {"scale": 2}}'>hellow</p>
<p>world!</p>

<script>
  window.addEventListener('load', function() {
  
    gleiten
      .animate()
      .on(gleiten.verticalScroll());
  
    gleiten
      .animate(document.getElementsByTagName('p'), {
        '0vh': {rotate: '0deg'},
        '50vh': {rotate: '90deg'}
      })
      .on(gleiten.verticalScroll());
  
  });
</script>
```

the first `<p>`(_hellow_) scales up and rotates, and the second `<p>`(_world!_) only rotates, as the page scrolls from `0vh` to `50vh`.

### bound to element scroll instead of document

```html
<div id="holder" style="height:50vh; overflow: auto">
  <div style="height: 100vh">
    <p data-gleiten='{"0vh": {"scale": 1}, "50vh": {"scale": 2}}'>hellow</p>
  </div>
</div>

<script>
  window.addEventListener('load', function() {
  
    gleiten
      .animate()
      .on(gleiten.verticalScroll(document.getElementById('holder')));
  
  });
</script>
```

will scale the `<p>` element up, but the animation is bound to scrolling of `#holder` element instead of body (body doesn't scroll).

### bound to a timeline

```html
<p data-gleiten='{"0s": {"scale": 1}, "1s": {"scale": 2}}'>hellow</p>

<script>
  window.addEventListener('load', function() {
  
    gleiten
      .animate()
      .on(gleiten.timeline('2s', { bounce: true }));
  
  });
</script>
```
