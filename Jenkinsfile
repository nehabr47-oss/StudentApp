pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/nehabr47-oss/StudentApp.git'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    bat 'sonar-scanner -Dsonar.projectKey=StudentApp -Dsonar.sources=.'
                }
            }
        }
    }
}