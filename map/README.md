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

// curried
> map(value => value + 1)([1, 2, 3])
[2, 3, 4]
```

## Specification

### `map((value, [index]), array)`
Returns an array containg results of applying each function to each value in array. Function can optionally use index of value.

### `map((value, [key]), object)`
Returns an object containing result of apply each function to each value in object. Function can optionally use key of value.

### `map(path, array)`
Returns an array containing end of path starting from each value in array.

## Unsuitable alternatives
| function        | array support      | array index support | object support     | object key support | property dot notation shorthand | curried + data last |
| ---             | :---:              | :---:               | :---:              | :---:              | :---:                           | :---:               |
| [ramda map][1]  | :heavy_check_mark: |                     | :heavy_check_mark: |                    |                                 | :heavy_check_mark:  |
| [lodash map][2] | :heavy_check_mark: | :heavy_check_mark:  | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark:              |                     |

[1]: http://ramdajs.com/docs/#map
[2]: https://lodash.com/docs/#map
[3]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map
