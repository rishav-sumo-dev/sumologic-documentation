---
id: netskope-webtx-source
title: Netskope WebTx Source
sidebar_label: Netskope WebTx
tags:
  - cloud-to-cloud
  - netskope-webtx
description: Our Netskope WebTx API integration ingests Web Transaction logs from Netskope Event Stream.
---

import ForwardToSiem from '/docs/reuse/forward-to-siem.md';
import useBaseUrl from '@docusaurus/useBaseUrl';

<img src={useBaseUrl('img/integrations/security-threat-detection/netskope.png')} alt="thumbnail icon" width="75"/>

The [Netskope WebTx API](https://docs.netskope.com/en/transaction-event-fields.html) integration ingests Web Transaction logs from Netskope Event Stream.

## Data collected

| Polling Interval | Data |
| :--- | :--- |
| 5 min |  [Web Transaction logs](https://docs.netskope.com/en/using-the-rest-api-v2-dataexport-iterator-endpoints.html) |

The netskope-webtx access a PubSub lite service hosted by Google to retrieve web transaction logs using the [v2 dataexport Iterator Endpoint](https://docs.netskope.com/en/using-the-rest-api-v2-dataexport-iterator-endpoints.html). Details on what is ingested can be found [here](https://docs.netskope.com/en/transaction-event-fields.html).

## Setup

### Vendor configuration

Netskope Web Transactions integration needs to be configured using Netskope Streaming credentials. You can collect the subscription path and credentials [here](https://docs.netskope.com/en/netskope-transaction-events.html).

1. You will need a subscription endpoint URL and subscription key to access the streamed events. Log in to your Netskope UI and go to **Settings > Tools > Event Streaming**. Copy your subscription endpoint and generate your download key from the Event Streaming page.
   :::info
   - The **REGENERATE ENDPOINT** button generates a new subscription path. After a new subscription path is generated, a new subscription key must be generated by clicking on the **GENERATE AND DOWNLOAD KEY** button.
   - The old subscription path and key expire. With a new subscription path, event streaming will start fresh from the beginning of the retention period which is 7 days by default.
   :::
1. After the transaction events feature is enabled in your account, you’ll be able to consume the data from the subscription endpoint.
1. To receive the events from the subscription, refer to the [Receiving messages from Lite subscriptions link](https://cloud.google.com/pubsub/lite/docs/subscribing). You can receive messages with various [Client libraries](https://cloud.google.com/pubsub/lite/docs/reference/libraries). Netskope retains transaction events for seven days by default if not consumed.
1. When you are finished configuring the file, download the JSON file.

### Source configuration

When you create a Netskope WebTx API Source, you add it to a Hosted Collector. Before creating the Source, identify the Hosted Collector you want to use or create a new Hosted Collector. For instructions, see [Configure a Hosted Collector](/docs/send-data/hosted-collectors/configure-hosted-collector).

1. [**Classic UI**](/docs/get-started/sumo-logic-ui-classic). In the main Sumo Logic menu, select **Manage Data > Collection > Collection**. <br/>[**New UI**](/docs/get-started/sumo-logic-ui). In the Sumo Logic top menu select **Configuration**, and then under **Data Collection** select **Collection**. You can also click the **Go To...** menu at the top of the screen and select **Collection**.
1. On the Collection page, click **Add Source** next to a Hosted Collector.
1. Search for and select **Netskope WebTx API**.
1. Enter a **Name** to display the Source in the Sumo web application. The description is optional.
1. (Optional) For **Source Category**, enter any string to tag the output collected from the Source. Category [metadata](/docs/search/get-started-with-search/search-basics/built-in-metadata) is stored in a searchable field called `_sourceCategory`.
1. **Forward to SIEM**. Check the checkbox to forward your data to [Cloud SIEM](/docs/cse/). <br/><ForwardToSiem/>
1. (Optional) **Fields**. Click the **+Add Field** link to define the fields you want to associate, each field needs a name (key) and value.
   * <img src={useBaseUrl('img/reuse/green-check-circle.png')} alt="green check circle.png" width="20"/> A green circle with a check mark is shown when the field exists and is enabled in the Fields table schema.
   * <img src={useBaseUrl('img/reuse/orange-exclamation-point.png')} alt="orange exclamation point.png" width="20"/> An orange triangle with an exclamation point is shown when the field doesn't exist in the Fields table schema. In this case, you'll see an option to automatically add or enable the nonexistent fields to the Fields table schema. If a field is sent to Sumo Logic but isn’t present or enabled in the schema, it’s ignored and marked as **Dropped**. 
1. **Netskope Streaming Credentials**. Upload the JSON file downloaded from google cloud platform.
1. When you are finished configuring the Source, click **Save**.

## Metadata fields

| Field | Value | Description |
| :--- | :--- | :--- |
| `_siemVendor` | `Netskope` | Set when **Forward To SIEM** is checked. |
| `_siemProduct` | `WebTx` | Set when **Forward To SIEM** is checked. |
| `_siemFormat` | `JSON` | Set when **Forward To SIEM** is checked. |
| `_siemEventID` | `webtx` | Set when **Forward To SIEM** is checked. |

## JSON schema

Sources can be configured using UTF-8 encoded JSON files with the Collector Management API. See [how to use JSON to configure Sources](/docs/send-data/use-json-configure-sources) for more details.

| Parameter | Type | Value | Required | Description |
|:--|:--|:--|:--|:--|
| schemaRef | JSON Object  | `{"type":"Netskope WebTx API"}` | Yes | Define the specific schema type. |
| sourceType | String | `"Universal"` | Yes | Type of source. |
| config | JSON Object | [Configuration object](#configuration-object) | Yes | Source type specific values. |

### Configuration Object

| Parameter | Type | Required | Default | Description | Example |
|:--|:--|:--|:--|:--|:--|
| name | String | Yes | `null` | Type a desired name of the source. The name must be unique per Collector. This value is assigned to the [metadata](/docs/search/get-started-with-search/search-basics/built-in-metadata) field `_source`. | `"mySource"` |
| description | String | No | `null` | Type a description of the source. | `"Testing source"`
| category | String | No | `null` | Type a category of the source. This value is assigned to the [metadata](/docs/search/get-started-with-search/search-basics/built-in-metadata) field `_sourceCategory`. See [best practices](/docs/send-data/best-practices) for details. | `"mySource/test"`
| fields | JSON Object | No | `null` | JSON map of key-value fields (metadata) to apply to the Collector or Source. Use the boolean field _siemForward to enable forwarding to SIEM.|`{"_siemForward": false, "fieldA": "valueA"}` |
| credentialsJson | String | Yes | `null` | Its the authentication credentials to access Netskope webtx Event Streaming service. |  |
| subscriptionPath | String | Yes | `null` | A subscription path is needed for the event streaming to start. |  |

### JSON example

```json reference
https://github.com/SumoLogic/sumologic-documentation/blob/main/static/files/c2c/netskope-webtx/example.json
```

### Terraform example

```sh reference
https://github.com/SumoLogic/sumologic-documentation/blob/main/static/files/c2c/netskope-webtx/example.tf
```

## FAQ

:::info
Click [here](/docs/c2c/info) for more information about Cloud-to-Cloud sources.
:::
