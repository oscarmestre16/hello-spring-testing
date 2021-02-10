pipeline {
    agent any

    options {
        ansiColor('xterm')
    }
    stages {
        
        stage('Test') {         
            steps {
               sh './gradlew publish'
            }
            

            }
        }
    }
}
