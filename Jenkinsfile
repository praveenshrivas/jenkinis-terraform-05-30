pipeline {
    agent any

    environment {
        AWS_DEFAULT_REGION = 'ap-south-1'
    }

    stages {
        stage('Terraform Init') {
            steps {
                echo "Initializing Terraform..."
                sh 'terraform init'
            }
        }

        stage('Terraform Plan') {
            steps {
                echo "Planning Terraform changes..."
                sh 'terraform plan -out=tfplan | tee tf-plan.log'
            }
        }

        stage('Terraform Apply') {
            steps {
                echo "Applying Terraform plan to create resources..."
                sh 'terraform apply -auto-approve | tee tf-output.log'
            }
        }
    }
}
