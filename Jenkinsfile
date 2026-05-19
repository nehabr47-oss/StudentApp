pipeline {
    agent any

    environment {
        IMAGE_NAME = "nehabr30/studentapp"
        IMAGE_TAG = "latest"
        DOCKER_CREDENTIALS = credentials('dockerhub-creds')
    }

    stages {

        stage('Clone') {
            steps {
                git branch: 'main',
                url: 'https://github.com/nehabr47-oss/StudentApp.git'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                script {
                    def scannerHome = tool 'SonarScanner'

                    withSonarQubeEnv('SonarQube') {
                        bat """
                        ${scannerHome}\\bin\\sonar-scanner.bat ^
                        -Dsonar.projectKey=StudentApp ^
                        -Dsonar.sources=. ^
                        -Dsonar.scanner.skipJreProvisioning=true
                        """
                    }
                }
            }
        }

        stage('Trivy File System Scan') {
            steps {
                bat '''
                trivy fs .
                '''
            }
        }

        stage('Docker Build') {
            steps {
                bat '''
                docker build -t %IMAGE_NAME%:%IMAGE_TAG% .
                '''
            }
        }

        stage('Docker Push') {
            steps {
                bat '''
                echo %DOCKER_CREDENTIALS_PSW% | docker login -u %DOCKER_CREDENTIALS_USR% --password-stdin
                docker push %IMAGE_NAME%:%IMAGE_TAG%
                '''
            }
        }
    }
}