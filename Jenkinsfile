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
                git url: 'http://10.250.12.1:8929/root/hello-spring-testing.git', branch:'master'
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
    }
}
