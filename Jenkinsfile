pipeline{
  agent any
  
  environment {
    AWS_DEFAULT_REGION = 'ap-south-1'  
  }

  stages{
    stage('Terraform init'){
      steps{
        echo "Initializing the Terraform"
        sh 'terraform init'
      }
    }

    stage('Terraform Plan'){
      steps{
        echo "Planning the Terraform"
        sh 'terraform plan'
      }
    }

    stage('Terraform Apply'){
      steps{
        echo "Initializing the Terraform"
        sh 'terraform apply -auto-approve'
      }
    }
    
  }

}
