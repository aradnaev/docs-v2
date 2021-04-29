---
title: experimental.subDuration() function
description: >
  The `experimental.subDuration()` function subtracts a duration from a time value and
  returns a the resulting time value.
aliases:
  - /influxdb/v2.0/reference/flux/stdlib/experimental/subduration/
  - /influxdb/cloud/reference/flux/stdlib/experimental/subduration/
menu:
  flux_0_x_ref:
    name: experimental.subDuration
    parent: experimental
weight: 302
flux/v0.x/tags: [date/time]
related:
  - /flux/v0.x/stdlib/experimental/addduration/
introduced: 0.39.0
---

The `experimental.subDuration()` function subtracts a duration from a time value and
returns the resulting time value.

_**Function type:** Transformation_

{{% warn %}}
This function will be removed once duration vectors are implemented.
See [influxdata/flux#413](https://github.com/influxdata/flux/issues/413).
{{% /warn %}}

```js
import "experimental"

experimental.subDuration(
  d: 12h,
  from: now(),
)
```

## Parameters

### d
The duration to subtract.

_**Data type:** Duration_

### from
The time to subtract the [duration](#d) from.

_**Data type:** Time_

## Examples

### Subtract six hours from a timestamp
```js
import "experimental"

experimental.subDuration(
  d: 6h,
  from: 2019-09-16T12:00:00Z,
)

// Returns 2019-09-16T06:00:00.000000000Z
```