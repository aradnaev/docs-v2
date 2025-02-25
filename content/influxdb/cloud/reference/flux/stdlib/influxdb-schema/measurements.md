---
title: schema.measurements() function
description: The schema.measurements() function returns a list of measurements in a specific bucket.
aliases:
  - /influxdb/cloud/reference/flux/functions/influxdb-v1/measurements/
menu:
  influxdb_cloud_ref:
    name: schema.measurements
    parent: InfluxDB schema
weight: 301
influxdb/v2.0/tags: [measurements]
related:
  - /influxdb/cloud/query-data/flux/explore-schema/
  - /{{< latest "influxdb" "v1" >}}/query_language/explore-schema#show-measurements, SHOW MEASUREMENTS in InfluxQL
introduced: 0.88.0
---

The `schema.measurements()` function returns a list of measurements in a specific bucket.
The return value is always a single table with a single column, `_value`.

```js
import "influxdata/influxdb/schema"

schema.measurements(bucket: "example-bucket")
```

## Parameters

### bucket
Bucket to retrieve measurements from.

_**Data type:** String_

## Function definition
```js
package schema

measurements = (bucket) =>
  tagValues(bucket: bucket, tag: "_measurement")
```

_**Used functions:**
[schema.tagValues()](/influxdb/cloud/reference/flux/stdlib/influxdb-schema/tagvalues)_
