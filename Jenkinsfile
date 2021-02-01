pipeline {
    agent any
    tools{
       jdk 'OpenJDK-15.0.2'
    }
    options {
        ansiColor('xterm')
    }
    stages {
        stage('Build') {
            steps {
                sh './gradlew assemble'
            }
            post {
                success {
                    archiveArtifacts 'build/libs/*jar'
                }
            }
        }
        stage('Test') {
            steps { 
                withGradle {               
                    sh './gradlew test'
                }
            }
            post {
                success {
                    archiveArtifacts 'build/test-results/test/TEST-*.xml'
                }
            }
        }
        stage('pitest'){
            steps{
                withGradle{
                    sh './gradlew clean pitest'
                }
            }
            post{
                always{
                    pitmutation mutationStatsFile: 'build/reports/pitest/**/mutation.xml'
                }
            }
        }
    }
}
