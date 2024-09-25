![Alt Text](https://github.com/lann87/cloud_infra_eng_ntu_coursework_alanp/blob/main/.misc/ntu_logo.png)  

# AWS CDK Deployment Process  

This README documents the basic AWS CDK deployment process, showing each step with screenshots of the CLI and AWS console. Follow along to learn how to use CDK for cloud infrastructure deployment.  

## Prerequisites  

Ensure you have the following installed before proceeding:  

- [AWS CLI](https://aws.amazon.com/cli/)  
- [Node.js](https://nodejs.org/)  
- [AWS CDK](https://docs.aws.amazon.com/cdk/latest/guide/home.html)  

Install the AWS CDK globally if you haven't:  

```sh
npm install -g aws-cdk  
```

## Step 1: Initialize the CDK Project

First, create a directory for your project and initialize CDK:

```sh
mkdir <name>-cdk
cd <name>-cdk
cdk init app --language typescript
npm run build
```

![Alt Text](https://github.com/lann87/11sep-cdk/blob/main/11sep-cdk-init-cli.png)

This will set up the necessary files and folders for your CDK project.

## Step 2: Bootstrapping the AWS Environment

Run the following command to bootstrap your AWS environment. This is necessary to provision the infrastructure required for deployment.

![Alt Text](https://github.com/lann87/11sep-cdk/blob/main/11sep-cdk-deploy1-cli.png)

## Step 3: Writing the CDK Stack  

Edit the lib/my-cdk-app-stack.ts file to define your infrastructure. Here's an example that provisions an S3 bucket:

typescript

```ts
import * as cdk from 'aws-cdk-lib';
import {aws_s3 as s3} from 'aws-cdk-lib';
// import * as sqs from  'aws-cdk-lib/aws-sqs';

export class MyCdkAppStack extends cdk.Stack {
  constructor(scope: Construct, id: string, props?: cdk.StackProps) {
    super(scope, id, props);

    // The code that defines your stack goes here
    new s3.Bucket(this, 'MyFirstBucket', {
      versioned: true
    })

    //  example resources
    //  const queue = new sqs.Queue(this, 'HelloCdkQueue', {
    //      visibilityTimeout: cdk.Duration.seconds(300)
    //  });
  }
}
```

## Step 4: Deploying the Stack & Modifying

To deploy your CDK stack, run the following command:

```bash
cdk deploy
```

You’ll be asked to confirm resource creation. Type yes to proceed.  

![Alt Text](https://github.com/lann87/11sep-cdk/blob/main/11sep-cdk-deploy2-cli.png)

![Alt Text](https://github.com/lann87/11sep-cdk/blob/main/11sep-cdk-deploy3-cli.png)

Once completed, the resources will be created in your AWS account.  

## Step 5: View Resources in AWS Console  

Navigate to the AWS Console and check the deployed resources (e.g., S3 bucket). You should see the bucket created by the CDK stack.  

![Alt Text](https://github.com/lann87/11sep-cdk/blob/main/11sep-cdk-console.png)

## Step 6: Destroying the Stack  

When you're done and want to clean up the resources, run the following command:  

```bash
cdk destroy
```

Confirm with yes to delete all resources.  

![Alt Text](https://github.com/lann87/11sep-cdk/blob/main/11sep-cdk-destroy-cli.png)

## Conclusion

This document demonstrates a simple CDK deployment process, from project initialization to cleaning up resources. For more complex use cases and customization, explore the [AWS CDK Documentation](https://docs.aws.amazon.com/cdk/v2/guide/home.html).
