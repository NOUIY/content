---
title: Date.prototype.setUTCMilliseconds()
short-title: setUTCMilliseconds()
slug: Web/JavaScript/Reference/Global_Objects/Date/setUTCMilliseconds
page-type: javascript-instance-method
browser-compat: javascript.builtins.Date.setUTCMilliseconds
sidebar: jsref
---

The **`setUTCMilliseconds()`** method of {{jsxref("Date")}} instances changes the milliseconds for this date according to universal time.

{{InteractiveExample("JavaScript Demo: Date.prototype.setUTCMilliseconds()")}}

```js interactive-example
const date = new Date("2018-01-24T12:38:29.069Z");

console.log(date.getUTCMilliseconds());
// Expected output: 69

date.setUTCMilliseconds(420);

console.log(date.getUTCMilliseconds());
// Expected output: 420
```

## Syntax

```js-nolint
setUTCMilliseconds(millisecondsValue)
```

### Parameters

- `millisecondsValue`
  - : An integer between 0 and 999 representing the milliseconds.

### Return value

Changes the {{jsxref("Date")}} object in place, and returns its new [timestamp](/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date#the_epoch_timestamps_and_invalid_date). If `millisecondsValue` is `NaN` (or other values that get [coerced](/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number#number_coercion) to `NaN`, such as `undefined`), the date is set to [Invalid Date](/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date#the_epoch_timestamps_and_invalid_date) and `NaN` is returned.

## Description

If a parameter you specify is outside of the expected range,
`setUTCMilliseconds()` attempts to update the date information in the
{{jsxref("Date")}} object accordingly. For example, if you use 1100 for
`millisecondsValue`, the seconds stored in the {{jsxref("Date")}}
object will be incremented by 1, and 100 will be used for milliseconds.

## Examples

### Using setUTCMilliseconds()

```js
const theBigDay = new Date();
theBigDay.setUTCMilliseconds(500);
```

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}

## See also

- {{jsxref("Date.prototype.getUTCMilliseconds()")}}
- {{jsxref("Date.prototype.setMilliseconds()")}}
