To run Terraform and interact with AWS from Jenkins, you typically configure these plugins:
- Terraform Plugin
     Allows Jenkins to run Terraform commands (init, plan, apply) directly in pipeline jobs.
- Pipeline Plugin
     Core plugin for writing Jenkins pipelines (Jenkinsfile).
- AWS Credentials Plugin
     Provides a secure way to store and inject AWS access keys into jobs.
- Credentials Binding Plugin
     Lets you bind stored credentials to environment variables for use in Terraform.
- Git Plugin
     To pull your Terraform code from a Git repository.

��� Configuring AWS Credentials in Jenkins
You need AWS credentials (Access Key ID + Secret Access Key) that have permissions to create VPC, EC2, etc.
Steps:
- Generate AWS IAM User Credentials
     In AWS Console → IAM → Create user (e.g., jenkins-terraform).
     Attach policies like AmazonEC2FullAccess, AmazonVPCFullAccess, or a custom least-privilege policy.
     Download the Access Key ID and Secret Access Key.
- Add Credentials in Jenkins
     Go to Jenkins Dashboard → Manage Jenkins → Credentials → Global → Add Credentials.
     Select AWS Credentials (from AWS plugin).
     Enter Access Key ID and Secret Access Key.
     Give it an ID (e.g., aws-jenkins).
- Use Credentials in Pipeline In your Jenkinsfile, bind the credentials to environment variables:

