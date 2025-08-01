---
title: VMware Carbon Black Cloud Endpoint Standard V2
description: ''
---

import useBaseUrl from '@docusaurus/useBaseUrl';

<img src={useBaseUrl('/img/platform-services/automation-service/app-central/logos/vmware-carbon-black-cloud-endpoint-standard-v2.png')} alt="vmware-carbon-black-cloud-endpoint-standard-v2" width="70"/>

***Version: 2.2  
Updated: Mar 4, 2024***

VMware Carbon Black Cloud Endpoint Standard Integration allows security operators to collect information and take action on remote endpoints in real-time using API V6.

## Actions

* **Carbon Black Cloud Alerts Daemon** (*Daemon*) - Daemon to automatically gather alerts.
* **Delete File** (*Containment*) - Delete a File from a device.
* **Get Alert** (*Enrichment*) - Get a specific Alert.
* **Get Device** (*Enrichment*) - Retrieve info about a device.
* **Get Device Quarantine Status** (*Enrichment*) - Get a specific Device Quarantine Status.
* **Get Device Vulnerability** (*Enrichment*) - Get a specific Device Vulnerability.
* **Get Group Alerts** (*Enrichment*) - Get a specific Group of Alerts.
* **Quarantine** (*Containment*) - Quarantine the specified device within Carbon Black Cloud.
* **Search Process** (*Enrichment* ) - Queries all events using input search criteria and returns a list of processes.
* **Terminate Process** (*Containment*) - Terminate process on a device.

## Configure VMware Carbon Black Cloud Endpoint Standard V2 in Automation Service and Cloud SOAR

import IntegrationsAuth from '../../../../reuse/integrations-authentication.md';
import IntegrationCertificate from '../../../../reuse/automation-service/integration-certificate.md';
import IntegrationEngine from '../../../../reuse/automation-service/integration-engine.md';
import IntegrationLabel from '../../../../reuse/automation-service/integration-label.md';
import IntegrationProxy from '../../../../reuse/automation-service/integration-proxy.md';
import IntegrationTimeout from '../../../../reuse/automation-service/integration-timeout.md';

<IntegrationsAuth/>
* <IntegrationLabel/>
* **Server URL**. Enter your VMWare Carbon Black Cloud Endpoint Standard V2 server URL.

* **Organization Key**. Enter your [VMWare Carbon Black Cloud Endpoint Standard V2 organization key](https://developer.carbonblack.com/reference/carbon-black-cloud/authentication/#org-key).

* **API ID/Connector ID**. [VMWare Carbon Black Cloud Endpoint Standard V2 API ID](https://developer.carbonblack.com/reference/carbon-black-cloud/authentication/#authenticate-your-request).

* **API Secret Key**. Enter the secret for the API ID.
* <IntegrationTimeout/>
* <IntegrationCertificate/>
* <IntegrationEngine/>
* <IntegrationProxy/>

<img src={useBaseUrl('/img/platform-services/automation-service/app-central/integrations/misc/vmware-carbon-black-endpoint-standard-v2-configuration.png')} style={{border:'1px solid gray'}} alt="VMware Carbon Black Cloud Endpoint Standard V2 configuration" width="400"/>

For information about Carbon Black Cloud Endpoint Standard V2, see [Carbon Black Cloud documentation](https://techdocs.broadcom.com/us/en/carbon-black/cloud.html).

## Change Log

* February 3, 2022 - First upload
* July 11, 2023 (v2.1) - Updated the integration with Environmental Variables
* March 4, 2024 (v2.2) - Updated code for compatibility with Python 3.12
