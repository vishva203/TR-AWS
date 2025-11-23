pipeline {
  agent any
  environment {
    AWS_CREDS = credentials('aws-jenkins')
  }
  stages {
    stage('Terraform Init') {
      steps {
        sh '''
          export AWS_ACCESS_KEY_ID=$AWS_CREDS_USR
          export AWS_SECRET_ACCESS_KEY=$AWS_CREDS_PSW
          terraform init
        '''
      }
    }
    stage('Terraform Destroy') {
      steps {
        sh '''
          terraform plan -out=tfplan
          terraform destroy -auto-approve tfplan
        '''
      }
    }
  }
}