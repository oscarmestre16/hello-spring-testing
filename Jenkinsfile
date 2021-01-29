
pipeline {
    agent any
    options {
        ansiColor('xterm')
    }
    stages {
        stage('Test') {
            steps {
                sh './gradlew test'
                archiveArtifacts artifacts: 'build/test-results/test/TEST-*.xml'
            }
        stage('Build') {
            steps {                
                sh './gradlew assemble'
            }
        }
        stage('deploy') {
            steps {
                sh 'docker-compose up -d'
            }
