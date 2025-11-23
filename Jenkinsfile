pipeline {
  agent any

  environment {
    AWS_REGION = "ap-south-1"
  }

  stages {

    stage('Terraform Init') {
      steps {
        withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', credentialsId: 'aws-jenkins']]) {
          sh '''
            echo "AWS Identity Check:"
            aws sts get-caller-identity

            terraform init -input=false
          '''
        }
      }
    }

    stage('Terraform Apply') {
      steps {
        withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', credentialsId: 'aws-jenkins']]) {
          sh '''
            terraform plan -out=tfplan
            terraform apply -auto-approve tfplan
          '''
        }
      }
    }

  }
}
