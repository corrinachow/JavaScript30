# JS + CSS Clock

This exercise creates a live analog clock using only JavaScript and CSS.

## Live Demo

[CodePen](https://codepen.io/julianmintz/full/JpNXEa/)

## Notes

`transform-origin: 100%` changes the point of rotation to the end of the element (x-axis).  By default the element rotates on its centre axis (default transform origin: 50%)

`transform: rotate(90deg)` changes the hand position to point to 12 o'clock (π/2).  The default position is equivalent to π.

```css
    .hand {
...
      transform-origin: 100%;
      transform: rotate(90deg);
```

`new Date()` is used to get the current time.

`now.getSeconds()` retrieves the current second.

`(now.getSeconds() / 60) * 360` takes the current second, divides it by 60 seconds to get a ratio between the seconds hand and the 12 o'clock reference, and converts it into degrees by multiplying by 360 degrees

e.g. 40 seconds corresponds to an angle of (40 seconds/ 60 seconds) * 360 degrees = 240 degrees.  The same principle is used for the minute hand.

The hour hand needs to take into account the position of the minute hand (e.g. at 4:30, the hour hand should be half way between 4 and 5).  The minutes are factored in using `((now.getMinutes() / 60) * 30 )` where 30 degrees is represents the rotation from hour to the next.

`90` is added to offset the `transform: rotate(90deg)` added to the CSS, otherwise the hands would count degrees starting from the π position.

```JavaScript
  function setDate() {
    const now = new Date(),
    secondsDegrees = 6 * now.getSeconds() + 90,
    minutesDegrees = 6 * now.getMinutes() + 90,
    hourDegrees = (now.getHours() * 30) + ((now.getMinutes() / 60) * 30 ) + 90;
...
```

`.style.transform` access the transform property and changes it according to the degrees that was calculated in the previous step.  `setInterval` then calls on the setDate function every 1000 milliseconds (1 second).

```JavaScript
    secondHand.style.transform = `rotate(${secondsDegrees}deg)`;
    minuteHand.style.transform = `rotate(${minutesDegrees}deg)`;
    hourHand.style.transform = `rotate(${hourDegrees}deg)`;
  }
  setInterval(setDate, 1000);
```

## Resources

[Clock face SVG](https://cssanimation.rocks/clocks/)

The black circle in the centre of the clock is added using the `::after`[pseudo-class](https://www.w3schools.com/css/css_pseudo_classes.asp).

```css
.clock:after {
      background: #000;
      border-radius: 50%;
      content: "";
      position: absolute;
      left: 50%;
      top: 50%;
      transform: translate(-50%, -50%);
      width: 5%;
      height: 5%;
    }
```

[Create a grid background](https://stackoverflow.com/questions/3540194/how-to-make-a-grid-like-graph-paper-grid-with-just-css)

`linear-gradient(to right, lightblue 2px, transparent 2px)` creates a gradient that starts with a 2px *lightblue* line, the rest of the gradient is trasparent.  The same occurs on the y-axis.  This is repeated every 20 px x 20 px

```css
body {
      ...
      background-size: 20px 20px;
      background-image: linear-gradient(to right, lightblue 2px, transparent 2px), linear-gradient(to bottom, lightblue 2px, transparent 2px)
    }
