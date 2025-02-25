---
title: slack.endpoint() function
description: >
  The `slack.endpoint()` function sends a message to Slack that includes output data.
aliases:
  - /influxdb/v2.0/reference/flux/functions/slack/endpoint/
menu:
  influxdb_2_0_ref:
    name: slack.endpoint
    parent: Slack
weight: 202
influxdb/v2.0/tags: [endpoints]
---

The `slack.endpoint()` function sends a message to Slack that includes output data.

_**Function type:** Output_

```js
import "slack"

slack.endpoint(
  url: "https://slack.com/api/chat.postMessage",
  token: "mySuPerSecRetTokEn"
)
```

## Parameters

### url
The Slack API URL.
Defaults to `https://slack.com/api/chat.postMessage`.

{{% note %}}
If using a Slack webhook, you'll receive a Slack webhook URL when you
[create an incoming webhook](https://api.slack.com/incoming-webhooks#create_a_webhook).
{{% /note %}}

_**Data type:** String_

### token
The [Slack API token](https://get.slack.help/hc/en-us/articles/215770388-Create-and-regenerate-API-tokens)
used to interact with Slack.
Defaults to `""`.

{{% note %}}
A token is only required if using the Slack chat.postMessage API.
{{% /note %}}

_**Data type:** String_

## Usage
`slack.endpoint` is a factory function that outputs another function.
The output function requires a `mapFn` parameter.

### mapFn
({{< req >}}) A function that builds the record used to generate the POST request.
Requires an `r` parameter.

_**Data type:** Function_

`mapFn` accepts a table row (`r`) and returns a record that must include the following fields:

- `channel`
- `text`
- `color`

_For more information, see [`slack.message()`](/influxdb/v2.0/reference/flux/stdlib/slack/message/)_

## Examples

##### Send critical statuses to a Slack endpoint
```js
import "slack"

toSlack = slack.endpoint(url: "https://hooks.slack.com/services/EXAMPLE-WEBHOOK-URL")

crit_statuses = from(bucket: "example-bucket")
  |> range(start: -1m)
  |> filter(fn: (r) => r._measurement == "statuses" and r.status == "crit")

crit_statuses
  |> toSlack(mapFn: (r) => ({
      channel: "Alerts",
      text: r._message,
      color: "danger",
    })
  )()
```
