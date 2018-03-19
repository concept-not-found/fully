# @fully specified and tested single function packages

## Problem with npm packages
 * Hard to trust tiny unused packages
 * Packages with deep dependencies have a huge security surface area
 * Packages don't need to follow semver
 * Large packages bloat webapp bundles
 * Premature "minification" of packages bloat code size
 
## Solution: @fully trusted packages
@fully earns your trust by fully specifying and testing functions. @fully follows [Compatible Versioning][1] to avoid "bug fixes" that break your code. @fully does not process the source code, making it easy verify the integrity.
 
### @fully specified
 * fixed number of arguments
 * specified valid set of parameters
 * specified behaviour for each valid set of parameters

### @fully tested
 * each specified behaviour is tested
 * exceed full test coverage
 
### @fully compatible
 * follows [Compatible Versioning][1]
 * specified with the goal of minimizing the need for change
 
### @fully transparent
 * all code is open source on github
 * all functions are unmanipulated with published sha512 hashes
 * source code is identical to one hosted in npm
 
## @fully principles
 * pragmatic over completeness or minimalism
 * correctness over purity
 * layman over functional goobly goop

## Common features
 * [pure function][4]
 * [currying][2]
 * exported as [ES6 modules][3]
 
## Alternatives
 * [Ramda][5] with [babel-plugin-ramda][6]
 * [Lodash][7] with [babel-plugin-lodash][8] or [lodash-modularized][9]

[1]: https://github.com/staltz/comver
[2]: http://fr.umio.us/favoring-curry/
[3]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import
[4]: https://en.wikipedia.org/wiki/Pure_function
[5]: http://ramdajs.com
[6]: https://www.npmjs.com/package/babel-plugin-ramda
[7]: https://lodash.com
[8]: https://www.npmjs.com/package/babel-plugin-lodash
[9]: https://www.npmjs.com/browse/keyword/lodash-modularized
