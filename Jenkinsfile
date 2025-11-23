pipeline {
  agent any

  environment {
    AWS_CREDS = credentials('aws-jenkins')
    AWS_REGION = "ap-south-1"      // <-- ADD THIS
  }

  stages {

    stage('Terraform Init') {
      steps {
        sh '''
          export AWS_ACCESS_KEY_ID="$AWS_CREDS_USR"
          export AWS_SECRET_ACCESS_KEY="$AWS_CREDS_PSW"
          export AWS_REGION="$AWS_REGION"

          echo "Using AWS Access Key: $AWS_ACCESS_KEY_ID"

          terraform init -input=false
        '''
      }
    }

    stage('Terraform Destroy') {
      steps {
        sh '''
          export AWS_ACCESS_KEY_ID="$AWS_CREDS_USR"
          export AWS_SECRET_ACCESS_KEY="$AWS_CREDS_PSW"
          export AWS_REGION="$AWS_REGION"

          terraform plan -destroy -out=tfplan -input=false
          terraform apply -auto-approve tfplan
        '''
      }
    }

  }
}
