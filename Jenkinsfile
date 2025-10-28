pipeline {
    agent any

    stages {
        stage('Terraform Init & Apply') {
            steps {
                sh '''
                terraform init
                terraform apply -auto-approve
                terraform refresh
                terraform output -raw ec2_public_ip > ec2_ip.txt
                cat ec2_ip.txt
                '''
            }
        }

        stage('Archive EC2 IP Artifact') {
            steps {
                archiveArtifacts artifacts: 'ec2_ip.txt', fingerprint: true
            }
        }
    }
    post {
        success {
            echo "✅ Terraform completed successfully — triggering Ansible pipeline..."
            build job: 'Ansible-demo', propagate: false // <-- change to exact name of your Ansible pipeline
        }
        failure {
            echo "❌ Terraform failed — not triggering Ansible pipeline."
        }
    }
}
