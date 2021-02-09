pipeline {
    agent any

    options {
        ansiColor('xterm')
    }
    stages {
        stage('Setup') {
            steps {
               sh './gradlew dependencyCheckUpdate'
            }
        }
        stage('Test') {         
            steps {
               sh './gradlew dependencyCheckAnalyze'
            }
            post {
                always {
                    junit 'build/reports/*.json'
                }
            }
        }
    }
}
