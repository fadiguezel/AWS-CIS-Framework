# CIS AWS Foundation Framework

Caution, this benchmark is still in development and has some minor bugs. The Readme could use some improvements too, I already know ;)

## CIS AWS Foundation Benchmark++ in the AWS Cloud

The CIS AWS Foundation Framework is a collection of CloudFormation templates for assesing and monitoring the security of you AWS account. The framework is built upon the [AWS CIS Compliance Quick Start](https://github.com/aws-quickstart/quickstart-compliance-cis-benchmark) which deploys and configures a standardized architecture for the Center for Internet Security (CIS) AWS Foundations Benchmark.

The CIS Benchmarks are guidelines for best practices developed and maintained by a handful of experts. It's a good starting point for assessing the security of your infrastructure and hardening it. But the benchmark is definitely not the single point of truth. Depending on the company some controls may be obsolete or not applicable. For other companies the exisitng CIS controls may not be sufficient and additional checks need to be implemented. The AWS CIS Compliance Quick Start provides a great way to rollout the benchmark for an account, but it lacks the possibility to modify or extend the CIS controls.

## Additional Feautures

- Modularization - the cis-benchmark template was splitted up into 4 different modules, each representing a section of the CIS Foundation Benchmark.
- Add exceptions to rules when necessary.
- Remediation - planned

## Deployment

To deploy the application create a s3 bucket, set the right ACLs and upload the templates using following snippet:

### Create bucket
```bash
aws s3 mb s3://#{bucket_name} --region eu-central-1
```

### Put policy on bucket
Substitute the placeholder in the policy with the name of your bucket. Afterwards run
```bash
aws s3api put-bucket-policy --bucket #{bucket_name} --policy file://#{path_to_policy}
```

### Upload tempalate files to s3 bucket
```bash
aws s3 cp #{path-to-repo}/templates s3://#{bucket_name}/#{prefix}/templates --recursive
```

### Create the stack

Go to `https://#{region}.console.aws.amazon.com/cloudformation/home` and click on the `Create Stack` button. Choose `Specify an Amazon S3 template URL` and add the link to the `main.template` from the s3 bucket.
