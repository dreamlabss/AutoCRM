pipeline {
    agent{
        node {
            label 'ubuntu'
        }
    }

    environment {
        DOCKER_RESISRTY = 'true'
    }
    
    stages {
        stage('Clonning Git') {
            steps {
                checkout scm
            }
        }

        stage('SCA') {
            steps {
                build 'SCA-SAST-SNYK-CRM'
            }
        }

        stage('SAST') {
            steps {
                build 'SCA-SAST-SONARQUBE-CRM'
            }
        }
        
        
        stage('Building docker conatiners, installing dependencies and makeing migrations') {
            steps {
                sh "cd docker && make down"
                sh "cd docker && make up"
            }
        }
    
        
        
        stage('DAST') {
            steps {
                build 'SECURITY-DAST-Arachini'
            }
        }
        
    }
}