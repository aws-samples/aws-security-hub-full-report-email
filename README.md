## How to Setup a Recurring AWS Security Hub Full Report Email
This solution uses AWS Security Hub API, AWS Lambda, Amazon S3, and Amazon SNS. List of findings are aggregated into csv file, to help identify common security issues that may require remediation action. 

### Overview
Security Hub includes various security standards and integrations that you can enable to understand your overall security state. A recurring Security Hub Full Report email will provide recipients with a proactive communication summarizing the security posture and improvement within AWS Accounts.

## How the solution works
1.	An EventBridge time-based event invokes a Lambda function for processing.
2.	The Lambda function gets finding results from Security Hub API and writes them into a CSV files
3. It uploads them as CSV into Amazon S3 and generates a pre authenticated link.
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
14. WorkflowState 
15. WorkflowStatus
16. RecordState 
17. Processed_at
18. Finding title
19. Finding description 
20. Severity
21. Region
22. AccountId
23. ResourceType
24. ResourceId

**Note:** That report can be extended with additional field as needed, by modifying the Lambda function.

## Deployment Steps
1.	Download the CloudFormation template **security-hub-email-summary-cf-template.json** 
2. Copy security-hub-full-report-email.json **to an S3 bucket within your target AWS account** and region. Copy the object URL for the CloudFormation template.
3. On AWS account console, open the service **CloudFormation**. Click on **Create Stack** with new resources.
4.	Enter the S3 Object URL for the security-hub-full-report-email.json which you uploaded in step 1 in the text box for Amazon S3 URL under Specify template.
5.	Click on **Next**. On next page, enter a name for the stack.
6.	On the same page, enter values for the input **parameters**.
7.	Click **Next**.
8.	Accept all defaults in screens that follow and create the stack. Click **Next**.
9.	**Check** I acknowledge that AWS CloudFormation might create IAM resources. Click **Create Stack**.

## Test Solution
You can send a test email once the deployment is complete and you have confirmed the SNS subscription email.  Navigate to the Lambda console and locate the function Lambda function named SendSecurityHubFullReportEmail. Perform a [manual invocation](https://docs.aws.amazon.com/lambda/latest/dg/getting-started-create-function.html#get-started-invoke-manually) with any event payload to receive an email shortly. 

## Security

See [CONTRIBUTING](CONTRIBUTING.md#security-issue-notifications) for more information.

## License

This library is licensed under the MIT-0 License. See the LICENSE file.

