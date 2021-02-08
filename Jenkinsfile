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
               withSonarQubeEnv(credentialsId: '366cad3b5c2e3fc5f6bf3a6b01a08205d5ca1f11', installationName: 'local'){
                    sh'.gradlew sonarqube'
               }
            }
            post {
               always {
                    recordIssues enabledForFailure: true, tool: spotBugs(pattern: 'build/reports/spotbugs/*.xml')
                    recordIssues enabledForFailure: true, tool: pmdParser(pattern: 'build/reports/pmd/*.xml')
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
        stage('sonarqube') {
            steps {
                withGradle {
                configFileProvider([configFile(fileId: 'GradleProperties-sonarqube',
                 targetLocation: 'gradle.properties')])
                    sh './gradlew sonarqube'
                }
            }
        }
    }
}