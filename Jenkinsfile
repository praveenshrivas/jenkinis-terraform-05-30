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
                sh 'terraform plan'
            }
        }

        stage('Terraform Apply') {
            steps {
                echo "Applying Terraform plan to create resources..."
                sh 'terraform apply -auto-approve'
            }
        }
    }
}
