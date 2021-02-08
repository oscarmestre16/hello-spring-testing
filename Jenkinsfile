pipeline {
    agent any

    options {
        ansiColor('xterm')
    }
    stages {
        stage('Build') {
            steps {
               sh './gradlew clean test check'
            }
            post {
                always {
                    junit 'build/test-result/test/TEST-*.xml'
                }
            }
        }
        stage('QA') {
            steps { 
                withGradle {               
                    sh './gradlew check'
                }
            }
            post {
                always {
                    recordIssues enabledForFailure: true, tool: pmdParser(pattern: 'build/reports/pmd/*.xml')
                }
            }
            stage('QA') {
                  steps {
                     withGradle {
                        sh './gradlew assemble'
                     }
                  }
                  post {
                    success {
                       archiveArtifacts 'build/libs/*.jar'
                    }
                  }
            }
        }
    }
}
