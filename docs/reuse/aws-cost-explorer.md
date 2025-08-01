To configure an AWS Cost Explorer Source:

1. [**Classic UI**](/docs/get-started/sumo-logic-ui-classic). In the main Sumo Logic menu, select **Manage Data > Collection > Collection**. <br/>[**New UI**](/docs/get-started/sumo-logic-ui). In the Sumo Logic top menu select **Configuration**, and then under **Data Collection** select **Collection**. You can also click the **Go To...** menu at the top of the screen and select **Collection**. 
1. On the Collection page, click **Add Source** next to a Hosted Collector.
1. Search for and select **AWS Cost Explorer**.<br/>  <img src="/img/send-data/aws-cost-explorer-icon.png" alt="aws-cost-explorer-icon" width="10%" />
1. Enter a **Name** for the Source in the Sumo Logic console. The **Description** is optional.<br/>  <img src="/img/integrations/amazon-aws/cost-explorer-v2-1-1.png" alt="cost-explorer-v2-1-1.png" width="400" />
1. (Optional) For **Source Category**, enter any string to tag the output collected from the Source. Category [metadata](/docs/search/get-started-with-search/search-basics/built-in-metadata) is stored in a searchable field called `_sourceCategory`.
1. For [Fields](/docs/manage/fields), click the **+Add** link to add custom log metadata. Define the fields you want to associate. Each field needs a name (key) and value.
   * <img src="/img/reuse/green-check-circle.png" alt="green check circle.png" width="20"/> A green circle with a check mark is shown when the field exists and is enabled in the Fields table schema.
   * <img src="/img/reuse/orange-exclamation-point.png" alt="orange exclamation point.png" width="20"/> An orange triangle with an exclamation point is shown when the field doesn't exist, or is disabled in the Fields table schema. In this case, you'll see an option to automatically add or enable the nonexistent fields to the Fields table schema. If a field is sent to Sumo Logic but isn’t present or enabled in the schema, it’s ignored and marked as **Dropped**.<br/><br/>It is preferable to add an **account** field (for the dashboards) and assign it a friendly name to identify the corresponding AWS account.<br/> ![accountField.png](/img/send-data/accountField.png)
1. For the **AWS Access Key** and **AWS Secret Key**, provide the IAM User access key and secret key you want to use to authenticate collection requests. Make sure your IAM user has the following IAM policy attached with it.
   ```json
   {
       "Version": "2012-10-17",
       "Statement": [
           {
               "Sid": "VisualEditor0",
               "Effect": "Allow",
               "Action": [
                   "ce:Describe*",
                   "ce:Get*",
                   "ce:List*",
                   "ec2:DescribeRegions"
               ],
               "Resource": "*"
           }
       ]
   }
   ```
1. (Optional) For the **Enable Regions** field, provide the regions which need to be monitored for cost. The cost incurred across these regions will be fetched separately. The region list here includes all the standard AWS regions along with “global”. “Global” region includes services like Amazon CloudFront, Amazon Route 53, and Amazon IAM. If the field is left empty (default behavior), then data will be fetched from all the enabled regions of the respective AWS account. It is recommended to provide only the regions which are actively used and need to be monitored for cost. This will save the AWS cost for running this source on unused regions.
1. For the **Cost Type**, provide supported cost types / MetricTypes. For details on the CostType, see Amazon's [Understanding your AWS Cost Datasets: A Cheat Sheet](https://aws.amazon.com/blogs/aws-cloud-financial-management/understanding-your-aws-cost-datasets-a-cheat-sheet/).
    * AmortizedCost
    * BlendedCost
    * NetAmortizedCost
    * NetUnblendedCost
    * UnblendedCost
1. For **Granularity**, provide 2 supported granularities for each of the MetricTypes (or cost types):
    * Daily Costs (Polled every 12h)
    * Monthly Costs (Polled every day)
1. Add **[Processing Rules](/docs/send-data/collection/processing-rules)**.
1. Click **Submit** when complete.
