pipeline {
    agent any

    options {
        ansiColor('xterm')
    }
    stages {
        //stage('Setup') {
          //  steps {
           //    sh './gradlew dependencyCheckUpdate'
           // }
        //}
        stage('Test') {         
            steps {
               sh './gradlew dependencyCheckAnalyze'
            }
            post {
               always {
                  //junit 'build/test-results/test/TEST-*.xml'
                  junit 'build/reports/*.xml'
                  dependencyCheckPublisher pattern: 'build/reports/dependency-check-report.xml'
               }

            }
        }
    }
}
