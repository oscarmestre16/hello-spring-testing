pipeline {
    agent any

    options {
        ansiColor('xterm')
    }
    stages {
        
        stage('Test') {         
            steps {               
               withCredentials([string(credentialsId: 'gitLabPrivateToken', variable: 'gitLabPrivateToken')]){
                   sh './gradlew publish'
               }

            }

            }
        }
    }
}
