## ARJ-Stack: CodePipeline for CloudFormation Stacks

This project has the direction of how AWS DevOps service (CodePipeline, CodeBuild) can be used to create Pipeline for a project based on CloudFormation Templates. 

### Resources
This project features the following components:

#### pipeline

This folder contains the CloudFormation Template used for building the CodePipeline for the projects
- `codepipeline-infrastructure.yml` - Create Code Pipeline for the project `arjstack-infrastructure`.

- Please note that upload the Template files placed in this folder into S3 bucket [S3 Key] `arjstack-devops/pipeline-templates` and use this S3 location `https://s3.amazonaws.com/arjstack-devops/pipeline-templates/codepipeline-infrastructure.yml` while creating CloudFormation Stack for CodePipeline 
  - If not, Cloudformation will automatically create a bucket for you if you will go with the approach of uploading template file while creating stack for pipeline

#### infrastructure

This folder contains the Cloudformation Template used in provisioning AWS resources as well as `buildspec.yml` and corresponding json files for CodeBuild 

- Please note all the files of this folder should be committed in the code commit repository `arjstack-infrastructure`.

### Requirements

| Resource | Name | Purpose |
|------|---------|---------|
| <a name="codecommit_repository"></a> [codecommit_repository](#requirement\_codecommit\_repository) | `"arjstack-infrastructure"` | CodeCommit Repository where the CFN Templates will be stored to provision the AWS resources |
| <a name="s3_bucket"></a> [s3_bucket](#requirement\_s3\_bucket) | `"arjstack-devops"` | This bucket is used to store the Cloudformation Templates used for creating CodePipeline and to store CodePipeline and CodeBuild Artifacts |
| <a name="sns_topic"></a> [sns_topic](#requirement\_sns\_topic) | `"arjstack-devops-notification"` | This SNS topic is used for notification in Appproval stage |
| <a name="sns_topic_subscription"></a> [sns_topic_subscription](#requirement\_sns\_topic\_subscription) |  | Subscription to SNS topic so that reviewer is notified (preferably Email based subscription) |

### Inputs - CloudFormation Stack for the Pipelines
---

#### Pipeline of the project `arjstack-infrastructure`

| Name | Description | Type | Default | Required | Example|
|:------|:------|:------|:------|:------:|:------|
| <a name="ProjectName"></a> [ProjectName](#input\_ProjectName) | Name of the Project. | `string` | `"ARJStack-Infrastructure"` | no |  |
| <a name="ProjectRepoName"></a> [ProjectRepoName](#input\_ProjectRepoName) | Name of the repo which contains CFN template for provisioning Infrastructure. | `string` |  | yes | `"arjstack-infrastructure"` |
| <a name="ArtifactStoreS3Location"></a> [ArtifactStoreS3Location](#input\_ArtifactStoreS3Location) | Name of the S3 bucket to store CodePipeline artifact. | `string` |  | yes | `"arjstack-devops"` |
| <a name="NotificationTopic"></a> [NotificationTopic](#input\_NotificationTopic) | Name of the SNS topic to send approval notification. | `string` |  | yes | `"arjstack-devops-notification"` |


### Authors

Module is maintained by [Ankit Jain](https://github.com/ankit-jn) with help from [these professional](https://github.com/ankit-jn/codepipeline-cloudformation/graphs/contributors).
