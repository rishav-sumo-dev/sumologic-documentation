---
title: Neurons ITSM
description: ''
---
import useBaseUrl from '@docusaurus/useBaseUrl';

<img src={useBaseUrl('/img/platform-services/automation-service/app-central/logos/neurons-itsm.png')} alt="neurons-itsm" width="70"/>

***Version: 1.1  
Updated: Jul 06, 2023***

Ivanti Neurons ITSMis IT service management solution that transforms help desks and support teams into strategic business.

## Actions

* **List Incidents** (*Enrichment*) - Fetches all records for incidents.
* **Create Problem** (*Containment*) - Creates problem.
* **Create Change** (*Containment*) - Creates change.
* **Create Incident Neurons ITSM** (*Containment*) - Creates incident.
* **Close Incident** (*Containment*) - Close an incident using a quick action.

## Neurons ITSM configuration

To [access Neurons for ITSM](https://help.ivanti.com/ht/help/en_US/ISM/2025/admin-user/Content/Common/How%20to%20Log%20In.htm), specify the URL for your tenant that has been sent to you by email. 

To [view your API Key](https://help.ivanti.com/ht/help/en_US/ISM/2025/admin-user/Content/Configure/API/Using-REST-API-Key.htm) from the Configuration Console, click **Configure > Security Controls > API Keys** to open the API Keys workspace. The application displays the API keys. Copy your key.

## Configure Neurons ITSM in Automation Service and Cloud SOAR

import IntegrationsAuth from '../../../../reuse/integrations-authentication.md';
import IntegrationCertificate from '../../../../reuse/automation-service/integration-certificate.md';
import IntegrationEngine from '../../../../reuse/automation-service/integration-engine.md';
import IntegrationLabel from '../../../../reuse/automation-service/integration-label.md';
import IntegrationProxy from '../../../../reuse/automation-service/integration-proxy.md';
import IntegrationTimeout from '../../../../reuse/automation-service/integration-timeout.md';

<IntegrationsAuth/>
* <IntegrationLabel/>
* **Tenant URL**. Enter your Neurons ITSM [tenant URL](https://help.ivanti.com/ht/help/en_US/ISM/2025/admin-user/Content/Configure/LogIn/Log_In_Using_URLs.htm).

* **API Key**. The [API key](https://help.ivanti.com/ht/help/en_US/ISM/2025/admin-user/Content/Configure/API/Using-REST-API-Key.htm) you [copied earlier](#neurons-itsm-configuration).
* <IntegrationCertificate/>
* <IntegrationTimeout/>
* <IntegrationEngine/>
* <IntegrationProxy/>

<img src={useBaseUrl('/img/platform-services/automation-service/app-central/integrations/misc/neurons-itsm-configuration.png')} style={{border:'1px solid gray'}} alt="Neurons ITSM configuration" width="400"/>

For information about Neurons for ITSM, see [Neurons or ITSM documentation](https://help.ivanti.com/ht/help/en_US/ISM/2025/admin-user/Content/Common/Getting%20Started.htm).

## Change Log

* August 25, 2022 - First upload
* September 1, 2022 - New Logo
* July 6, 2023 (v1.1)
	+ Updated the integration with Environmental Variables
	+ Changed type to Notification for following actions:
		- Create Change
		- Create Incident Neurons
		- Create Problem
