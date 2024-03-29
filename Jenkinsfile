pipeline {
    agent any
    environment {
        AWS_ACCESS_KEY_ID     = credentials('jenkins-secret-key')
        AWS_SECRET_ACCESS_KEY = credentials('jenkins-secret')
    }
    stages {
        stage('Terraform Initialization') {
            steps {
                sh 'terraform init'
                sh 'pwd'
                sh 'ls -al'
                sh 'printenv'
            }
        }
        stage('Terraform Format') {
            steps {
                sh 'terraform fmt -check'
            }
        }
        stage('Terraform Validate') {
            steps {
                sh 'terraform validate'
            }
        }
        stage('Terraform Planning') {
            steps {
                sh 'terraform plan -no-color'
                input message: "Approve build or Discard?"
            }
        }
        stage('Terraform Apply') {
            steps {
                sh 'terraform apply -auto-approve'
            }
        }
        stage('Terraform Destroy') {
            steps {
                sh 'terraform destroy -auto-approve'
                input message: "Approve Destroying of resource build or Discard?"
            }
        }
    }
}
