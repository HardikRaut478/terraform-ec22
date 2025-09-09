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
                sh 'terraform plan'
            }
        }

        stage('Terraform Apply') {
            steps {
                sh 'terraform apply --auto-approve'
            }
        }
    }

    post {
        always {
            echo "✅ Pipeline finished!"
        }
        success {
            echo "🎉 Terraform Apply completed successfully."
        }
        failure {
            echo "❌ Pipeline failed. Please check the logs."
        }
    }
}
