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
          echo "DEBUG: AWS_ACCESS_KEY_ID=$AWS_CREDS_USR"
          echo "DEBUG: AWS_SECRET_ACCESS_KEY=$AWS_CREDS_PSW"
          terraform init -input=false
        '''
      }
    }

    stage('Terraform Destroy') {
      steps {
        sh '''
          export AWS_ACCESS_KEY_ID=$AWS_CREDS_USR
          export AWS_SECRET_ACCESS_KEY=$AWS_CREDS_PSW
          terraform plan -destroy -out=tfplan -input=false
          terraform apply -auto-approve tfplan
        '''
      }
    }
  }
}