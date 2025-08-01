---
id: azure-storage
title: Azure Storage
description: Learn about the Sumo Logic collection process for the Azure Storage service.
---

import useBaseUrl from '@docusaurus/useBaseUrl';

<img src={useBaseUrl('img/integrations/microsoft-azure/azure-storage.png')} alt="Thumbnail icon" width="50"/>

[Azure Storage](https://learn.microsoft.com/en-us/azure/storage/common/storage-introduction) is Microsoft's cloud storage solution for modern data storage scenarios offering highly available, massively scalable, durable, and secure storage for a variety of data objects in the cloud. This integration helps in monitoring the transaction volume and read/write activity of all your storage accounts.

In Azure Storage, [storage accounts](https://learn.microsoft.com/en-us/azure/storage/common/storage-account-overview) allow you to create and manage the following storage services:

* **[Blob storage](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blobs-overview)** stores any type of text or binary data, such as a document, media file, or application installer. You can set Blob storage for private access or share contents publicly to the Internet. Blob storage serves the same purpose as both AWS S3 and EBS.
* **[Table storage](https://learn.microsoft.com/en-us/azure/storage/tables/table-storage-overview)**. Stores structured datasets. Table storage is a NoSQL key-attribute data store that allows for rapid development and fast access to large quantities of data. Similar to AWS SimpleDB and DynamoDB services.
* **[Queue storage](https://learn.microsoft.com/en-us/azure/storage/queues/storage-queues-introduction)**. Provides messaging for workflow processing and for communication between components of cloud services.
* **[File storage](https://learn.microsoft.com/en-us/azure/storage/files/storage-files-introduction)**. Offers shared storage for legacy applications using the standard Server Message Block (SMB) protocol. File storage is used in a similar manner to EFS in the AWS platform.

## Log and metric types

For Azure Storage, you can collect the following logs and metrics:

- **Resource logs**, which provide an insight into operations that were performed within an Azure resource. For a complete schema for resource logs refer to the documentation below:
    * [Azure Blob Storage schema](https://learn.microsoft.com/en-us/azure/storage/blobs/monitor-blob-storage-reference#resource-logs)
    * [Azure File Storage schema](https://learn.microsoft.com/en-us/azure/storage/files/storage-files-monitoring-reference#resource-logs)
    * [Azure Queue Storage schema](https://learn.microsoft.com/en-us/azure/storage/queues/monitor-queue-storage-reference#resource-logs)
    * [Azure File Storage schema](https://learn.microsoft.com/en-us/azure/storage/tables/monitor-table-storage-reference#resource-logs)

    Requests made by the Blob storage service itself, such as log creation or deletion, aren't logged. For a complete list of the logged data, see [Storage logged operations and status messages](https://learn.microsoft.com/en-us/rest/api/storageservices/storage-analytics-logged-operations-and-status-messages).

- **Activity logs** provide insight into any subscription-level or management group-level events that have occurred in Azure. To learn more, refer to [Azure documentation](https://learn.microsoft.com/en-us/azure/azure-monitor/essentials/activity-log-schema).

- **Metrics** for Azure Storage are in the namespaces given below:
    * [Microsoft.Storage/storageAccounts](https://learn.microsoft.com/en-us/azure/azure-monitor/reference/supported-metrics/microsoft-storage-storageaccounts-metrics)
    * [Microsoft.Storage/storageAccounts/blobServices](https://learn.microsoft.com/en-us/azure/azure-monitor/reference/supported-metrics/microsoft-storage-storageaccounts-blobservices-metrics)
    * [Microsoft.Storage/storageAccounts/fileServices](https://learn.microsoft.com/en-us/azure/azure-monitor/reference/supported-metrics/microsoft-storage-storageaccounts-fileservices-metrics)
    * [Microsoft.Storage/storageAccounts/queueServices](https://learn.microsoft.com/en-us/azure/azure-monitor/reference/supported-metrics/microsoft-storage-storageaccounts-queueservices-metrics)
    * [Microsoft.Storage/storageAccounts/tableServices](https://learn.microsoft.com/en-us/azure/azure-monitor/reference/supported-metrics/microsoft-storage-storageaccounts-tableservices-metrics)

    :::note
    Only metrics with `category=Transaction` can be exported from the diagnostic settings export feature.
    :::

    Click on the above namespaces to learn more about the supported metrics. For a complete list of the dimensions that Azure Storage supports, refer to the documentation below:

    * [Azure Blob Storage Metrics dimensions](https://learn.microsoft.com/en-us/azure/storage/blobs/monitor-blob-storage-reference#metrics-dimensions)
    * [Azure File Storage Metrics dimensions](https://learn.microsoft.com/en-us/azure/storage/files/storage-files-monitoring-reference#metrics)
    * [Azure Queue Storage Metrics dimensions](https://learn.microsoft.com/en-us/azure/storage/queues/monitor-queue-storage-reference#metrics)
    * [Azure Table Storage Metrics dimensions](https://learn.microsoft.com/en-us/azure/storage/tables/monitor-table-storage-reference#metrics)

    :::info
    Capacity metrics are currently not supported via Diagnostic Settings.
    :::

## Setup

Azure service sends monitoring data to Azure Monitor, which can then [stream data to Eventhub](https://learn.microsoft.com/en-us/azure/azure-monitor/essentials/stream-monitoring-data-event-hubs). Sumo Logic supports:

* Logs collection from [Azure Monitor](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-get-started) using our [Azure Event Hubs source](/docs/send-data/collect-from-other-data-sources/azure-monitoring/ms-azure-event-hubs-source/).
* Activity Logs collection from [Azure Monitor](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-get-started) using our [Azure Event Hubs source](/docs/send-data/collect-from-other-data-sources/azure-monitoring/ms-azure-event-hubs-source/). It is recommended to create a separate source for activity logs. If you are already collecting these logs, you can skip this step.
* Metrics collection using our [Azure Metrics Source](/docs/send-data/hosted-collectors/microsoft-source/azure-metrics-source).

You must explicitly enable diagnostic settings for each storage service (blob, queue, table, and file) and each storage account that you want to monitor. You can forward logs to the same event hub provided they satisfy the limitations and permissions as described [here](https://learn.microsoft.com/en-us/azure/azure-monitor/essentials/diagnostic-settings?tabs=portal#destination-limitations).

When you configure the event hubs source or HTTP source, plan your source category to ease the querying process. A hierarchical approach allows you to make use of wildcards. For example: `Azure/Storage/Logs`, `Azure/Storage/Metrics`.

### Configure metrics collection

import MetricsSourceBeta from '../../reuse/metrics-source-beta.md';

<MetricsSourceBeta/>

### Configure logs collection

#### Diagnostic logs

In this section, you will configure a pipeline for shipping diagnostic logs from Azure Monitor to an Event Hub.

1. To set up the Azure Event Hubs source in Sumo Logic, refer to [Azure Event Hubs Source for Logs](/docs/send-data/collect-from-other-data-sources/azure-monitoring/ms-azure-event-hubs-source/).
1. To create the Diagnostic settings in the Azure portal, refer to the [Azure documentation](https://learn.microsoft.com/en-gb/azure/data-factory/monitor-configure-diagnostics). Perform the steps below for each storage service (blob, queue, table, and file) and each storage account that you want to monitor.
   * Choose `Stream to an event hub` as the destination.
   * Select `allLogs`.
   * Use the Event hub namespace and Event hub name configured in the previous step in the destination details section. You can use the default policy `RootManageSharedAccessKey` as the policy name.
1. Tag the location field in the source with the right location value.
   <img src={useBaseUrl('img/integrations/microsoft-azure/Azure-Storage-Tag-Location.png')} alt="Azure Storage Tag Location" style={{border: '1px solid gray'}} width="500" />

#### Activity Logs

To collect activity logs, follow the instructions [here](/docs/integrations/microsoft-azure/audit). Do not perform this step in case you are already collecting activity logs for a subscription.

:::note
Since this source contains logs from multiple regions make sure that you do not tag this source with the location tag.
:::

##### Enabling Microsoft Defender for Cloud

For Security events, make sure you enable [Microsoft Defender for Cloud](https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-storage-azure-portal-enablement?tabs=enable-storage-account). If you have existing settings, click **Edit Settings**.
<img src={useBaseUrl('img/integrations/microsoft-azure/Microsoft-Cloud-Defender-Edit-Settings.png')} alt="Edit Settings" style={{border: '1px solid gray'}} width="800" />
In **Defender Plans** settings page turn on the **Azure Storage** status under **Cloud Workload Protection** section.
<img src={useBaseUrl('img/integrations/microsoft-azure/Microsoft-Cloud-Defender-Plans-Storage.png')} alt="Cloud Defender Plans Storage" style={{border: '1px solid gray'}} width="800" />


## Installing the Azure Storage app

Now that you have set up data collection, install the Azure Storage Sumo Logic app to use the pre-configured [dashboards](#viewing-the-azure-storage-app-dashboards) that provide visibility into your environment for real-time analysis of overall usage.

import AppInstallIndexV2 from '../../reuse/apps/app-install-index-option.md';

<AppInstallIndexV2/>

As part of the app installation process, the following fields will be created by default:

- `tenant_name`. This field is tagged at the collector level. You can get the tenant name using the instructions [here](https://learn.microsoft.com/en-us/azure/active-directory-b2c/tenant-management-read-tenant-name#get-your-tenant-name).
- `location`. The region the resource name belongs to.
- `subscription_id`. ID associated with a subscription where the resource is present.
- `resource_group`. The resource group name where the Azure resource is present.
- `provider_name`. Azure resource provider name (for example, Microsoft.Network).
- `resource_type`. Azure resource type (for example, storage accounts).
- `resource_name`. The name of the resource (for example, storage account name).
- `service_type`. Type of the service that can be accessed with an Azure resource.
- `service_name`. Services that can be accessed with an Azure resource (for example, in Azure Container Instances the service is Subscriptions).

## Viewing the Azure Storage app dashboards

import ViewDashboardsIndex from '../../reuse/apps/view-dashboards-index.md';

<ViewDashboardsIndex/>

### Overview

The **Azure Storage - Overview** dashboard provides insights into transactions by storage account, storage type, and API name.

Use this dashboard to:
    * Monitor Availability by storage account.
    * Monitor Errors by storage account.
    * View Total Ingress by storage account.
    * View Total Egress by storage account.
    * View Max Success E2E Latency.
    * View Max Success Server Latency.
    * View transactions by storage account.

<img src={useBaseUrl('https://sumologic-app-data-v2.s3.amazonaws.com/dashboards/AzureStorage/Azure-Storage-Overview.png')} alt="Azure Storage Overview dashboard" style={{border: '1px solid gray'}} width="800" />

### Access

The **Azure Storage - Access** dashboard provides insights into transactions by location, TLS version, and also shows the distribution by user agent and identity type.

Use this dashboard to:
    * View transactions by location.
    * View transactions by TLS version.
    * View distribution by user agent.
    * View distribution by identity type.

<img src={useBaseUrl('https://sumologic-app-data-v2.s3.amazonaws.com/dashboards/AzureStorage/Azure-Storage-Access.png')} alt="Azure Storage Overview Access" style={{border: '1px solid gray'}} width="800" />

### Operations

The **Azure Storage - Operations** dashboard provides details like total write in bytes, total read, total ingress by storage account, and total egress by storage account. It also provides storage account statistic insights such as total read count, read bytes, max/avg read latency, total write count, write bytes, and max/avg write latency. In addition, it also displays the status code trend.

Use this dashboard to:
    * View amount of write data in MB.
    * View amount of read data in MB.
    * View Non 200 status code by Service Type.
    * View Transactions by Service Type.
    * View Storage Account Write Statistics.
    * View Storage Account Read Statistics.
    * Monitor Total Ingress by Service Type.
    * Monitor Total Egress by Service Type.
    * Monitor Total Ingress by API name.
    * Monitor Total Egress by API name.

<img src={useBaseUrl('https://sumologic-app-data-v2.s3.amazonaws.com/dashboards/AzureStorage/Azure-Storage-Operations.png')} alt="Azure Storage Overview Operations" style={{border: '1px solid gray'}} width="800" />

### Blob Service

The **Azure Storage - Blob Service** dashboard provides details like read bytes, write bytes, last 10 operations, read/write trend by service type, and top 10 read/write by resource name.

Use this dashboard to:
    * View amount of read data in MB.
    * View amount of write data in MB.
    * View Read vs Write.
    * View Reads by Container Name.
    * View Writes by Container Name.
    * View Container Name by Failed Operations.
    * View Top 10 Resources by Failures.
    * View Top 10 Resources by Latency.
    * View Top 10 Resources by Reads(MB).
    * View Top 10 Resources by Writes(MB).

<img src={useBaseUrl('https://sumologic-app-data-v2.s3.amazonaws.com/dashboards/AzureStorage/Azure-Storage-Blob-Service.png')} alt="Azure Storage Blob Service dashboard" style={{border: '1px solid gray'}} width="800" />

### File Service

The **Azure Storage - File Service** dashboard provides details like read bytes, write bytes, last 10 operations, read/write trend by service type, and top 10 read/write by resource name.

Use this dashboard to:
    * View amount of read data in MB.
    * View amount of write data in MB.
    * View Read vs Write.
    * View Reads by File Share.
    * View Writes by File Share.
    * View File Share by Failed Operations.
    * View Top 10 Resources by Failures.
    * View Top 10 Resources by Latency.
    * View Top 10 Resources by Reads(MB).
    * View Top 10 Resources by Writes(MB).

<img src={useBaseUrl('https://sumologic-app-data-v2.s3.amazonaws.com/dashboards/AzureStorage/Azure-Storage-File-Service.png')} alt="Azure Storage File Service dashboard" style={{border: '1px solid gray'}} width="800" />

### Queue Service

The **Azure Storage - Queue Service** dashboard provides details like read bytes, write bytes, last 10 operations, read/write trend by service type, and top 10 read/write by resource name.

Use this dashboard to:
    * View amount of read data in MB.
    * View amount of write data in MB.
    * View Read vs Write.
    * View Reads by Queue Service.
    * View Writes by Queue Service.
    * View Queue Service by Failed Operations.
    * View Top 10 Resources by Failures.
    * View Top 10 Resources by Latency.
    * View Top 10 Resources by Reads(MB).
    * View Top 10 Resources by Writes(MB).

<img src={useBaseUrl('https://sumologic-app-data-v2.s3.amazonaws.com/dashboards/AzureStorage/Azure-Storage-Queue-Service.png')} alt="Azure Storage Queue Service dashboard" style={{border: '1px solid gray'}} width="800" />

### Table Service

The **Azure Storage - Table Service** dashboard provides details like read bytes, write bytes, last 10 operations, read/write trend by service type, and top 10 read/write by resource name.

Use this dashboard to:
    * View amount of read data in MB.
    * View amount of write data in MB.
    * View Read vs Write.
    * View Reads by Table Service.
    * View Writes by Table Service.
    * View Table Service by Failed Operations.
    * View Top 10 Resources by Failures.
    * View Top 10 Resources by Latency.
    * View Top 10 Resources by Reads(MB).
    * View Top 10 Resources by Writes(MB).

<img src={useBaseUrl('https://sumologic-app-data-v2.s3.amazonaws.com/dashboards/AzureStorage/Azure-Storage-Table-Service.png')} alt="Azure Storage Table Service dashboard" style={{border: '1px solid gray'}} width="800" />

### Audit control plane operations

The **Azure Storage - Audit control plane operations** dashboard provides details like changes, read/write/delete specific changes, different operations used, top 10 operations that caused most errors, and most common errors.

Use this dashboard to:
    * View last 24 hours changes.
    * View changes - read, write, and delete.
    * View operations used.
    * View Top 10 operations that caused the most errors.
    * View Top 10 most common errors.
    * View requests with anonymous access.
    * view Operations that caused server-side throttling errors.

<img src={useBaseUrl('https://sumologic-app-data-v2.s3.amazonaws.com/dashboards/AzureStorage/Azure-Storage-Audit-control-plane-operations.png')} alt="Azure Storage audit control plane operations dashboard" style={{border: '1px solid gray'}} width="800" />

### Security and policy

The **Azure Storage - Security and Policy** dashboard provides security, policy, and recommendation details.

Use this dashboard to:
    * View recent security events.
    * View total security events.
    * View total denied policy events.
    * View recent failed policy events.
    * View recent success policy events.
    * View total recommendation events.
    * View recent recommendation events.

<img src={useBaseUrl('https://sumologic-app-data-v2.s3.amazonaws.com/dashboards/AzureStorage/Azure-Storage-Security-and-policy.png')} alt="Azure Storage Security and policy dashboard" style={{border: '1px solid gray'}} width="800" />

### Health

The Azure Storage health dashboard provides information about the service health and alerts.

Use this dashboard to:
    * View recent service health incidents.
    * Monitor service health by event type.
    * View service health by event type-Time chart.
    * View recent alerts.
    * View total alerts.
    * View alerts over time.
    * View recent resource health incidents.
    * Monitor resource health by event type.

<img src={useBaseUrl('https://sumologic-app-data-v2.s3.amazonaws.com/dashboards/AzureStorage/Azure-Storage-Health.png')} alt="Azure Storage health dashboard" style={{border: '1px solid gray'}} width="800" />

### Availability

The **Azure Storage - Availability** metrics dashboard provides details like availability in percentage, availability by API name, and trend by API name and by storage type.

Use this dashboard to:
    * Monitor availability percentage.
    * Monitor availability percentage trend by Storage Type.
    * View API with < 100 availability.
    * Monitor availability percentage by API name.
    * Monitor availability percentage trend by Storage Account.

<img src={useBaseUrl('https://sumologic-app-data-v2.s3.amazonaws.com/dashboards/AzureStorage/Azure-Storage-Availability.png')} alt="Azure storage availability dashboard" style={{border: '1px solid gray'}} width="800" />

### Failures

The **Azure Storage - Failures** metrics dashboard provides details like failing transactions by API name, response type, storage account, and storage type.

Use this dashboard to:
    * Monitor Failed transactions by authentication.
    * Monitor Failed transactions by response type.
    * Monitor Failed request count by status text.
    * Monitor Failed Transactions.
    * Monitor Failed Transaction by Category.
    * Monitor Non-zero status code by storage account.
    * Monitor Failed transactions by API name.
    * Monitor Failed transactions by service type.
    * Monitor Failed transactions by authentication.
    * Monitor Failed transactions by response type.
    * Monitor Recent failed request.

<img src={useBaseUrl('https://sumologic-app-data-v2.s3.amazonaws.com/dashboards/AzureStorage/Azure-Storage-Failures.png')} alt="Azure Storage Failures dashboard" style={{border: '1px solid gray'}} width="800" />

### Performance

The **Azure Storage - Performance** metrics dashboard provides details like failing transactions by API name, response type, storage account, and storage type.

Use this dashboard to:
    * Monitor Average Success Server Latency.
    * Monitor average success E2E latency.
    * View Average Latency(ms) of successful calls by API name.
    * View Success E2E Latency vs. Success Server Latency (ms).
    * View Success E2E Latency vs. Success Server Latency (ms) by Service Type.
    * View Top 10 Success Server Latency by API name.
    * View SuccessE2ELatency(ms).
    * View SuccessServerLatency(ms).
    * View Top 10 high latency transactions.

<img src={useBaseUrl('https://sumologic-app-data-v2.s3.amazonaws.com/dashboards/AzureStorage/Azure-Storage-Performance.png')} alt="Azure Storage Performance dashboard" style={{border: '1px solid gray'}} width="800" />

## Create monitors for Azure Storage

import CreateMonitors from '../../reuse/apps/create-monitors.md';

<CreateMonitors/>

### Azure Storage alerts
These alerts are metric based and will work for all Azure Storage.

| Alert Name | Alert Description and Conditions | Alert Condition | Recover Condition |
|:--|:--|:--|:--|
| `Azure Storage - Availability` | This alert is triggered when average Availability is less than 90%. Also, a warning type alert will be triggered when average Availability is less than 95%. | Percentage < = 90 | Percentage > 90 |
| `Azure Storage - Success E2E Latency` | This alert is triggered when Success E2E Latency is greater than 1000 MilliSeconds. | MilliSeconds > = 1000 | MilliSeconds < 1000 |
| `Azure Storage - Success Server Latency` | This alert is triggered when Success Server Latency greater than 1000. | MilliSeconds > = 1000 | MilliSeconds < 1000 |
| `Azure Storage - Transactions` | This alert is triggered when Transactions count greater than 500. | Count > = 500 | Count < 500 |
| `Azure Storage - Used Capacity(GB)` | This alert is triggered when Used Capacity(GB) greater than 100. | Byted(GB) > = 100 | Byted(GB) < 100 |

## Upgrade/Downgrade the Azure Storage app (optional)

import AppUpdate from '../../reuse/apps/app-update.md';

<AppUpdate/>

## Uninstalling the Azure Storage app (optional)

import AppUninstall from '../../reuse/apps/app-uninstall.md';

<AppUninstall/>

## Troubleshooting

### HTTP Logs and Metrics Source used by Azure Functions

To troubleshoot metrics collection, follow the instructions in [Collect Metrics from Azure Monitor > Troubleshooting metrics collection](/docs/send-data/collect-from-other-data-sources/azure-monitoring/collect-metrics-azure-monitor/#troubleshooting-metrics-collection).
