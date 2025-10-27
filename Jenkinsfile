pipeline {
    agent any

    stages {
        stage('Terraform Init & Apply') {
            steps {
                sh '''
                cd terraform
                terraform init
                terraform apply -auto-approve
                terraform output -raw ec2_public_ip > ec2_ip.txt
                cat ec2_ip.txt
                '''
            }
        }

        stage('Archive EC2 IP Artifact') {
            steps {
                archiveArtifacts artifacts: 'terraform/ec2_ip.txt', fingerprint: true
            }
        }
    }
}
