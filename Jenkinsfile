pipeline {
    agent any

    environment {
        AWS_DEFAULT_REGION = 'us-east-1'
        AWS_ACCESS_KEY_ID     = credentials('aws-access-key-id')
        AWS_SECRET_ACCESS_KEY = credentials('aws-secret-access-key')
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master',
                    url: 'https://github.com/HardikRaut478/terraform-ec22.git'
            }
        }

        stage('Terraform Init') {
            steps {
                sh 'terraform init'
            }
        }

        stage('Terraform Validate') {
            steps {
                sh 'terraform validate'
            }
        }

        stage('Terraform Plan') {
            steps {
                sh 'terraform plan -out=tfplan'
            }
        }

        stage('Terraform Apply') {
            when {
                branch 'master'
            }
            steps {
                input(message: "Approve EC2 creation?", ok: "Apply")
                sh 'terraform apply -auto-approve tfplan'
            }
        }
    }

    post {
        always {
            echo "Pipeline finished"
        }
    }
}
