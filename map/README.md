# `map`
Like [Array.prototype.map][3], but made functional, added Object support, and property dot notation shorthand.
## Usage
**same as `[1, 2, 3].map(value => value + 1)`**
```js
> map(value => value + 1, [1, 2, 3])
[2, 3, 4]
```
**same as `[1, 2, 3].map((value, index) => value + index)`**
```js
> map((value, index) => value + index, [1, 2, 3])
[1, 3, 5]
```
**property shorthand**
```js
> map('name', [{name: 'bob', age: 34}, {name: 'fred', age: 18}, {name: 'alice', age: 27}])
['bob', 'fred', 'alice']
```
**property dot notation shorthand**
```js
> map('favorite.food', [{name: 'bob', favorite: {food: 'cookies'}}, {name: 'fred', favorite: {food: 'cake'}}, {name: 'alice', favorite: {food: 'cheese'}}])
['cookies', 'cake', 'cheese']
```
**returns undefined if property path is not present**
```js
> map('favorite.food', [{name: 'bob'}, {name: 'fred', favorite: {food: 'cake'}}])
[undefined, 'cake']
```
**Object support**
```js
> map(value => value + 1, {a: 1, b: 2, c: 3})
{a: 2, b: 3, c: 4}
```
**optional Object key**
```js
> map((value, key) => `${key}|${value}`, {a: 1, b: 2, c: 3})
{a: 'a|1', b: 'b|2', c: 'c|3'}
```
**currying**
```js
> map(value => value + 1)([1, 2, 3])
[2, 3, 4]
```

## Specification
### `output_array = map(function callback(value, index), input_array)`
### `output_array = map(function callback(value, index))(input_array)`
**empty input returns empty output**
```js
> map(x => x, [])
[]
```
**pure, input is unchanged**
```js
> input = [1, 2, 3]
[1, 2, 3]
> map(value => value + 1, input)
[2, 3, 4]
> input
[1, 2, 3]
```
**function is applied to each value in array**
```js
> map(value => ({value}), [1, 2, 3])
[{value: 1}, {value: 2}, {value: 3}]
```
**index is available to function**
```js
> map((value, index) => ({value, index}), [1, 2, 3])
[{value: 1, index: 0}, {value: 2, index: 1}, {value: 3, index: 2}]
```
**same order in input as output**
```js
> map(value => ({value}), [1, 2, 3])
[{value: 1}, {value: 2}, {value: 3}]
```
**values in sparse arrays are treated as undefined**
```js
> map((value, index) => ({value, index}), [1, , 3])
[{value: 1, index: 0}, {value: undefined, index: 1}, {value: 3, index: 2}]
```
**currying**
```js
> map(value => value + 1)([1, 2, 3])
[2, 3, 4]
```
**first parameter must be a function or string**
```js
> map(undefined, [])
Error: first parameter must be a function or string
```
**a thrown error, will be propagated**
```js
> map(() => throw new Error('oops'), [1, 2, 3])
Error: oops
```
**function will not be evaluated for empty array**
```js
> map(() => throw new Error('oops'), [])
[]
```

### `output_object = map(function callback(value, key), input_object)`
### `output_object = map(function callback(value, key))(input_object)`
**empty input returns empty output**
```js
> map(x => x, {})
{}
```
**pure, input is unchanged**
```js
> input = {a: 1, b: 2, c: 3}
{a: 1, b: 2, c: 3}
> map(value => value + 1, input)
{a: 2, b: 3, c: 4}
> input
{a: 1, b: 2, c: 3}
```
**function is applied to each value in object**
```js
> map(value => value + 1, {a: 1, b: 2, c: 3})
{a: 2, b: 3, c: 4}
```
**key is available to function**
```js
> map((value, key) => ({value, key}), {a: 1, b: 2, c: 3})
[{value: 1, key: 'a'}, {value: 2, key: 'b'}, {value: 3, key: 'c'}]
```
**only enumerable properties will be mapped**
```js
> input = {a: 1, b: 2, c: 3}
{a: 1, b: 2, c: 3}
> Object.defineProperty(input, 'd', {value: 4, enumerable: false})
{a: 1, b: 2, c: 3}
> map(value => value + 1, input)
{a: 2, b: 3, c: 4}
```
**currying**
```js
> map(value => value + 1)({a: 1, b: 2, c: 3})
{a: 2, b: 3, c: 4}
```
**first parameter must be a function or string**
```js
> map(undefined, {})
Error: first parameter must be a function or string
```
**a thrown error, will be propagated**
```js
> map(() => throw new Error('oops'), {a: 1, b: 2, c: 3})
Error: oops
```
**function will not be evaluated for empty object**
```js
> map(() => throw new Error('oops'), {})
[]
```

### `output_array = map(path, input_array)`
### `output_array = map(path)(input_array)`
**empty input returns empty output**
```js
> map('name', [])
[]
```
**pure, input is unchanged**
```js
> input = [{name: 'bob', age: 34}, {name: 'fred', age: 18}]
[{name: 'bob', age: 34}, {name: 'fred', age: 18}]
> map('name', [{name: 'bob', age: 34}, {name: 'fred', age: 18}])
['bob', 'fred']
> input
[{name: 'bob', age: 34}, {name: 'fred', age: 18}]
```
**string is path applied as accessor for each object in array**
```js
> map('name', [{name: 'bob', age: 34}, {name: 'fred', age: 18}])
['bob', 'fred']
```
**strings are dot separated paths applied as accessor for each object in array**
```js
> map('school.name', [{name: 'bob', school: {name: 'oxford'}}, {name: 'fred', school: {name: 'stanford'}])
['oxford', 'standford']
```
**same order in input as output**
```js
> map('name', [{name: 'bob', age: 34}, {name: 'fred', age: 18}])
['bob', 'fred']
```
**objects with no matching key return undefined**
```js
> map('name', [{name: 'bob', age: 34}, {age: 18}])
['bob', undefined]
```
**undefined values in array return undefined**
```js
> map('name', [{name: 'bob', age: 34}, undefined])
['bob', undefined]
```
**values in sparse arrays are treated as undefined**
```js
> map('name', [{name: 'bob', age: 34}, , {name: 'alice', age: 27}])
['bob', undefined, 'alice']
```
**currying**
```js
> map('name')([{name: 'bob', age: 34}, {name: 'fred', age: 18}])
['bob', 'fred']
```
**first parameter must be a function or string**
```js
> map(undefined, [])
Error: first parameter must be a function or string
```
**empty string is rejected as likely programming error**
```js
> map('', [{name: 'bob', age: 34}, {name: 'fred', age: 18}])
Error: first parameter cannot be empty string
```

### expected failures
**second parameter must be an array or object**
```js
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
