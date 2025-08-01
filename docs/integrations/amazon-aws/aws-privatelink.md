---
id: aws-privatelink
title: Sumo Logic Connector for AWS PrivateLink (Beta)
sidebar_label: AWS PrivateLink (Beta)
description: AWS PrivateLink provides private connectivity between VPCs, AWS services, and your on-premises networks, without exposing your traffic to the public internet.
---

import useBaseUrl from '@docusaurus/useBaseUrl';

<head>
  <meta name="robots" content="noindex" />
</head>

<p><a href="/docs/beta"><span className="beta">Beta</span></a></p>

<!-- Originally added as a beta article with SUMO-187085. -->

Sumo Logic provides the ability to configure private connectivity between your AWS Infrastructure and Sumologic via [AWS PrivateLink](https://aws.amazon.com/privatelink). This prevents any traffic from being accessible to the public internet.

Following sources are supported for AWS PrivateLink:

- **Installed Collector sources**. Data collected on Installed collectors deployed on customer VPC and sent to Sumo Logic.
- **Sumo Logic OpenTelemetry Distro Collector sources**. Data collected on OpenTelemetry Distro collectors deployed on customer VPC and sent to Sumo Logic.
- **HTTPs sources**. Data sent by the applications hosted in customers VPC and sent over to Sumologic using [HTTP Logs and Metrics Source](/docs/send-data/hosted-collectors/http-source/logs-metrics/) and Kinesis Firehose Source for Logs and Metrics.
- **OTLP Source**. An [OTLP/HTTP Source](/docs/send-data/hosted-collectors/http-source/otlp/) is an endpoint for receiving OTLP-formatted Logs and Metrics from OpenTelemetry collectors using [OTLP exporter](https://github.com/open-telemetry/opentelemetry-collector/tree/v0.99.0/exporter/otlphttpexporter#otlphttp-exporter).

The following sources are not supported for AWS PrivateLink:

- Cloud Syslog
- AWS S3
- AWS Cloudwatch source
- RUM sources

## Enable PrivateLink for ALB

To send data to Sumo Logic through AWS PrivateLink, you'll need to configure an internal endpoint in your VPC for Installed Collectors to send data to.

With the NLB-created and ALB-registered as a target, requests over AWS PrivateLink to the NLB are forwarded to the ALB.

Sumo Logic exposes AWS PrivateLink endpoints to different [regions that depend on your Sumo Logic deployment](/docs/api/about-apis/getting-started/#sumo-logic-endpoints-by-deployment-and-firewall-security). If you're using the VPC in a different region where the Sumo Logic PrivateLink endpoint service is set up, you need to set up VPC peering. Either way, you need to create an endpoint.

<div class="responsive-table">

| Deployment | Collection endpoint | OpenTelemetry collector endpoint | AWS Region of Sumo PrivateLink endpoint service |
|:-----------|:---------------------|:----------------------------------|:------------------------------------------------|
| AU         | `collectors.au.sumologic.com` | `open-collectors.au.sumologic.com` | `ap-southeast-2` |
| CA         | `collectors.ca.sumologic.com` | `open-collectors.ca.sumologic.com` | `ca-central-1` |
| DE         | `collectors.de.sumologic.com` | `open-collectors.de.sumologic.com` | `eu-central-1` |
| EU         | `collectors.eu.sumologic.com`<br/>`endpoint1.collection.eu.sumologic.com` | `open-collectors.eu.sumologic.com` | `eu-west-1` |
| JP         | `collectors.jp.sumologic.com` | `open-collectors.jp.sumologic.com` | `ap-northeast-1` |
| KR         | `collectors.kr.sumologic.com` | `open-collectors.kr.sumologic.com` | `ap-northeast-2` |
| US1        | `collectors.sumologic.com`<br/>`endpoint1.collection.sumologic.com`<br/>`endpoint2.collection.sumologic.com`<br/>`endpoint3.collection.sumologic.com`<br/>`endpoint4.collection.sumologic.com`<br/>`endpoint5.collection.sumologic.com` | `open-collectors.sumologic.com` | `us-east-1` |
| US2        | `collectors.us2.sumologic.com`<br/>`endpoint1.collection.us2.sumologic.com`<br/>`endpoint2.collection.us2.sumologic.com`<br/>`endpoint3.collection.us2.sumologic.com`<br/>`endpoint4.collection.us2.sumologic.com`<br/>`endpoint5.collection.us2.sumologic.com`<br/>`endpoint6.collection.us2.sumologic.com`<br/>`endpoint7.collection.us2.sumologic.com`<br/>`endpoint8.collection.us2.sumologic.com`<br/>`endpoint9.collection.us2.sumologic.com` | `open-collectors.us2.sumologic.com` | `us-west-2` |

</div>

### Create an endpoint to connect with the Sumo Logic endpoint service

* The service name is provided by Sumo Logic and will accept the endpoint connection request once we know you initiated the connection.
* Select the VPC where the Sumo Logic collector will be installed or where HTTP requests will be made for HTTP Sources.

  <img src={useBaseUrl('img/integrations/amazon-aws/privatelink-create-endpoint.png')} alt="CreateEndpoint" width="500"/>

### No VPC Peering

If the VPC is in the same [AWS region as your deployment](/docs/api/about-apis/getting-started/#sumo-logic-endpoints-by-deployment-and-firewall-security), you do not need to set up VPC peering. Navigate to **Actions**, then select **Modify private DNS name**.

![Endpoint](/img/integrations/amazon-aws/privatelink-endpoints.png)

Check the box to enable private DNS names.

<img src={useBaseUrl('img/integrations/amazon-aws/privatelink-dns-checkbox.png')} alt="DnsCheckpoint" width="550"/>

### VPC Peering

If the VPC is not in the same [AWS region as your deployment](/docs/api/about-apis/getting-started/#sumo-logic-endpoints-by-deployment-and-firewall-security), you'll need to [set up VPC peering](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-peering.html).

1. Create the VPC peering connection between the region for the client-side VPC and the region where the Sumo Logic PrivateLink service is configured.
2. Create a Route53 private hosted zone. Select the VPC peered in the region where our server-side region is located.
3. With the created private hosted zone, add an **A** record. Select the peered VPC in region **us-west-2**, where the Sumo Logic server-side infrastructure is located.<br/> ![QuickRecord](/img/integrations/amazon-aws/privatelink-quickcreaterecord.png)
4. Add the other peered VPC in the other region into the Route53-hosted zone.
