pipeline {
    agent any

    options {
        ansiColor('xterm')
    }
    stages {
        
        stage('Test') {         
            steps {
                withGradle{
                    sh './gradlew assemble'
                 }
            }
            post {
                success{
                    archiveArtifacts 'build/libs/*.jar'
                        withCredentials([string(credentialsId: 'gitLabPrivateToken', variable: 'gitLabPrivateToken')]){
                        sh './gradlew publish'
                    }
                }
            }
        }
    }
}
