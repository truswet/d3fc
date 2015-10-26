---
layout: component
title: Extent
component: util/extent.js
namespace: util
---

 The extent function enhances the functionality of the equivalent D3 extent function, allowing you to pass an array of fields, or accessors, which will be used to derive the extent of the supplied array. For example, if you have an array of items with properties of 'high' and 'low', you can use `fc.util.extent()(data, ['high', 'low'])` to compute the extent of your data.

```js
  var data = [{low: 10, high: 30}, {low: 12, high: 40}];
  var fields = ['high', 'low'];

  fc.util.extent()(data, fields); // [10, 40]
```

 The range can be modified by using the `pad` property. Pad will scale the calculated range by the given amount. If the calculated range is `[10, 20]` then the result of padding by '1' will be `[5, 25]`. `pad(0)` is an identity.

```js
  fc.util.extent()
      .pad(0.5)(data, fields); // [2.5, 47.5]
```

 The range can be extended to include a fixed value, using the `include` property. The range is extended after padding, so the order of setting the properties is not important. If the included value was already within the range there will be no change.

```js
  fc.util.extent()
      .include(0)(data, fields); // [0, 40]
  fc.util.extent()
      .pad(0.5)
      .include(0)(data, fields); // [0, 47.5]
```

Extent can also be used on an array of arrays.

```js
  var data = [[{low: 2, high: 5}, {low: 1, high: 3}], [{low: 0, high: 6}]];
  fc.util.extent()(data, ['high', 'low']); // [0, 6]  

```