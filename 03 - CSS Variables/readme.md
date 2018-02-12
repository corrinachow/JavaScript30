# Update CSS Variables with JS

This exercise uses JavaScript and [CSS variables](https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_variables) to make live changes to HTML elements.

## Live Demo

[CodePen](https://codepen.io/julianmintz/full/QQvVGo/)

## Notes

There are variables you can work with in [SASS](http://sass-lang.com/documentation/#Variables), but after the code is compiled, those values remain fixed.  With CSS variables, the values can be changed while running the program with JavaScript.

A variable is set using `--varName: <VALUE>;`

They need to be assigned to a component along with their default values:

```css
:root {
  --base: #2da58a;
  --spacing: 10px;
  --blur: 10px;
  --border-radius: 5px;
}
```

They are accessed using the `var()` function:

```css
img {
  padding: var(--spacing);
  background: var(--base);
  filter: blur(var(--blur));
  border-radius: var(--border-radius);
}

```

To access them using JavaScript, create a new variable selecting the element:

```JavaScript
  const inputs = document.querySelectorAll('.controls input');
```

Add event listeners for the inputs, for multiple inputs, use the `forEach()` method<sup>1</sup>.  The `change` and `mousemove` event listeners will wait for new slider or colour values.

```JavaScript
  inputs.forEach(input => input.addEventListener('change', handleUpdate));
  inputs.forEach(input => input.addEventListener('mousemove', handleUpdate));
```

The arbitrary `sizing` attribute is assigned to each element using data-&ast; to store the the desired units for the CSS styles (e.g. `px`, `%`).

`dataset` is an object that contains all the data attributes from an element.  Since the colours do not have a sizing attribute, `this.dataset.sizing` will return `undefined`.

Change the style using `.style.setProperty()` where `--${this.name}` fetches the input's `name` value, so it's important that the element's name in the HTML matches the CSS property.

```JavaScript
  function handleUpdate() {
    const suffix = this.dataset.sizing || '';
    document.documentElement.style.setProperty(`--${this.name}`, this.value + suffix);
  }
```

<sup>1</sup>: `document.querySelectorAll` will return an object called a [NodeList](https://developer.mozilla.org/en-US/docs/Web/API/NodeList) which differs from an array but possesses some array methods like `forEach()`.

## Resources

Image from [Alexas_Fotos](https://pixabay.com/en/peacock-beautiful-colorful-bird-3080897/) on Pixabay.

