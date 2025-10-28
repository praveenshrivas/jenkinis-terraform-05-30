pipeline {
    agent any

    environment {
        AWS_DEFAULT_REGION = 'ap-south-1'
    }

    stages {
        stage('Terraform Init and Apply') {
            steps {
                echo "Initializing Terraform..."
                sh '''
                terraform init
                terraform apply -auto-approve
                terraform output -raw ec2_public_ip > ec2_ip.txt
                cat ec2_ip.txt
                '''
            }
        }
        stage('Archive the Artifacts'){
            steps{
                archiveArtifacts artifacts:'ec2_ip.txt', fingerprint: true
            }
        }
    }
    post{
        success{
            echo "Terraform Completed Successfully-Trigerring Ansible Pipeline"
            build job: 'Ansible-demo', propogate: false
        }
        failure{
            echo "Terraform Build failed."
        }
    }
}
