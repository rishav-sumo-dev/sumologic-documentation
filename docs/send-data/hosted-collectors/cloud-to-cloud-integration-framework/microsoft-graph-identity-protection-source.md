---
id: microsoft-graph-identity-protection-source
title: Microsoft Graph Identity Protection Source
sidebar_label: Microsoft Graph Identity Protection
tags:
  - cloud-to-cloud
  - microsoft-graph-identity-protection
description: The Microsoft Graph Identity Protection Source collects Risk Detection and Risky User from the Microsoft Graph Identity Protection API.
---

import ForwardToSiem from '/docs/reuse/forward-to-siem.md';
import useBaseUrl from '@docusaurus/useBaseUrl';

<img src={useBaseUrl('img/send-data/ms-graph.svg')} alt="icon" width="40"/>

The [Microsoft Graph](https://docs.microsoft.com/en-us/graph/overview) Identity Protection Source collects [Risk Detection](https://docs.microsoft.com/en-us/graph/api/riskdetection-list?view=graph-rest-1.0) and [Risky User](https://docs.microsoft.com/en-us/graph/api/riskyuser-list?view=graph-rest-1.0) data from the Microsoft Graph [Identity Protection API](https://docs.microsoft.com/en-us/graph/api/resources/identityprotectionroot?view=graph-rest-1.0). It
securely stores the required authentication, scheduling, and state tracking information.

If you want to explicitly allow the static IP addresses used for this Source on your firewall see our [table of static IP addresses by deployment](cloud-to-cloud-source-versions.md).

## Data collected

| Polling Interval | Data |
| :--- | :--- |
| 5 min |  [Risk Detection](https://docs.microsoft.com/en-us/graph/api/riskdetection-list?view=graph-rest-1.0) |
| 5 min |  [Risky User](https://docs.microsoft.com/en-us/graph/api/riskyuser-list?view=graph-rest-1.0) |

## Setup

### Vendor configuration

The Source requires the creation and registration of a service application within the [Azure Active Directory portal](https://aad.portal.azure.com/).

The user creating the service application does not need to be an administrator. However, an administrator is needed to grant the application the appropriate permissions to the Identity and Access API.

Use the following steps to create a service application:

1. Log in to the [Azure Active Directory Portal](https://aad.portal.azure.com/)
1. Then select **Azure Active Directory** in the left menu.
    ![Azure AD step 2.png](/img/send-data/Azure-AD-step-2.png)
1. Then select **App Registrations**.<br/>
    ![Azure AD step 3 red box.png](/img/send-data/Azure-AD-step-3-red-box.png)
1. Then select **New Registration**. Go through the registration process, providing a name for the application. Selecting **Accounts in this organizational directory only** is sufficient.
    ![Azure new registration in step 4.png](/img/send-data/Azure-new-registration-in-step-4.png)
1. After the Application is registered (created), be sure to copy the **Application (client) ID** and the **Directory (tenant) ID**. These are used later as configuration parameters in Sumo Logic when creating the Microsoft Graph Identity Protection Source.
    ![Azure created app in step 5.png](/img/send-data/Azure-created-app-in-step-5.png)
1. Within the Application configuration page, select **Certificates and Secrets** to create an Application Client Secret Key.
    ![Azure AD step 6.png](/img/send-data/Azure-AD-step-6.png)
1. Copy the **Client Secret Value** (pictured below). It's needed later in Sumo Logic when creating the Microsoft Graph Identity Protection Source.
    ![Azure AD step 7.png](/img/send-data/Azure-AD-step-7.png)
1. Request the appropriate permissions for the application. Click on **API Permissions**, then **Add a permission** and select **Microsoft Graph**. From there select (or search for) the following permissions. An Administrator must approve (grant) these permissions before the integration will function.

| API |  Account Type |  Permissions |
|:----------------|:----------------------------------------|:----------------------------|
| Risk Detection | Delegated (work or school account)     | IdentityRiskEvent.Read.All |
| Risk Detection | Delegated (personal Microsoft account) | Not supported.             |
| Risk Detection | Application                            | IdentityRiskEvent.Read.All |
| Risky User     | Delegated (work or school account)     | IdentityRiskyUser.Read.All |
| Risky User     | Delegated (personal Microsoft account) | Not supported.             |
| Risky User     | Application                            | IdentityRiskyUser.Read.All |
![azure ad step 8.png](/img/send-data/azure-ad-step-8.png)

### Source configuration

When you create a Microsoft Graph Identity Protection Source, you add it to a Hosted Collector. Before creating the Source, identify the Hosted Collector you want to use or create a new Hosted Collector. For instructions, see [Create a Hosted Collector](/docs/send-data/hosted-collectors/configure-hosted-collector).

To configure a Microsoft Graph Identity Protection Source:

1. [**Classic UI**](/docs/get-started/sumo-logic-ui-classic). In the main Sumo Logic menu, select **Manage Data > Collection > Collection**. <br/>[**New UI**](/docs/get-started/sumo-logic-ui). In the Sumo Logic top menu select **Configuration**, and then under **Data Collection** select **Collection**. You can also click the **Go To...** menu at the top of the screen and select **Collection**.
1. On the Collectors page, click **Add Source** next to a Hosted Collector.
1. Search for and select **Microsoft Graph Identity Protection Source**.
1. Enter a **Name** to display for the Source in the Sumo web application. The description is optional.
1. (Optional) For **Source Category**, enter any string to tag the output collected from the Source. Category metadata is stored in a searchable field called `_sourceCategory`.
1. **Forward to SIEM**. Check the checkbox to forward your data to [Cloud SIEM](/docs/cse/). <br/><ForwardToSiem/>
1. (Optional) **Fields.** Click the **+Add Field** link to define the fields you want to associate, each field needs a name (key) and value.
   * <img src={useBaseUrl('img/reuse/green-check-circle.png')} alt="green check circle.png" width="20"/> A green circle with a check mark is shown when the field exists and is enabled in the Fields table schema.
   * <img src={useBaseUrl('img/reuse/orange-exclamation-point.png')} alt="orange exclamation point.png" width="20"/> An orange triangle with an exclamation point is shown when the field doesn't exist in the Fields table schema. In this case, you'll see an option to automatically add or enable the nonexistent fields to the Fields table schema. If a field is sent to Sumo Logic but isn’t present or enabled in the schema, it’s ignored and marked as **Dropped**. 
1. Provide the **Directory (tenant) ID** and **Application (client) ID** you got after you registered (created) the Azure Application in step 5 of the setup section.
1. **Application Client Secret Value**. Provide the Application Client Secret Value you created in step 7 of the setup section.
1. **Supported APIs to collect**. Select one or more of the available APIs, **riskDetections** and **riskyUsers**.
1. When you are finished configuring the Source, click **Submit**.

## Metadata fields

| Field | Value | Description |
| :--- | :--- | :--- |
| `_siemVendor` | `Microsoft` | Set when **Forward To SIEM** is checked. |
| `_siemProduct` | `Graph Identity Protection API` | Set when **Forward To SIEM** is checked. |
| `_siemFormat` | `JSON` | Set when **Forward To SIEM** is checked. |
| `_siemEventID` | `riskDetections` or `riskyUsers` | The `_siemEventId` is set to the type of data ingested. |

## JSON schema

Sources can be configured using UTF-8 encoded JSON files with the Collector Management API. See [how to use JSON to configure Sources](/docs/send-data/use-json-configure-sources) for details. 

| Parameter | Type | Value | Required | Description |
|:--|:--|:--|:--|:--|
| schemaRef | JSON Object  | `{"type":"MS Graph Identity Protection"}` | Yes | Define the specific schema type. |
| sourceType | String | `"Universal"` | Yes | Type of source. |
| config | JSON Object | [Configuration object](#configuration-object) | Yes | Source type specific values. |

### Configuration Object

| Parameter | Type | Required | Default | Description | Example |
|:--|:--|:--|:--|:--|:--|
| name | String | Yes | `null` | Type a desired name of the source. The name must be unique per Collector. This value is assigned to the [metadata](/docs/search/get-started-with-search/search-basics/built-in-metadata) field `_source`. | `"mySource"` |
| description | String | No | `null` | Type a description of the source. | `"Testing source"`
| category | String | No | `null` | Type a category of the source. This value is assigned to the [metadata](/docs/search/get-started-with-search/search-basics/built-in-metadata) field `_sourceCategory`. See [best practices](/docs/send-data/best-practices) for details. | `"mySource/test"`
| fields | JSON Object | No | `null` | JSON map of key-value fields (metadata) to apply to the Collector or Source. Use the boolean field _siemForward to enable forwarding to SIEM.|`{"_siemForward": false, "fieldA": "valueA"}` |
| tenant_id | String | Yes | `null` | Provide the Directory (tenant) ID you got after you registered (created) the Azure Application. |  |
| secret_key | String | Yes |  `null`| Provide the Application Client Secret Value you created in Azure. | |
| application_id | String | Yes | `null` | Provide the Application (client) ID you got after you registered (created) the Azure Application. |  |
| supported_apis | Array of strings | Yes | `null` | Define one or more of the available APIs to collect: Devices, and Users. | ["Devices","Users"] |  

### JSON example

```json reference
https://github.com/SumoLogic/sumologic-documentation/blob/main/static/files/c2c/microsoft-graph-identity-protection/example.json
```

### Terraform example

```sh reference
https://github.com/SumoLogic/sumologic-documentation/blob/main/static/files/c2c/microsoft-graph-identity-protection/example.tf
```

## FAQ

:::info
Click [here](/docs/c2c/info) for more information about Cloud-to-Cloud sources.
:::
