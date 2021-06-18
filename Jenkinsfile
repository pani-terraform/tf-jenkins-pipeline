pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/pani-terraform/tf-jenkins-pipeline']]])
            }
        }
    }
    stage('init') {
        steps {
            sh '''
            terraform init
            '''
        }
    }
    stage('validate') {
        steps {
            sh '''
            terraform validate
            '''
        }
    }
    stage('plan') {
        steps {
            sh '''
            export AWS_CRED=/home/pani/.aws/credentials
            terraform plan
            '''
        }
    }
    stage('apply') {
        steps {
            sh '''
            export AWS_CRED=/home/pani/.aws/credentials
            terraform apply -auto-approve
            '''
        }
    }
}
