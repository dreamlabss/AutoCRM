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
        
        
        
        stage('Pulling-image-server') {
            steps {
                sh "cd docker"
                sh "make down"
                sh "make up"
            }
        }
    
        
        
        stage('AST') {
            steps {
                build 'SECURITY-DAST-Arachini'
            }
        }
        
    }
}