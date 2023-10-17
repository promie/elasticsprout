# ElasticSprout

ElasticSprout is a robust automation tool tailored for AWS Elastic Beanstalk deployments. It harnesses the power of AWS's managed service, utilising the AWS SDK version 3, to simplify and optimize the deployment, management, and scaling of applications in the AWS cloud environment. Whether you're launching a straightforward web application or orchestrating an intricate enterprise-level system, ElasticSprout guarantees a smooth and proficient deployment workflow.

## Key Features:
- **Automated Deployments**: Experience hassle-free deployment with intuitive one-click solutions that eradicate manual tasks.
- **Version Management**: Efficiently manage, and effortlessly switch between, different versions of your application hosted on Elastic Beanstalk.
- **Environment Configuration**:  Define and instantly apply configurations to your Elastic Beanstalk environments without a hitch.
- **Leverage AWS SDK v3**: Built upon the modern AWS SDK version 3, ElasticSprout ensures optimal compatibility, enhanced performance, and streamlined API interactions with AWS services.

Elevating the capabilities of the original Ruby Beanstalkify, the Node TypeScript implementation of ElasticSprout delivers enhanced performance, type safety, and a superior developer experience. By leveraging the resilience of TypeScript coupled with the versatility of the Node ecosystem, ElasticSprout sets the gold standard for AWS Elastic Beanstalk automation.

## Prerequisites
- **Node.js**: Requires Node.js version 18 or higher. Make sure to have the appropriate version installed before using ElasticSprout.
```bash
node --version
```
- **ts-node**: Necessary for running the acceptance tests. Ensure you have ts-node installed globally or as a development dependency.
```bash
npm install -g ts-node
```
OR
```bash
npm install ts-node --save-dev
```

## Install
```bash
npm install elasticsprout
```

## Usage

```typescript
import ElasticSprout from 'elasticsprout';

const sprout = new ElasticSprout({
  credentials: {
    accessKeyId: 'YOUR_ACCESS_KEY',
    secretAccessKey: 'YOUR_SECRET_KEY'
  },
  region: 'ap-southeast-2'
});

// Deploy configuration
const deployConfig = {
  archiveFilePath: 'PATH_TO_YOUR_ZIP_FILE',
  environmentName: 'YOUR_ENVIRONMENT_NAME',
  awsStackName: '64bit Amazon Linux 2023 v6.0.1 running Node.js 18',
  tags: [
    {
      Key: 'YOUR_TAG_KEY',
      Value: 'YOUR_TAG_VALUE'
    },
    // ... additional tags as needed
  ]
};

// Deploy using async/await
async function deployApp() {
  try {
    const data = await sprout.deploy(deployConfig);
    /*
    Outputs:
    {
      appName: 'test-website',
      appVersion: 'foo',
      envName: 'test-website-prod',
      envUrl: 'tech-website-12345.ap-southeast-2.elasticbeanstalk.com'
    }
    */
    console.log(data);
  } catch (error) {
    console.error('Error during deployment:', error);
  }
}

deployApp();
```

## Unit test

```bash
npm run test
```

## Acceptance test
- Create `credentials.json` within folder `acceptance`
```JSON
{
  "credentials": {
    "accessKeyId": "XXX",
    "secretAccessKey": "XXX"
  },
  "region": "ap-southeast-2"
}

```
- Run `ts-node acceptance/index.ts`
- It should create automatically two random elasticbeanstalk environments
