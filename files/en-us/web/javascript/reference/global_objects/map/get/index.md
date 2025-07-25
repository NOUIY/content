---
title: Map.prototype.get()
short-title: get()
slug: Web/JavaScript/Reference/Global_Objects/Map/get
page-type: javascript-instance-method
browser-compat: javascript.builtins.Map.get
sidebar: jsref
---

The **`get()`** method of {{jsxref("Map")}} instances returns a specified element from this map. If the
value that is associated to the provided key is an object, then you will get a
reference to that object and any change made to that object will effectively
modify it inside the `Map` object.

{{InteractiveExample("JavaScript Demo: Map.prototype.get()")}}

```js interactive-example
const map = new Map();
map.set("bar", "foo");

console.log(map.get("bar"));
// Expected output: "foo"

console.log(map.get("baz"));
// Expected output: undefined
```

## Syntax

```js-nolint
get(key)
```

### Parameters

- `key`
  - : The key of the element to return from the `Map` object.

### Return value

The element associated with the specified key, or
{{jsxref("undefined")}} if the key can't be found in the `Map` object.

## Examples

### Using get()

```js
const myMap = new Map();
myMap.set("bar", "foo");

console.log(myMap.get("bar")); // Returns "foo"
console.log(myMap.get("baz")); // Returns undefined
```

### Using get() to retrieve a reference to an object

```js
const arr = [];
const myMap = new Map();
myMap.set("bar", arr);

myMap.get("bar").push("foo");

console.log(arr); // ["foo"]
console.log(myMap.get("bar")); // ["foo"]
```

Note that the map holding a reference to the original object effectively means the object cannot be garbage-collected, which may lead to unexpected memory issues. If you want the object stored in the map to have the same lifespan as the original one, consider using a {{jsxref("WeakMap")}}.

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}

## See also

- {{jsxref("Map")}}
- {{jsxref("Map.prototype.set()")}}
- {{jsxref("Map.prototype.has()")}}
