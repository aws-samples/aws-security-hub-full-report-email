## How to Setup a Recurring AWS Security Hub CSV Full Report with email notification
This solution uses AWS Security Hub API, AWS Lambda, Amazon S3, and Amazon SNS. List of findings are aggregated into csv file, to help identify common security issues that may require remediation action. 

### Overview
Security Hub includes various security standards and integrations that you can enable to understand your overall security state. A recurring Security Hub CSV full report with email notification that provides recipients with a proactive communication summarizing the security posture and improvement within AWS Accounts.

This solution assumes that Security Hub is enabled in your AWS account. If it isn’t enabled, set up the service so that you can start seeing a comprehensive view of security findings across your AWS accounts.

## How the solution works
1.	An EventBridge time-based event invokes a Lambda function for processing.
2.	The Lambda function gets finding results from Security Hub API and writes them into a CSV file.
3.  It uploads them as CSV into Amazon S3 and generates a pre authenticated link.
4.	SNS sends the email notification to the address provided during deployment.
5.	The email includes a link to download the file.

## Fields are included in the report
1.	Finding id
2.	ProductArn 
3.	ProductName
4.	CompanyName 
5.	GeneratorId 
6.	SecurityControlId
7.	CreatedAt
8.	UpdatedAt
9.	Confidence
10. RemediationText
11. RemediationUrl
12. SourceUrl
13. Compliance Status
14. WorkflowStatus
15. RecordState 
16. Processed_at
17. Finding title
18. Finding description 
19. Severity
20. Region
21. AccountId
22. ResourceType
23. ResourceId
24. ResourceTags

**Note:** That report can be extended with additional field as needed, by modifying the Lambda function.

## Deployment Steps
1. Download the CloudFormation template **security-hub-email-summary-cf-template.json** 
2. On AWS account console, open the service **CloudFormation**.
3. Click on **Create Stack** with new resources. Select **Template is ready** and then **Upload a template file**.
4. Using **Choose file**, select the security-hub-full-report-email.json file which you downloaded in step 1.
5. Click on **Next**. On next page, enter a name for the stack.
6. On the same page, enter values for the input **parameters**.
7. Click **Next**.
8. Accept all defaults in screens that follow and create the stack. Click **Next**.
9. **Check** I acknowledge that AWS CloudFormation might create IAM resources. Click **Create Stack**.

## Test Solution
You can send a test email once the deployment is complete and you have confirmed the SNS subscription email.  Navigate to the Lambda console and locate the function Lambda function named SendSecurityHubFullReportEmail. Perform a [manual invocation](https://docs.aws.amazon.com/lambda/latest/dg/getting-started-create-function.html#get-started-invoke-manually) with any event payload to receive an email shortly. 

## Security

See [CONTRIBUTING](CONTRIBUTING.md#security-issue-notifications) for more information.

## License

This library is licensed under the MIT-0 License. See the LICENSE file.

