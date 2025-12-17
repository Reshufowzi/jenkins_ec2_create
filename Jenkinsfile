pipeline {
    agent any

    environment {
        AWS_DEFAULT_REGION = "ap-south-1"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git url: 'https://github.com/Reshufowzi/jenkins_ec2_create.git', branch: 'main'
            }
        }

        stage('Terraform Init') {
            steps {
                withCredentials([[
                    $class: 'AmazonWebServicesCredentialsBinding',
                    credentialsId: 'aws-creds'
                ]]) {
                    sh '''
                        cd infra
                        terraform init
                    '''
                }
            }
        }

        stage('Terraform Plan') {
            steps {
                withCredentials([[
                    $class: 'AmazonWebServicesCredentialsBinding',
                    credentialsId: 'aws-creds'
                ]]) {
                    sh '''
                        cd infra
                        terraform plan
                    '''
                }
            }
        }

        stage('Terraform Apply') {
            steps {
                withCredentials([[
                    $class: 'AmazonWebServicesCredentialsBinding',
                    credentialsId: 'aws-creds'
                ]]) {
                    sh '''
                        cd infra
                        terraform apply -auto-approve
                    '''
                }
            }
        }
    }
}

