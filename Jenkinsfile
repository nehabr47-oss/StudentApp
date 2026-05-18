pipeline {
    agent any

    tools {
        sonarRunner 'SonarScanner'
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
                withSonarQubeEnv('SonarQube') {
                    bat '''
                    sonar-scanner -Dsonar.projectKey=StudentApp -Dsonar.sources=.
                    '''
                }
            }
        }
    }
}