## AWS Lambda Usage

NOTE: Using Lambda may incur costs in your AWS account. Please make sure you have checked
the pricing for AWS Lambda and CloudWatch before continuing.

Running ssosync once means that any changes to your Google directory will not appear in
AWS SSO. To sync. regularly, you can run ssosync via AWS Lambda.

:warning: You find it in the [AWS Serverless Application Repository](https://eu-west-1.console.aws.amazon.com/lambda/home#/create/app?applicationId=arn:aws:serverlessrepo:us-east-2:004480582608:applications/SSOSync).

## SAM

You can use the AWS Serverless Application Model (SAM) to deploy this to your account.

> Please, install the [AWS SAM CLI](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-sam-cli-install.html) and [GoReleaser](https://goreleaser.com/install/).

Specify an Amazon S3 Bucket for the upload with `export S3_BUCKET=<YOUR_BUCKET>`.

Execute `make package` in the console. Which will package and upload the function to the bucket. You can then use the `packaged.yaml` to configure and deploy the stack in [AWS CloudFormation Console](https://console.aws.amazon.com/cloudformation).

### Example

Build

```bash
aws cloudformation validate-template --template-body  file://template.yaml 1>/dev/null &&
sam validate &&
sam build && make go-build
```

Deploy

```bash
cp ./ssysonc .aws-sam/build/SSOSyncFunction/dist/ssosync_linux_amd64_v1/ssosync
sam deploy --guided
```

## License

[Apache-2.0](/LICENSE)
