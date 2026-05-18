pipeline {
    agent any

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
                        -Dsonar.sources=.
                        """
                    }
                }
            }
        }
    }
}