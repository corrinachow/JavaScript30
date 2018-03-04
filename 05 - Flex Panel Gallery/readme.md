# Flex Panel Gallery

This exercise creates a flexbox panel gallery.

## Live Demo

[CodePen](https://codepen.io/julianmintz/full/WMZZvL/)

## Notes

The panels are set up by defining a flex container using `display: flex` and `flex-direction: column` to align them vertically.  `flex: 1` evenly distributes the individual panels across the page.

```css
.panels {
  min-height:100vh;
  overflow: hidden;
  display: flex;
}

.panel {
  ...
  flex: 1;
  flex-direction: column;
}
```

`.panel` is also going to contain the transition properties which will be listened for in the JS:

```css
transition:
  font-size 0.7s cubic-bezier(0.61,-0.19, 0.7,-0.11),
  flex 0.7s cubic-bezier(0.61,-0.19, 0.7,-0.11),
  background 0.2s;
```

The children of the panel also have a transition effect:

```css
.panel > * {
  transition:transform 0.5s;
  ...
}
```

To hide the top and bottom elements when a panel is inactive, it is translated by 100% in either direction on the y-axis:
```css
.panel > *:first-child {transform: translateY(-100%); }
.panel > *:last-child {transform: translateY(100%); }
```

They will appear when a panel is opened by translating them to their default positionat 0%:

```css
.panel.open-active > *:first-child {transform: translateY(0%); }
.panel.open-active > *:last-child {transform: translateY(0%); }
```

The effect to make the panel larger is done so using the `flex` property.  Because the value is set to 5, it will take up 5 times as much space as the original:
```css
.panel.open {
  font-size:40px;
  flex: 5;
}
```

The JavaScript contains the event listeners for `'click'` which toggles the panels opening and closing (changing the flex value from 1 to 5), and listens for a transition end event where the property name includes the string 'flex'.

This is done to account for the naming discrepancies between browsers.


```
const panels = document.querySelectorAll('.panel');

function toggleOpen() {
  this.classList.toggle('open')
}

//Chrome + FF transitionend event.propertyName === flex-grow
//Safari transitionend event.propertyName === flex
function toggleActive(e) {
  if (e.propertyName.includes('flex')) {
    this.classList.toggle('open-active')
  }
}

panels.forEach(panel => panel.addEventListener('click', toggleOpen));
panels.forEach(panel => panel.addEventListener('transitionend', toggleActive));
```

## Events

- **click**
- **transitionend**

## Resources

[A Complete Guide to Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/) from CSS-Tricks



