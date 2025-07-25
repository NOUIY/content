---
title: Iterator.prototype.every()
short-title: every()
slug: Web/JavaScript/Reference/Global_Objects/Iterator/every
page-type: javascript-instance-method
browser-compat: javascript.builtins.Iterator.every
sidebar: jsref
---

The **`every()`** method of {{jsxref("Iterator")}} instances is similar to {{jsxref("Array.prototype.every()")}}: it tests whether all elements produced by the iterator pass the test implemented by the provided function. It returns a boolean value.

## Syntax

```js-nolint
every(callbackFn)
```

### Parameters

- `callbackFn`
  - : A function to execute for each element produced by the iterator. It should return a [truthy](/en-US/docs/Glossary/Truthy) value to indicate the element passes the test, and a [falsy](/en-US/docs/Glossary/Falsy) value otherwise. The function is called with the following arguments:
    - `element`
      - : The current element being processed.
    - `index`
      - : The index of the current element being processed.

### Return value

`true` if `callbackFn` returns a {{Glossary("truthy")}} value for every element. Otherwise, `false`.

## Description

`every()` iterates the iterator and invokes the `callbackFn` function once for each element. It returns `false` immediately if the callback function returns a falsy value. Otherwise, it iterates until the end of the iterator and returns `true`. If `every()` returns `false`, the underlying iterator is closed by calling its `return()` method.

The main advantage of iterator helpers over array methods is that they are lazy, meaning that they only produce the next value when requested. This avoids unnecessary computation and also allows them to be used with infinite iterators. With infinite iterators, `every()` returns `false` as soon as the first falsy value is found. If the `callbackFn` always returns a truthy value, the method never returns.

## Examples

### Using every()

```js
function* fibonacci() {
  let current = 1;
  let next = 1;
  while (true) {
    yield current;
    [current, next] = [next, current + next];
  }
}

const isEven = (x) => x % 2 === 0;
console.log(fibonacci().every(isEven)); // false

const isPositive = (x) => x > 0;
console.log(fibonacci().take(10).every(isPositive)); // true
console.log(fibonacci().every(isPositive)); // Never completes
```

Calling `every()` always closes the underlying iterator, even if the method early-returns. The iterator is never left in a half-way state.

```js
const seq = fibonacci();
console.log(seq.every(isEven)); // false
console.log(seq.next()); // { value: undefined, done: true }
```

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}

## See also

- [Polyfill of `Iterator.prototype.every` in `core-js`](https://github.com/zloirock/core-js#iterator-helpers)
- [es-shims polyfill of `Iterator.prototype.every`](https://www.npmjs.com/package/es-iterator-helpers)
- {{jsxref("Iterator")}}
- {{jsxref("Iterator.prototype.find()")}}
- {{jsxref("Iterator.prototype.some()")}}
- {{jsxref("Array.prototype.every()")}}
