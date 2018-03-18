# `map`
Like [Array.prototype.map][3], but made functional, added Object support, and property dot notation shorthand.
## Usage
```js
// same as [1, 2, 3].map(value => value + 1)
> map(value => value + 1, [1, 2, 3])
[2, 3, 4]

// same as [1, 2, 3].map((value, index) => value + index)
> map((value, index) => value + index, [1, 2, 3])
[1, 3, 5]

// property shorthand
> map('name', [{name: 'bob', age: 34}, {name: 'fred', age: 18}, {name: 'alice', age: 27}])
['bob', 'fred', 'alice']

// property dot notation shorthand
> map('favorite.food', [{name: 'bob', favorite: {food: 'cookies'}}, {name: 'fred', favorite: {food: 'cake'}}, {name: 'alice', favorite: {food: 'cheese'}}])
['cookies', 'cake', 'cheese']

// Object support
> map(value => value + 1, {a: 1, b: 2, c: 3})
{a: 2, b: 3, c: 4}

// optional Object key
> map((value, key) => `${key}|${value}`, {a: 1, b: 2, c: 3})
{a: 'a|1', b: 'b|2', c: 'c|3'}

// currying
> map(value => value + 1)([1, 2, 3])
[2, 3, 4]
```

## Specification
### `map((value, [index]), array)`
```js
// pure, input is unchanged
> input = [1, 2, 3]
[1, 2, 3]
> map(value => value + 1, array)
[2, 3, 4]
> input
[1, 2, 3]

// function is applied to each value in array in the same order as array
> map(value => ({value}), [1, 2, 3])
[{value: 1}, {value: 2}, {value: 3}]

// index is available to function
> map((value, index) => ({value, index}), [1, 2, 3])
[{value: 1, index: 0}, {value: 2, index: 1}, {value: 3, index: 2}]

// values in sparse arrays are treated as undefined
> map((value, index) => ({value, index}), [1, , 3])
[{value: 1, index: 0}, {value: undefined, index: 1}, {value: 3, index: 2}]

// currying
> map(value => value + 1)([1, 2, 3])
[2, 3, 4]

// first parameter must be a function or string
> map(undefined, [])
Error: first parameter must be a function or string

// a thrown error, will be propagated
> map(() => throw new Error('oops'), [1, 2, 3])
Error: oops

// function will not be evaluated for empty array
> map(() => throw new Error('oops'), [])
[]
```

### `map((value, [key]), object)`
```js
```

### `map(path, array)`
```js
```

### expected failures
```js
// second parameter must be an array or object
> map(x => x, undefined)
Error: second parameter must be an array or object

```

## Unsuitable alternatives
| function        | array support      | array index support | object support     | object key support | property dot notation shorthand | currying + data last |
| ---             | :---:              | :---:               | :---:              | :---:              | :---:                           | :---:                |
| [ramda map][1]  | :heavy_check_mark: |                     | :heavy_check_mark: |                    |                                 | :heavy_check_mark:   |
| [lodash map][2] | :heavy_check_mark: | :heavy_check_mark:  | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark:              |                      |

[1]: http://ramdajs.com/docs/#map
[2]: https://lodash.com/docs/#map
[3]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map
