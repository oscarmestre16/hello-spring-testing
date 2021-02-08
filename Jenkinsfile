pipeline {
    agent any

    options {
        ansiColor('xterm')
    }
    stages {
        stage('Test') {
            steps {
               sh './gradlew clean test check'
            }
            post {
                always {
                    junit 'build/test-results/test/TEST-*.xml'
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
                    recordIssues enabledForFailure: true, tool: spotBugs(pattern: 'build/reports/spotbugs/*.xml')
                }
            }
        }
        stage('Build') {
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
