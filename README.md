# Harmony Standard Libary Format #

This is a collection of possible module sorting formats for Harmony. It is all
purely theoretical in nature, without any binding permanence.

## Rationale ##

JavaScript is one of the few modular languages at this point that doesn't
separate its standard core library into modules. The DOM implements its entire
API in the core namespace, which isn't very modular. Many developers use AMD or
Browserify to make their own code modular, even though the extended API is not.
Node developers have a neat API module library with few added globals to
interface with it, namely `require`, `module`, and `exports`. They still have
`process` as a global because of its more common use.

## Format ##

I have a couple personally proposed formats, but they aren't the only
possibilities out there, and I'm open to adding new ones to the list. These
below are simply bulleted tree diagrams. The types represented should be
relatively self-explanatory.

Notes on my suggestions:

1. `encodeURI(Component)`, `decodeURI(Component)`, and URIError have been
   combined into a single namespace called URI in my suggestions.
2. The choice of `@@module` to denote the standard library modules was inspired
   by the shorthand of `@@symbol` used by the ES6 spec to represent common
   symbols used internally by many of the built-in types and internal
   functions/methods. It is also already conveniently prohibited by both
   CommonJS/Node and AMD module systems.
3. You may/probably will have to rename the files before you test them. Here's a
   couple really easy one-liners for you to rename all of them:
   - Bash/many others: `for i in *;do cp $i ${i:2:-3};done`
   - Windows: `for /r %I in(*)do(set n=%i&&xcopy /r %n% %n:2:-3%)`

### Java/Closure-like ###

See ./java-like for import bindings if you want to test.

```js
/**
 * @@arrays
 *
 * The specialized array types (i.e. typed arrays).
 */
import Float32Array from '@@arrays/Float32Array';
import Float64Array from '@@arrays/Float64Array';
import Int8Array from '@@arrays/Int8Array';
import Int16Array from '@@arrays/Int16Array';
import Int32Array from '@@arrays/Int32Array';
import Uint8Array from '@@arrays/Uint8Array';
import Uint8ClampedArray from '@@arrays/Uint8ClampedArray';
import Uint16Array from '@@arrays/Uint16Array';
import Uint32Array from '@@arrays/Uint32Array';

/**
 * @@base
 *
 * The base types. All of these are automatically imported by default.
 */
import Array from '@@base/Array';
import Boolean from '@@base/Boolean';
import Error from '@@base/Error';
import EvalError from '@@base/EvalError';
import Function from '@@base/Function';
import Generator from '@@base/Generator';
import Number from '@@base/Number';
import Object from '@@base/Object';
import RangeError from '@@base/RangeError';
import ReferenceError from '@@base/ReferenceError';
import RegExp from '@@base/RegExp';
import Set from '@@base/Set';
import String from '@@base/String';
import Symbol from '@@base/Symbol';
import SyntaxError from '@@base/SyntaxError';
import TypeError from '@@base/TypeError';
import WeakMap from '@@base/WeakMap';
import WeakSet from '@@base/WeakSet';

/**
 * @@util
 *
 * The utility types and APIs.
 */
import ArrayBuffer from '@@base/ArrayBuffer';
import DataView from '@@base/DataView';
import Date from '@@base/Date';
import Intl from '@@base/Intl';
import JSON from '@@base/JSON';
import Promise from '@@base/Promise';
import Reflect from '@@base/Reflect';
import URI from '@@base/URI';
```

### Pythonic/Node-like ###

**Note:**

These modules are imported by default:

Module Name:       | Imported Binding:
-------------------|------------------
`@@Array`          | `Array`
`@@Boolean`        | `Boolean`
`@@EvalError`      | `EvalError`
`@@Function`       | `Function`
`@@Generator`      | `Generator`
`@@Number`         | `Number`
`@@Object`         | `Object`
`@@RangeError`     | `RangeError`
`@@ReferenceError` | `ReferenceError`
`@@RegExp`         | `RegExp`
`@@Set`            | `Set`
`@@String`         | `String`
`@@Symbol`         | `Symbol`
`@@SyntaxError`    | `SyntaxError`
`@@TypeError`      | `TypeError`
`@@WeakMap`        | `WeakMap`
`@@WeakSet`        | `WeakSet`

These are also marked in the list below with `// ** //`.

```js
import ArrayBuffer from '@@ArrayBuffer';
import Array from '@@Array';                   // ** //
import Boolean from '@@Boolean';               // ** //
import DataView from '@@DataView';
import Date from '@@Date';
import Error from '@@Error';                   // ** //
import EvalError from '@@EvalError';           // ** //
import Float32Array from '@@Float32Array';
import Float64Array from '@@Float64Array';
import Function from '@@Function';             // ** //
import Generator from '@@Generator';           // ** //
import Int16Array from '@@Int16Array';
import Int32Array from '@@Int32Array';
import Int8Array from '@@Int8Array';
import Intl from '@@Intl';
import JSON from '@@JSON';
import Number from '@@Number';                 // ** //
import Object from '@@Object';                 // ** //
import Promise from '@@Promise';
import RangeError from '@@RangeError';         // ** //
import ReferenceError from '@@ReferenceError'; // ** //
import Reflect from '@@Reflect';
import RegExp from '@@RegExp';                 // ** //
import Set from '@@Set';                       // ** //
import String from '@@String';                 // ** //
import Symbol from '@@Symbol';                 // ** //
import SyntaxError from '@@SyntaxError';       // ** //
import TypeError from '@@TypeError';           // ** //
import Uint16Array from '@@Uint16Array';
import Uint32Array from '@@Uint32Array';
import Uint8Array from '@@Uint8Array';
import Uint8ClampedArray from '@@Uint8ClampedArray';
import URI from '@@URI';
import WeakMap from '@@WeakMap';               // ** //
import WeakSet from '@@WeakSet';               // ** //
```

## License ##

For the minimal code that exists in this repository...

This is free and unencumbered public domain software. For more information, see
http://unlicense.org/ or the accompanying UNLICENSE file.
