---
title: pearsonr() function
description: The `pearsonr()` function computes the Pearson R correlation coefficient between two streams by first joining the streams, then performing the covariance operation normalized to compute R.
aliases:
  - /influxdb/v2.0/reference/flux/functions/transformations/aggregates/pearsonr
  - /influxdb/v2.0/reference/flux/functions/built-in/transformations/aggregates/pearsonr/
  - /influxdb/v2.0/reference/flux/stdlib/built-in/transformations/aggregates/pearsonr/
  - /influxdb/v2.0/reference/flux/stdlib/built-in/transformations/pearsonr/
  - /influxdb/cloud/reference/flux/stdlib/built-in/transformations/pearsonr/
menu:
  flux_0_x_ref:
    name: pearsonr
    parent: universe
weight: 102
flux/v0.x/tags: [transformations]
introduced: 0.7.0
---

The `pearsonr()` function computes the Pearson R correlation coefficient between two streams
by first joining the streams, then performing the covariance operation normalized to compute R.

_**Output data type:** Float_

```js
pearsonr(x: stream1, y: stream2, on: ["_time", "_field"])
```

## Parameters

### x {data-type="stream of tables"}
First input stream used in the operation.

### y {data-type="stream of tables"}
Second input stream used in the operation.

### on {data-type="array of strings"}
List of columns to join on.

## Examples
```js
stream1 = from(bucket:"example-bucket")
  |> range(start:-15m)
  |> filter(fn: (r) =>
    r._measurement == "mem" and
    r._field == "used"
  )

stream2 = from(bucket:"example-bucket")
  |> range(start:-15m)
  |> filter(fn: (r) => r
    ._measurement == "mem" and
    r._field == "available"
  )

pearsonr(x: stream1, y: stream2, on: ["_time"])
```

## Function definition
```js
pearsonr = (x,y,on) =>
  cov(x:x, y:y, on:on, pearsonr:true)
```