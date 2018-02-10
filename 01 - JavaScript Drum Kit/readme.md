# JavaScript Drum Kit

This project aims to imitate the functionality of a keyboard and reproduces 9 different sounds depending on the key pressed.

## Notes

Using the HTML [data-* ](https://developer.mozilla.org/en-US/docs/Learn/HTML/Howto/Use_data_attributes)attribute, each `div.key` and `audio` element is bound together with the `data-key` attribute.

```html
    <div data-key="65" class="key">
      <kbd>A</kbd>
      <span class="sound">clap</span>
    </div>
...
<audio data-key="65" src="sounds/clap.wav"></audio>
```

The script waits for a `keydown` event, then calls the `playSound` function when a key is pressed.

```JavaScript
window.addEventListener('keydown', playSound);
```

`document.querySelector()` returns the first element within the document that matches the selector, in this case, the path to the `audio` file and the `div.key`.

`audio` is used to play the sound clip, and 'playing' is added as an HTML element class to `.key` elements.

```JavaScript
function playSound(e) {
  const audio = document.querySelector(`audio[data-key="${e.keyCode}"]`);
  const key = document.querySelector(`.key[data-key="${e.keyCode}"]`);
  if(!audio) return;
  audio.currentTime = 0//rewinds to start
  audio.play();
  key.classList.add('playing');
};
```

An event listener is added to each `key` element, and when the transition from `.key` to `.playing` ends, the `removeTransition` function is called.

```JavaScript
const keys = document.querySelectorAll('.key');
keys.forEach(key => key.addEventListener('transitionend', removeTransition))
```

```css
.key {
...
  transition: all 0.07s ease;
...
}

.playing {
  transform: scale(1.1);
...
}
```

`removeTransition` checks if the argument `e` does not contain the property `transform`; if doesn't, the function execution ends.  If it does, as in, if `div.key` also has the class `.playing`, `.playing` is removed returning `div.key` to its original size.

```JavaScript
function removeTransition(e) {
  if (e.propertyName !== 'transform') return;
  this.classList.remove('playing');
}
```

## Events
- **key events:** user presses a key
- **transitionend:** a css transition has completed.
