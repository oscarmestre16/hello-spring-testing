pipeline {
    agent any
    tools{
       jdk 'OpenJDK-15.0.2'
    }
    options {
        ansiColor('xterm')
    }
    stages {
        stage('Test') {
            steps {
                git url: 'http://10.250.12.1:8929/root/hello-spring-testing.git', branch:'master'
                sh './gradlew test'
            }
        stage('Build') {
            steps {                
                sh './gradlew assemble'
            }
        }
