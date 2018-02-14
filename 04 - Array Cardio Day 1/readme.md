# Array Cardio 1

The following build-in array methods are covered in this exercise:

- [filter](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)
- [map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)
- [sort](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)
- [reduce](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce)

## Live Demo

TBD

## Notes

`filter()` creates a new array with all the elements that given the condition in the callback function.

The example returns a list of inventors born between 1500 and 1600.

```JavaScript
const fifteen = inventors.filter(inventor => inventor.year >= 1500 && inventor.year <= 1600);
```

`map()` method creates a new array with the results of the callback function on every element in the calling array.

The example loops through the `inventors` array and returns the inventor's first name followed by their last name:

```JavaScript
const fullNames = inventors.map(inventor => `${inventor.first} ${inventor.last}`);
```

`reduce()` applies a function against an accumulator using each element in the array from left to right.

```JavaScript
var totalYears = 0;

for(var i = 0; i < inventors.length; i++) {
  totalYears += inventors[i].year
}
```

Re-written using the `reduce()` method:

```JavaScript
const totalYears = inventors.reduce((total, inventor) => total + (inventor.passed - inventor.year), 0) //0 represents the initial value
```

`sort()` method loops through and sorts of element of an array according to the compare function.

To sort in ascending order, if `a` is larger than `b`, move `a` up an index:
```JavaScript
 arr.sort((a, b) => a > b ? 1 : -1);
```

Objects can be sorted using the values of their properties, where if `a` comes before `b`, its index is increased by 1:
```JavaScript
const alpha = people.sort((lastOne, nextOne) => {
      const [aLast, aFirst] = lastOne.split(', ');
      const [bLast, bFirst] = nextOne.split(', ');
      return aLast > bLast ? 1 : -1;
    });
```

## Resources

`.querySelector()` can be used on any DOM element, not just document
