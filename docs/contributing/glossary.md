---
id: glossary
title: Glossary
description: This glossary provides an alphabetized list of technical term definitions used in Sumo Logic.
---

This glossary defines Sumo Logic terms that you are likely to encounter when you read our documentation. It does not provide common industry terms unless those terms also represent Sumo Logic features.

If you're looking for usage guidance, see [Word List](/docs/contributing/word-list).

:::tip
We also maintain a [DevOps and Security Glossary](https://www.sumologic.com/glossary).
:::

## A

**[Absolute expressions](/docs/search/get-started-with-search/search-basics/time-range-expressions)**. Used in time range expressions, when setting a specific time range of a search. For example, 04/01/2018 20:32:00 to 04/01/2018 20:35:00 will run the search from April 1, 2018 at 8:32 PM until April 1, 2018 at 8:35 PM.

**[Access Key](/docs/manage/security/access-keys)**. A key, generated by Sumo Logic, that you use to securely register new Collectors and to access Sumo Logic APIs.

**[Admin mode](/docs/manage/content-sharing/admin-mode)**. If your Sumo Logic role grants you the **Manage Content** capability, you can switch to Admin mode so that you can move content from one folder to another for anyone in your organization, and mark content “Admin Recommended”.

**[Admin recommended](/docs/manage/content-sharing/admin-mode/#move-important-content-to-admin-recommended)**. An area at the top of the Sumo Logic Library in the Left-Nav that lists highlighted content. A Sumo Logic user with the Manage Content capability can add content to the admin recommended list.

**[Aggregate](/docs/search/search-query-language/group-aggregate-operators)**. A group of data returned by a search, displayed in a simple table in the Aggregates tab of the Search page.

**[Alert](/docs/alerts)**. A notification you can configure for a scheduled search. There are multiple alert types, such as Email, Script Action, ServiceNow Connection, Webhook, and Save to Index.

**[Allowlist](/docs/manage/security/create-allowlist-ip-cidr-addresses)**. Sumo Logic’s Service Allowlist Settings allow you to explicitly grant access to specific IP addresses and/or CIDR notations for logins, APIs, and dashboard access.

**[Amazon S3 Audit Source](/docs/send-data/hosted-collectors/amazon-aws/amazon-s3-audit-source)**. The Amazon S3 Audit Source, also called Server Access Logging, tracks and collects your Amazon S3 bucket's activity logs.

**[Apps](/docs/integrations)**. Sumo Logic Apps (short for applications) deliver out-of-the-box Dashboards, reports, saved searches, and field extraction for popular data Sources, such as AWS, Windows, Apache, and many more. When a customer installs an app in Sumo Logic, preconfigured searches and Dashboards are customized with the customer's Source configurations and populated in a folder. Customers then can monitor their system's behavior visually using the Dashboards.

**[Autocomplete](/docs/search/get-started-with-search/search-basics/search-autocomplete)**. On the Search page of the Sumo Logic user interface, the search autocomplete dropdown dialog offers suggestions to make query writing easier. Suggestions include simple logic that offers common default queries, keywords, metadata terms, and search operators. The autocomplete dialog also includes links to Help topics for more information.

**[Automation Service](/docs/cse/automation/about-automation-service-and-cloud-siem)**. In Cloud SIEM, a service that automatically runs tasks such as sending notifications or adding data to records when security incidents occur.


## B

**[Burst limit](/docs/metrics/manage-metric-volume/metric-throttling)**. The point at which Sumo Logic slows metric data ingestion to keep it within your allowable contracted limits. Metric data volume is measured in Data Points per Minute (DPM). Sumo Logic allows for spikes in metrics ingestion until it reaches a calculated burst limit, then starts throttling your data sources.




## C

**[Capability](/docs/manage/users-roles/roles/role-capabilities)**. In Sumo Logic role-based access control (RBAC), you grant the users with a role the right to perform a particular function by assigning the corresponding capability to the role. For example, the “Manage Collectors” capability allows a user to install and manage installed and hosted Collectors and Sources.

**[Carbon 2.0](/docs/metrics/introduction/metric-formats#carbon-20)**. A plaintext metric format in which metrics are identified by key-value pairs. In Carbon 2.0, the actual thing being measured is identified by intrinsic tags; additional metadata is provided in meta tags. Sumo’s [HTTP source](/docs/send-data/hosted-collectors/http-source) and [Streaming Metric Source](/docs/send-data/installed-collectors/sources/streaming-metrics-source) support Carbon 2.0 metrics.

**[Cardinality](/docs/metrics/logs-to-metrics/#manage-metric-cardinality)**. Refers to the uniqueness of values in a database column or metric dimension. High cardinality metrics are metrics with dimensions that have many different values, which can result in a high volume of unique time series. In Sumo Logic, you can use a transformation rule to aggregate high cardinality data from ephemeral sources into higher-level metrics that you want to analyze over time.

**[Clobber](/docs/send-data/installed-collectors/collector-installation-reference/force-collectors-name-clobber/)**. During the installation process, use the clobber flag in situations where you're creating a new Collector that will use a name that is already in use by another Collector. Clobber deletes (clobbers) the existing collector with the same name.

<!--
**[Cloud](/docs/get-started#sumo-logic-cloud)**. The Sumo Logic Cloud is a secure, scalable repository for all of your operations, security, compliance, development, and other log data. The Sumo Logic Cloud stores, indexes, parses, and analyzes data, and provides unlimited horsepower with elastic scalability.
-->

**[Collector](/docs/send-data/choose-collector-source)**. Sumo Logic Collectors are lightweight applications that allow you to connect your environment to Sumo Logic in order to collect message data. There are two types of Collectors. Installed Collectors are configured on machines in your deployment for Sources such as Local File, Remote File, Syslog, Local Windows Event Logs, Remote Windows Event Logs, and Script. Hosted Collectors require no installation, and are used to collect data from various services like Amazon S3 or over HTTP and Syslog.

**[Content Administrator](/docs/manage/content-sharing/admin-mode)**. In the Sumo Logic Library, you can chose **View as Content Administrator** to enter Admin Mode, so you can manage content for your organization. In Admin mode you can migrate content from one location to another, and highlight important content in the **Admin Recommended** folder.

**[Content sharing](/docs/manage/content-sharing)**. A Sumo Logic feature that allows you to share searches, dashboards, and folders with a user, a role, or combinations of the two.




## D

**[Dashboard](/docs/dashboards)**. Dashboards contain a collection of real time Panels that provide a graphical representation of your organization's data. Panels are created by running search queries. From the resulting data in the Search page's Aggregates tab, you can display that data using different types of charts. Once Panels are created, they are saved to a Dashboard.

<!--
**[Dashboard Theme](/docs/dashboards)**. In Dashboards, you can toggle the background color scheme from Light mode to Dark mode.
-->

**[Data access level](/docs/dashboards/set-data-access-level)**. The data access level for a dashboard determines what data a user with whom the dashboard is shared can view in the dashboard.

**[Data Forwarding](/docs/manage/data-forwarding)**. When enabled, the Data Forwarding feature allows Sumo Logic to upload data to an Amazon S3 bucket that belongs to your organization. Log messages are saved as CSV files in compressed gzip files. They are accumulated and returned right after being ingested by Sumo Logic.

**[Data Panel](/docs/dashboards/panels)**. Panels are placed on Dashboards and provide a graphical representation of your organization's data. Data Panels are created by running search queries. From the resulting data in the Search page's Aggregates tab, you can display that data using different types of charts. Once Panels are created, they are saved to a Dashboard. See also, Text Panel.

**[Data Type](/docs/get-started/faq)**. A Data Type is a specific type of log used with a Sumo Logic Source or App, such as Apache, MySQL, or Windows IIS. You can also use a custom Data Type for a custom application.

**[Data Volume Index](/docs/manage/ingestion-volume/data-volume-index)**. The Data Volume Index automatically provides data that allows you to understand your account’s data ingest volume in bytes and number of log messages processed overall. The Data Volume Index gives you better visibility into how much data you are sending to Sumo Logic, allowing you to proactively manage your systems’ behavior and to fine tune your data ingest with respect to the data plan for your Sumo Logic subscription.

**[Deployment](/docs/api/about-apis/getting-started/#sumo-logic-endpoints-by-deployment-and-firewall-security)**. Sumo Logic has several deployments that are assigned depending on the geographic location and the date an account is created.

<!--
**Dimension**. In [Carbon 2.0](/docs/metrics/introduction/metric-formats#carbon-20) and [Prometheus](/docs/metrics/introduction/metric-formats#prometheus) metrics, dimensions are the one or more space-separated key-value pairs that uniquely identify what is being measured. Dimensions are also referred to as intrinsic tags and labels.
-->

**[Disabled metric source](/docs/metrics/manage-metric-volume/disabled-metrics-sources)**. A metric source that Sumo Logic has disabled because it has received too many unique time series. A disabled metric source will stop receiving data, and that data cannot be recovered.

**[DPM](/docs/metrics/manage-metric-volume/data-limits-for-metrics)**. Stands for data points per minute. Metric data volume is measured in DPM. For example, a CPU metric reported on a single host every 15 seconds produces 4 DPM.




## E

**[Ephemeral](/docs/send-data/installed-collectors/collector-installation-reference/set-collector-as-ephemeral)**. Refers to data sources, such as containers, that are created and destroyed as appropriate, resulting in a high volume log data or metrics. In Sumo Logic, you can set a collector to be ephemeral—Sumo Logic deletes an ephemeral collector automatically after it has been offline for 12 hours.

**[Endpoints](/docs/api/about-apis/getting-started/#sumo-logic-endpoints-by-deployment-and-firewall-security)**. Sumo Logic has several pods that are assigned depending on the geographic location and the date an account is created. Sumo Logic redirects your browser to the correct login URL and also redirects Collectors to the correct endpoint. However, if you're using an API you'll need to manually direct requests to the correct API endpoint; API calls are not redirected to another endpoint.

**[Enrichment](/docs/cse/integrations/enrichments-and-indicators)**. In Cloud SIEM, addition of data to records that provides more information for analysis of security incidents.

**[Entity](/docs/cse/records-signals-entities-insights/view-manage-entities)**. In Cloud SIEM, a unique actor encountered in incoming messages, such as a user, IP address, or host.

**[Exclude rule](/docs/send-data/collection/processing-rules/include-and-exclude-rules)**. Exclude rules are a type of Processing Rule that specifies log messages that you do not want to send to Sumo Logic, think of it as an "allowlist" filter.


## F

**[Favorite](/docs/get-started/library)**. The Favorites tab displays searches and Dashboards that you refer to frequently, or content that you want to keep handy. In the Library, on the Personal and Org tabs, you can "favorite" content to make it appear on the Favorites tab. Just click the star icon for your saved search, Dashboard, installed app, or folder, and it will be saved to the Favorites tab for easy access. You can also favorite saved searches from the Search page, and favorite Dashboards from the Dashboards page.

**[Fields](/docs/manage/fields)**. Fields allow you to reference log data based on meaningful associations. They act as metadata tags that are assigned to your logs so you can search with them. Each field contains a key-value pair, where the field name is the key. Fields may be referred to as Log Metadata Fields.

**[Field Extraction Rule](/docs/manage/field-extractions)**. Field Extraction can be set up as rules that parse out fields as log messages are ingested. This means that instead of running a query to parse out fields, that work is done automatically so when it's time to run a search the fields are already available in results.

**[Fingerprint](/docs/send-data/installed-collectors/configuration/#fingerprint)**. A fingerprint consists of the first 2048 bytes of a file and is used by Installed Collectors to track what data has been collected.

**[Flow Graph](/docs/integrations/amazon-aws/guardduty-benchmark)**. A graph or map that dynamically displays a directional flow from a source to a target. Such as the flow of cyber threats from the geographic locations of sources to their targets, dynamically illustrated in the Threat Sources and Targets by Geography panel of the [Amazon GuardDuty Global Baseline](/docs/integrations/amazon-aws/guardduty-benchmark) dashboard.


## G

**[Geo lookup](/docs/search/search-query-language/search-operators/geo-lookup-map)**. Sumo Logic can match a [parsed](/docs/search/search-query-language/parse-operators) IPv4 or IPv6 address to its geographical location on a map. To create the map the **lookup** operator matches parsed IP addresses to their physical location based on the latitude and longitude of where the addresses originated.

**[Graphite](/docs/metrics/introduction/metric-formats#graphite)**. A plaintext metric format where the thing you’re measuring is identified by a dot-separated string, referred to as a metric path. Sumo’s [HTTP source](/docs/send-data/hosted-collectors/http-source) and [Streaming Metric Source](/docs/send-data/installed-collectors/sources/streaming-metrics-source) support Graphite metrics.

**[Group](/docs/search/search-query-language/group-aggregate-operators)**. Group-by functions include `count`, `count_distinct`, `sum`, `avg`, `stddev`, `max`, `min`, `last`, and `first`. You can use "group" or "by" instead of "group by", so `"count (*) group by user"` is equivalent to `"count by user"`. All group-by functions create a corresponding field preceded by an underscore, for example, `_count`.




## H

**[Hash rules](/docs/send-data/collection/processing-rules/hash-rules)**. Hash rules replace a message with a unique, randomly-generated code to protect sensitive or proprietary information. You may want to hash unique identifiers, such as credit card numbers or user names. By hashing this type of data, you can still track it, even though it's fully hidden.

**[Host Metrics](/docs/integrations/hosts-operating-systems/host-metrics)**. The Sumo Logic app for Host Metrics allows you to collect local host metrics and display them using predefined search queries and dashboards. The app provides dashboards to display analysis of local host metrics for the CPU, disk, memory, network, and TCP.

**[Hosted Collectors](/docs/send-data/hosted-collectors)**. Hosted Collectors do not require installation or registration, nor do Hosted Collectors have physical requirements, since they're hosted by Sumo Logic in AWS.


## I

**[If operator](/docs/search/search-query-language/search-operators/if)**. A ternary operator used to evaluate a condition as either true or false, with values assigned for each outcome. It is a shorthand way to express an if-else condition.

**[Include rule](/docs/send-data/collection/processing-rules/include-and-exclude-rules)**. Include rules are a type of Processing Rule that is used to send only the data you'd like in your Sumo Logic account (an "allowlist" filter). This type of filter can be very useful when the list of log data you want to send to Sumo Logic is easier to filter than setting up exclude filters for all of the types of messages you'd like to exclude.

**[Ingest Budget](/docs/manage/ingestion-volume/ingest-budgets)**. Ingest budgets control the capacity of daily log ingestion volume sent to Sumo Logic from Collectors.

**[Insight](/docs/cse/get-started-with-cloud-siem/about-cse-insight-ui)**. In Cloud SIEM, a group of signals clustered around a single entity that are generated when an entity’s Activity Score exceeds a threshold.

**[Installed Collector](/docs/send-data/installed-collectors)**. Installed Collectors are deployed in your environment, either on a local machine, a machine in your organization, or even an Amazon Machine Image (AMI). Installed Collectors require a software download and installation. Upgrades to Collector software are released regularly by Sumo Logic.

**[Installation Token](/docs/manage/security/installation-tokens)**. Installation Tokens are assigned to your organization and are used to register Installed Collectors to your Sumo Logic account. They do not expire and can only be used to register Installed Collectors. You can deactivate, reactivate, or delete tokens at any time.

**[Intrinsic tags](/docs/metrics/introduction/metric-formats#carbon-20)**. In Carbon 2.0-formatted metrics, intrinsic tags are the one or more space-separated key-value pairs that uniquely identify what is being measured. Intrinsic tags are also referred to as dimensions.


## K

**[Kubernetes Views](/docs/observability/kubernetes/monitoring)**. Allows you to intuitively filter on four hierarchical components of your Kubernetes system to focus your search on nodes, deployments, services, or namespaces. Kubernetes Views make it easier to traverse your Kubernetes hierarchy to monitor specific components, identify problems, discover root problems, and take progressive action.


## L

**[Library](/docs/get-started/library)**. The Library provides a central location for shared and saved content in your Sumo Logic account, as well as content shared by others in your organization. In addition to shared and saved searches, Dashboards can be saved and shared in the Library.

**[Live Tail](/docs/search/live-tail)**. Sumo Logic Live Tail allows you to see a real-time live feed of log events associated with a Source or Collector. The live feeds can help you with development and troubleshooting. You can see all log messages as they come in, but they are not sorted as they are with Search.

**[Local Configuration File Management](/docs/send-data/use-json-configure-sources/local-configuration-file-management)**. Local Configuration File Management allows you to set up and manage Sources on an Installed Collector using one or more JSON files.

**[LogCompare](/docs/search/behavior-insights/logcompare)**. LogCompare allows you to compare a section of your log messages from one point in time with the same section at another point in time, and display the changes in patterns.

**[LogReduce](/docs/search/behavior-insights/logreduce)**. LogReduce uses fuzzy logic to cluster messages together based on string and pattern similarity. Use the LogReduce button and operator to quickly assess activity patterns for things like a range of devices or traffic on a website.

**[Logs-to-Metrics](/docs/metrics/logs-to-metrics)**. A Sumo Logic feature you can use to extract or create metrics from log data. You can extract metrics that are embedded in logs, or count logs as a metric.




## M

**[Mapper](/docs/cse/schema/create-structured-log-mapping)**. In Cloud SIEM, a script that maps message fields to record attributes.

**[Markdown](/docs/dashboards/panels/markdown-syntax)**. Used in Dashboards, you can add Text Panels to include titles or text descriptions. Use Markdown syntax to add bold or italic formatting, bullet lists, code font, and other formatting. See Help for details.

**[Mask rule](/docs/send-data/collection/processing-rules/mask-rules)**. Mask rules are a type of Processing Rule that replaces an expression with a mask string that you can customize—another option to protect data, such as passwords, that you wouldn't normally track.

**[Messages tab](/docs/search/get-started-with-search/search-page/set-messages-tab-preferences)**. When you run a search query, messages display in the Message tab in the lower half of the browser window of the Search page.

**[Metadata](/docs/send-data/data-enrichment)**. Data about other data. If the logs and metrics you ingest have associated metadata, you can leverage it for more targeted log searches and metric queries. Metadata for metrics includes both intrinsic tags and meta tags.

**[Meta tags](/docs/metrics/introduction/metric-formats#carbon-20)**. In Carbon 2.0-formatted metrics, meta tags are the key-value pairs for a metric that provide additional, but not identifying information about the thing being measured. A meta tag is a piece of metadata that might be useful in querying your metrics.

**[Metric rules editor](/docs/metrics/metric-rules-editor)**. A page in the Sumo Logic web app for creating metric rules.

**[Metric rules](/docs/metrics/metric-rules-editor)**. A Sumo Logic feature that allows you to tag metrics with data derived from the metric identifier. Then, you can use those tags in metric queries.

**[Metric throttling](/docs/metrics/manage-metric-volume/metric-throttling)**. A Sumo Logic feature that throttles your metric sources when you exceed your DPM burst limit. Your ingestion is slowed down until the rate of ingestion is within the allowable contracted limits.

**[Metrics Transformation Rules](/docs/metrics/metrics-transformation-rules)**. Metrics transformation rules allow you control how long raw metrics are retained. You can also aggregate metrics at collection time and specify a separate retention period for the aggregated metrics.

**[Metric volume index](/docs/manage/ingestion-volume/data-volume-index/metrics-data-volume-index)**. A Sumo Logic index to which Sumo Logic writes messages with information about the volume of metrics you are ingesting.

<!--
**[Microservices](/docs/integrations/app-development)**. The microservices architecture enables you to structure applications as collections of loosely coupled services that are fine-grained, with protocols that are lightweight. Building applications using different smaller services improves modularity and provides for the continuous delivery and deployment of large, complex applications.
-->

**[Multiline](/docs/send-data/reference-information/collect-multiline-logs)**. Log messages that span multiple lines are called multiline messages.


## O

**[Organization](/docs/manage/manage-subscription/create-and-manage-orgs/manage-org-settings)**. In Sumo Logic, org, or organization, refers to your company’s Sumo Logic account (not an individual user’s account).

**Outlier**. Outliers are log data or metric values in a sequence that seem unexpected, and might indicate an operational or performance issue. In Sumo Logic, you can use the [outlier operator](/docs/search/search-query-language/search-operators/outlier) to identify outliers in log data. In addition, Sumo Logic has a [metrics outlier](/docs/metrics/metrics-operators/outlier/) operator that identifies metric data points that are outside the range of expected values.




## P

**[Panel](/docs/dashboards/panels)**. Formerly Monitors. Real-time Panels provide a graphical representation of your organization's data. Data Panels are created by running search queries. From the resulting data in the Search page's Aggregates tab, you can display that data using different types of charts. Once Panels are created, they are saved to a Dashboard.

**[Parse operator](/docs/search/search-query-language/parse-operators/parse-predictable-patterns-using-an-anchor)**. The parse operator (also called the parse anchor) parses strings according to specified start and stop anchors, and then labels them as fields for use in subsequent functions in the query such as sorting, grouping, or other functions. Parse options include "parse anchor" or "parse regex" for using regular expressions to form more complex parse queries. It is acceptable to use "parse" for "parse anchor", or "extract" for "parse regex".

**[Parser](/docs/cse/schema/parser-editor)**. In Cloud SIEM, a script that parses logs and normalizes them into structured records.

**[Partition](/docs/manage/partitions)**. Sumo Logic allows you to filter a subset of the messages in an Index into a Partition. Partitioning messages in an Index improves search query performance, as the total number of messages that need to be searched is reduced. Once messages are routed to a Partition, you can limit your search to those messages using the Partition name in a search query.

**[Pinned searches](/docs/get-started/library)**. The Pinned Search feature allows you to start a search, then “pin” it, so it will continue running in the background independent of the browser session. Then, you can close the Search tab or log out and find your results later in the Library on the Recent tab in a folder named Pinned Searches.

**[Processing rules](/docs/send-data/collection/processing-rules)**. A Sumo Logic feature you can use to filter or forward log data ingested by Sumo Logic from a Sumo Logic source. You can use processing rules to include or exclude messages, and to mask or hash sensitive information in logs. You can also forward matching messages to external destinations, including AWS S3.

**[Prometheus](/docs/send-data/collect-from-other-data-sources/collect-prometheus-metrics/)**. A metric format in which a time series is uniquely identified by its metric name and a set of labels in key-value pairs format. Sumo’s [HTTP source](/docs/send-data/hosted-collectors/http-source) and [Streaming Metric source](/docs/send-data/installed-collectors/sources/streaming-metrics-source) support Prometheus metrics. Sumo’s [Kubernetes solution](/docs/observability/kubernetes) also collects Prometheus metrics.


## Q

**[quantization](/docs/metrics/introduction/metric-quantization)**. The process by which Sumo Logic aggregates raw metric data points over a particular time bucket. Similar to “timeslice” in logs, Sumo Logic will automatically bucket your datapoints into quantization intervals based on the timerange of your search. For example, 5 second quantization intervals for a 15-minute search and 15 seconds for a 60-minute search.

**[quantize operator](/docs/metrics/metrics-operators/quantize/)**. An operator you can use is metric queries to specify the size of the time buckets over which Sumo Logic will aggregate metrics, and the aggregation method Sumo Logic will use to quantize the data.




## R

**[Receipt Time](/docs/search/get-started-with-search/build-search/use-receipt-time)**. You can display search results in the order that the Collector received the messages in milliseconds.

**[RBAC](/docs/manage/users-roles/roles/role-based-access-control/)**. Sumo Logic supports Role-Based Access Control (RBAC) to allow Administrators to customize system access. With RBAC, Administrators create roles for groups of users who perform various job functions. Users are not assigned permissions directly, but inherit permissions through roles (or even through a single role). Role assignments can grant users permissions to access some data sets, or can restrict users from accessing types of data.

**[Record](/docs/cse/records-signals-entities-insights/view-records-signal)**. In Cloud SIEM, a collection of normalized data created from a message.

**[Relative expressions](/docs/search/get-started-with-search/search-basics/time-range-expressions)**. Used in time range expressions, when setting the non-absolute time limits of a search. For example, -1d, -1d -12h, -12h -60m.

**[Role](/docs/manage/users-roles/roles/)**. In Sumo Logic role-based access control (RBAC), you grant users access to data and to Sumo Logic functions using roles. You assign role capabilities and a role search filter to a role, and assign one or more roles to a user.

**[Role search filter](/docs/manage/users-roles/roles/construct-search-filter-for-role)**. A search filter for a role defines what log data a user with that role can access. You can define a search filter using keywords, wildcards, and selected Sumo Logic metadata fields and logical operators.

**[Rollup tables](/docs/metrics/manage-metric-volume/metric-ingestion-and-storage)**. Metric data is stored in Sumo Logic as raw data points, and aggregated over one minute and one hour resolutions. The one minute and one hour aggregated metrics are referred to as rollup tables. Raw data is retained for 7 days, one-minute rollups for 30 days and one-hour rollups for 13 months.

**[Rule](/docs/cse/rules/about-cse-rules)**. In Cloud SIEM, set of logic that creates signals based on information in incoming records.



## S

**[SAML](/docs/manage/security/saml)**. Sumo Logic supports self-provisioning of Security Assertion Markup Language (SAML) to enable Single Sign-On (SSO). In addition to basic SAML configuration, you can choose optional on-demand user creation (via SAML 2.0 assertions), and designate custom log in and/or log out portals.

**[Scheduled Search](/docs/alerts/scheduled-searches/schedule-search)**. When you save a log search, you can schedule it to run it on a periodic basis, and configure an alert that will issue a notification every time the search runs, or when a condition you specify is met.

**[Scheduled View](/docs/manage/scheduled-views)**. A Scheduled View is a pre-aggregated index of a subset of data. After building a Scheduled View, you'll be able to run queries against that data set. Because the data is pre-aggregated, meaning that query you'll use to create a Scheduled View contains an aggregate function, search results return much quicker. Additionally, queries run against a Scheduled View cannot time out. Queries that run against Views can be used in scheduled searches, Dashboards, and in ad hoc searches.

**[Search Autocomplete](/docs/search/get-started-with-search/search-basics/search-autocomplete)**. See Autocomplete.

**[Search Templates](/docs/search/get-started-with-search/build-search/search-templates)**. Search templates simplify searches for users by providing easy to select input choices. You can have search templates replace any text in a query, including fields, keywords, and arguments to operators.

**[Service Allowlist Settings](/docs/manage/security/create-allowlist-ip-cidr-addresses)**. Service Allowlist Settings allow you to explicitly grant access to specific IP addresses and/or CIDR notations.

**[Signal](/docs/cse/records-signals-entities-insights/view-records-signal)**. In Cloud SIEM, an indicator of an event of interest that fires when rule conditions are met.

**[Single Value Chart](/docs/dashboards/panels/single-value-charts)**. A Single Value chart is useful for displaying the results of a query that returns only a single value or record, in order to make that value stand out at a glance. If the query returns more than one value in the Aggregation tab, only the first value is displayed in the Single Value chart.

**[Sources](/docs/send-data)**. Sources are configured on Sumo Logic Collectors and collect customer data.

**[Subqueries](/docs/search/subqueries)**. Subqueries allow you to filter and evaluate conditions for a log query when you may not be sure of the exact filter or condition criteria but you can write a short query to set them for you. Subqueries use one query to pass results back to another query to narrow down or evaluate the set of messages that are searched in that query.

**[Support Account](/docs/manage/security/enable-support-account)**. A support account is a special Sumo Logic user account that you can enable so that Sumo Logic support personnel can access your Sumo Logic org. Typically, you enable your support account for a limited period of time, just long enough to allow Sumo Logic support to diagnose a problem or answer a question.




## T

**[Text Panel](/docs/dashboards/panels/#text-panel)**. Used in Dashboards, you can add Text Panels to include titles or text descriptions. See also Markdown.

**[Throttling](/docs/manage/ingestion-volume/log-ingestion)**. Slows the rate of ingestion across all Collectors in an account to not exceed the allowable rate.

**[Time Compare](/docs/search/time-compare)**. Time Compare uses the compare operator to compare current aggregated search results with aggregated data from a past time period.

**[Time series](/docs/dashboards/panels#time-series-panel)**. A set of timestamped values of a specific measurement.

**[Timeslice operator](/docs/search/search-query-language/search-operators/timeslice)**. Timeslice segregates search results by a time period, or by a number of buckets over a search's time range.

**[Transaction operator](/docs/search/search-query-language/transaction-analytics/transaction-operator)**. Groups logs in a sequence by referencing a unique identifier in your logs and parsing out meaningful states of the transaction. Results can be returned by the transactions themselves, states, or flow (latency). A flow chart is available when returned by flow.

**[Transactionize operator](/docs/search/search-query-language/transaction-analytics/transactionize-operator)**. Groups logs that match on any fields you specify. Unlike other **group by** operators, where the logs in a group must match on all defined fields, transactionize just needs one field to match in order to assign logs to the same group.


## U

**[user.properties](/docs/send-data/installed-collectors/collector-installation-reference/user-properties)**. The user.properties file is used to pass Collector parameters for some installation methods.


## W


**[`where` operator](/docs/search/search-query-language/search-operators/where)**. A conditional operator that can precede or follow another operator. Example combinations include "where x matches y", "where x in (a, b, c)", "where x not in (a, b, c)" and "where a > 1 and b / 4 &lt; sqrt(x)".
