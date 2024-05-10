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
                build 'SCA-SAST-SNYK'
            }
        }

        stage('SAST') {
            steps {
                build 'SCA-SAST-SONARQUBE'
            }
        }
        
        stage('Build-and-tag') {
            when {
                expression { DOCKER_RESISRTY = 'true' }
            }
            steps {
                script {
                    def app = docker.build("dreamlabssdock/php8symfony")
                    env.DOCKER_APP = app         
                }
            }
        }
        
        stage('Pulling-image-server') {
            steps {
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