---
title: Write data with the InfluxDB API
weight: 206
description: >
  Use the `/write` endpoint of the InfluxDB API to write data to InfluxDB.
menu:
  influxdb_cloud:
    parent: Developer tools
    name: Write API
---
Write data to InfluxDB using an HTTP request to the InfluxDB API `/write` endpoint.
Use the `POST` request method and include the following in your request:

| Requirement          | Include by                                               |
|:-----------          |:----------                                               |
| Organization         | Use the `org` query parameter in your request URL.       |
| Bucket               | Use the `bucket` query parameter in your request URL.    |
| Precision            | Use the `precision` query parameter in your request URL. |
| API token | Use the `Authorization: Token` header.                   |
| Line protocol        | Pass as plain text in your request body.                 |

#### Example

The URL in the examples depends on your [InfluxDB Cloud region](/influxdb/cloud/reference/regions/).

{{< code-tabs-wrapper >}}
{{% code-tabs %}}
[Curl](#)
[Node.js](#)
{{% /code-tabs %}}
{{% code-tab-content %}}
```sh
curl -XPOST "https://cloud2.influxdata.com/api/v2/write?org=YOUR_ORG&bucket=YOUR_BUCKET&precision=s" \
  --header "Authorization: Token YOURAUTHTOKEN" \
  --data-raw "
mem,host=host1 used_percent=23.43234543 1556896326
mem,host=host2 used_percent=26.81522361 1556896326
mem,host=host1 used_percent=22.52984738 1556896336
mem,host=host2 used_percent=27.18294630 1556896336
"
```
{{% /code-tab-content %}}
{{% code-tab-content %}}
```js
{{< api/v2dot0/nodejs/write >}}
```
{{% /code-tab-content %}}
{{< /code-tabs-wrapper >}}

{{% note %}}
To compress data when writing to InfluxDB, set the `Content-Encoding` header to `gzip`.
Compression reduces network bandwidth, but increases server-side load.

```bash
curl -XPOST "https://cloud2.influxdata.com/api/v2/write?org=YOUR_ORG&bucket=YOUR_BUCKET&precision=s" \
  --header "Authorization: Token YOURAUTHTOKEN" \
  --header "Content-Encoding: gzip" \
  --data-raw "
mem,host=host1 used_percent=23.43234543 1556896326
mem,host=host2 used_percent=26.81522361 1556896326
mem,host=host1 used_percent=22.52984738 1556896336
mem,host=host2 used_percent=27.18294630 1556896336
"
```
{{% /note %}}

_For information about **InfluxDB API response codes**, see
[InfluxDB API Write documentation](/influxdb/cloud/api/#operation/PostWrite)._
