---
id: stix-taxii-2-client-source
title: STIX/TAXII 2 Client Source
sidebar_label: STIX/TAXII 2 Client
keywords:
  - cloud-to-cloud
  - stix
  - taxii
description: Learn how to set up a STIX/TAXII 2.x client to collect threat intelligence indicators into the Sumo Logic environment.
---

import useBaseUrl from '@docusaurus/useBaseUrl';

The STIX/TAXII 2 Client source supports collecting threat intelligence indicators from STIX/TAXII 2.0 and 2.1 versions. For more information, see [About Sumo Logic Threat Intelligence](/docs/security/threat-intelligence/about-threat-intelligence/).

The legacy STIX/TAXII 1.x versions are not supported with this source. Use [STIX/TAXII 1 Client Source](/docs/send-data/hosted-collectors/cloud-to-cloud-integration-framework/stix-taxii-1-client-source/) for version 1.x versions.

[STIX/TAXII](https://oasis-open.github.io/cti-documentation/) are two standards used together to exchange threat intelligence information between systems. STIX defines the format and structure of the data. TAXII defines how the API endpoints are served and accessed by clients.

## Data collected

This source collects threat intelligence indicators from a vendor's STIX/TAXII 2.x endpoints. This means the specific endpoints we collect data from are the endpoints defined in the [TAXII standard](https://oasis-open.github.io/cti-documentation/taxii/intro). Vendor APIs must follow the standard. The source will collect all indicators from the TAXII server when it runs for the first time and it will check for updates once an hour. This one-hour polling interval can be adjusted in the source configuration.

## Setup

### Vendor configuration

:::note
The threat intel vendor must follow the STIX/TAXII 2.0 or 2.1 standard.
:::

1. Identify a vendor who uses the STIX/TAXII 2.0 or 2.1 standard for sharing threat intelligence indicators.
1. Follow their documentation to obtain the following information:
   * The STIX/TAXII version they provide (either 2.0 or 2.1)
   * The TAXII Discovery URL
   * Your authentication credentials if required


### Source configuration

When you create an TAXII 2 Client Source, you add it to a Hosted Collector. Before creating the Source, identify the Hosted Collector you want to use or create a new Hosted Collector. For instructions, see [Configure a Hosted Collector and Source](/docs/send-data/hosted-collectors/configure-hosted-collector).

To configure a TAXII 2 Client Source:
1. [**Classic UI**](/docs/get-started/sumo-logic-ui-classic). In the main Sumo Logic menu, select **Manage Data > Collection > Collection**. <br/>[**New UI**](/docs/get-started/sumo-logic-ui). In the Sumo Logic top menu select **Configuration**, and then under **Data Collection** select **Collection**. You can also click the **Go To...** menu at the top of the screen and select **Collection**.
1. On the Collection page, click **Add Source** next to a Hosted Collector.
1. Search for and select **TAXII 2 Client**.
1. Enter a **Name** for the Source. The description is optional.
1. (Optional) For **Source Category**, enter any string to tag the output collected from the Source. Category metadata is stored in a searchable field called `_sourceCategory`.
1. (Optional) **Fields**. Click the **+Add** button to define the fields you want to associate. Each field needs a name (key) and value.
   * <img src={useBaseUrl('img/reuse/green-check-circle.png')} alt="green check circle.png" width="20"/> A green circle with a check mark is shown when the field exists and is enabled in the Fields table schema.
   * <img src={useBaseUrl('img/reuse/orange-exclamation-point.png')} alt="orange exclamation point.png" width="20"/> An orange triangle with an exclamation point is shown when the field doesn't exist in the Fields table schema. In this case, you'll see an option to automatically add or enable the nonexistent fields to the Fields table schema. If a field is sent to Sumo Logic that does not exist in the Fields schema it is ignored, known as dropped.
1. **Sumo Logic Threat Intel Source ID**. Enter the name you want to use for the source that will be created in the [Threat Intelligence](/docs/security/threat-intelligence/about-threat-intelligence/) tab in Sumo Logic. The threat intelligence indicators will be stored in this source. Do not use spaces in the name.
1. **Authentication**. Select the authentication type:
   * **Basic**. Provide your vendor username and password.
   * **API Key**. Provide:
      * How to use the key (either in the HTTP request header or HTTP request URL parameters).
      * The location where to use the key, such as the HTTP header key name (for example, `Authorization`).
      * The API key.
      * The API key prefix (optional).
   * **Bearer**. Provide the bearer auth token.
   * **None**. Select if no authorization is needed.
1. **STIX/TAXII Configuration**:
    1. **Version**. Select the STIX/TAXII version the vendor is using (2.0 or 2.1).
    1. **API Root URL Source**. Enter:
       * **Discovery URL**. Enter the TAXII Discovery URL provided by the vendor (optional).
       * **Root URL(s)**. Enter the TAXII root URL(s). For example, `https://stix2.mysource.org/my-root`.
    1. **Collection Id(s)**. Enter the collection IDs for TAXII (optional).
1. **Other Settings**:
    1. (Optional) **Set Indicators Limit Per Page**. Set the maximum number of indicators to return per page. The default is 99.
    1. (Optional) **Polling Interval**. Set how frequently to poll for new or updated indicators. It must be between 5 minutes and 48 hours.
1. When you are finished configuring the Source, click **Save**.

## JSON Configuration

Sources can be configured using UTF-8 encoded JSON files with the Collector Management API. See [Use JSON to Configure Sources](/docs/send-data/use-json-configure-sources) for details. 

| Parameter | Type | Value | Required | Description |
|:--|:--|:--|:--|:--|
| schemaRef | JSON Object  | `{"type":"TAXII 2 Client"}` | Yes | Define the specific schema type. |
| sourceType | String | `"Universal"` | Yes | Type of source. |
| config | JSON Object | [Configuration object](#configuration-object) | Yes | Source type specific values. |

### Configuration Object

| Parameter | Type | Required | Default | Description | Example |
|:---|:---|:---|:---|:---|:---|
| name | String | Yes | `null` | Type a desired name of the source. The name must be unique per Collector. This value is assigned to the [metadata](/docs/search/get-started-with-search/search-basics/built-in-metadata) field `_source`. | `"mySource"` |
| description | String | No | `null` | Type a description of the source. | `"Testing source"`
| category | String | No | `null` | Type a category of the source. This value is assigned to the [metadata](/docs/search/get-started-with-search/search-basics/built-in-metadata) field `_sourceCategory`. See [best practices](/docs/send-data/best-practices) for details. | `"mySource/test"`
| fields | JSON Object | No | `null` | JSON map of key-value fields (metadata) to apply to the Collector or Source. Use the boolean field `_siemForward` to enable forwarding to SIEM.|`{"_siemForward": false, "fieldA": "valueA"}` |
| ti_user_source_id | String | Yes | `null` | Your Sumo Logic threat intel destination source name |  |
| ti_version | String | Yes | `2.1` | The STIX/TAXII server version used |  |
| ti_discovery_url | String | Yes | `null` | The STIX/TAXII discovery URL |  |
| http_user | String | No | `null` | HTTP basic authentication username |  |
| http_password | String | No | `null` | HTTP basic authentication password |  |

### JSON example

```json reference
https://github.com/SumoLogic/sumologic-documentation/blob/main/static/files/c2c/taxii-2/example.json
```

### Terraform example

```sh reference
https://github.com/SumoLogic/sumologic-documentation/blob/main/static/files/c2c/taxii-2/example.tf
```

### Recommended configurations

Below is a list of Sumo Logic recommended configuration examples for specific threat intel vendors using TAXII 2.

| Vendor | Notes |
| :-- | :-- |
| <a href="/files/c2c/taxii-2/cisa-dhs-config.json" target="_blank">CISA DHS Automated Indicator Sharing (AIS)</a> | No authentication setup is required. Sumo Logic uses it's own certificates for authentication. |
| <a href="/files/c2c/taxii-2/cybersixgill-config.json" target="_blank">Cybersixgill</a> | Be sure to specify collection `102` in the configuration. |
| <a href="/files/c2c/taxii-2/dragos-config.json" target="_blank">Dragos</a> |
| <a href="/files/c2c/taxii-2/eclecticiq-config.json" target="_blank">Eclecticiq</a> | |
| <a href="/files/c2c/taxii-2/recorded-future-config.json" target="_blank">Recorded Future</a> | Use your API key as the HTTP password and leave the username blank. Currently, the Recorded Future TAXII v2 service supports Recorded Future’s [default and large risk lists](https://support.recordedfuture.com/hc/en-us/articles/115008327148-Default-and-Large-Risk-Lists). For more specific risk lists based on an individual risk rule, use Recorded Future’s TAXII v1 service. |
| <a href="/files/c2c/taxii-2/palo-alto-unit42-config.json" target="_blank">PaloAlto Unit42</a> | |

## FAQ

:::info
Click [here](/docs/c2c/info) for more information about Cloud-to-Cloud sources.
:::
