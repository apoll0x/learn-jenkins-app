pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
                sh '''
                echo "Testowy komunikat! $JOB_NAME"
                echo "Witaj, użytkowniku!"
                echo "Test!"
                '''
            }
        }
    }
}
