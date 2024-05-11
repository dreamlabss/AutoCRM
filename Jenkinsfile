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
        
        stage('Pulling-image-server') {
            steps {
                sh "cd docker && make down"
                sh "cd docker && make up"
            }
        } 
        
        stage('AST') {
            steps {
                build 'SECURITY-DAST-Arachini'
            }
        }
        
    }
}