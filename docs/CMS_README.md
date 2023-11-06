# Connected Mobility Solution on AWS

**[Connected Mobility Solution on AWS](https://aws.amazon.com/solutions/implementations/connected-mobility-solution-on-aws/)** | **[🚧 Feature request](https://github.com/aws-solutions/connected-mobility-solution-on-aws/issues/new?assignees=&labels=enhancement&template=feature_request.md&title=)** | **[🐛 Bug Report](https://github.com/aws-solutions/connected-mobility-solution-on-aws/issues/new?assignees=&labels=bug&template=bug_report.md&title=)** | **[❓ General Question](https://github.com/aws-solutions/connected-mobility-solution-on-aws/issues/new?assignees=&labels=question&template=general_question.md&title=)**

**Note**: If you want to use the solution without building from source, navigate to the [AWS Solution Page](https://solution-page.com).

<font size="5"> **If you want to jump straight into building and deploying, [click here](#build-and-deploy-the-solution)**</font>

## Table of Contents
- [Connected Mobility Solution on AWS](#connected-mobility-solution-on-aws)
  - [Table of Contents](#table-of-contents)
  - [Solution Overview](#solution-overview)
  - [Architecture Diagrams](#architecture-diagrams)
    - [Solution Architecture Diagram](#solution-architecture-diagram)
    - [ACDP Architecture Diagram](#acdp-architecture-diagram)
    - [CMS Backstage Architecture Diagram](#cms-backstage-architecture-diagram)
    - [ACDP Deployment Sequence Diagram](#acdp-deployment-sequence-diagram)
    - [Module Deployment Sequence Diagram](#module-deployment-sequence-diagram)
  - [CMS Modules](#cms-modules)
    - [Environment](#environment)
  - [Build and Deploy the Solution](#build-and-deploy-the-solution)
    - [Prerequisites](#prerequisites)
    - [Required Software Dependency Versions](#required-software-dependency-versions)
    - [Clone the Repository](#clone-the-repository)
    - [Developer Environment Dependency Installations (OSX)](#developer-environment-dependency-installations-osx)
      - [Developer Environment Dependency Verifications](#developer-environment-dependency-verifications)
    - [Developer Environment Dependency Installations - Continued](#developer-environment-dependency-installations---continued)
      - [Developer Environment Dependency Verifications - Continued](#developer-environment-dependency-verifications---continued)
    - [Solution Dependency Installation](#solution-dependency-installation)
  - [Deployment Pre-Requisites](#deployment-pre-requisites)
  - [Deploy](#deploy)
    - [Create a .env file or set environment variables in the shell](#create-a-env-file-or-set-environment-variables-in-the-shell)
      - [Create .env file (preferred option)](#create-env-file-preferred-option)
      - [Set environment variables (secondary option)](#set-environment-variables-secondary-option)
    - [Verify CDK Context](#verify-cdk-context)
    - [Run CDK Bootstrap](#run-cdk-bootstrap)
    - [Upload S3 Deployment Assets (Backstage `template.yaml`s and AWS Proton service template `.tar`s)](#upload-s3-deployment-assets-backstage-templateyamls-and-aws-proton-service-template-tars)
    - [Deploy the Automotive Cloud Developer Portal](#deploy-the-automotive-cloud-developer-portal)
    - [Monitoring the Automotive Cloud Developer Portal Deployment](#monitoring-the-automotive-cloud-developer-portal-deployment)
    - [Bootstrap Proton](#bootstrap-proton)
    - [Deploy CMS Modules via Backstage](#deploy-cms-modules-via-backstage)
      - [CMS Module Deployment Order](#cms-module-deployment-order)
        - [Deployment Order of Modules with Dependencies](#deployment-order-of-modules-with-dependencies)
        - [Modules Without Dependencies](#modules-without-dependencies)
      - [Example Module Deployment via Backstage](#example-module-deployment-via-backstage)
  - [Cost scaling](#cost-scaling)
  - [Collection of Operational Metrics](#collection-of-operational-metrics)
  - [Building Open-Source Distributable](#building-open-source-distributable)
  - [Teardown](#teardown)
  - [Developer Guide](#developer-guide)
    - [Pre-Commit Hooks](#pre-commit-hooks)
    - [Unit Test](#unit-test)
  - [License](#license)

## Solution Overview

The Connected Mobility Solution on AWS (CMS) provides the automotive
industry customers the capability to connect vehicle, track location,
detect non-nominal behavior, predict & schedule maintenance (including
ordering parts), predict EV battery health, send notifications, control
vehicle functions remotely, personalize vehicle, visualize data, monetize
data, and integrate with external call centers for assistance calls.

For more information and a detailed deployment guide, visit the
[Connected Mobility Solution on AWS](https://aws.amazon.com/solutions/implementations/connected-mobility-solution-on-aws/)
solution page.

## Architecture Diagrams

### Solution Architecture Diagram
![Solution Architecture Diagram](./architecture/diagrams/cms-all-modules-architecture-diagram.svg)

### ACDP Architecture Diagram

![ACDP Architecture Diagram](./architecture/diagrams/cms-acdp-architecture-diagram.svg)

### CMS Backstage Architecture Diagram

![CMS Backstage Architecture Diagram](./architecture/diagrams/cms-backstage-architecture-diagram.svg)

### ACDP Deployment Sequence Diagram

![ACDP Deployment Sequence Diagram](./sequence/cms-acdp-deployment-sequence-diagram.svg)

### Module Deployment Sequence Diagram
![Module Deployment Sequence Diagram](./sequence/cms-module-deployment-sequence-diagram.svg)

## CMS Modules

For detailed information visit the module's README

- [Alerts](./templates/modules/cms_alerts_on_aws/v1/instance_infrastructure/README.md)
- [API](./templates/modules/cms_api_on_aws/v1/instance_infrastructure/README.md)
- [Connect & Store](./templates/modules/cms_connect_store_on_aws/v1/instance_infrastructure/README.md)
- [EV Battery Health](./templates/modules/cms_ev_battery_health_on_aws/v1/instance_infrastructure/README.md)
- [Provisioning](./templates/modules/cms_provisioning_on_aws/v1/instance_infrastructure/README.md)
- [Authentication](./templates/modules/cms_user_authentication_on_aws/v1/instance_infrastructure/README.md)
- [Vehicle Simulator](./templates/modules/cms_vehicle_simulator_on_aws/v1/instance_infrastructure/README.md)

### Environment

For reference, there is a proton environment setup with further
details in its [README](./templates/environments/cms_environment/v1/infrastructure/README.md).

## Build and Deploy the Solution

### Prerequisites

- [NVM](https://github.com/nvm-sh/nvm)
- [Pyenv](https://github.com/pyenv/pyenv)
- [Pipenv](https://pipenv.pypa.io/en/latest/installation/)

### Required Software Dependency Versions

| Dependency | Version  |
|------------|----------|
| [NPM](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm)      | 9.6.7       |
| [NodeJS](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm)   | 18.17.1      |
| [Python](https://www.python.org)                                              | 3.10.9     |

### Clone the Repository

```bash
git clone https://github.com/aws-solutions/connected-mobility-solution-on-aws.git
cd connected-mobility-solution-on-aws
```

### Developer Environment Dependency Installations (OSX)

```bash
brew install pyenv
pip install pipenv --user
brew install nvm
```

#### Developer Environment Dependency Verifications

Before continuing, verify the required dependencies are useable.

```bash
pyenv --version
pipenv --version
nvm --version
```

### Developer Environment Dependency Installations - Continued

```bash
nvm install
nvm use
pyenv install -s
```

#### Developer Environment Dependency Verifications - Continued

Before continuing, verify the environment runtimes match the expected versions.
Refer to the [dependency table](#required-software-dependency-versions).

```bash
python --version
npm --version
node --version
```

### Solution Dependency Installation

Now that you have the correct developer environment dependencies, you can install the dependencies used by the solution using make. This may take a moment.

```bash
make install
source ./.venv/bin/activate
```

## Deployment Pre-Requisites

- A Route53 Hosted Zone in the deployment account.
- Necessary environment and solution dependencies installed. Refer to the [Prerequisites](###Prerequisites) section for details.
- Shell environment variables. Refer to the upcoming [set environment variables](#create-a-env-file-or-set-environment-variables-in-the-shell) section for details.

## Deploy

Refer to the [deployment diagram](#architecture-diagrams) for a detailed walk-through of what is deployed.

### Create a .env file or set environment variables in the shell

**NOTE: Refer to the Makefile to see what environment variables can be set as well as their defaults.**

- ROUTE53_BASE_DOMAIN is optional, if unset the base domain will be assumed to be the same as the ROUTE53_ZONE_NAME variable. This must be set to a superset of the ROUTE53_ZONE_NAME (*.${ROUTE53_ZONE_NAME})
- BACKSTAGE_TEMPLATE_S3_UPDATE_REFRESH_MINS: set this to something small such as `1 minute` for development,
otherwise it is recommended to have longer refresh intervals for cost savings.

#### Create .env file (preferred option)

NOTE: Do not use quotes around values in the .env file or else the make commands will fail

Use the following command to create a .env file

```bash
cat > .env <<EOL
USER_EMAIL=you@domain.com
ROUTE53_ZONE_NAME=domain.com
ROUTE53_BASE_DOMAIN=subdomain.domain.com
LOG_LEVEL=info
CMS_SOLUTION_VERSION=v0.0.0
BACKSTAGE_TEMPLATE_S3_UPDATE_REFRESH_MINS=30
BACKSTAGE_NAME=Default Name
BACKSTAGE_ORG=Default Name
EOL
```

#### Set environment variables (secondary option)

```bash
export USER_EMAIL="you@domain.com"
export ROUTE53_ZONE_NAME="domain.com"
export ROUTE53_BASE_DOMAIN="subdomain.domain.com"
export LOG_LEVEL="info"
export CMS_SOLUTION_VERSION="v0.0.0"
export BACKSTAGE_TEMPLATE_S3_UPDATE_REFRESH_MINS="30"
export BACKSTAGE_NAME="Default Name"
export BACKSTAGE_ORG="Default Org"
```

### Verify CDK Context

Prior to deploying, confirm that the expected deployment configuration has been picked up by the cdk context.

```bash
make cdk-context
```

### Run CDK Bootstrap

If the CDK has not been used in the region of the AWS account you are deploying to,
you must first bootstrap it in order for deployments to work.

```bash
make bootstrap
```

### Upload S3 Deployment Assets (Backstage `template.yaml`s and AWS Proton service template `.tar`s)

```bash
make upload-s3-deployment-assets
```

### Deploy the Automotive Cloud Developer Portal

```bash
make deploy
```

### Monitoring the Automotive Cloud Developer Portal Deployment

After the CDK deployment is completed, browse to [CodePipeline](https://console.aws.amazon.com/codesuite/codepipeline/pipelines)
in the AWS console and verify that the "Backstage-Pipeline" execution completes successfully.

![Successful CodePipeline Execution](./images/readme/deployment-codepipeline-success.png)

After the pipeline has completed, the deployment can be considered successfully complete and Backstage is ready for use.

> **NOTE:** It can take up to 10 minutes after the Backstage pipeline completes for Amazon Cognito's auth domain to become available for use with Backstage.

### Bootstrap Proton

> **NOTE:** The S3 location where deployment assets were uploaded to is in your AWS account, and should have a name of the format `<AWS_ACCOUNT>-cms-resources-<AWS_REGION>`

1. Sign in the [AWS Management Console](https://aws.amazon.com/console/), select your Region, and navigate to the [AWS Proton Service Templates](https://console.aws.amazon.com/proton/home/templates/services) page.
2. Select `Create service template` for each module template you wish to register.
  ![Proton Create Service Template](documentation/images/readme/proton-create-service-template.png)
3. Fill in the required fields (The following instructions detail how to register the CMS Vehicle Simulator Module template. The same steps can be applied to other modules as well by selecting the proper s3 path)
   1. Select the `Use your own template bundle in S3 Option`

      ![Proton S3 bundle option](documentation/images/readme/proton-s3-bundle.png)
   2. Select `Browse S3` and locate the bucket where the templates were uploaded.

      ![Proton Browse S3](documentation/images/readme/proton-browse-s3.png)

      ![Proton Choose Bucket](documentation/images/readme/proton-choose-bucket.png)
   3. Locate the latest tar for the vehicle_simulator module template (the Amazon S3 path should be of the format `../<SOLUTION_VERSION>/modules/<MODULE_NAME>/proton/`) Press the `Choose` button
      ![Proton Choose Template Object](documentation/images/readme/proton-choose-template-tar.png)
   4. In the repository, locate the [Vehicle Simulator Proton Template YAML](templates/modules/cms_vehicle_simulator_on_aws/template.yaml) and find the template name under the `metadataName` property. This will be under the `aws:proton:create-service` action. Use it to populate the `Service template name`
      ![Proton Find Template Name](documentation/images/readme/proton-module-template-name.png)
      ![Proton Enter Template Name](documentation/images/readme/proton-enter-template-name.png)
   5. Set the `Compatible environment templates` to `cms_environment`
      ![Proton Template Compatible Env Setting](documentation/images/readme/proton-template-compatible-env-setting.png)
   6. Leave the remaining settings as default and click `Create Service Template`.
   7. After you receive a message stating `Successfully created service template cms_vehicle_simulator_on_aws.`, then select template version `1.0` and click `Publish` to make it available for use by Backstage
      ![Proton Publish Template Version](documentation/images/readme/proton-publish-template-version.png)

### Deploy CMS Modules via Backstage

#### CMS Module Deployment Order

Some CMS on AWS modules have dependencies on other modules and must be deployed in order.
Others do not have dependencies on other modules and can be deployed in any order, as long as the ACDP has been deployed first.

The deployment order that must be observed is as follows:

##### Deployment Order of Modules with Dependencies

1. CMS Authentication
2. CMS Alerts
3. CMS Connect and Store
4. CMS API
5. CMS EV Battery Health

##### Modules Without Dependencies

- CMS Vehicle Provisioning
- CMS Vehicle Simulator

#### Example Module Deployment via Backstage

The following instructions detail how to deploy the CMS Vehicle Simulator Module.
The same steps can be applied to other modules as well by replacing the URLs and names.

1.	Navigate to the CMS Backstage URL in a web browser (ROUTE53_BASE_DOMAIN that was specified during deployment).
2.	Sign in to Backstage using the credentials that were emailed to the user-email specified during deployment.
3.	Follow the prompts to create a new password and set up multi-factor authentication (MFA).
4. On Backstage, navigate to the `Create` page available from the `Catalog` menu in the side bar. Select the `CHOOSE` button on the `CMS Vehicle Simulator on AWS` card.

  ![Vehicle Simulator Choose Card](./images/readme/backstage-choose-vehicle-sim-card.png)
5. Fill in the form as required by the Vehicle Simulator template and click the `Next Step` button.

  ![Vehicle Simulator Form Page 1](./images/readme/backstage-vehicle-simulator-form.png)
6. Click the `Create` button.
   ![Vehicle Simulator Form Confirmation](./images/readme/backstage-vehicle-simulator-form-confirm.png)
7. Monitor the deployment and ensure that the Vehicle Simulator module deploys successfully.

   ![Vehicle Simulator Deployment Successful](./images/readme/backstage-vehicle-simulator-deployment-success.png)

## Cost scaling

Refer to the implementation guide for pricing information.

## Collection of Operational Metrics

This solution collects anonymous operational metrics to help AWS improve
the quality and features of the solution. For more information, including
how to disable this capability, please see the
[implementation guide](https://docs.aws.amazon.com/solutions/latest/connected-mobility-solution-on-aws/operational-metrics.html).

## Building Open-Source Distributable

```bash
# Cleanup any files not needed for the build
./deployment/clean-for-deploy.sh
# Create open source build distribution
./deployment/build-open-source-dist.sh $SOLUTION_NAME
```

- Validate that the assets within the output folder are accurate and that there are no missing files.

## Teardown

This solution creates multiple CloudFormation deployments; both from the top level cdk deploy as well as additional stacks
from Proton and CodePipeline executions. Some resources cannot be torn down directly via the AWS Console or by using the AWS CLI.

The following commands assume the stage is `dev`, for other stages, replace `dev` with the appropriate value.

1. Capture and store the deployment UUID of the solution.

   - This is used to look for any resources not destroyed by CloudFormation after teardown completes

   ```bash
   make get-deployment-uuid
   ```

   output will be a uuidv4 string:

   ```bash
   XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX
   ```

2. Delete CMS on AWS Modules in AWS Proton and CloudFormation that were deployed via Backstage
   1. In AWS Proton, Navigate to the `Services` view and delete any service attached to the
   `cms-environment` Environment. Wait until all services successfully delete.

      > **NOTE:** You have to click the link into the service to be able to delete it via the `Actions` dropdown

   ![Delete CMS Module Proton Service](documentation/images/readme/delete-cms-module-proton-service.png)
      - If the delete fails in AWS Proton, and the CodeBuild `cdk destroy` task shows an error in the CodeBuild logs, most likely the module attempting
        to be deleted has a dependency blocking the deletion. Continue tearing down the rest of the modules and try again.
        Refer to the AWS Proton CodeBuild logs and CloudFormation console output for additional information.
      - If the delete fails in AWS Proton, but the CloudFormation stack for the module is deleted successfully,
      most likely AWS Proton needs an additional role for account level CodeBuild.
      You will observe the following error: `AccountSettings.pipelineCodeBuildRoleArn has not been configured.`
      In this case, go to `Account Settings` and configure a role.
         > **WARNING:** Proton's UI requires a GitHub Repository connection to configure roles.  To get around this, set the roles using a CLI command.

            ```bash
            aws proton update-account-settings \
            --pipeline-codebuild-role-arn arn:aws:iam::11111111111:role/cms-dev-cmsprotonenvironmentprotoncodebuildroleXXX-XXXXXX \
            --pipeline-service-role-arn arn:aws:iam::11111111111:role/service-role/proton_role
            ```

   1. After AWS Proton shows that all services have been deleted, verify in the
      CloudFormation console that all CMS on AWS modules have been deleted, and if not, delete them.

1. Delete AWS Proton Service Templates, Environment, and Environment Templates.
      NOTE: if you wish to keep services that have been deployed via backstage, skip these steps.
   1. Navigate to the `Service Templates` view in AWS Proton and delete any CMS on AWS service templates.

      ![Delete Proton Service Templates](documentation/images/readme/delete-proton-service-templates.png)

      WARNING: If you receive the following Validation Exception: `Service template has major versions that must first be deleted.`,
      then you must run the delete command multiple times until all of the major versions have been deleted
      for the service template.

   2. Navigate to the `Environments` view and delete the `cms_environment` Environment.

      ![Delete Proton Environment](documentation/images/readme/delete-proton-environment.png)

      WARNING: If you receive the following Validation Exception:
      `Environment template has major versions that must first be deleted.`, then you must run the
      delete command multiple times until all of the major versions have been deleted for the environment template.

   3. Navigate to the `Environment Templates` view and delete the `cms_environment` Environment Template.
      ![Delete Proton Environment Template](documentation/images/readme/delete-proton-env-template.png)

   4. Validate on the AWS Proton dashboard that all resources have been removed.
      ![Validate Proton Teardown](documentation/images/readme/validate-proton-teardown.png)

   5. Navigate to CloudFormation and delete the AWS Proton CodeBuild stack (AWSProton-Codebuild-#######).
      ![Delete Proton CodeBuild CFN](documentation/images/readme/delete-proton-codebuild-cfn.png)

   6. Verify that the `cms-environment` stack was removed when tearing down AWS Proton, and if not, delete it.

2. Delete the Backstage CloudFormation Stacks

   Navigate to CloudFormation and delete the following stacks:
   - cms-backstage-dev
   - cms-backstage-env-dev

   ![Delete Backstage Stacks](documentation/images/readme/delete-backstage-cfn.png)

  > **NOTE:** The `cms-backstage-dev` stack might fail to delete due to the ACM certificate creation custom resource.
  After delete fails, click delete again and select retain on the custom resource.
  This will not leave any resources in the account.

  ![Delete Backstage with Cert Error](documentation/images/readme/delete-backstage-on-cert-error.png)

1. Delete the CMS Backstage Amazon ECR repository

   Navigate to Amazon ECR, and delete the repository called `backstage`.

   ![Delete ECR Repository](documentation/images/readme/ecr-delete-backstage-repo.png)

2. Delete the CMS on AWS CloudFormation Stacks

   Navigate to CloudFormation and delete the `cms-environment` and `cms-dev` stacks.

   > **WARNING:** This is your last opportunity to capture the deployment UUID. Please make sure you have captured
   it using the make command specified in step 1 of the [Teardown](##Teardown) section.

   ![Delete CMS Dev Stack](documentation/images/readme/cfn-delete-cms-dev-stack.png)

3. Manually cleanup the following resources:
   - S3 Buckets
   - Cognito User Pool
   - KMS Keys

   Locate the leftover resources using the following command which first requires you to export the `DEPLOYMENT_UUID` variable using the value previously acquired from AWS Systems Manager.

   If you tore down the CMS on AWS stack without capturing the UUID, the below command can be run by removing
   the `Solutions:DeploymentUUID` Key filter, however the results will include other CMS on AWS stacks if they exist,
   so use this method with caution.

   ```bash
   export DEPLOYMENT_UUID=<DEPLOYMENT_UUID_VALUE_FROM_SSM>

   aws resourcegroupstaggingapi get-resources --tag-filters \
   Key=Solutions:SolutionID,Values=SO0241 \
   Key=Solutions:DeploymentUUID,Values=$DEPLOYMENT_UUID \
   --query "ResourceTagMappingList[*].ResourceARN"
   ```

   This query results in a list of ARNs to assist you with locating the resources in the AWS Console. Resources can then be manually deleted, or deleted via a script, utilizing the resource ARNs where appropriate.

   > **WARNING:** Some resources may take some time to cleanup after CloudFormation finishes tearing down, and could show in the
   output even if they no longer exist.  For example, Amazon VPC, Fargate, and Amazon ECS resources can remain queryable for up to
   30 minutes after deletion.

   Example Output:
   ```json
   [
      "arn:aws:cognito-idp:us-east-1:11111111111:userpool/us-east-1_XXXXXXXX",
      "arn:aws:dynamodb:us-east-1:11111111111:table/cms-alerts-on-aws-stack-dev-cmsalertsusersubscriptionsconstructuseremailsubscriptionstableXXXXXXXXXXX",

      "arn:aws:ecs:us-east-1:11111111111:task-definition/cms-backstage-dev:1",
      "arn:aws:ecs:us-east-1:11111111111:task-definition/cms-backstage-dev:2",
      "arn:aws:s3:::cms-connect-store-on-aws-connectstoreconnectstore-XXXXXXXXXXX",
      "arn:aws:s3:::cms-dev-cmsprotonenvironmentprotonenvironmentbuck-XXXXXXXXXXX",
      "arn:aws:dynamodb:us-east-1:11111111111:table/cms-alerts-on-aws-stack-dev-cmsalertsnotificationconstructnotificationstableXXXXXXX-XXXXXXXXXX",
      "arn:aws:logs:us-east-1:11111111111:log-group:cms-backstage-dev-cmsbackstagebackstageloggroupXXXXXXXX-XXXXX",
      "arn:aws:logs:us-east-1:11111111111:log-group:cms-dev-cmspipelinescmsvpcloggroupXXXXXXXX-XXXXX",
      "arn:aws:s3:::cms-dev-cmspipelinesbackstagecodepipelineartifact-XXXXXXXXXX",
      "arn:aws:s3:::cms-backstage-dev-cmsbackstagebackstageelblogsbuc-XXXXXXXXXX",
      "arn:aws:acm:us-east-1:11111111111:certificate/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
      "arn:aws:cognito-idp:us-east-1:11111111111:userpool/us-east-1_XXXXXXX",
      "arn:aws:logs:us-east-1:11111111111:log-group:cms-connect-store-on-aws-stack-dev-connectstoreconnectstoreiotconnectivitylog1234abc-XXXXXXXXX",
      "arn:aws:rds:us-east-1:11111111111:cluster-snapshot:cms-backstage-env-dev-snapshot-cmsbackstageenvbackstageaurorapostgresXXXXX-XXXXXXXXX",
      "arn:aws:s3:::cms-connect-store-on-aws-connectstoreconnectstore-XXXXXXXXXXX",
      "arn:aws:s3:::cms-backstage-env-dev-cmsbackstageenvbackstagecat-XXXXXXXXXXX",
      "arn:aws:kms:us-east-1:11111111111:key/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
      "arn:aws:kms:us-east-1:11111111111:key/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
      "arn:aws:kms:us-east-1:11111111111:key/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
      "arn:aws:kms:us-east-1:11111111111:key/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
   ]
   ```

## Developer Guide

### Pre-Commit Hooks

This solution contains a number of linters and checks to ensure code quality.
If you are not planning to commit code back to source, you can run the pre-commit hooks manually
using the following command:

```bash
pre-commit run --all
```

### Unit Test

After making changes, run unit tests to make sure added customization
passes the tests:

```bash
./deployment/run-unit-tests.sh
```

## License

Copyright Amazon.com, Inc. or its affiliates. All Rights Reserved.

Licensed under the Apache License, Version 2.0 (the "License").
You may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
